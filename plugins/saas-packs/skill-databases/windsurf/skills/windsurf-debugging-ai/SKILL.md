---
name: "windsurf-debugging-ai"
description: |
  Execute use Cascade for intelligent debugging and error analysis. Activate when users mention
  "debug with ai", "error analysis", "cascade debug", "find bug",
  or "troubleshoot code". Handles AI-assisted debugging workflows. Use when debugging issues or troubleshooting. Trigger with phrases like "windsurf debugging ai", "windsurf ai", "windsurf".
allowed-tools: "Read,Grep,Glob,Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Windsurf Debugging AI

Leverage Cascade for intelligent debugging and rapid error resolution.

## Overview

This skill enables AI-assisted debugging within Windsurf. Cascade analyzes error messages, stack traces, and code context to identify root causes and suggest fixes. It learns from your codebase patterns to provide contextually relevant debugging assistance, reducing time spent on common errors and helping identify subtle bugs that might otherwise be missed.

## Prerequisites

- Windsurf IDE with Cascade enabled
- Application with reproducible issues
- Debug configuration set up
- Error logs accessible
- Understanding of application architecture

## Directory Structure

```
project-root/
    .windsurf/
        debug/
            error-patterns.json      # Known error patterns
                # Common error signatures
                # Resolution strategies
                # Prevention recommendations

            debug-sessions/
                session-YYYY-MM-DD.json  # Debug session logs
                    # Error contexts captured
                    # AI analysis results
                    # Resolution steps taken

            breakpoint-sets/
                api-debugging.json       # API debug breakpoints
                    # Request entry points
                    # Response handlers
                    # Error boundaries

                state-debugging.json     # State management breakpoints
                    # State mutation points
                    # Effect triggers
                    # Selector evaluations

    .vscode/
        launch.json                  # Debug configurations
            # Application debug configs
            # Test debug configs
            # Attach configurations

        tasks.json                   # Debug task definitions
            # Pre-debug build tasks
            # Log clearing tasks
            # Environment setup
```

## AI Debugging Features

### Error Analysis
- Stack trace interpretation
- Root cause identification
- Similar error matching
- Fix suggestion generation

### Context Gathering
- Variable state inspection
- Call stack analysis
- Log correlation
- Environment comparison

## Instructions

1. **Capture Error Context**
   - Reproduce the error
   - Capture stack trace and logs
   - Note environmental conditions

2. **Analyze with Cascade**
   - Share error message with Cascade
   - Provide relevant code context
   - Review AI analysis

3. **Investigate Root Cause**
   - Set breakpoints at suggested locations
   - Inspect variable states
   - Trace execution flow

4. **Apply Fix**
   - Implement Cascade-suggested fix
   - Test fix thoroughly
   - Verify error is resolved

5. **Document for Prevention**
   - Add to error patterns if new
   - Update tests to catch regression
   - Share learnings with team

## Output

- Root cause analysis
- Fix recommendations
- Debug session logs
- Prevention strategies

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Debugger not attaching | Port conflict | Check debug port, kill conflicting processes |
| Breakpoint not hitting | Source maps issue | Verify source maps, rebuild |
| Variable undefined | Wrong scope | Check breakpoint location, scope context |
| Cascade missing context | Insufficient code shared | Include more relevant files |
| Fix introduced regression | Incomplete analysis | Add more test coverage, review fix scope |

## Examples

**Example: Analyze Stack Trace**
Request: "Why am I getting TypeError: Cannot read property 'map' of undefined?"
Result: Analysis shows API response changed format, suggests defensive coding

**Example: Debug Race Condition**
Request: "Help find intermittent bug in user authentication"
Result: Identifies race condition in token refresh, suggests async fix

**Example: Memory Leak Investigation**
Request: "Application memory grows over time, help find the leak"
Result: Identifies event listener not being cleaned up, shows fix

## Resources

- [Windsurf Debugging Guide](https://docs.windsurf.ai/features/debugging)
- [AI-Assisted Debugging](https://docs.windsurf.ai/cascade/debugging)
- [Debug Configuration Reference](https://docs.windsurf.ai/reference/debug-config)

## Success Criteria

- 90% root cause identification rate
- Fix suggestions within 3 interactions
- 55% reduction in resolution time
