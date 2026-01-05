---
name: "cursor-keybindings"
description: |
  Manage master Cursor keyboard shortcuts and customize keybindings. Triggers on "cursor shortcuts",
  "cursor keybindings", "cursor keyboard", "cursor hotkeys", "cursor commands". Use when working with cursor keybindings functionality. Trigger with phrases like "cursor keybindings", "cursor keybindings", "cursor".
allowed-tools: "Read, Write, Edit, Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Cursor Keybindings & Shortcuts

## Overview

This skill helps you master Cursor keyboard shortcuts and customize keybindings. It provides a complete reference for AI-specific shortcuts, standard editor commands, and guidance on resolving conflicts with Vim mode or other extensions.

## AI-Specific Shortcuts

### Core AI Commands
| Action | Mac | Windows/Linux | Description |
|--------|-----|---------------|-------------|
| AI Chat | Cmd+L | Ctrl+L | Open chat panel |
| New Chat | Cmd+Shift+L | Ctrl+Shift+L | Start fresh conversation |
| Composer | Cmd+I | Ctrl+I | Multi-file AI edits |
| Inline Edit | Cmd+K | Ctrl+K | Quick AI edit on selection |
| Accept Completion | Tab | Tab | Accept ghost text |
| Reject Completion | Esc | Esc | Dismiss suggestion |
| Next Suggestion | Alt+] | Alt+] | Cycle completions |
| Previous Suggestion | Alt+[ | Alt+[ | Cycle back |
| Trigger Completion | Ctrl+Space | Ctrl+Space | Force suggestion |

### Completion Control
| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| Accept Word | Ctrl+Right | Ctrl+Right |
| Accept Line | Cmd+Right | End |
| Partial Accept | Hold Tab | Hold Tab |

## Standard Editor Shortcuts

### File Operations
| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| New File | Cmd+N | Ctrl+N |
| Open File | Cmd+O | Ctrl+O |
| Save | Cmd+S | Ctrl+S |
| Save All | Cmd+Alt+S | Ctrl+K S |
| Close Tab | Cmd+W | Ctrl+W |
| Reopen Closed | Cmd+Shift+T | Ctrl+Shift+T |

### Navigation
| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| Quick Open | Cmd+P | Ctrl+P |
| Go to Symbol | Cmd+Shift+O | Ctrl+Shift+O |
| Go to Line | Cmd+G | Ctrl+G |
| Go to Definition | F12 | F12 |
| Peek Definition | Alt+F12 | Alt+F12 |
| Find References | Shift+F12 | Shift+F12 |
| Command Palette | Cmd+Shift+P | Ctrl+Shift+P |

### Editing
| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| Cut Line | Cmd+X | Ctrl+X |
| Copy Line | Cmd+C | Ctrl+C |
| Move Line Up | Alt+Up | Alt+Up |
| Move Line Down | Alt+Down | Alt+Down |
| Duplicate Line | Cmd+Shift+D | Ctrl+Shift+D |
| Delete Line | Cmd+Shift+K | Ctrl+Shift+K |
| Comment Line | Cmd+/ | Ctrl+/ |
| Block Comment | Cmd+Shift+/ | Ctrl+Shift+/ |

### Multi-Cursor
| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| Add Cursor | Alt+Click | Alt+Click |
| Add Cursor Above | Cmd+Alt+Up | Ctrl+Alt+Up |
| Add Cursor Below | Cmd+Alt+Down | Ctrl+Alt+Down |
| Select All Occurrences | Cmd+Shift+L | Ctrl+Shift+L |
| Add Next Occurrence | Cmd+D | Ctrl+D |

## Customizing Keybindings

### Access Keybindings
```
Cmd+K Cmd+S (Mac)
Ctrl+K Ctrl+S (Windows/Linux)

Or: Command Palette > "Preferences: Open Keyboard Shortcuts"
```

### Custom Keybinding Example
```json
// keybindings.json
[
  {
    "key": "cmd+shift+c",
    "command": "cursor.newChat",
    "when": "editorTextFocus"
  },
  {
    "key": "cmd+shift+g",
    "command": "cursor.generateCode",
    "when": "editorTextFocus"
  }
]
```

### Cursor-Specific Commands
```json
// Available cursor.* commands
"cursor.newChat"
"cursor.toggleChat"
"cursor.acceptCompletion"
"cursor.rejectCompletion"
"cursor.triggerCompletion"
"cursor.openComposer"
"cursor.inlineEdit"
```

## Vim Mode Keybindings

### Enable Vim Mode
```
Settings > Extensions > Vim
```

### Cursor + Vim Recommended
```json
// settings.json
{
  "vim.useCtrlKeys": false,  // Preserve Cursor AI shortcuts
  "vim.handleKeys": {
    "<C-l>": false,  // Allow Cursor chat
    "<C-k>": false,  // Allow Cursor inline edit
    "<C-i>": false   // Allow Cursor composer
  }
}
```

## Shortcut Cheat Sheet

### Quick Reference Card
```
┌─────────────────────────────────────────────────────┐
│  CURSOR AI SHORTCUTS                                │
├─────────────────────────────────────────────────────┤
│  Chat:     Cmd+L      │  Composer:    Cmd+I        │
│  Inline:   Cmd+K      │  New Chat:    Cmd+Shift+L  │
│  Accept:   Tab        │  Reject:      Esc          │
├─────────────────────────────────────────────────────┤
│  NAVIGATION                                         │
├─────────────────────────────────────────────────────┤
│  Quick Open:  Cmd+P   │  Command:     Cmd+Shift+P  │
│  Go to Def:   F12     │  Find Refs:   Shift+F12    │
├─────────────────────────────────────────────────────┤
│  EDITING                                            │
├─────────────────────────────────────────────────────┤
│  Comment:     Cmd+/   │  Duplicate:   Cmd+Shift+D  │
│  Multi-Sel:   Cmd+D   │  Move Line:   Alt+Up/Down  │
└─────────────────────────────────────────────────────┘
```

## Prerequisites

- Cursor IDE installed
- Access to Keyboard Shortcuts editor
- Understanding of modifier keys (Cmd/Ctrl, Alt/Option, Shift)
- Optional: Vim mode extension if using Vim bindings

## Instructions

1. Open Keyboard Shortcuts (Cmd+K Cmd+S)
2. Search for the command to rebind
3. Click the pencil icon to edit
4. Press your new key combination
5. Resolve any conflicts shown
6. Save and test the new binding

## Output

- Customized keyboard shortcuts
- Resolved keybinding conflicts
- Vim mode compatibility (if configured)
- Personalized workflow efficiency

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Shortcut not working | Conflict with extension or system | Check for conflicts in Keyboard Shortcuts |
| Wrong action triggered | Multiple bindings on same key | Remove conflicting bindings |
| Vim mode conflicts | Vim captures Cursor shortcuts | Configure vim.handleKeys to exclude Cursor keys |
| System shortcut override | macOS/Windows intercepts key | Change system shortcut or use different binding |

## Examples

**Example: Custom Chat Shortcut**
Request: "Change AI chat shortcut from Cmd+L to Cmd+Shift+C"
Result: New keybinding added in keybindings.json for cursor.newChat

**Example: Vim Mode Configuration**
Request: "Use Vim mode but keep Cursor AI shortcuts working"
Result: Configure vim.handleKeys to pass through Cmd+L, Cmd+K, and Cmd+I

## Resources

- [VS Code Key Bindings](https://code.visualstudio.com/docs/getstarted/keybindings)
- [Cursor Keyboard Shortcuts](https://cursor.com/docs/shortcuts)
- [Vim Extension Configuration](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)
