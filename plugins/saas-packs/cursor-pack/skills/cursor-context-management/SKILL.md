---
name: "cursor-context-management"
description: |
  Optimize context window usage in Cursor. Triggers on "cursor context",
  "context window", "context limit", "cursor memory", "context management". Use when working with cursor context management functionality. Trigger with phrases like "cursor context management", "cursor management", "cursor".
allowed-tools: "Read, Write, Edit, Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Cursor Context Management

## Overview

This skill helps optimize context window usage in Cursor. It covers understanding context sources, efficient @-mention strategies, conversation management, and techniques to avoid context overflow for better AI response quality.

## Understanding Context

### What is Context?
```
Context = Information sent to AI with your prompt
- Selected code
- Open files
- @-mentioned files
- Conversation history
- .cursorrules
- Codebase index references
```

### Context Window Limits
```
Model context limits (tokens):
- GPT-3.5 Turbo: ~16K tokens
- GPT-4: ~8K tokens (32K extended)
- GPT-4 Turbo: ~128K tokens
- Claude 3.5 Sonnet: ~200K tokens
- Claude 3 Opus: ~200K tokens

Rule of thumb: 1 token ≈ 4 characters
```

## Context Sources

### Automatic Context
```
Cursor automatically includes:
1. Selected code (highest priority)
2. Current file content
3. Recently edited code
4. Import/dependency information
5. .cursorrules content
```

### Manual Context (@-mentions)
```
@filename.ts - Specific file
@folder/ - Folder contents
@codebase - Search indexed code
@docs - Documentation
@web - Web search results
@git - Git history
@terminal - Terminal output
```

## Context Optimization Strategies

### Prioritize Relevant Code
```
Most effective:
1. Select exactly the code you're asking about
2. @-mention directly related files
3. Reference patterns to follow

Less effective:
- Including entire files when only function needed
- @-mentioning unrelated files
- Large conversation history
```

### Minimize Context Waste
```
Do:
- Select specific functions, not entire files
- Use @file only for relevant files
- Start new chat when topic changes
- Be concise in prompts

Don't:
- @-mention "just in case"
- Keep long conversation threads
- Include commented-out code
- Add unnecessary explanations
```

### Context-Efficient Prompts
```
Inefficient:
"I have this code and it's not working and I need help
understanding what's wrong with it and how to fix it
because it throws an error when I run it"

Efficient:
"Fix TypeError: Cannot read 'map' of undefined
@api/users.ts line 45"
```

## Managing Large Codebases

### Selective Indexing
```yaml
# .cursorignore - reduce indexed context
node_modules/
dist/
build/
*.log
*.lock
test/fixtures/
docs/
```

### Strategic @codebase Queries
```
Specific:
"@codebase where is handleUserLogin defined?"

Too broad:
"@codebase show me all the code"
```

### Using Summaries
```
For large files, ask for summary first:
"Summarize the main exports from @lib/utils.ts"

Then dive into specifics:
"Explain the dateFormatter function in detail"
```

## Conversation Context

### When to Start New Chat
```
Start new chat when:
- Switching to unrelated topic
- Context feels polluted
- AI seems confused
- Responses are slow/truncated
- Starting fresh task
```

### Preserving Important Context
```
If switching topics but need context:
1. Copy important code/decisions
2. Start new chat
3. Paste relevant context
4. Continue with fresh window
```

### Multi-Turn Optimization
```
Good flow:
Turn 1: "Create user authentication"
Turn 2: "Add password reset to auth"
Turn 3: "Add rate limiting to auth"

Bad flow:
Turn 1: "Create user authentication"
Turn 2: "How do I sort arrays in Python?"
Turn 3: "Back to auth - add reset"
(Context confused)
```

## Context Indicators

### Recognizing Context Issues

```
Signs of context overflow:
- Truncated responses
- AI "forgets" earlier discussion
- Slower responses
- Less accurate suggestions
- AI asks for information you provided

Solutions:
- Start new chat
- Reduce @-mentions
- Select less code
- Use larger context model
```

### Monitoring Context Usage
```
Watch for:
- Response quality degradation
- Increased latency
- Incomplete code generation
- References to wrong files
```

## Advanced Techniques

### Layered Context
```
Layer 1: .cursorrules (always present)
Layer 2: @-mentions (specific files)
Layer 3: Selection (immediate focus)
Layer 4: Prompt (your question)

Optimize each layer:
- .cursorrules: Essential patterns only
- @-mentions: Only truly needed files
- Selection: Exact code in question
- Prompt: Clear, concise question
```

### Context Priming
```
Start chat with context summary:
"Working on auth module. Using JWT, refresh tokens,
httpOnly cookies. Following patterns in @lib/auth.ts.
Need to add password reset."

Then ask specific questions:
"Create the reset token generation function"
```

### Reference vs Include
```
Reference (efficient):
"Follow the pattern in UserService"

Include (uses context):
"@services/UserService.ts create similar for Products"

Use references when AI already has indexed context
```

## Best Practices

### Chat Session Management
```
1. One topic per chat session
2. Clear context between major changes
3. Summarize decisions before long gaps
4. Export important decisions to docs
```

### @-mention Strategy
```
Essential: Files you're directly modifying
Helpful: Files with patterns to follow
Wasteful: Entire folders "for context"

Start minimal, add if AI needs more
```

### Code Selection
```
Select precisely:
- The function with the issue
- The type definition needed
- The specific error location

Not:
- Entire files
- Multiple unrelated functions
- Large code blocks "just in case"
```

## Prerequisites

- Cursor IDE with AI features active
- Understanding of context window limits
- Project with code files
- Familiarity with @-mention syntax

## Instructions

1. Understand your model's context limit
2. Select only relevant code before chatting
3. Use specific @-mentions for file context
4. Start new conversations for new topics
5. Monitor response quality for context issues
6. Clear context when switching tasks

## Output

- Optimized context usage
- Better AI response quality
- Faster response times
- Efficient @-mention patterns
- Clean conversation management

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Context length exceeded | Too much selected or @-mentioned | Reduce selection, fewer @-mentions |
| AI forgetting earlier context | Context window overflow | Start new chat, re-state important context |
| Slow responses | Large context processing | Use smaller context, switch model |
| Irrelevant suggestions | Context pollution | Start fresh chat, be more specific |

## Examples

**Example: Efficient Debugging Context**
Request: "Fix TypeError on line 45" with only the relevant function selected
Result: Fast, accurate fix without context overflow

**Example: Context Priming for Complex Task**
Request: Start with summary of architecture, then ask specific questions
Result: AI maintains relevant context throughout conversation

## Resources

- [Context Window Guide](https://cursor.com/docs/context)
- [Model Context Limits](https://cursor.com/docs/models)
- [Effective Prompting](https://cursor.com/docs/prompting)
