---
name: "cursor-install-auth"
description: |
  Install Cursor IDE and configure authentication. Triggers on "install cursor",
  "setup cursor", "cursor authentication", "cursor login", "cursor license". Use when working with cursor install auth functionality. Trigger with phrases like "cursor install auth", "cursor auth", "cursor".
allowed-tools: "Read, Write, Edit, Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Cursor Installation & Authentication

## Overview

This skill guides you through installing Cursor IDE and configuring authentication. It covers installation on macOS, Linux, and Windows, plus sign-in options, license activation, and API key configuration for custom model access.

## Installation Methods

### macOS
```bash
# Download from cursor.com or use Homebrew
brew install --cask cursor

# Verify installation
cursor --version
```

### Linux
```bash
# Download AppImage from cursor.com
chmod +x cursor-*.AppImage
./cursor-*.AppImage

# Or extract and install
./cursor-*.AppImage --appimage-extract
sudo mv squashfs-root /opt/cursor
sudo ln -s /opt/cursor/cursor /usr/local/bin/cursor
```

### Windows
```powershell
# Download installer from cursor.com
# Or use winget
winget install Cursor.Cursor
```

## Authentication Setup

### Sign In Options
1. **GitHub** - Recommended for developers
2. **Google** - Quick sign-in
3. **Email** - Traditional email/password

### First Launch Authentication
```
1. Launch Cursor
2. Click "Sign In" in bottom-left
3. Choose authentication method
4. Complete browser-based OAuth
5. Return to Cursor - automatically authenticated
```

## License Activation

### Free Tier
- 2000 completions/month
- 50 slow premium requests/month
- Basic AI features

### Pro Tier ($20/month)
- Unlimited completions
- 500 fast premium requests/month
- Priority support

### Business Tier ($40/user/month)
- Everything in Pro
- Admin dashboard
- SSO support
- Usage analytics

## API Key Configuration

### Using Your Own API Keys
```json
// Settings > Models > API Keys
{
  "openai": "sk-...",
  "anthropic": "sk-ant-...",
  "azure": {
    "apiKey": "...",
    "endpoint": "https://your-resource.openai.azure.com"
  }
}
```

### Model Selection with Custom Keys
- OpenAI: GPT-4, GPT-4 Turbo, GPT-3.5 Turbo
- Anthropic: Claude 3.5 Sonnet, Claude 3 Opus
- Azure OpenAI: Your deployed models

## Verification Checklist

```
[ ] Cursor installed and launches
[ ] Signed in with preferred method
[ ] License tier confirmed (Free/Pro/Business)
[ ] API keys configured (if using own keys)
[ ] Test completion working
[ ] Settings synced (if applicable)
```

## Common Issues

### "Authentication Failed"
- Clear browser cache and retry
- Check firewall/proxy settings
- Try different auth method

### "License Not Found"
- Sign out and sign back in
- Check cursor.com account status
- Contact support if persists

### "API Key Invalid"
- Verify key hasn't expired
- Check key has correct permissions
- Ensure correct model access

## Prerequisites

- Supported operating system (macOS, Linux, or Windows)
- Internet connection for download and authentication
- Admin rights for installation (if required)
- Optional: API keys for custom model access

## Instructions

1. Download Cursor from cursor.com or package manager
2. Install using platform-specific method
3. Launch Cursor and click "Sign In"
4. Choose authentication method (GitHub, Google, Email)
5. Complete OAuth flow in browser
6. Return to Cursor - automatically authenticated

## Output

- Installed Cursor IDE
- Authenticated user account
- Activated license (Free, Pro, or Business)
- Ready-to-use AI features

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Installation failed | Permissions or disk space | Run as admin, free disk space |
| Authentication failed | Browser or network issue | Clear cookies, try different auth method |
| License not found | Account not synced | Sign out and back in, verify subscription |
| API key invalid | Expired or wrong format | Regenerate key, check permissions |

## Examples

**Example: macOS Installation**
Request: "Install Cursor on macOS"
Result: Download DMG, drag to Applications, launch and sign in

**Example: Linux Installation**
Request: "Install Cursor on Ubuntu"
Result: Download AppImage, chmod +x, run and authenticate

## Resources

- [Cursor Download](https://cursor.com/download)
- [System Requirements](https://cursor.com/docs/requirements)
- [Cursor Pricing](https://cursor.com/pricing)
- [Account Settings](https://cursor.com/settings)
