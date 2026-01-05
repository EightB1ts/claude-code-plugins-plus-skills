---
name: sentry-rate-limits
description: |
  Manage Sentry rate limits and quota optimization.
  Use when hitting rate limits, optimizing event volume,
  or managing Sentry costs.
  Trigger with phrases like "sentry rate limit", "sentry quota",
  "reduce sentry events", "sentry 429".
allowed-tools: Read, Write, Edit, Grep
version: 1.0.0
license: MIT
author: Jeremy Longshore <jeremy@intentsolutions.io>
---

# Sentry Rate Limits

## Overview
Manage event volume and avoid hitting Sentry rate limits.

## Understanding Rate Limits

### Types of Limits
1. **Organization Quota** - Total events per billing period
2. **Project Rate Limit** - Events per minute per project
3. **Key Rate Limit** - Events per DSN key

### Checking Current Usage
```bash
# Via API
curl -H "Authorization: Bearer $SENTRY_AUTH_TOKEN" \
  "https://sentry.io/api/0/organizations/$ORG/stats/v2/?field=sum(quantity)"
```

## Strategies to Reduce Event Volume

### 1. Error Sampling
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  // Sample 10% of errors
  sampleRate: 0.1,

  // Or use dynamic sampling
  beforeSend(event, hint) {
    // Always send critical errors
    if (event.level === 'fatal') return event;

    // Sample other errors
    if (Math.random() > 0.1) return null;
    return event;
  },
});
```

### 2. Transaction Sampling
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  // Sample 5% of transactions
  tracesSampleRate: 0.05,

  // Or dynamic sampling
  tracesSampler: (ctx) => {
    // Always trace errors
    if (ctx.parentSampled) return true;

    // Skip health checks
    if (ctx.transactionContext.name.includes('health')) return 0;

    // Lower rate for high-volume endpoints
    if (ctx.transactionContext.name.includes('/api/')) return 0.01;

    return 0.1;
  },
});
```

### 3. Ignore Common Errors
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  ignoreErrors: [
    // Browser errors
    'ResizeObserver loop limit exceeded',
    'ResizeObserver loop completed with undelivered notifications',

    // Network errors
    'Network request failed',
    'Failed to fetch',
    'Load failed',

    // User-caused
    'User aborted',
    'AbortError',
  ],

  denyUrls: [
    // Third-party scripts
    /extensions\//i,
    /^chrome:\/\//i,
    /^moz-extension:\/\//i,
  ],
});
```

### 4. Deduplication
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  integrations: [
    new Sentry.Integrations.Dedupe(),
  ],

  // Custom fingerprinting for grouping
  beforeSend(event) {
    if (event.exception?.values?.[0]?.type === 'NetworkError') {
      event.fingerprint = ['network-error', event.request?.url];
    }
    return event;
  },
});
```

### 5. Client-Side Filtering
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  beforeSend(event, hint) {
    const error = hint.originalException;

    // Don't send validation errors
    if (error?.name === 'ValidationError') return null;

    // Don't send 4xx client errors
    if (error?.status >= 400 && error?.status < 500) return null;

    // Don't send during development
    if (process.env.NODE_ENV === 'development') return null;

    return event;
  },
});
```

## Server-Side Controls

### Project Rate Limits
```bash
# Set via API
curl -X PUT \
  -H "Authorization: Bearer $SENTRY_AUTH_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"options": {"sentry:rate-limit": 100}}' \
  "https://sentry.io/api/0/projects/$ORG/$PROJECT/"
```

### Inbound Filters (Sentry Dashboard)
1. Navigate to Project Settings > Inbound Filters
2. Enable filters:
   - Legacy browsers
   - Browser extensions
   - Localhost events
   - Web crawlers

## Monitoring Usage

```typescript
// Log when approaching limits
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  beforeSend(event) {
    // Track local event count
    eventCount++;

    if (eventCount > WARNING_THRESHOLD) {
      console.warn(`High Sentry volume: ${eventCount} events`);
    }

    return event;
  },
});
```

## Prerequisites

- Understanding of current event volume
- Sentry billing plan known
- High-volume endpoints identified
- Noisy error patterns documented

## Instructions

1. Check current usage via Sentry API or dashboard stats
2. Implement error sampling with sampleRate for non-critical errors
3. Configure dynamic transaction sampling with tracesSampler
4. Add ignoreErrors patterns for common noisy errors
5. Enable deduplication integration to reduce duplicates
6. Apply client-side filtering in beforeSend hook
7. Set project rate limits via API or dashboard
8. Enable inbound filters for legacy browsers and extensions
9. Monitor event volume and set up quota alerts
10. Adjust sample rates based on billing period usage

## Output
- Optimized sample rates configured
- Rate limiting rules applied
- Event filtering implemented
- Quota usage monitoring setup

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `429 Too Many Requests` | Rate limit exceeded | Implement client-side sampling |
| `Quota exhausted` | Event volume too high | Enable inbound filters and reduce sample rates |
| `Critical errors missed` | Over-aggressive filtering | Always capture fatal errors at 100% |
| `Billing spike` | Sudden traffic increase | Set up spend alerts and rate limits |

## Examples

**Example: Handle Rate Limit Hit**
Request: "We're getting 429 errors from Sentry"
Result: Implement adaptive sampling, add ignoreErrors patterns, enable server-side inbound filters.

## Resources
- [Sentry Quota Management](https://docs.sentry.io/product/accounts/quotas/)
- [Sampling Strategies](https://docs.sentry.io/platforms/javascript/configuration/sampling/)
