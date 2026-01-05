---
name: "windsurf-mcp-integration"
description: |
  Manage integrate MCP servers with Windsurf for extended capabilities. Activate when users mention
  "mcp integration", "model context protocol", "external tools", "mcp server",
  or "cascade tools". Handles MCP server configuration and integration. Use when working with windsurf mcp integration functionality. Trigger with phrases like "windsurf mcp integration", "windsurf integration", "windsurf".
allowed-tools: "Read,Write,Edit,Bash(cmd:*)"
version: 1.0.0
license: MIT
author: "Jeremy Longshore <jeremy@intentsolutions.io>"
---

# Windsurf MCP Integration

Integrate Model Context Protocol servers for extended AI capabilities.

## Overview

This skill enables integration of MCP (Model Context Protocol) servers with Windsurf, extending Cascade's capabilities with external tools and services. MCP allows Cascade to interact with databases, filesystems, APIs, and custom tools through a standardized protocol. Configure servers, manage permissions, and enable seamless tool access within your AI-assisted development workflow.

## Prerequisites

- Windsurf IDE with MCP support enabled
- Node.js 18+ or Python 3.10+ for MCP servers
- MCP server packages installed (npm or pip)
- Network access for remote MCP servers
- Understanding of MCP protocol basics
- Admin permissions for server configuration

## Directory Structure

```
project-root/
    .windsurf/
        mcp/
            config.json                  # MCP configuration
                # Enabled servers
                # Connection settings
                # Authentication

            servers/
                filesystem.json          # Filesystem MCP server
                    # Allowed paths
                    # Operation permissions
                    # Sandbox settings

                database.json            # Database MCP server
                    # Connection strings
                    # Query permissions
                    # Schema access

                git.json                 # Git MCP server
                    # Repository access
                    # Operation limits
                    # Branch permissions

                custom/
                    internal-api.json    # Custom internal API server
                        # Endpoint configuration
                        # Authentication tokens
                        # Rate limits

            tools/
                tool-registry.json       # Available MCP tools
                    # Tool definitions
                    # Parameter schemas
                    # Usage examples

                tool-permissions.json    # Tool access control
                    # User permissions
                    # Context restrictions
                    # Audit requirements

            schemas/
                request-schema.json      # MCP request schema
                    # Tool invocation format
                    # Parameter validation
                    # Response handling

                response-schema.json     # MCP response schema
                    # Success formats
                    # Error handling
                    # Streaming support
```

## MCP Features

### Available Servers
- Filesystem operations
- Database queries
- Git operations
- Custom API integrations

### Security
- Sandboxed execution
- Permission controls
- Audit logging
- Rate limiting

## Instructions

1. **Enable MCP Servers**
   - Select required servers from available options
   - Configure connection parameters and credentials
   - Set sandboxing and permission boundaries

2. **Configure Tools**
   - Register tools in tool-registry.json
   - Define parameter schemas with validation rules
   - Set access controls per tool or tool group

3. **Set Up Authentication**
   - Configure API keys or OAuth for remote servers
   - Set up credential rotation schedules
   - Enable audit logging for sensitive operations

4. **Test Integration**
   - Verify tool access from Cascade panel
   - Test with sample operations
   - Monitor response times and error rates

5. **Deploy to Team**
   - Document available tools and usage
   - Share configuration with team members
   - Set up monitoring dashboards

## Output

- Configured MCP servers accessible via Cascade
- Tool registry with all available operations
- Permission matrix for access control
- Audit logs for tool invocations

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| Server connection failed | Network or auth issue | Check credentials, verify network access |
| Tool not found | Unregistered tool | Add tool to registry, restart server |
| Permission denied | Insufficient access | Update tool-permissions.json |
| Rate limit exceeded | Too many requests | Implement request queuing, increase limits |
| Schema validation error | Invalid parameters | Check parameter types against schema |

## Examples

**Example: Enable Filesystem Server**
Request: "Set up MCP filesystem server for project directory access"
Result: Cascade can read/write files, search content, and navigate directories

**Example: Connect Database Server**
Request: "Integrate PostgreSQL MCP server for query execution"
Result: Cascade can query database, analyze schemas, and generate reports

**Example: Custom API Integration**
Request: "Add MCP server for internal documentation API"
Result: Cascade can search and retrieve internal documentation

## Resources

- [MCP Protocol Specification](https://modelcontextprotocol.io/docs)
- [Windsurf MCP Guide](https://docs.windsurf.ai/features/mcp)
- [MCP Server Development](https://modelcontextprotocol.io/docs/servers)

## Success Criteria

- MCP tools available in Cascade
- Sub-second response times
- External capabilities accessible seamlessly
