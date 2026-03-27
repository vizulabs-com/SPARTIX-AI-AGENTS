# System Architecture

## Overview

The `.spartix` system is a hub-and-spoke multi-agent operating system where all operational authority flows through the Chief Orchestrator (CO), all user communication flows through the Requirements Discovery and Approval Gate Agent (RDAG), and all knowledge persistence flows through the Wiki Custodian (WKC).

## Architecture Layers

### Layer 0: Session Bootstrap
- **Session Rules Loader (SRL)** loads all rules in priority order
- Establishes the active rule context for the session
- Must complete before any other operation

### Layer 1: User Interface
- **RDAG** is the sole user-facing agent
- Collects requirements, asks clarifications, requests approvals
- Routes user actions and configuration updates
- No other agent may communicate with the user

### Layer 2: Orchestration
- **CO** owns the complete project state
- Discovers agents, skills, hooks, and rules
- Decides assignment sequence and routing
- Sends execution intent to TBEP
- Receives all completion reports
- Sends wiki update packets to WKC
- Maintains user-visible workflow progress

### Layer 3: Task Preparation
- **TBEP** converts orchestration intent into detailed execution packets
- Defines scope, inputs, outputs, testing, review, and completion criteria
- Returns prepared packets to CO

### Layer 4: Knowledge Persistence
- **WKC** maintains the wiki as the single source of truth
- Receives wiki update packets only from CO
- Updates all history, decisions, tasks, and completion state

### Layer 5: Specialist Execution
- **400+ specialist agents** across 27 domain categories
- Execute only tasks assigned through CO
- Use approved skills, obey mandatory hooks
- Return structured completion reports to CO only

### Layer 6: Quality Gates
- **23 Review-Only Specialists** validate work quality
- **18 Enforcement Agents** ensure governance compliance
- All review results flow back to CO

## Agent Discovery

### Built-in Agent Discovery
1. CO scans `AGENTS/` directory recursively
2. CO reads `SYSTEM/agent-registry.json` for the master index
3. CO validates each agent file against the required format
4. CO builds an in-memory capability map indexed by domain and specialization

### Custom Agent Discovery
1. CO scans `custom-agents/` directory recursively
2. CO reads `SYSTEM/custom-agent-registry.json` if present
3. CO validates each custom agent against the required format
4. CO checks for naming conflicts with built-in agents
5. CO registers valid custom agents in the capability map
6. CO logs invalid or conflicting custom agents for user review

### Agent Selection Priority
1. If a built-in agent exactly matches the required specialization, use it
2. If a custom agent provides a more specific match (e.g., client-specific), prefer it
3. If both match equally, prefer built-in unless a rule override exists
4. CO documents the selection rationale in the workflow feed

## Skill Discovery

1. CO scans `SKILLS/` and reads `SKILLS/skill-index.json`
2. CO scans `custom-skills/` and reads `custom-skills/custom-skill-index.json`
3. CO validates skill metadata and availability
4. CO builds a skill availability map
5. Specialist agents request skills through CO approval

## Hook Discovery

1. CO scans `HOOKS/` and reads `HOOKS/hook-index.json`
2. CO scans `custom-hooks/` and reads `custom-hooks/custom-hook-index.json`
3. CO registers mandatory hooks (always enforced) and optional hooks
4. CO injects mandatory hooks into every task packet
5. Optional hooks are included based on task context and rules

## Session Startup Sequence

1. SRL loads `RULES/system/` (immutable system constraints)
2. SRL loads `RULES/user/` (user custom rules — loaded before project rules)
3. SRL loads `RULES/project/` (project-specific rules)
4. SRL loads `RULES/agents/` (agent-specific rules)
5. SRL loads `RULES/skills/` (skill-specific rules)
6. SRL loads `RULES/hooks/` (hook-specific rules)
7. SRL loads `RULES/sessions/` (session-specific rules)
8. SRL applies `RULES/overrides/` (explicit override declarations)
9. SRL resolves conflicts using `RULES/rule-priority-map.json`
10. SRL builds the active rule context
11. SRL passes the active rule context to CO
12. CO initializes with the active rule context
13. CO discovers agents, skills, and hooks
14. CO reads the current wiki state from `WIKI/`
15. CO signals readiness to RDAG
16. RDAG greets the user and begins requirement collection
