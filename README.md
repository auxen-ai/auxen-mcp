# Auxen MCP Server

This is the **public manifest repo** for the Auxen MCP (Model Context Protocol) server. The server itself runs at `https://api.auxen.ai/mcp` — this repo exists so registries (Smithery, Glama, the official MCP registry) have a canonical place to read metadata from.

## Connect

The Auxen MCP server is a **remote, StreamableHTTP** server. Add it to your MCP client by URL:

```
https://api.auxen.ai/mcp
```

Authentication uses **OAuth 2.1 + PKCE** (recommended for browser-based clients) or a direct Auxen API key (`auxen_live_*` / `auxen_test_*`) sent as `Authorization: Bearer <key>`.

### OAuth flow

The discovery metadata is at:

- `https://api.auxen.ai/.well-known/oauth-authorization-server` (RFC 8414)
- `https://api.auxen.ai/.well-known/oauth-protected-resource` (RFC 9728)

Clients that support [Dynamic Client Registration (RFC 7591)](https://datatracker.ietf.org/doc/html/rfc7591) — including Claude.ai's Connectors Directory — can register themselves automatically. After registration the client redirects the user's browser to `https://api.auxen.ai/oauth/authorize`, the user logs in to Auxen and approves the connection on `https://auxen.ai/oauth/authorize`, and the client receives an authorization code that exchanges for an access token at `https://api.auxen.ai/oauth/token`.

### Direct key (programmatic)

For agents that don't go through a browser, generate an `auxen_live_*` (or `auxen_test_*`) key at <https://auxen.ai/dashboard/api-keys> and send it as `Authorization: Bearer <key>` on every MCP call.

## Tools

| Tool | Effect | Hint |
|------|--------|------|
| `auxen_list_models` | List available models, optionally filtered by size | read-only |
| `auxen_get_instance_status` | Get status, endpoint, api_key for an instance | read-only |
| `auxen_list_instances` | List all instances on the account | read-only |
| `auxen_get_balance` | Read USD credits + active subscriptions | read-only |
| `auxen_provision_model` | Provision a new model instance — **spends money** | destructive |
| `auxen_destroy_instance` | Destroy an instance — **irreversible** | destructive |

## What is Auxen?

Auxen provisions private, dedicated GPU instances running open-source models (Llama 3.1, Qwen 2.5, Mistral, Gemma 2, Phi-3). Each instance is fully private — no shared inference, no third-party routing. Pay-per-minute billing, no subscriptions.

For the human-facing documentation:

- Website: <https://auxen.ai>
- Architecture explainer: <https://auxen.ai/architecture>
- Agent reference: <https://auxen.ai/agent-reference.md>
- Concise reference for LLMs: <https://auxen.ai/llms.txt>
- OpenAPI 3.1 spec: <https://api.auxen.ai/openapi.json>

## Support

- Email: <hello@auxen.ai>
- Status: <https://status.auxen.ai>
