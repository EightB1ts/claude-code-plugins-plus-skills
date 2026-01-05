---
name: sentry-reliability-patterns
description: |
  Build reliable Sentry integrations.
  Use when handling SDK failures gracefully,
  implementing retry logic, or ensuring error tracking uptime.
  Trigger with phrases like "sentry reliability", "sentry failover",
  "sentry sdk failure handling", "resilient sentry setup".
allowed-tools: Read, Write, Edit, Grep
version: 1.0.0
license: MIT
author: Jeremy Longshore <jeremy@intentsolutions.io>
---

# Sentry Reliability Patterns

## Overview
Build reliable Sentry integrations that handle failures gracefully.

## Graceful Degradation

### SDK Initialization Failure Handling
```typescript
import * as Sentry from '@sentry/node';

function initSentryWithFallback() {
  try {
    Sentry.init({
      dsn: process.env.SENTRY_DSN,
      // ... config
    });

    // Verify initialization
    const client = Sentry.getCurrentHub().getClient();
    if (!client) {
      throw new Error('Sentry client not initialized');
    }

    console.log('Sentry initialized successfully');
    return true;
  } catch (error) {
    console.error('Sentry initialization failed:', error);

    // App continues without error tracking
    return false;
  }
}

const sentryEnabled = initSentryWithFallback();

// Wrap capture functions
export function captureError(error: Error, context?: object) {
  if (sentryEnabled) {
    Sentry.captureException(error, { extra: context });
  }
  // Always log locally
  console.error('Error:', error.message, context);
}
```

### Missing DSN Handling
```typescript
Sentry.init({
  // DSN can be undefined - SDK will be disabled
  dsn: process.env.SENTRY_DSN,

  // This won't throw if DSN is missing
  enabled: !!process.env.SENTRY_DSN,

  beforeSend(event) {
    // Only called if DSN is set
    return event;
  },
});

// Safe to call even without DSN
Sentry.captureMessage('Test'); // No-op if disabled
```

## Network Failure Handling

### Retry with Backoff
```typescript
import * as Sentry from '@sentry/node';

class RetryTransport {
  private maxRetries = 3;
  private baseDelay = 1000;

  async send(request: any): Promise<any> {
    let lastError: Error | undefined;

    for (let attempt = 0; attempt < this.maxRetries; attempt++) {
      try {
        return await this.doSend(request);
      } catch (error) {
        lastError = error as Error;

        // Don't retry on client errors (4xx)
        if (this.isClientError(error)) {
          throw error;
        }

        // Exponential backoff
        const delay = this.baseDelay * Math.pow(2, attempt);
        await this.sleep(delay);
      }
    }

    throw lastError;
  }

  private isClientError(error: any): boolean {
    return error?.statusCode >= 400 && error?.statusCode < 500;
  }

  private sleep(ms: number): Promise<void> {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }

  private async doSend(request: any) {
    // Actual send implementation
  }
}
```

### Offline Event Queue
```typescript
class OfflineQueue {
  private queue: Sentry.Event[] = [];
  private maxSize = 100;
  private isOnline = true;

  constructor() {
    // Monitor connectivity
    this.startConnectivityCheck();
  }

  async send(event: Sentry.Event): Promise<void> {
    if (this.isOnline) {
      try {
        await Sentry.captureEvent(event);
        await this.flushQueue(); // Send queued events
      } catch (error) {
        this.enqueue(event);
      }
    } else {
      this.enqueue(event);
    }
  }

  private enqueue(event: Sentry.Event): void {
    if (this.queue.length >= this.maxSize) {
      this.queue.shift(); // Remove oldest
    }
    this.queue.push(event);
  }

  private async flushQueue(): Promise<void> {
    while (this.queue.length > 0 && this.isOnline) {
      const event = this.queue[0];
      try {
        await Sentry.captureEvent(event);
        this.queue.shift();
      } catch {
        break; // Stop flushing on error
      }
    }
  }

  private startConnectivityCheck(): void {
    setInterval(async () => {
      this.isOnline = await this.checkConnectivity();
      if (this.isOnline) {
        await this.flushQueue();
      }
    }, 30000);
  }

  private async checkConnectivity(): Promise<boolean> {
    try {
      await fetch('https://sentry.io/api/0/', { method: 'HEAD' });
      return true;
    } catch {
      return false;
    }
  }
}
```

## Circuit Breaker Pattern

### Sentry Circuit Breaker
```typescript
enum CircuitState {
  CLOSED = 'CLOSED',     // Normal operation
  OPEN = 'OPEN',         // Failing, skip calls
  HALF_OPEN = 'HALF_OPEN' // Testing recovery
}

class SentryCircuitBreaker {
  private state = CircuitState.CLOSED;
  private failures = 0;
  private lastFailure = 0;
  private readonly failureThreshold = 5;
  private readonly resetTimeout = 60000; // 1 minute

  async capture(error: Error): Promise<void> {
    if (this.state === CircuitState.OPEN) {
      if (Date.now() - this.lastFailure > this.resetTimeout) {
        this.state = CircuitState.HALF_OPEN;
      } else {
        // Circuit open - skip Sentry call
        console.warn('Sentry circuit open, skipping capture');
        return;
      }
    }

    try {
      await Sentry.captureException(error);
      await Sentry.flush(2000);

      // Success - reset circuit
      if (this.state === CircuitState.HALF_OPEN) {
        this.state = CircuitState.CLOSED;
        this.failures = 0;
      }
    } catch (err) {
      this.failures++;
      this.lastFailure = Date.now();

      if (this.failures >= this.failureThreshold) {
        this.state = CircuitState.OPEN;
        console.error('Sentry circuit opened due to failures');
      }

      throw err;
    }
  }

  getState(): CircuitState {
    return this.state;
  }
}

const sentryCircuit = new SentryCircuitBreaker();
```

## Timeout Handling

### Request Timeout
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  // Transport options
  transportOptions: {
    // Set reasonable timeouts
    headers: {},
  },
});

// Wrap with timeout
async function captureWithTimeout(
  error: Error,
  timeoutMs = 5000
): Promise<string | null> {
  return new Promise((resolve) => {
    const timeout = setTimeout(() => {
      console.warn('Sentry capture timed out');
      resolve(null);
    }, timeoutMs);

    const eventId = Sentry.captureException(error);

    Sentry.flush(timeoutMs - 100).finally(() => {
      clearTimeout(timeout);
      resolve(eventId);
    });
  });
}
```

### Graceful Shutdown
```typescript
async function shutdown(signal: string): Promise<void> {
  console.log(`Received ${signal}, shutting down gracefully...`);

  // Give Sentry time to flush
  const flushed = await Sentry.close(10000);
  console.log(`Sentry flushed: ${flushed}`);

  process.exit(0);
}

process.on('SIGTERM', () => shutdown('SIGTERM'));
process.on('SIGINT', () => shutdown('SIGINT'));
```

## Dual-Write Pattern

### Write to Multiple Destinations
```typescript
interface ErrorTracker {
  capture(error: Error, context?: object): void;
}

class SentryTracker implements ErrorTracker {
  capture(error: Error, context?: object): void {
    Sentry.captureException(error, { extra: context });
  }
}

class ConsoleTracker implements ErrorTracker {
  capture(error: Error, context?: object): void {
    console.error('[ERROR]', error.message, context);
  }
}

class FileTracker implements ErrorTracker {
  capture(error: Error, context?: object): void {
    fs.appendFileSync(
      '/var/log/app-errors.log',
      JSON.stringify({ error: error.message, context, timestamp: new Date() }) + '\n'
    );
  }
}

class ReliableErrorTracker {
  private trackers: ErrorTracker[];

  constructor(trackers: ErrorTracker[]) {
    this.trackers = trackers;
  }

  capture(error: Error, context?: object): void {
    for (const tracker of this.trackers) {
      try {
        tracker.capture(error, context);
      } catch (e) {
        console.error('Tracker failed:', e);
        // Continue with other trackers
      }
    }
  }
}

// Use multiple trackers for reliability
const errorTracker = new ReliableErrorTracker([
  new SentryTracker(),
  new ConsoleTracker(),
  new FileTracker(),
]);
```

## Health Checks

### Sentry Health Check Endpoint
```typescript
app.get('/health/sentry', async (req, res) => {
  const client = Sentry.getCurrentHub().getClient();

  if (!client) {
    return res.status(503).json({
      status: 'unhealthy',
      reason: 'Sentry not initialized',
    });
  }

  // Test capture
  try {
    const testId = Sentry.captureMessage('Health check', {
      level: 'debug',
      tags: { type: 'health_check' },
    });

    const flushed = await Sentry.flush(2000);

    res.json({
      status: flushed ? 'healthy' : 'degraded',
      eventId: testId,
      flushed,
    });
  } catch (error) {
    res.status(503).json({
      status: 'unhealthy',
      error: (error as Error).message,
    });
  }
});
```

## Prerequisites

- Understanding of failure modes
- Fallback logging strategy
- Network reliability characteristics
- Graceful shutdown requirements

## Instructions

1. Wrap Sentry.init with try/catch for graceful initialization failure handling
2. Implement fallback capture function that logs locally if Sentry fails
3. Add retry with exponential backoff for network failures
4. Implement offline event queue for intermittent connectivity
5. Add circuit breaker pattern to skip Sentry after repeated failures
6. Configure request timeout with wrapper function
7. Implement graceful shutdown with Sentry.close() on SIGTERM
8. Set up dual-write pattern to multiple error trackers for redundancy
9. Create health check endpoint to verify Sentry connectivity
10. Test all failure scenarios to ensure application continues operating

## Output
- Graceful degradation implemented
- Circuit breaker pattern applied
- Offline queue configured
- Dual-write reliability enabled

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `SDK init failure crashes app` | No try/catch around init | Wrap init with fallback handling |
| `Events lost on network failure` | No offline queue | Implement retry with backoff |
| `Blocking request handling` | Awaiting Sentry capture | Use fire-and-forget pattern |
| `Shutdown losing events` | No flush before exit | Call Sentry.close() on SIGTERM |

## Examples

**Example: Implement Circuit Breaker**
Request: "Prevent Sentry failures from affecting application"
Result: Circuit breaker opens after 5 failures, skips Sentry calls for 1 minute, auto-recovers on success.

## Resources
- [Sentry Configuration](https://docs.sentry.io/platforms/javascript/configuration/)
- [Transport Options](https://docs.sentry.io/platforms/javascript/configuration/transports/)
