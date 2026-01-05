---
name: "cursor-local-dev-loop"
description: |
  Optimize local development workflow with Cursor. Triggers on "cursor workflow",
  "cursor development loop", "cursor productivity", "cursor daily workflow". Use when working with cursor local dev loop functionality. Trigger with phrases like "cursor local dev loop", "cursor loop", "cursor".
allowed-tools: "Read, Write, Edit, Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Cursor Local Development Loop

## Overview

This skill helps optimize your local development workflow with Cursor IDE. It provides guidance on daily development patterns, keyboard-driven workflows, and efficient AI-assisted coding practices to maximize productivity.

## Optimal Development Workflow

### Morning Startup
```bash
# 1. Open project
cursor /path/to/project

# 2. Let indexing complete (check status bar)
# 3. Review yesterday's changes
git diff HEAD~1

# 4. Check AI chat for context
# Cmd+L: "Summarize recent changes in this codebase"
```

### Feature Development Cycle

```
┌─────────────────────────────────────────┐
│  1. Define Task (Chat)                  │
│     Cmd+L: "I need to add user auth"    │
├─────────────────────────────────────────┤
│  2. Generate Scaffold (Composer)        │
│     Cmd+I: "Create auth module with..." │
├─────────────────────────────────────────┤
│  3. Iterate with Tab Completion         │
│     Write code, accept AI suggestions   │
├─────────────────────────────────────────┤
│  4. Debug with Chat                     │
│     Select error, Cmd+L: "Why fails?"   │
├─────────────────────────────────────────┤
│  5. Refactor with Inline Edit           │
│     Select code, Cmd+K: "Optimize"      │
└─────────────────────────────────────────┘
```

## Keyboard-Driven Workflow

### Essential Shortcuts
| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| AI Chat | Cmd+L | Ctrl+L |
| Composer | Cmd+I | Ctrl+I |
| Inline Edit | Cmd+K | Ctrl+K |
| Accept Completion | Tab | Tab |
| Reject Completion | Esc | Esc |
| New Chat | Cmd+Shift+L | Ctrl+Shift+L |

### Navigation
| Action | Mac | Windows/Linux |
|--------|-----|---------------|
| Go to File | Cmd+P | Ctrl+P |
| Go to Symbol | Cmd+Shift+O | Ctrl+Shift+O |
| Search All | Cmd+Shift+F | Ctrl+Shift+F |
| Terminal | Cmd+` | Ctrl+` |

## Context Management

### Feeding Context to AI
```
Method 1: Select code before chatting
- Highlight relevant code
- Press Cmd+L
- Your selection is included

Method 2: @-mention files
- In chat: @filename.py explain this

Method 3: Add to context
- Right-click file > "Add to AI Context"
```

### Clearing Context
- Start new chat: Cmd+Shift+L
- Clear context: Click "Clear" in chat panel

## Git Integration Workflow

### Pre-Commit Review
```bash
# Stage changes
git add -A

# Ask AI to review
# Cmd+L: "Review my staged changes for issues"
```

### Commit Message Generation
```
# In chat:
"Generate commit message for staged changes"
```

### Conflict Resolution
```
# When conflicts occur:
1. Open conflicting file
2. Select conflict markers
3. Cmd+L: "Resolve this merge conflict, keeping feature X"
```

## Testing Workflow

### Generate Tests
```
# Select function
# Cmd+L: "Write comprehensive tests for this function"
```

### Debug Failing Tests
```
# Copy test output
# Cmd+L: "This test is failing: [paste]. Why?"
```

### TDD with Cursor
```
1. Write test first (with AI help)
2. Cmd+I: "Implement function to pass this test"
3. Iterate until green
```

## Performance Tips

### Keep Cursor Fast
- Close unused tabs
- Limit open files to relevant ones
- Use workspace-specific settings

### Optimize AI Responses
- Be specific in prompts
- Include file paths when relevant
- Break large tasks into smaller prompts

### Background Processes
- Terminal runs in background
- Tests can run while coding
- Use split views effectively

## Prerequisites

- Cursor IDE installed and configured
- Project with development environment set up
- Git repository initialized
- Basic familiarity with Cursor AI features

## Instructions

1. Open project and let indexing complete
2. Review recent changes with git diff
3. Use Chat (Cmd+L) for planning and architecture
4. Use Composer (Cmd+I) for multi-file scaffolding
5. Use Tab completion for implementation
6. Use Inline Edit (Cmd+K) for quick fixes
7. Commit with AI-generated messages

## Output

- Efficient keyboard-driven workflow
- AI-assisted feature development
- Streamlined git integration
- Rapid iteration cycle

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Slow AI responses | Network or model choice | Switch to faster model, check connection |
| Lost context mid-task | Long conversation or topic switch | Start new chat, re-state context |
| Completions not matching | .cursorrules outdated | Update rules with current patterns |
| Performance issues | Too many open files | Close unused tabs, restart Cursor |

## Examples

**Example: Morning Development Startup**
Request: "Summarize recent changes and what needs work today"
Result: AI provides summary of git diff and identifies next steps

**Example: TDD Workflow**
Request: Write test first, then "Implement function to pass this test"
Result: AI generates implementation matching test requirements

## Resources

- [Cursor Workflow Guide](https://cursor.com/docs/workflow)
- [Keyboard Shortcuts Reference](https://cursor.com/docs/shortcuts)
- [Developer Productivity Tips](https://cursor.com/blog/productivity)
