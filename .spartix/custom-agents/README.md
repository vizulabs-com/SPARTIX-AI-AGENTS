# Custom Agents Ecosystem

## Overview

Custom agents are user-defined specialist agents that extend the built-in agent pool. They follow the exact same format as built-in agents and are discovered, validated, and registered by CO during session initialization.

## How Custom Agents Are Discovered

1. CO scans `custom-agents/` directory recursively during session initialization
2. CO reads `SYSTEM/custom-agent-registry.json` if it exists
3. CO identifies all `.md` files in the directory tree
4. Each file is treated as a potential custom agent definition

## How Custom Agents Are Validated

1. CO checks that the file has the required frontmatter (name, description, argument-hint, tools)
2. CO checks that all required sections are present (Identity, Purpose, Use This Agent When, Core Responsibilities, Inputs, Outputs, Rules, Handoff Targets, Forbidden Actions)
3. CO checks that the agent follows the specialist-only principle (not a generalist)
4. CO checks that the agent does not claim forbidden capabilities (user communication, wiki writing, etc.)

## How Custom Agents Are Registered

1. Valid custom agents are added to `SYSTEM/custom-agent-registry.json`
2. Each entry includes: path, name, code, category, domain, capabilities, validation status
3. Invalid agents are logged with the reason for rejection

## How Custom Agents Are Prioritized

1. Built-in agents are the default choice for standard specializations
2. Custom agents are preferred when they provide a more specific match (e.g., client-specific)
3. Rule overrides can force custom agent preference for specific domains or clients
4. CO documents the selection rationale in the workflow feed

## Grouping Structure

### by-application/
Custom agents grouped by application type:
- `web/` — Web application specialists
- `mobile/` — Mobile application specialists
- `desktop/` — Desktop application specialists
- `saas/` — SaaS platform specialists
- `ecommerce/` — E-commerce specialists
- `analytics/` — Analytics platform specialists
- `enterprise/` — Enterprise system specialists

### by-domain/
Custom agents grouped by technical domain:
- `payments/` — Payment processing specialists
- `security/` — Security specialists
- `ai/` — AI/ML specialists
- `blockchain/` — Blockchain specialists
- `bigdata/` — Big data specialists
- `realtime/` — Real-time system specialists
- `mcp/` — MCP integration specialists
- `n8n/` — n8n workflow specialists
- `cli/` — CLI tooling specialists
- `docker/` — Docker specialists
- `dashboards/` — Dashboard specialists
- `prompting/` — Prompt engineering specialists

### by-client/
Custom agents grouped by client:
- `client-a/` — Client A specific agents
- `client-b/` — Client B specific agents
- `internal/` — Internal team agents

### shared/
Common reusable custom agents that apply across multiple contexts.

## Custom Agent Template

All custom agents must follow the exact same format as built-in agents. See `SYSTEM/agent-format-template.md` for the required template.
