---
name: zai-cli
description: |
  Execute z.AI CLI providing vision, search, reader, and GitHub exploration via CLI and MCP.
  Use when user needs image/video analysis, OCR, UI-to-code conversion, error diagnosis,
  real-time web search, web page to markdown extraction, or GitHub code exploration.
  Trigger with phrases like "analyze this image", "search the web for", "read this page",
  "explore this repo", or "use zai". Requires Z_AI_API_KEY.
allowed-tools: Read, Write, Edit, Bash(cmd:*), WebFetch
version: 1.0.0
license: Apache-2.0
author: Numman Ali <numman.ali@gmail.com>
---

# ZAI CLI

## Overview

ZAI CLI provides access to Z.AI capabilities including image/video analysis, real-time web search, web page extraction, and GitHub code exploration. It integrates with Claude Code via MCP protocol for seamless AI-powered content analysis.

## Prerequisites

- Node.js 18+ installed
- Z_AI_API_KEY environment variable set
- API key from https://z.ai/manage-apikey/apikey-list
- Network access to Z.AI API endpoints

## Instructions

1. Obtain an API key from Z.AI platform
2. Export your API key: `export Z_AI_API_KEY="your-key"`
3. Run `npx zai-cli doctor` to verify setup
4. Use `npx zai-cli --help` to see available commands
5. Try basic commands like vision, search, read, or repo
6. Use `--help` on any subcommand for detailed options

Access Z.AI capabilities via `npx zai-cli`. The CLI is self-documenting - use `--help` at any level.

## Setup

```bash
export Z_AI_API_KEY="your-api-key"
```

Get a key at: https://z.ai/manage-apikey/apikey-list

## Commands

| Command | Purpose | Help |
|---------|---------|------|
| vision | Analyze images, screenshots, videos | `--help` for 8 subcommands |
| search | Real-time web search | `--help` for filtering options |
| read | Fetch web pages as markdown | `--help` for format options |
| repo | GitHub code search and reading | `--help` for tree/search/read |
| tools | List available MCP tools | |
| tool | Show tool schema | |
| call | Raw MCP tool invocation | |
| code | TypeScript tool chaining | |
| doctor | Check setup and connectivity | |

## Quick Start

```bash
# Analyze an image
npx zai-cli vision analyze ./screenshot.png "What errors do you see?"

# Search the web
npx zai-cli search "React 19 new features" --count 5

# Read a web page
npx zai-cli read https://docs.example.com/api
npx zai-cli read https://docs.example.com/api --with-images-summary --no-gfm

# Explore a GitHub repo
npx zai-cli repo search facebook/react "server components"
npx zai-cli repo search openai/codex "config" --language en
npx zai-cli repo tree openai/codex --path codex-rs --depth 2

# Check setup
npx zai-cli doctor
```

## Output

Default: **data-only** (raw output for token efficiency).
Use `--output-format json` for `{ success, data, timestamp }` wrapping.

## Advanced

For raw MCP tool calls (`tools`, `tool`, `call`), Code Mode, and performance tuning (cache/retries),
see `references/advanced.md`.

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Z_AI_API_KEY not set | Environment variable missing | Export the key: `export Z_AI_API_KEY="your-api-key"` |
| Invalid API key | Key revoked or incorrect | Verify key at https://z.ai/manage-apikey/apikey-list |
| Rate limit exceeded | Too many requests | Wait and retry, or upgrade API tier |
| Network timeout | Connectivity issues or slow response | Check internet connection, retry with longer timeout |
| File not found | Invalid path to image/video | Verify file path exists and is accessible |
| Unsupported format | Image/video format not supported | Convert to supported format (PNG, JPG, MP4) |
| Repository not found | Invalid GitHub repo path | Verify repository exists and is public (or authenticated) |
| Empty search results | No matches for query | Broaden search terms or check spelling |

## Examples

**Example: Analyze Screenshot for Errors**
Request: "Check this screenshot for any error messages"
Result: Vision analysis identifies error dialog, extracts error text, and suggests potential fixes based on the error content

**Example: Research Topic with Web Search**
Request: "Find the latest React 19 features"
Result: Returns top 5 search results with titles, URLs, and summaries of React 19 features from authoritative sources

**Example: Convert Web Page to Markdown**
Request: "Get the API documentation from this URL as markdown"
Result: Fetches page content, converts to clean markdown format, preserving code blocks and structure

**Example: Explore GitHub Repository**
Request: "Search the openai/codex repo for configuration handling"
Result: Returns matching files and code snippets showing how configuration is implemented in the repository

## Resources

- [Z.AI Platform](https://z.ai/)
- [Z.AI API Key Management](https://z.ai/manage-apikey/apikey-list)
- [zai-cli npm Package](https://www.npmjs.com/package/zai-cli)
- [Z.AI Documentation](https://docs.z.ai/)
- [MCP Protocol Reference](https://modelcontextprotocol.io/)
