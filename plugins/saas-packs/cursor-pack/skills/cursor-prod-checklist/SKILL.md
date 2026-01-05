---
name: "cursor-prod-checklist"
description: |
  Execute production readiness checklist for Cursor IDE setup. Triggers on "cursor production",
  "cursor ready", "cursor checklist", "optimize cursor setup". Use when working with cursor prod checklist functionality. Trigger with phrases like "cursor prod checklist", "cursor checklist", "cursor".
allowed-tools: "Read, Write, Edit, Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Cursor Production Readiness Checklist

## Overview

This skill provides a comprehensive production readiness checklist for Cursor IDE setup. It covers authentication, configuration, security, performance optimization, and team standards to ensure your Cursor environment is properly configured for professional use.

## Initial Setup

### Authentication & Licensing
```
[ ] Signed into Cursor account
[ ] Subscription tier confirmed (Free/Pro/Business)
[ ] API keys configured (if using own)
[ ] Team seats assigned (if Business)
[ ] SSO configured (if Enterprise)
```

### Core Configuration
```
[ ] Default AI model selected
[ ] Completion model configured
[ ] Chat model configured
[ ] Composer model configured
[ ] Privacy mode set appropriately
```

## Project Configuration

### .cursorrules Setup
```
[ ] .cursorrules file created
[ ] Coding standards defined
[ ] Framework-specific rules added
[ ] Team conventions documented
[ ] Examples included for complex patterns
```

### Sample .cursorrules
```yaml
# .cursorrules
project: my-app
language: typescript
framework: nextjs

rules:
  - Use TypeScript strict mode
  - Prefer functional components
  - Use Tailwind for styling
  - Write tests for all business logic
  - Use async/await over callbacks
  - Handle all error cases explicitly

naming:
  components: PascalCase
  functions: camelCase
  constants: SCREAMING_SNAKE_CASE
  files: kebab-case

imports:
  order:
    - react
    - next
    - third-party
    - @/components
    - @/lib
    - relative

testing:
  framework: vitest
  coverage: 80%
```

### Indexing Configuration
```
[ ] .cursorignore configured
[ ] Large directories excluded
[ ] Build outputs excluded
[ ] Indexing completed successfully
[ ] @codebase queries working
```

## Performance Optimization

### Editor Performance
```
[ ] Unused extensions disabled
[ ] File watcher exclusions set
[ ] Max open editors limited
[ ] Search exclusions configured

Settings:
{
  "files.watcherExclude": {
    "**/node_modules/**": true,
    "**/.git/**": true,
    "**/dist/**": true
  },
  "search.exclude": {
    "**/node_modules": true,
    "**/dist": true
  },
  "editor.maxTokenizationLineLength": 10000
}
```

### AI Performance
```
[ ] Appropriate models selected for tasks
[ ] Completion delay tuned
[ ] Context management optimized
[ ] Rate limits understood
```

## Security Configuration

### Privacy Settings
```
[ ] Privacy mode configured (on/off per need)
[ ] Sensitive files excluded from AI
[ ] API keys secured
[ ] Team data policies reviewed

Privacy Mode:
- ON: Code not sent to AI (limited features)
- OFF: Full AI features (code processed externally)
```

### Sensitive File Handling
```
# .cursorignore - security sensitive
.env*
*.pem
*.key
secrets/
credentials/
config/production.json
```

## Team Configuration (Business/Enterprise)

### Team Standards
```
[ ] Shared .cursorrules in repo
[ ] Team keybindings documented
[ ] Common extensions list
[ ] AI usage guidelines
[ ] Code review process updated
```

### Admin Setup
```
[ ] Team members invited
[ ] Roles assigned
[ ] Usage limits set
[ ] Billing configured
[ ] Analytics enabled
```

## Workflow Integration

### Git Integration
```
[ ] Git commands accessible
[ ] Pre-commit hooks compatible
[ ] AI commit messages configured
[ ] Branch protection understood
```

### CI/CD Awareness
```
[ ] CI config files indexed
[ ] .cursorrules includes CI patterns
[ ] Build scripts documented
[ ] Deployment patterns known to AI
```

## Backup & Recovery

### Settings Backup
```
[ ] Settings Sync enabled (optional)
[ ] .cursorrules in version control
[ ] Keybindings exported
[ ] Extension list documented
```

### Recovery Plan
```
[ ] Know how to reset Cursor
[ ] Backup extension list
[ ] Document custom settings
[ ] Test clean install procedure
```

## Verification Tests

### AI Features Test
```
[ ] Tab completion working
[ ] Chat responding
[ ] Composer creates files
[ ] @codebase returns results
[ ] @file mentions work
```

### Performance Test
```
[ ] Startup time acceptable (< 10s)
[ ] No UI lag during editing
[ ] Completions appear quickly (< 500ms)
[ ] Memory usage reasonable (< 2GB)
```

## Documentation

### For New Team Members
```
[ ] Setup guide written
[ ] .cursorrules explained
[ ] Key shortcuts documented
[ ] AI usage best practices
[ ] Troubleshooting guide
```

### For Ongoing Use
```
[ ] Update .cursorrules with new patterns
[ ] Document discovered tips
[ ] Track model preferences
[ ] Note effective prompts
```

## Maintenance Schedule

### Weekly
```
[ ] Clear unused chat history
[ ] Review completion accuracy
[ ] Check for Cursor updates
```

### Monthly
```
[ ] Review .cursorrules effectiveness
[ ] Optimize indexing exclusions
[ ] Audit extension list
[ ] Check subscription usage
```

### Quarterly
```
[ ] Full settings review
[ ] Team feedback collection
[ ] Evaluate new models/features
[ ] Update documentation
```

## Prerequisites

- Cursor IDE installed
- Project workspace ready for configuration
- Team alignment on coding standards
- Understanding of Cursor features and settings

## Instructions

1. Complete authentication and licensing setup
2. Create and configure .cursorrules file
3. Set up .cursorignore for indexing exclusions
4. Configure security and privacy settings
5. Verify all AI features working correctly
6. Document setup for team onboarding

## Output

- Production-ready Cursor configuration
- Optimized AI settings for project
- Security-compliant setup
- Documented team standards
- Maintenance schedule established

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| AI features not working | Missing authentication | Sign in and verify subscription |
| Poor completion quality | Missing .cursorrules | Create comprehensive rules file |
| Indexing issues | Missing .cursorignore | Add exclusions for large directories |
| Performance problems | Suboptimal settings | Review and apply performance checklist |

## Examples

**Example: New Project Setup**
Request: "Set up Cursor for production use on new TypeScript project"
Result: Complete configuration with .cursorrules, .cursorignore, settings, and verified features

**Example: Team Onboarding Checklist**
Request: "Create onboarding checklist for new team member"
Result: Step-by-step setup guide with verification tests

## Resources

- [Cursor Setup Guide](https://cursor.com/docs/setup)
- [Enterprise Configuration](https://cursor.com/docs/enterprise)
- [Security Best Practices](https://cursor.com/security)
