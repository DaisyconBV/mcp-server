# Daisycon MCP Servers

[![MCP Protocol](https://img.shields.io/badge/MCP-Streamable%20HTTP-blue)](https://mcp.daisycon.com/mcp.json)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE.md)

Official Model Context Protocol (MCP) servers for the **Daisycon** affiliate network, hosted at `mcp.daisycon.com`. Each server exposes one area of the Daisycon API as MCP tools over **Streamable HTTP** (JSON-RPC 2.0). AI assistants (Claude, Cursor, custom agents) connect directly: no SDK, no wrapper.

## Servers

| Server                                           | Endpoint                                  | Auth          | Summary                                                              |
| ------------------------------------------------ | ----------------------------------------- | ------------- | -------------------------------------------------------------------- |
| [Campaigns](#campaigns-public-no-authentication) | `https://mcp.daisycon.com/campaigns/mcp`  | None (public) | Public Daisycon Campaign Search MCP - no authentication required.    |
| [Advertiser](#advertiser-oauth)                  | `https://mcp.daisycon.com/advertiser/mcp` | OAuth         | Daisycon Advertiser MCP - programs, leads, financials, integrations. |
| [Publisher](#publisher-oauth)                    | `https://mcp.daisycon.com/publisher/mcp`  | OAuth         | Daisycon Publisher MCP - campaigns, media, statistics, transactions. |

Every server shares: Streamable HTTP transport, JSON-RPC 2.0, primary protocol version `2026-07-28` with legacy support for `2025-11-25`, `2025-06-18`, `2025-03-26`, `2024-11-05` (negotiated via `initialize`).

## Campaigns (public, no authentication)

- **Endpoint**: `POST https://mcp.daisycon.com/campaigns/mcp`
- **Scope**: `campaigns.read`

| Tool                   | Scope            | Description                                                                           |
| ---------------------- | ---------------- | ------------------------------------------------------------------------------------- |
| `getAllPublicPrograms` | `campaigns.read` | See [`/campaigns/llms.txt`](https://mcp.daisycon.com/campaigns/llms.txt) for details. |

**Claude Code & Claude Desktop**

```json
{
    "mcpServers": {
        "daisycon-campaigns": {
            "type": "http",
            "url": "https://mcp.daisycon.com/campaigns/mcp"
        }
    }
}
```

or:

```bash
claude mcp add --transport http daisycon-campaigns https://mcp.daisycon.com/campaigns/mcp
```

**OpenAI Responses API**

```json
{
    "tools": [
        {
            "type": "mcp",
            "server_label": "daisycon-campaigns",
            "server_url": "https://mcp.daisycon.com/campaigns/mcp"
        }
    ]
}
```

**Google ADK**

```python
McpToolset(connection_params=StreamableHTTPConnectionParams(url="https://mcp.daisycon.com/campaigns/mcp"))
```

**Cursor / Windsurf**: **Settings** → **Features** → **MCP Servers** → **Add New MCP Server** → type
**HTTP** / **Streamable HTTP** → URL `https://mcp.daisycon.com/campaigns/mcp`.

## Advertiser (OAuth)

- **Endpoint**: `POST https://mcp.daisycon.com/advertiser/mcp`
- **Scopes**: `advertiser.read`, `advertiser.write`
- **Custom tools**: `list`, `session_list`, `session_revoke`, plus the full Advertiser API surface, auto-exposed from its OpenAPI specification. Live catalogue: [`/advertiser/llms.txt`](https://mcp.daisycon.com/advertiser/llms.txt) or `tools/list`.
- **Authorization**: OAuth 2.1 with PKCE and Dynamic Client Registration / Client ID Metadata Documents; most MCP clients handle this automatically on first connection.

**Claude Code & Claude Desktop**

```json
{
    "mcpServers": {
        "daisycon-advertiser": {
            "type": "http",
            "url": "https://mcp.daisycon.com/advertiser/mcp"
        }
    }
}
```

or:

```bash
claude mcp add --transport http daisycon-advertiser https://mcp.daisycon.com/advertiser/mcp
```

**OpenAI Responses API**

```json
{
    "tools": [
        {
            "type": "mcp",
            "server_label": "daisycon-advertiser",
            "server_url": "https://mcp.daisycon.com/advertiser/mcp"
        }
    ]
}
```

**Google ADK**

```python
McpToolset(connection_params=StreamableHTTPConnectionParams(url="https://mcp.daisycon.com/advertiser/mcp"))
```

**Cursor / Windsurf**: **Settings** → **Features** → **MCP Servers** → **Add New MCP Server** → type
**HTTP** / **Streamable HTTP** → URL `https://mcp.daisycon.com/advertiser/mcp`.

## Publisher (OAuth)

- **Endpoint**: `POST https://mcp.daisycon.com/publisher/mcp`
- **Scopes**: `publisher.read`, `publisher.write`
- **Custom tools**: `list`, `earnings_digest`, `top_performers`, `opportunity_scout`, `session_list`, `session_revoke`, plus the full Publisher API surface, auto-exposed from its OpenAPI specification. Live catalogue: [`/publisher/llms.txt`](https://mcp.daisycon.com/publisher/llms.txt) or `tools/list`.
- **Authorization**: OAuth 2.1 with PKCE and Dynamic Client Registration / Client ID Metadata Documents; most MCP clients handle this automatically on first connection.

**Claude Code & Claude Desktop**

```json
{
    "mcpServers": {
        "daisycon-publisher": {
            "type": "http",
            "url": "https://mcp.daisycon.com/publisher/mcp"
        }
    }
}
```

or:

```bash
claude mcp add --transport http daisycon-publisher https://mcp.daisycon.com/publisher/mcp
```

**OpenAI Responses API**

```json
{
    "tools": [
        {
            "type": "mcp",
            "server_label": "daisycon-publisher",
            "server_url": "https://mcp.daisycon.com/publisher/mcp"
        }
    ]
}
```

**Google ADK**

```python
McpToolset(connection_params=StreamableHTTPConnectionParams(url="https://mcp.daisycon.com/publisher/mcp"))
```

**Cursor / Windsurf**: **Settings** → **Features** → **MCP Servers** → **Add New MCP Server** → type
**HTTP** / **Streamable HTTP** → URL `https://mcp.daisycon.com/publisher/mcp`.

## Registry entry and domain verification

`server.json` in this repository is the official MCP registry entry covering every server listed above. Domain ownership for the `com.daisycon.mcp` namespace is proven by `https://mcp.daisycon.com/.well-known/mcp-registry-auth`, scoped to this exact subdomain.

## Resources

- [Daisycon MCP index (`llms.txt`)](https://mcp.daisycon.com/llms.txt)
- [Machine-readable server index (`mcp.json`)](https://mcp.daisycon.com/mcp.json)

## License

Released under the [MIT License](LICENSE.md).
