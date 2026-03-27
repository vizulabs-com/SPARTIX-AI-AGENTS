# Full System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        .spartix SYSTEM ARCHITECTURE                         │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌──────────┐                                                               │
│  │   USER   │◄──────────────────────────────────────────────────────┐       │
│  └────┬─────┘                                                       │       │
│       │ requests, responses, approvals, actions                     │       │
│       ▼                                                             │       │
│  ┌─────────────────────────────────────────────┐                    │       │
│  │  LAYER 1: USER INTERFACE                     │                    │       │
│  │  ┌───────────────────────────────────────┐   │                    │       │
│  │  │  RDAG (Requirements Discovery &       │   │  user-visible      │       │
│  │  │  Approval Gate Agent)                 │   │  workflow feed      │       │
│  │  │  • Collects requirements              │   │────────────────────┘       │
│  │  │  • Asks clarifications                │   │                            │
│  │  │  • Requests approvals                 │   │                            │
│  │  │  • Requests user actions              │   │                            │
│  │  └──────────────┬────────────────────────┘   │                            │
│  └─────────────────┼────────────────────────────┘                            │
│                    │ approved requirements,                                   │
│                    │ validated responses                                      │
│                    ▼                                                          │
│  ┌─────────────────────────────────────────────────────────────────────┐     │
│  │  LAYER 0: SESSION BOOTSTRAP                                         │     │
│  │  ┌─────────────────────┐                                            │     │
│  │  │  SRL (Session Rules  │  active rule context                      │     │
│  │  │  Loader Agent)       │──────────────────┐                        │     │
│  │  │  • Loads all rules   │                  │                        │     │
│  │  │  • Resolves conflicts│                  │                        │     │
│  │  └─────────────────────┘                  │                        │     │
│  └───────────────────────────────────────────┼────────────────────────┘     │
│                                              ▼                              │
│  ┌─────────────────────────────────────────────────────────────────────┐     │
│  │  LAYER 2: ORCHESTRATION                                             │     │
│  │  ┌───────────────────────────────────────────────────────────────┐  │     │
│  │  │  CO (Chief Orchestrator)                                      │  │     │
│  │  │  • Owns complete project state                                │  │     │
│  │  │  • Discovers agents, skills, hooks                            │  │     │
│  │  │  • Decides next task and agent                                │  │     │
│  │  │  • Assigns work via task packets                              │  │     │
│  │  │  • Receives all completion reports                            │  │     │
│  │  │  • Routes clarifications to RDAG                              │  │     │
│  │  │  • Sends wiki updates to WKC                                  │  │     │
│  │  │  • Maintains workflow feed                                    │  │     │
│  │  └──┬──────────┬──────────────┬──────────────┬───────────────────┘  │     │
│  └─────┼──────────┼──────────────┼──────────────┼──────────────────────┘     │
│        │          │              │              │                             │
│        ▼          ▼              ▼              ▼                             │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────────────────┐    │
│  │ LAYER 3  │ │ LAYER 4  │ │ LAYER 6  │ │ LAYER 5: SPECIALIST          │    │
│  │ TBEP     │ │ WKC      │ │ REVIEW   │ │ EXECUTION                    │    │
│  │ (Task    │ │ (Wiki    │ │ AGENTS   │ │                              │    │
│  │ Breakdown│ │ Custodian│ │ (23)     │ │ 400+ Specialist Agents       │    │
│  │ Agent)   │ │ Agent)   │ │          │ │ across 27 domain categories  │    │
│  │          │ │          │ │ ENFORCE  │ │                              │    │
│  │ Prepares │ │ Updates  │ │ AGENTS   │ │ Execute tasks via packets    │    │
│  │ task     │ │ wiki     │ │ (18)     │ │ Use approved skills          │    │
│  │ packets  │ │ pages    │ │          │ │ Obey mandatory hooks         │    │
│  └──────────┘ └──────────┘ └──────────┘ │ Return reports to CO only    │    │
│                                          └──────────────────────────────┘    │
│                                                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐     │
│  │  SUPPORTING SYSTEMS                                                 │     │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐           │     │
│  │  │  SKILLS  │  │  HOOKS   │  │  RULES   │  │  WIKI    │           │     │
│  │  │  Built-in│  │  Built-in│  │  System  │  │  Single  │           │     │
│  │  │  Custom  │  │  Custom  │  │  User    │  │  Source  │           │     │
│  │  │          │  │  Pre/Mid │  │  Project │  │  of      │           │     │
│  │  │          │  │  Post    │  │  Agent   │  │  Truth   │           │     │
│  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘           │     │
│  └─────────────────────────────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────────────────────┘
```
