---
name: "windsurf-multi-file-editing"
description: |
  Manage multi-file edits with Cascade coordination. Activate when users mention
  "multi-file edit", "edit multiple files", "cross-file changes", "refactor across files",
  or "batch modifications". Handles coordinated multi-file operations. Use when working with windsurf multi file editing functionality. Trigger with phrases like "windsurf multi file editing", "windsurf editing", "windsurf".
allowed-tools: Read,Write,Edit,Grep,Glob
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Windsurf Multi-File Editing

Execute coordinated changes across multiple files with Cascade assistance.

## Overview

This skill enables coordinated multi-file editing operations within Windsurf using Cascade AI. It provides atomic changes across multiple files, ensuring consistency when renaming symbols, moving code, or making cross-file refactoring changes. The skill handles dependency tracking, preview generation, and rollback capabilities for safe multi-file operations.

## Prerequisites

- Windsurf IDE installed and configured
- Active Cascade AI subscription
- Project workspace initialized with `.windsurf/` directory
- Git or version control for rollback safety
- Understanding of project file structure and dependencies

## Directory Structure

```
project-root/
    .windsurf/
        operations/
            pending-edits.json       # Queued multi-file operations
                # Files to be modified
                # Change descriptions
                # Dependency order

            edit-history.json        # Completed operation log
                # Timestamps and changes
                # Rollback information
                # Success/failure status

            templates/
                rename-pattern.json  # Rename operation template
                    # Find/replace patterns
                    # File scope definitions
                    # Exclusion rules

                feature-add.json     # Feature addition template
                    # Files to create/modify
                    # Import updates
                    # Test file additions

    src/
        components/                  # Example component directory
            ComponentA.tsx           # Component implementation
                # Renamed imports
                # Updated references
                # Consistent changes

            ComponentA.test.tsx      # Corresponding test file
                # Synchronized test updates
                # Import path corrections

            index.ts                 # Barrel export file
                # Updated exports
                # Maintained ordering
```

## Multi-File Operations

### Common Patterns
- **Rename** - Update symbol across all usages
- **Move** - Relocate file with import updates
- **Extract** - Pull code into new file
- **Inline** - Merge files together

### Safety Mechanisms
- Preview changes before applying
- Atomic rollback capability
- Syntax validation per file
- Reference integrity checking

## Instructions

1. **Scope the Operation**
   - Identify all affected files using search/grep
   - Map file dependencies and import relationships
   - Plan change order based on dependencies

2. **Configure Operation Template**
   - Select appropriate template (rename, move, extract)
   - Define find/replace patterns or transformations
   - Set file scope and exclusion rules

3. **Generate Preview**
   - Run Cascade analysis on affected files
   - Review all proposed modifications
   - Verify no unintended changes

4. **Execute with Preview**
   - Apply changes atomically across all files
   - Cascade validates syntax after each change
   - Monitor progress in edit-history.json

5. **Verify Results**
   - Run syntax checks on modified files
   - Execute test suite to catch regressions
   - Validate all references resolve correctly

## Output

- Modified files with consistent changes applied
- `edit-history.json` log with operation details
- Rollback snapshot for recovery if needed
- Validation report with syntax check results

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Circular dependency detected | Files have mutual imports | Break cycle by extracting shared code |
| Syntax error after edit | Invalid code generated | Review template patterns, use rollback |
| Reference not found | Missing import or export | Check file scope includes all references |
| Operation timeout | Too many files affected | Split into smaller batches |
| Rollback failed | Git state inconsistent | Manual recovery from edit-history.json |

## Examples

**Example: Rename Component Across Project**
Request: "Rename UserCard component to ProfileCard across all files"
Result: Updates component file, test file, all imports, and barrel exports atomically

**Example: Extract Utility Function**
Request: "Extract formatDate function from utils.ts to date-utils.ts"
Result: Creates new file, moves function, updates all import statements

**Example: Move Component to New Directory**
Request: "Move Button component from components/ to ui/components/"
Result: Relocates files, updates all relative imports, maintains test associations

## Resources

- [Windsurf Multi-File Editing Documentation](https://docs.windsurf.ai/features/multi-file-editing)
- [Cascade AI Coordination Guide](https://docs.windsurf.ai/cascade/coordination)
- [Atomic Operations Best Practices](https://docs.windsurf.ai/best-practices/atomic-ops)

## Success Criteria

- All files modified atomically
- Consistent syntax across changes
- No broken references
