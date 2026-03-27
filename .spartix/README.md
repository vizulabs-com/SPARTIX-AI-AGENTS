# .spartix — AI Operating System Specification

## Executive Summary

The `.spartix` system is a production-grade, multi-agent AI operating system specification designed to govern the full lifecycle of software projects through strict orchestration, transparent workflows, and documentation-first execution governance.

### Core Design Principles

1. **Single Communication Owner**: Only the Requirements Discovery and Approval Gate Agent (RDAG) communicates with the user.
2. **Single Orchestration Owner**: Only the Chief Orchestrator (CO) owns the full project state and distributes work.
3. **Single Wiki Owner**: Only the Wiki Custodian (WKC) writes to the wiki.
4. **No Direct Handoffs**: Specialist agents never hand off work to each other directly.
5. **No Execution Without Approval**: All work requires clarified, approved requirements and detailed task packets.
6. **Full Transparency**: The user sees every workflow step, agent assignment, and status change.
7. **Extensibility**: Custom agents, skills, hooks, and rules are first-class citizens.
8. **Documentation as Truth**: The wiki is the single source of truth for all project knowledge.

### System Scale

- **5 Control Layer Agents** governing orchestration, communication, task breakdown, wiki, and rules
- **400+ Built-in Specialist Agents** across 27 domain categories
- **23 Review-Only Specialists** for quality gates
- **18 Enforcement Agents** for governance compliance
- **Custom agent ecosystem** with grouping by application, domain, client, and shared
- **Skills, Hooks, and Rules** ecosystems with full custom extensibility
- **Wiki** as the single source of truth
- **Packets and Reports** for structured data flow
- **User-visible workflow transparency** with real-time status tracking

### Operating Model

```
User ↔ RDAG ↔ CO ↔ TBEP → Specialist Agents → CO → WKC → Wiki
                ↑                                    |
                └────────────────────────────────────┘
```

The system enforces a hub-and-spoke model where CO is the central operational brain. All work flows through CO. All user communication flows through RDAG. All wiki updates flow through WKC. All task preparation flows through TBEP. All rules are loaded by SRL at session start.

---

## Quick Navigation

| Section | Location |
|---------|----------|
| Agent Definitions | `AGENTS/` |
| Custom Agents | `custom-agents/` |
| Skills | `SKILLS/` |
| Custom Skills | `custom-skills/` |
| Hooks | `HOOKS/` |
| Custom Hooks | `custom-hooks/` |
| Rules | `RULES/` |
| Wiki | `WIKI/` |
| System Docs | `SYSTEM/` |
| Diagrams | `DIAGRAMS/` |
| Packets & Reports | `PACKETS/` |
| Workflows | `WORKFLOWS/` |

---

## File Type Policy

See `SYSTEM/file-type-policy.md` for the complete file type policy defining which folders use `.md`, `.json`, or mixed formats.

## Getting Started

1. Read this README for the executive summary
2. Review `SYSTEM/architecture.md` for the full system architecture
3. Review `SYSTEM/operating-model.md` for the operating model
4. Review `SYSTEM/dataflow.md` for end-to-end dataflow
5. Review `WORKFLOWS/` for workflow definitions
6. Review `DIAGRAMS/` for visual representations
7. Review `AGENTS/00_CONTROL_LAYER/` for the five control agents
8. Browse domain-specific agents in `AGENTS/01-31`
