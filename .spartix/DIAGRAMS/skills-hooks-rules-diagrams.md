# Skill Usage Flow Diagram

```
┌──────────────┐
│  SPECIALIST   │  Needs to use a skill during execution
│  AGENT        │
└──────┬───────┘
       │ Checks task packet for approved skills
       ▼
┌──────────────────────────────────────────┐
│  APPROVED SKILLS LIST (from task packet)  │
│  ├── Skill A (built-in)                   │
│  ├── Skill B (custom)                     │
│  └── Skill C (built-in)                   │
└──────────────┬───────────────────────────┘
               │
               ├──► Skill is in approved list → USE IT
               │    └── Execute skill
               │         └── Record skill usage in completion report
               │
               └──► Skill is NOT in approved list → CANNOT USE
                    └── Report to CO that additional skill is needed
                         └── CO evaluates and may update task packet

SKILL DISCOVERY BY CO:
  ┌──────────────┐
  │     CO       │
  └──────┬───────┘
         │
         ├──► Read SKILLS/skill-index.json
         │    └── Built-in skills with metadata
         │
         ├──► Read custom-skills/custom-skill-index.json
         │    └── Custom skills with metadata
         │
         └──► Build skill availability map
              └── Include in task packets as "approved skills"
```

# Hook Trigger Flow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    HOOK TRIGGER FLOW                          │
└─────────────────────────────────────────────────────────────┘

  TASK EXECUTION LIFECYCLE:

  ┌─────────────────┐
  │  PRE-ACTION      │  Triggered BEFORE specialist begins work
  │  HOOKS           │  Examples:
  │                   │  • Validate inputs
  │                   │  • Check permissions
  │                   │  • Log start event
  │                   │  • Enforce pre-conditions
  └────────┬──────────┘
           │
           ▼
  ┌─────────────────┐
  │  SPECIALIST      │  Executes the task
  │  EXECUTION       │
  └────────┬──────────┘
           │
           ▼
  ┌─────────────────┐
  │  MID-PROCESS     │  Triggered DURING execution at checkpoints
  │  HOOKS           │  Examples:
  │                   │  • Progress logging
  │                   │  • Intermediate validation
  │                   │  • Resource usage checks
  │                   │  • Compliance checkpoints
  └────────┬──────────┘
           │
           ▼
  ┌─────────────────┐
  │  POST-ACTION     │  Triggered AFTER specialist completes
  │  HOOKS           │  Examples:
  │                   │  • Validate outputs
  │                   │  • Log completion event
  │                   │  • Trigger notifications
  │                   │  • Enforce post-conditions
  └────────┬──────────┘
           │
           ▼
  ┌─────────────────┐
  │  GLOBAL HOOKS    │  Always active regardless of task
  │                   │  Examples:
  │                   │  • Audit logging
  │                   │  • Security monitoring
  │                   │  • Performance tracking
  └───────────────────┘

  MANDATORY vs OPTIONAL:
  ┌──────────────────────────────────────────────┐
  │  MANDATORY HOOKS: Always enforced. Included   │
  │  in every task packet by CO. Cannot be         │
  │  skipped by any agent.                         │
  │                                                │
  │  OPTIONAL HOOKS: Included based on task        │
  │  context and active rules. CO decides which    │
  │  optional hooks apply per task.                │
  └──────────────────────────────────────────────┘
```

# Rules Loading Hierarchy Diagram

```
┌─────────────────────────────────────────────────────────────┐
│              RULES LOADING HIERARCHY                          │
│              (Loaded by SRL at session start)                 │
└─────────────────────────────────────────────────────────────┘

  LOADING ORDER (top = loaded first, bottom = loaded last):

  1. ┌─────────────────────────────────────────┐
     │  SYSTEM RULES (RULES/system/)           │  IMMUTABLE
     │  Base safety and operational constraints │  Cannot be overridden
     │  Always loaded first                     │
     └─────────────────────────────────────────┘
           │
  2. ┌─────────────────────────────────────────┐
     │  USER CUSTOM RULES (RULES/user/)        │  LOADED BEFORE PROJECT
     │  User-defined preferences and standards  │  Can override project rules
     │  Loaded before project rules             │  Cannot override system rules
     └─────────────────────────────────────────┘
           │
  3. ┌─────────────────────────────────────────┐
     │  PROJECT RULES (RULES/project/)         │
     │  Project-specific governance             │  Cannot override system or
     │  Loaded after user rules                 │  user rules
     └─────────────────────────────────────────┘
           │
  4. ┌─────────────────────────────────────────┐
     │  AGENT RULES (RULES/agents/)            │
     │  Agent-specific behavior constraints     │
     └─────────────────────────────────────────┘
           │
  5. ┌─────────────────────────────────────────┐
     │  SKILL RULES (RULES/skills/)            │
     │  Skill usage constraints                 │
     └─────────────────────────────────────────┘
           │
  6. ┌─────────────────────────────────────────┐
     │  HOOK RULES (RULES/hooks/)              │
     │  Hook trigger and enforcement rules      │
     └─────────────────────────────────────────┘
           │
  7. ┌─────────────────────────────────────────┐
     │  SESSION RULES (RULES/sessions/)        │
     │  Session-specific overrides              │
     └─────────────────────────────────────────┘
           │
  8. ┌─────────────────────────────────────────┐
     │  OVERRIDES (RULES/overrides/)           │
     │  Explicit override declarations          │  Applied last
     │  Must not override system rules          │  Highest user priority
     └─────────────────────────────────────────┘

  CONFLICT RESOLUTION:
  ┌──────────────────────────────────────────────┐
  │  Resolved using RULES/rule-priority-map.json  │
  │  System rules always win                       │
  │  User rules override project rules             │
  │  Explicit overrides apply last (except system) │
  │  Unresolvable conflicts flagged for CO         │
  └──────────────────────────────────────────────┘
```

# Session Bootstrap Diagram

```
  NEW SESSION
       │
       ▼
  ┌─────────┐
  │   SRL   │ ──► Load system rules
  │         │ ──► Load user custom rules
  │         │ ──► Load project rules
  │         │ ──► Load agent/skill/hook/session rules
  │         │ ──► Apply overrides
  │         │ ──► Resolve conflicts
  │         │ ──► Build active rule context
  └────┬────┘
       │ active rule context
       ▼
  ┌─────────┐
  │   CO    │ ──► Load rule context
  │         │ ──► Discover built-in agents (AGENTS/ + registry)
  │         │ ──► Discover custom agents (custom-agents/ + registry)
  │         │ ──► Discover skills (SKILLS/ + custom-skills/)
  │         │ ──► Discover hooks (HOOKS/ + custom-hooks/)
  │         │ ──► Read wiki state (WIKI/)
  │         │ ──► Build complete project state
  │         │ ──► Signal readiness
  └────┬────┘
       │
       ▼
  ┌─────────┐
  │  RDAG   │ ──► Greet user
  │         │ ──► Begin requirement collection
  └─────────┘
```
