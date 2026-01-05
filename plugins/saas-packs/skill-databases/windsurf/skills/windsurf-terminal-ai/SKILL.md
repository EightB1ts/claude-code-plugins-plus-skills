---
name: "windsurf-terminal-ai"
description: |
  Execute leverage AI-assisted terminal commands and debugging. Activate when users mention
  "terminal help", "command suggestion", "debug terminal", "shell assistance",
  or "cli help". Handles AI-enhanced terminal operations. Use when working with windsurf terminal ai functionality. Trigger with phrases like "windsurf terminal ai", "windsurf ai", "windsurf".
allowed-tools: "Read,Bash(cmd:*),Grep"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Windsurf Terminal AI

Leverage AI-assisted terminal commands for efficient debugging and operations.

## Overview

This skill enables AI-assisted terminal operations within Windsurf. Cascade can suggest commands, explain error messages, generate complex shell scripts, and help debug terminal output. It understands common CLI tools, build systems, and DevOps commands to provide contextually relevant assistance for command-line workflows.

## Prerequisites

- Windsurf IDE with integrated terminal
- Shell environment configured (bash, zsh, etc.)
- Understanding of command-line basics
- Project-specific CLI tools installed
- PATH configured for required tools

## Directory Structure

```
project-root/
    .windsurf/
        terminal/
            command-history.json     # AI-analyzed command history
                # Successful patterns
                # Error contexts
                # Suggested alternatives

            aliases.json             # AI-suggested aliases
                # Frequent command shortcuts
                # Project-specific commands
                # Workflow automation

            snippets/
                debug-commands.sh    # Common debug commands
                    # Log inspection commands
                    # Process monitoring
                    # Network diagnostics

                build-commands.sh    # Build workflow commands
                    # Clean build sequences
                    # Incremental builds
                    # Artifact management

    .bashrc / .zshrc                 # Shell configuration
        # Windsurf terminal integration
        # AI completion setup
        # Custom prompt configuration

    scripts/
        common-tasks.sh              # Reusable task scripts
            # Parameterized commands
            # Error handling
            # Logging integration
```

## AI Terminal Features

### Command Suggestions
- Context-aware completions
- Error correction proposals
- Alternative command options
- Parameter hints

### Debugging Assistance
- Error message interpretation
- Log analysis suggestions
- Stack trace navigation
- Environment diagnostics

## Instructions

1. **Enable AI Assistance**
   - Configure terminal AI integration
   - Set up suggestion triggers
   - Enable error analysis

2. **Configure Command Library**
   - Document common commands
   - Create reusable scripts
   - Set up aliases for frequent tasks

3. **Set Up Error Handling**
   - Enable error forwarding to Cascade
   - Configure log collection
   - Set up diagnostics scripts

4. **Optimize Workflows**
   - Identify repetitive command patterns
   - Automate common sequences
   - Create parameterized templates

5. **Build Team Knowledge**
   - Share useful commands
   - Document project-specific CLIs
   - Create onboarding scripts

## Output

- Command suggestions and completions
- Error analysis and fixes
- Optimized command aliases
- Reusable shell scripts

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Command not found | Missing tool or PATH | Install tool or update PATH |
| Permission denied | Insufficient rights | Use sudo or fix permissions |
| Syntax error | Malformed command | Review command syntax with Cascade |
| Network timeout | Connectivity issue | Check network, retry with timeout |
| Script failed | Logic or environment error | Debug with set -x, check variables |

## Examples

**Example: Debug Failed Command**
Request: "npm install failed with ENOENT error"
Result: Analysis shows missing directory, suggests mkdir or path fix

**Example: Generate Complex Command**
Request: "Find all files modified in last 24 hours over 1MB"
Result: `find . -type f -mtime -1 -size +1M -exec ls -lh {} \;`

**Example: Script Generation**
Request: "Create script to backup database and upload to S3"
Result: Shell script with pg_dump, compression, aws s3 cp with error handling

## Resources

- [Windsurf Terminal Guide](https://docs.windsurf.ai/features/terminal)
- [AI Command Assistance](https://docs.windsurf.ai/cascade/terminal)
- [Shell Scripting Best Practices](https://docs.windsurf.ai/guides/shell-scripts)

## Success Criteria

- 80% reduction in command errors
- Context-aware completions
- 45% reduction in debugging time
