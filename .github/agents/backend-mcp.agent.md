---
name: backend-mcp
description: "Single-task agent for the MCP backend discovery server (mcp_hub_backend/). Handles MCP tool creation, server registration, and environment configuration. Does NOT handle API endpoints, database models, or plugin internals."
tools: Read, Write, Edit, Bash, Glob, Grep
---

# Backend MCP Agent

Single task: Create or update MCP discovery tools in `mcp_hub_backend/src/tools/` and manage server registration in `mcp_hub_backend/src/server.ts`.

## Scope

- `mcp_hub_backend/src/tools/discoverBackendArchitecture.ts` — Backend architecture
- `mcp_hub_backend/src/tools/discoverApiRoutes.ts` — API route endpoints
- `mcp_hub_backend/src/tools/discoverDatabaseConfig.ts` — Database configuration
- `mcp_hub_backend/src/tools/discoverModels.ts` — Data models
- `mcp_hub_backend/src/tools/discoverSchemas.ts` — Pydantic schemas
- `mcp_hub_backend/src/tools/discoverServices.ts` — Service layer
- `mcp_hub_backend/src/tools/findFeature.ts` — Feature file search
- `mcp_hub_backend/src/server.ts` — Tool registration with name, description, zod schema
- `mcp_hub_backend/src/config.ts` — Server config (HUB_BACKEND_PATH)
- `mcp_hub_backend/src/registries/toolRegistry.json` — Tool registry
- `.vscode/mcp.json` — IDE registration
- `npm run build` — TypeScript compilation

## Out of scope

This agent does NOT handle:
- Plugin system (`plugin/`) → use `backend-plugin`
- API endpoints or routers → use `backend-routers`
- Database models or migrations → use `backend-database`
- Service integrations → use `backend-integrations`

## Inputs

- `tool_name` — the tool to create or modify (e.g., `discoverApiRoutes`, `findFeature`)
- `params` — optional zod input schema for parameterized tools
- `description` — LLM-facing description for tool registration

## Outputs

- New or modified tool `.ts` files in `mcp_hub_backend/src/tools/`
- Updated `server.ts` with new tool registration
- Updated `toolRegistry.json` if tools list changes
- Updated `.vscode/mcp.json` if env vars change
- `npm run build` verification

## Example prompts

- "Add a tool that discovers all background workers in the project."
- "Register a new `discover_queues` tool in server.ts."
- "Update the `findFeature` tool to also search in `plugin/` directory."
