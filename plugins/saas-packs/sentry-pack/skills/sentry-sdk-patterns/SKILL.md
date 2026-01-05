---
name: sentry-sdk-patterns
description: |
  Execute best practices for using Sentry SDK in TypeScript and Python.
  Use when implementing error handling patterns, structuring Sentry code,
  or optimizing SDK usage.
  Trigger with phrases like "sentry best practices", "sentry patterns",
  "sentry sdk usage", "sentry code structure".
allowed-tools: Read, Write, Edit, Grep
version: 1.0.0
license: MIT
author: Jeremy Longshore <jeremy@intentsolutions.io>
---

# Sentry SDK Patterns

## Overview
Best practices and patterns for using Sentry SDK effectively.

## Prerequisites
- Sentry SDK installed and configured
- Understanding of error handling concepts
- Familiarity with async/await patterns

## Instructions

1. Create a centralized error handler module for consistent error capture
2. Implement scoped context for transactions and operations
3. Add structured breadcrumbs for debugging context
4. Configure error boundaries in frameworks (React, Vue, etc.)
5. Use custom fingerprinting for better issue grouping
6. Implement async error handling with proper scope propagation
7. Add performance tracing for critical paths
8. Configure sampling rates based on traffic volume

### Pattern 1: Centralized Error Handler
```typescript
// lib/sentry.ts
import * as Sentry from '@sentry/node';

export function captureError(
  error: Error,
  context?: Record<string, unknown>
): string {
  return Sentry.captureException(error, {
    extra: context,
    tags: { handler: 'centralized' },
  });
}

export function captureWarning(
  message: string,
  context?: Record<string, unknown>
): void {
  Sentry.captureMessage(message, {
    level: 'warning',
    extra: context,
  });
}
```

### Pattern 2: Async Error Wrapper
```typescript
export function withSentry<T>(
  fn: () => Promise<T>,
  context?: Record<string, unknown>
): Promise<T> {
  return fn().catch((error) => {
    Sentry.captureException(error, { extra: context });
    throw error;
  });
}

// Usage
await withSentry(
  () => fetchUserData(userId),
  { userId, operation: 'fetchUser' }
);
```

### Pattern 3: Express Error Middleware
```typescript
import * as Sentry from '@sentry/node';
import express from 'express';

const app = express();

// Request handler creates span
app.use(Sentry.Handlers.requestHandler());

// Routes
app.get('/api/data', async (req, res) => {
  // Your route logic
});

// Error handler must be before any other error middleware
app.use(Sentry.Handlers.errorHandler());

// Custom error handler
app.use((err, req, res, next) => {
  res.status(500).json({ error: 'Internal server error' });
});
```

### Pattern 4: Scoped Context
```typescript
Sentry.withScope((scope) => {
  scope.setTag('operation', 'payment');
  scope.setUser({ id: userId });
  scope.setExtra('amount', amount);

  Sentry.captureException(error);
});
```

### Pattern 5: Breadcrumbs
```typescript
// Add breadcrumb before operation
Sentry.addBreadcrumb({
  category: 'payment',
  message: `Processing payment of $${amount}`,
  level: 'info',
  data: { userId, amount },
});

// If error occurs, breadcrumbs provide context
try {
  await processPayment(userId, amount);
} catch (error) {
  Sentry.captureException(error);
}
```

## Output
- Clean, maintainable error handling code
- Consistent error context across application
- Efficient Sentry SDK usage

## Best Practices

### Error Categorization
```typescript
enum ErrorCategory {
  VALIDATION = 'validation',
  NETWORK = 'network',
  DATABASE = 'database',
  AUTHENTICATION = 'auth',
  EXTERNAL_SERVICE = 'external',
}

function categorizeError(error: Error): ErrorCategory {
  if (error.name === 'ValidationError') return ErrorCategory.VALIDATION;
  if (error.message.includes('ECONNREFUSED')) return ErrorCategory.NETWORK;
  // ... more categorization
  return ErrorCategory.EXTERNAL_SERVICE;
}

Sentry.setTag('error_category', categorizeError(error));
```

### Fingerprinting
```typescript
Sentry.captureException(error, {
  fingerprint: ['{{ default }}', 'payment-processing'],
});
```

## Examples

**Example: Implement Centralized Error Handler**
Request: "Create a reusable error handling module for our Node.js API"
Result: Created lib/sentry.ts with captureError function, scope management, and breadcrumb utilities

**Example: Add Transaction Tracing**
Request: "Track performance of our checkout flow"
Result: Implemented transaction with child spans for cart, payment, and confirmation steps

### Python Patterns
```python
import sentry_sdk
from contextlib import contextmanager

@contextmanager
def sentry_scope(tags: dict = None, extra: dict = None):
    with sentry_sdk.push_scope() as scope:
        if tags:
            for key, value in tags.items():
                scope.set_tag(key, value)
        if extra:
            for key, value in extra.items():
                scope.set_extra(key, value)
        yield scope

# Usage
with sentry_scope(tags={'operation': 'sync'}, extra={'count': 100}):
    perform_sync_operation()
```

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `Sentry is not defined` | SDK not imported | Verify import statement and package installation |
| `DSN parse error` | Malformed DSN string | Check DSN format from Sentry project settings |
| `Event dropped due to sample rate` | Sample rate too low | Increase `sampleRate` value or use dynamic sampling |
| `Network error` | Connectivity issues | Check network access to Sentry ingest endpoint |

## Resources
- [Sentry SDK Docs](https://docs.sentry.io/platforms/)
- [Sentry Best Practices](https://docs.sentry.io/product/issues/best-practices/)

## Next Steps
Proceed to `sentry-error-capture` for advanced error capture techniques.
