---
name: sentry-multi-env-setup
description: |
  Configure Sentry across multiple environments.
  Use when setting up Sentry for dev/staging/production,
  managing environment-specific configurations, or isolating data.
  Trigger with phrases like "sentry environments", "sentry staging setup",
  "multi-environment sentry", "sentry dev vs prod".
allowed-tools: Read, Write, Edit, Grep
version: 1.0.0
license: MIT
author: Jeremy Longshore <jeremy@intentsolutions.io>
---

# Sentry Multi-Environment Setup

## Overview
Configure Sentry properly across development, staging, and production environments.

## Environment Configuration

### Basic Setup
```typescript
import * as Sentry from '@sentry/node';

const environment = process.env.NODE_ENV || 'development';

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: environment,

  // Environment-specific settings
  enabled: environment !== 'development',
  debug: environment === 'development',
});
```

### Environment-Specific Sample Rates
```typescript
const sampleRates: Record<string, { errors: number; traces: number }> = {
  development: { errors: 1.0, traces: 1.0 },
  staging: { errors: 1.0, traces: 0.5 },
  production: { errors: 1.0, traces: 0.1 },
};

const rates = sampleRates[environment] || sampleRates.production;

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment,
  sampleRate: rates.errors,
  tracesSampleRate: rates.traces,
});
```

## Project Structure Options

### Option 1: Single Project, Multiple Environments
```
Organization: mycompany
└── Project: myapp
    ├── Environment: development
    ├── Environment: staging
    └── Environment: production
```

**Pros:** Unified view, easier correlation
**Cons:** Noisy in development, shared quotas

### Option 2: Separate Projects Per Environment
```
Organization: mycompany
├── Project: myapp-development
├── Project: myapp-staging
└── Project: myapp-production
```

**Pros:** Clean separation, independent quotas
**Cons:** Multiple DSNs to manage

### Option 3: Hybrid (Recommended)
```
Organization: mycompany
├── Project: myapp-production    # Production only
└── Project: myapp-nonprod       # Dev + Staging
```

## DSN Management

### Environment Variables
```bash
# .env.development
SENTRY_DSN=https://xxx@sentry.io/dev-project

# .env.staging
SENTRY_DSN=https://xxx@sentry.io/staging-project

# .env.production
SENTRY_DSN=https://xxx@sentry.io/prod-project
```

### Conditional DSN Loading
```typescript
function getSentryDSN(): string | undefined {
  if (process.env.NODE_ENV === 'development') {
    return undefined; // Disable in development
  }
  return process.env.SENTRY_DSN;
}

Sentry.init({
  dsn: getSentryDSN(),
  environment: process.env.NODE_ENV,
});
```

## Filtering by Environment

### In Sentry Dashboard
1. Go to Issues or Performance
2. Use environment filter dropdown
3. Select specific environment

### Programmatic Filtering
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,

  beforeSend(event) {
    // Add environment context
    event.tags = {
      ...event.tags,
      deploy_region: process.env.DEPLOY_REGION,
      feature_flags: process.env.FEATURE_FLAGS,
    };
    return event;
  },
});
```

## Alert Rules by Environment

### Production-Only Alerts
```yaml
# Alert only for production errors
conditions:
  - type: event.environment
    value: production
  - type: event.level
    value: error
actions:
  - type: notify_email
    targetIdentifier: oncall@company.com
```

### Staging Alerts (Lower Priority)
```yaml
conditions:
  - type: event.environment
    value: staging
actions:
  - type: slack
    channel: #staging-alerts
```

## Best Practices

1. **Never use production DSN in development**
2. **Set appropriate sample rates per environment**
3. **Use environment tags consistently**
4. **Configure alerts per environment**
5. **Disable or reduce noise in development**

## Prerequisites

- Environment naming convention defined
- DSN management strategy
- Sample rate requirements per environment
- Alert routing per environment

## Instructions

1. Set environment option in SDK init to match deployment target
2. Configure environment-specific sample rates (100% dev, 10% prod)
3. Choose project structure (single with environments vs separate projects)
4. Set up separate DSNs per environment in environment variables
5. Implement conditional DSN loading to disable in development
6. Add environment context and tags in beforeSend hook
7. Configure environment filters in Sentry dashboard
8. Create production-only alert rules with appropriate conditions
9. Set up lower-priority staging alerts for development feedback
10. Document environment configuration and best practices for team

## Output
- Environment-specific Sentry configuration
- Separate or shared projects configured
- Environment-based alert rules
- Sample rates optimized per environment

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `Dev errors in prod dashboard` | Shared DSN | Use separate DSN per environment or disable in dev |
| `Environment filter not working` | Environment not set | Verify `environment` option in SDK init |
| `Staging alerts overwhelming` | Same alert rules as prod | Configure environment-specific alert conditions |
| `Sample rates inconsistent` | Hard-coded values | Use environment-based configuration object |

## Examples

**Example: Three-Environment Setup**
Request: "Configure Sentry for dev, staging, and production"
Result: Single project with environment tags, 100% sampling in dev/staging, 10% in production, alerts only for production.

## Resources
- [Sentry Environments](https://docs.sentry.io/product/sentry-basics/environments/)
- [Filtering Events](https://docs.sentry.io/platforms/javascript/configuration/filtering/)
