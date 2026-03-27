# Control Layer Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    CONTROL LAYER WORKFLOW                         │
└─────────────────────────────────────────────────────────────────┘

  SESSION START
       │
       ▼
  ┌─────────┐
  │   SRL   │ ──── Loads rules in order:
  │         │      1. System rules (immutable)
  │         │      2. User custom rules
  │         │      3. Project rules
  │         │      4. Agent/Skill/Hook/Session rules
  │         │      5. Override declarations
  └────┬────┘
       │ active rule context
       ▼
  ┌─────────┐
  │   CO    │ ──── Initializes:
  │         │      1. Loads rule context
  │         │      2. Discovers agents
  │         │      3. Discovers skills & hooks
  │         │      4. Reads wiki state
  │         │      5. Builds project state
  └────┬────┘
       │ signals readiness
       ▼
  ┌─────────┐
  │  RDAG   │ ──── Begins user interaction:
  │         │      1. Greets user
  │         │      2. Collects requirements
  │         │      3. Asks clarifications
  │         │      4. Gets approval
  └────┬────┘
       │ approved requirements
       ▼
  ┌─────────┐
  │   CO    │ ──── Plans execution:
  │         │      1. Analyzes state
  │         │      2. Determines strategy
  │         │      3. Selects first task
  └────┬────┘
       │ execution intent
       ▼
  ┌─────────┐
  │  TBEP   │ ──── Prepares task packet:
  │         │      1. Defines scope
  │         │      2. Defines inputs/outputs
  │         │      3. Defines criteria
  │         │      4. Includes hooks/skills
  └────┬────┘
       │ prepared packet
       ▼
  ┌─────────┐
  │   CO    │ ──── Approves and assigns:
  │         │      1. Reviews packet
  │         │      2. Assigns to specialist
  │         │      3. Updates workflow feed
  └────┬────┘
       │ task packet
       ▼
  ┌──────────────┐
  │  SPECIALIST  │ ──── Executes:
  │              │      1. Validates inputs
  │              │      2. Uses skills
  │              │      3. Obeys hooks
  │              │      4. Produces output
  └──────┬───────┘
         │ completion report
         ▼
  ┌─────────┐
  │   CO    │ ──── Processes results:
  │         │      1. Receives report
  │         │      2. Assigns review (if needed)
  │         │      3. Updates workflow feed
  └────┬────┘
       │ wiki update packet
       ▼
  ┌─────────┐
  │   WKC   │ ──── Records in wiki:
  │         │      1. Updates relevant pages
  │         │      2. Confirms to CO
  └─────────┘
       │
       ▼
  CO selects next task → loop back to TBEP
  OR project complete → final wiki update → RDAG informs user
```
