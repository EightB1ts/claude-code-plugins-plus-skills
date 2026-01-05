---
name: "cursor-team-setup"
description: |
  Configure set up Cursor for teams and organizations. Triggers on "cursor team",
  "cursor organization", "cursor business", "cursor enterprise setup". Use when working with cursor team setup functionality. Trigger with phrases like "cursor team setup", "cursor setup", "cursor".
allowed-tools: "Read, Write, Edit, Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Cursor Team & Organization Setup

## Overview

This skill guides you through setting up Cursor for teams and organizations. It covers plan selection, member management, shared configurations, onboarding workflows, and team analytics to ensure consistent Cursor usage across your organization.

## Team Plans Overview

### Plan Comparison
```
Free (Individual):
- 2000 completions/month
- 50 slow premium requests
- Basic features

Pro ($20/user/month):
- Unlimited completions
- 500 fast premium requests
- Priority support
- All AI models

Business ($40/user/month):
- Everything in Pro
- Admin dashboard
- Team management
- Usage analytics
- SSO support
- Priority support

Enterprise (Custom):
- Everything in Business
- Custom contracts
- Dedicated support
- SLA guarantees
- Custom security
- On-premise options
```

## Setting Up Team Account

### Initial Setup
```
1. Go to cursor.com/settings/team
2. Click "Create Team"
3. Enter team name and details
4. Choose plan (Business/Enterprise)
5. Add billing information
6. Invite team members
```

### Team Structure
```
Organization
├── Team 1 (Engineering)
│   ├── Admin
│   ├── Member
│   └── Member
├── Team 2 (Design)
│   ├── Admin
│   └── Member
└── Billing Admin
```

## Member Management

### Inviting Members
```
Admin Dashboard > Members > Invite

Options:
- Email invitation
- Domain-based auto-join
- SSO provisioning (Enterprise)

Invite by email:
1. Enter email addresses
2. Select role (Admin/Member)
3. Send invitations
4. Track pending invites
```

### Role Management
```
Roles:

Owner:
- Full account control
- Billing management
- Delete organization

Admin:
- Manage members
- Configure settings
- View analytics
- Cannot delete org

Member:
- Use all features
- No admin access
- Cannot invite users
```

### Removing Members
```
Admin Dashboard > Members > Select User > Remove

Considerations:
- Immediate access revocation
- Settings preserved for 30 days
- Can be reinvited later
- Billing adjusts automatically
```

## Team Configuration

### Shared Settings
```json
// Recommended team settings (share via repo)

// .vscode/settings.json
{
  // Cursor defaults for team
  "cursor.chat.defaultModel": "gpt-4-turbo",
  "cursor.completion.model": "gpt-3.5-turbo",

  // Formatting consistency
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  // Disable conflicting features
  "editor.suggest.showInlineDetails": false
}
```

### Team .cursorrules
```yaml
# .cursorrules (committed to repo)

team: engineering
project: main-product

standards:
  # Coding standards
  - TypeScript strict mode required
  - ESLint + Prettier formatting
  - Conventional commits

  # Documentation
  - JSDoc for public functions
  - README for each module
  - ADRs for decisions

  # Testing
  - Unit tests for business logic
  - Integration tests for APIs
  - 80% coverage minimum

patterns:
  # Follow company patterns
  - See @docs/patterns.md
  - Use shared components from @ui
```

## Onboarding New Members

### Onboarding Checklist
```
[ ] Add to Cursor team
[ ] Send invite email
[ ] Share setup guide
[ ] Add to code repository
[ ] Install recommended extensions
[ ] Configure local settings
[ ] Sync .cursorrules
[ ] Test AI features work
[ ] Schedule training session
```

### Setup Documentation
```markdown
# Cursor Setup Guide

## 1. Accept Invitation
Click link in invitation email to join team.

## 2. Install Cursor
Download from cursor.com for your OS.

## 3. Sign In
Sign in with your work email.

## 4. Clone Repository
git clone [repo-url]
cd project

## 5. Verify Setup
- Open project in Cursor
- Wait for indexing to complete
- Test: Cmd+L and ask "What is this project?"

## 6. Extensions
Install recommended extensions:
Cmd+Shift+P > "Show Recommended Extensions"
```

## Team Workflows

### Code Review with Cursor
```
Team workflow:
1. Developer creates PR
2. Reviewer opens in Cursor
3. Uses @git diff for AI review
4. Comments with AI suggestions
5. Developer addresses feedback

AI-assisted review:
"@git diff main..feature/auth
Review this PR for:
- Security issues
- Performance concerns
- Code style violations
- Missing tests"
```

### Pair Programming
```
With Cursor, less need for real-time pairing:

Async collaboration:
1. Developer writes initial code
2. Uses Composer for scaffolding
3. Commits with clear messages
4. Reviewer uses AI to understand
5. AI-assisted feedback

When to still pair:
- Complex architecture decisions
- Knowledge transfer
- Onboarding new members
```

## Team Analytics

### Usage Dashboard
```
Admin Dashboard > Analytics

Metrics available:
- Total completions used
- Chat requests per user
- Model usage breakdown
- Active users per day
- Feature adoption rates
```

### Monitoring Usage
```
Track team efficiency:
- Completions accepted rate
- Time saved estimates
- Most used features
- Common error patterns

Adjust based on data:
- Identify training needs
- Optimize model selection
- Improve .cursorrules
```

## Cost Management

### Billing Overview
```
Admin Dashboard > Billing

View:
- Current plan details
- User count and cost
- Usage against limits
- Billing history
- Upcoming charges
```

### Optimizing Costs
```
Strategies:
1. Right-size team seats
   - Remove inactive users
   - Use viewer roles where appropriate

2. Optimize model usage
   - Use GPT-3.5 for simple tasks
   - Reserve GPT-4 for complex work

3. Training
   - Better prompts = fewer retries
   - Proper .cursorrules = better results
```

## Support Resources

### Getting Help
```
Priority by plan:
- Free: Community forums
- Pro: Email support
- Business: Priority support
- Enterprise: Dedicated support

Resources:
- docs.cursor.com
- Discord community
- GitHub discussions
- Support tickets (paid plans)
```

### Training Resources
```
For new team members:
1. Official documentation
2. Internal setup guide
3. .cursorrules walkthrough
4. Hands-on practice session
5. Ongoing tips sharing
```

## Security Considerations

### Team Security
```
[ ] Enable SSO (Enterprise)
[ ] Enforce 2FA
[ ] Regular access audits
[ ] Offboarding process
[ ] API key rotation
[ ] Privacy mode policies
```

### Data Handling
```
Understand data flow:
- Code sent to AI for processing
- Not stored long-term by Cursor
- Privacy mode for sensitive code
- Audit trail available
```

## Prerequisites

- Cursor Business or Enterprise subscription
- Admin access to Cursor organization
- Team roster and role assignments planned
- Billing and payment method configured

## Instructions

1. Create team at cursor.com/settings/team
2. Configure team plan and billing
3. Invite team members with appropriate roles
4. Set up shared .cursorrules in repository
5. Configure team analytics and usage tracking
6. Create onboarding documentation

## Output

- Configured team account with all members
- Role-based access control
- Shared configuration and standards
- Usage analytics and cost tracking
- Onboarding process documented

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Invitation not received | Email filtering or wrong address | Resend invite, check spam folder |
| Cannot assign role | Insufficient permissions | Contact organization owner |
| Usage over budget | Unexpected usage patterns | Review analytics, set usage guidelines |
| SSO not working | Configuration mismatch | Verify IdP settings match Cursor config |

## Examples

**Example: Small Team Setup**
Request: "Set up Cursor for a 10-person engineering team"
Result: Team created with roles, shared configuration, and onboarding guide

**Example: Onboarding New Developer**
Request: "Onboard new team member to our Cursor setup"
Result: Complete checklist from invitation to verified working setup

## Resources

- [Cursor Team Documentation](https://cursor.com/docs/teams)
- [Admin Dashboard Guide](https://cursor.com/docs/admin)
- [Team Best Practices](https://cursor.com/blog/teams)
