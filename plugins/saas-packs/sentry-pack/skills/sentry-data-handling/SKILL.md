---
name: sentry-data-handling
description: |
  Manage sensitive data properly in Sentry.
  Use when configuring PII scrubbing, data retention,
  GDPR compliance, or data security settings.
  Trigger with phrases like "sentry pii", "sentry gdpr",
  "sentry data privacy", "scrub sensitive data sentry".
allowed-tools: Read, Write, Edit, Grep
version: 1.0.0
license: MIT
author: Jeremy Longshore <jeremy@intentsolutions.io>
---

# Sentry Data Handling

## Overview
Configure Sentry to handle sensitive data properly and maintain compliance.

## PII Scrubbing

### Built-in Data Scrubbing
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  // Enable server-side scrubbing
  sendDefaultPii: false, // Default

  // Client-side scrubbing
  beforeSend(event) {
    // Remove sensitive headers
    if (event.request?.headers) {
      delete event.request.headers['Authorization'];
      delete event.request.headers['Cookie'];
      delete event.request.headers['X-API-Key'];
    }
    return event;
  },
});
```

### Custom Data Scrubbing
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  beforeSend(event, hint) {
    // Scrub email addresses
    if (event.user?.email) {
      event.user.email = '[REDACTED]';
    }

    // Scrub credit card numbers
    const ccRegex = /\b\d{4}[-\s]?\d{4}[-\s]?\d{4}[-\s]?\d{4}\b/g;
    if (event.message) {
      event.message = event.message.replace(ccRegex, '[CREDIT_CARD]');
    }

    // Scrub phone numbers
    const phoneRegex = /\b\d{3}[-.]?\d{3}[-.]?\d{4}\b/g;
    if (event.extra) {
      event.extra = JSON.parse(
        JSON.stringify(event.extra).replace(phoneRegex, '[PHONE]')
      );
    }

    return event;
  },
});
```

### Scrub Specific Fields
```typescript
function scrubSensitiveData(obj: Record<string, unknown>): Record<string, unknown> {
  const sensitiveKeys = [
    'password', 'secret', 'token', 'apiKey', 'api_key',
    'ssn', 'social_security', 'credit_card', 'cvv',
  ];

  return Object.entries(obj).reduce((acc, [key, value]) => {
    if (sensitiveKeys.some(k => key.toLowerCase().includes(k))) {
      acc[key] = '[FILTERED]';
    } else if (typeof value === 'object' && value !== null) {
      acc[key] = scrubSensitiveData(value as Record<string, unknown>);
    } else {
      acc[key] = value;
    }
    return acc;
  }, {} as Record<string, unknown>);
}

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  beforeSend(event) {
    if (event.extra) {
      event.extra = scrubSensitiveData(event.extra);
    }
    return event;
  },
});
```

## Server-Side Data Scrubbing

### Sentry Dashboard Settings
1. Project Settings → Security & Privacy
2. Enable "Data Scrubber"
3. Configure scrubbing rules:
   - Default fields (passwords, tokens, etc.)
   - Custom field patterns
   - IP address anonymization

### Advanced Data Scrubbing Rules
```json
{
  "applications": {
    "scrubData": true,
    "scrubDefaults": true,
    "sensitiveFields": [
      "password",
      "secret",
      "token",
      "apiKey",
      "ssn"
    ],
    "safeFields": [
      "username",
      "email_domain"
    ],
    "scrubIpAddresses": true
  }
}
```

## GDPR Compliance

### Right to Erasure (Delete User Data)
```bash
# Delete all events for a user
curl -X DELETE \
  -H "Authorization: Bearer $SENTRY_AUTH_TOKEN" \
  "https://sentry.io/api/0/projects/$ORG/$PROJECT/users/$USER_ID/"
```

### Programmatic User Data Deletion
```typescript
async function deleteUserData(userId: string) {
  const response = await fetch(
    `https://sentry.io/api/0/projects/${ORG}/${PROJECT}/users/${userId}/`,
    {
      method: 'DELETE',
      headers: {
        'Authorization': `Bearer ${SENTRY_AUTH_TOKEN}`,
      },
    }
  );
  return response.ok;
}
```

### User Consent Handling
```typescript
function initSentryWithConsent(hasConsent: boolean) {
  Sentry.init({
    dsn: hasConsent ? process.env.SENTRY_DSN : undefined,

    // Don't send any PII
    sendDefaultPii: false,

    // Anonymize user
    beforeSend(event) {
      if (event.user) {
        event.user = {
          id: hashUserId(event.user.id), // Pseudonymized ID
          // Remove all other user fields
        };
      }
      return event;
    },
  });
}
```

## Data Retention

### Configure Retention Period
- Organization Settings → Data Retention
- Options: 30, 60, 90 days (depends on plan)
- Shorter retention = better compliance, less storage

### Automatic Data Cleanup
```bash
# Events are automatically deleted after retention period
# No manual action required
```

## IP Address Handling

### Disable IP Collection
```typescript
Sentry.init({
  dsn: process.env.SENTRY_DSN,

  // Don't store IP addresses
  sendDefaultPii: false,

  // Or manually anonymize
  beforeSend(event) {
    if (event.user?.ip_address) {
      // Anonymize to /24 subnet
      const parts = event.user.ip_address.split('.');
      event.user.ip_address = `${parts[0]}.${parts[1]}.${parts[2]}.0`;
    }
    return event;
  },
});
```

### Server-Side IP Anonymization
Project Settings → Security & Privacy → "Prevent Storing of IP Addresses"

## Compliance Checklist

### GDPR Requirements
```
□ Data scrubbing enabled
□ IP anonymization enabled
□ User consent captured (if required)
□ Data retention policy set
□ Right to erasure process documented
□ Data processing agreement with Sentry
```

### HIPAA Considerations
```
□ Business Associate Agreement (BAA) with Sentry
□ PHI scrubbing configured
□ Audit logging enabled
□ Access controls configured
□ Encryption verified (Sentry uses TLS)
```

### PCI-DSS Requirements
```
□ Card data never sent to Sentry
□ Card numbers scrubbed in beforeSend
□ CVV/CVC never logged
□ Audit trail maintained
```

## Testing Data Scrubbing

```typescript
// Test that sensitive data is scrubbed
describe('Sentry data scrubbing', () => {
  it('should scrub credit card numbers', () => {
    const event = {
      message: 'Payment failed for card 4111-1111-1111-1111',
    };
    const scrubbed = beforeSend(event);
    expect(scrubbed.message).not.toContain('4111');
    expect(scrubbed.message).toContain('[CREDIT_CARD]');
  });
});
```

## Output
- PII scrubbing rules configured
- GDPR compliance documentation
- Data retention policies implemented
- User consent handling code

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `PII still appearing in events` | Scrubbing rules incomplete | Add patterns to `beforeSend` and server-side rules |
| `User deletion failed` | Invalid user ID | Verify user ID format matches Sentry records |
| `Data retention not applied` | Plan limitation | Check organization settings and plan features |
| `Consent tracking broken` | SDK initialized before consent | Use conditional DSN based on consent state |

## Examples

**Example: GDPR-Compliant Setup**
Request: "Configure Sentry for GDPR compliance"
Result: PII scrubbing enabled, IP anonymization active, consent-based initialization, data deletion endpoint implemented.

## Prerequisites

- Sentry project with admin access
- Compliance requirements documented (GDPR, HIPAA, PCI-DSS)
- List of sensitive data patterns to scrub
- Understanding of data retention requirements

## Instructions

1. Enable server-side data scrubbing in Project Settings > Security & Privacy
2. Configure client-side scrubbing in beforeSend hook for PII fields
3. Add custom scrubbing rules for credit cards, SSNs, and email patterns
4. Disable sendDefaultPii in SDK configuration
5. Configure IP address anonymization or disable IP collection
6. Set appropriate data retention period in organization settings
7. Implement user consent handling for GDPR compliance
8. Document right to erasure process with API deletion endpoint
9. Run tests to verify sensitive data is properly scrubbed
10. Complete compliance checklist for applicable regulations

## Resources
- [Sentry Data Privacy](https://docs.sentry.io/product/data-management-settings/data-privacy/)
- [GDPR Compliance](https://sentry.io/legal/gdpr/)
- [Data Scrubbing](https://docs.sentry.io/product/data-management-settings/scrubbing/)
