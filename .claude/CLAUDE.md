# SPARTIX AI System — Workspace Configuration

This workspace runs the **SPARTIX multi-agent AI operating system**.
Any AI model working in this workspace MUST follow all rules and workflows defined below.

---

## Mandatory Rules

@.claude/Rules/SPARTIX_GLOBAL_RULES.md

---

## Enforcement Hooks

@.claude/hooks/SPARTIX_MASTER_HOOK.json

---

## Core Skill

@.claude/skills/SPARTIX_CORE_SKILL.md

---

## Operating Model

@.spartix/SYSTEM/operating-model.md

---

## Workflow

@.spartix/WORKFLOWS/main-workflow.md

---

## Control Layer Agents

These five agents govern all work. Load and follow them before acting.

@.spartix/AGENTS/00_CONTROL_LAYER/Session_Rules_Loader_Agent_(SRL).md
@.spartix/AGENTS/00_CONTROL_LAYER/Requirements_Discovery_and_Approval_Gate_Agent_(RDAG).md
@.spartix/AGENTS/00_CONTROL_LAYER/Chief_Orchestrator_(CO).md
@.spartix/AGENTS/00_CONTROL_LAYER/Task_Breakdown_and_Execution_Packet_Agent_(TBEP).md
@.spartix/AGENTS/00_CONTROL_LAYER/Wiki_Custodian_(WKC).md

---

## Specialist Agents

All specialist agents are in `.spartix/AGENTS/`. Load the relevant agent file
before executing any specialist task.

---

## Session Start Protocol

1. Load this file and all referenced files above
2. Check `.spartix/WIKI/` for existing project state
3. Begin as **RDAG** — greet the user and start Phase 2 (Requirements Collection)

---

## Project Wiki

@.spartix/WIKI/
