---
name: "windsurf-refactoring-large"
description: |
  Manage large-scale refactoring with Cascade coordination. Activate when users mention
  "large refactoring", "codebase migration", "architecture refactor", "major refactoring",
  or "system-wide changes". Handles complex refactoring operations. Use when working with windsurf refactoring large functionality. Trigger with phrases like "windsurf refactoring large", "windsurf large", "windsurf".
allowed-tools: "Read,Write,Edit,Bash(cmd:*),Grep,Glob"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Windsurf Large-Scale Refactoring

Execute complex refactoring operations with Cascade AI coordination.

## Overview

This skill enables large-scale refactoring operations that span hundreds or thousands of files. It provides phased execution with checkpoints, comprehensive rollback capabilities, and AI-assisted planning. Ideal for architecture migrations, API version upgrades, dependency replacements, and codebase modernization efforts that would traditionally take weeks to complete manually.

## Prerequisites

- Windsurf IDE with Enterprise or Pro subscription
- Active Cascade AI connection
- Git repository with clean working state
- Comprehensive test suite for validation
- Backup strategy for critical code paths
- Team coordination for multi-developer codebases

## Directory Structure

```
project-root/
    .windsurf/
        refactoring/
            plans/
                current-refactor.json        # Active refactoring plan
                    # Scope definition
                    # Phase breakdown
                    # Progress tracking

                migration-plan.json          # Migration roadmap
                    # Source patterns
                    # Target patterns
                    # Rollback strategy

            phases/
                phase-1-analysis.json        # Analysis phase
                    # Files affected
                    # Dependencies mapped
                    # Risk assessment

                phase-2-preparation.json     # Preparation phase
                    # Tests added
                    # Backups created
                    # Rollback tested

                phase-3-execution.json       # Execution phase
                    # Change sequence
                    # Validation checkpoints
                    # Progress tracking

                phase-4-verification.json    # Verification phase
                    # Test results
                    # Performance comparison
                    # Documentation updates

            checkpoints/
                pre-refactor-snapshot.json   # Pre-refactor state
                    # File hashes
                    # Test baselines
                    # Metric baselines

                progress/
                    checkpoint-001.json      # Progress checkpoints
                        # Completed changes
                        # Pending changes
                        # Issues encountered

            rollback/
                rollback-plan.json           # Rollback strategy
                    # Rollback triggers
                    # Recovery steps
                    # Verification process

                backups/
                    README.md                # Backup index
                        # File locations
                        # Restore procedures
```

## Refactoring Features

### Planning
- Impact analysis
- Dependency mapping
- Risk assessment
- Phase definition

### Execution
- Atomic changes
- Progress tracking
- Checkpoint creation
- Validation at each step

## Instructions

1. **Analyze Scope**
   - Run Cascade analysis on target patterns
   - Map all affected files and dependencies
   - Identify high-risk areas and critical paths
   - Generate risk assessment report

2. **Create Plan**
   - Define phases based on dependency order
   - Set validation checkpoints between phases
   - Create rollback procedures for each phase
   - Document success criteria per phase

3. **Prepare Environment**
   - Add tests for untested code paths
   - Create pre-refactor snapshot
   - Verify rollback process works
   - Coordinate with team on freeze periods

4. **Execute with Cascade**
   - Apply changes incrementally by phase
   - Validate at each checkpoint
   - Track progress in phase files
   - Pause and review at milestones

5. **Verify Completion**
   - Run complete test suite
   - Compare performance metrics to baseline
   - Update documentation for changed APIs
   - Archive refactoring artifacts

## Output

- Refactored codebase with all patterns migrated
- Phase completion reports with metrics
- Before/after performance comparison
- Updated documentation and API references
- Archived rollback artifacts (kept 30 days)

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Checkpoint validation failed | Tests failing at checkpoint | Rollback to previous checkpoint, fix issues |
| Dependency conflict | Changed code breaks downstream | Map full dependency tree, adjust order |
| Performance regression | Refactored code slower | Profile and optimize before proceeding |
| Merge conflict | Parallel development | Coordinate freeze window, rebase plan |
| Rollback incomplete | Partial state restoration | Use backup files, manual intervention |

## Examples

**Example: API Version Migration**
Request: "Migrate all API v1 calls to v2 across the codebase"
Result: Phased migration with compatibility layer, gradual cutover, and v1 deprecation

**Example: Framework Upgrade**
Request: "Upgrade React class components to functional components with hooks"
Result: Systematic conversion with state migration, lifecycle method translation, and test updates

**Example: Architecture Restructure**
Request: "Move from monolithic services to domain-driven modules"
Result: Code reorganization with dependency injection, interface extraction, and module boundaries

## Resources

- [Windsurf Large Refactoring Guide](https://docs.windsurf.ai/features/large-refactoring)
- [Phased Execution Best Practices](https://docs.windsurf.ai/best-practices/phased-execution)
- [Rollback and Recovery](https://docs.windsurf.ai/features/rollback)

## Success Criteria

- All tests passing
- Zero runtime regressions
- Completed in days vs weeks
