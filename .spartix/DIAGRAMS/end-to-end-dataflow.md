# End-to-End Project Dataflow Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│           END-TO-END DATAFLOW: USER REQUEST → PROJECT COMPLETION         │
└─────────────────────────────────────────────────────────────────────────┘

  ┌──────┐
  │ USER │ ─── request ──────────────────────────────────────────┐
  └──────┘                                                       │
                                                                 ▼
  ┌────────────────────────────────────────────────────────────────────┐
  │ PHASE 1: SESSION BOOTSTRAP                                         │
  │                                                                     │
  │  SRL ──► loads rules ──► resolves conflicts ──► active rule ctx    │
  │                                                       │             │
  │  CO  ◄── active rule ctx ◄────────────────────────────┘             │
  │  CO  ──► discovers agents ──► discovers skills ──► discovers hooks  │
  │  CO  ──► reads wiki state ──► builds project state                  │
  │  CO  ──► signals readiness to RDAG                                  │
  └────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
  ┌────────────────────────────────────────────────────────────────────┐
  │ PHASE 2: REQUIREMENTS                                              │
  │                                                                     │
  │  RDAG ◄── user request                                              │
  │  RDAG ──► asks clarifications ──► user responds                     │
  │  RDAG ──► proposes summary ──► user approves                        │
  │  RDAG ──► passes approved requirements to CO                        │
  └────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
  ┌────────────────────────────────────────────────────────────────────┐
  │ PHASE 3-8: EXECUTION LOOP (repeats for each task)                  │
  │                                                                     │
  │  CO ──► analyzes state ──► selects task + agent                     │
  │         │                                                           │
  │         ▼                                                           │
  │  CO ──► sends intent to TBEP                                        │
  │         │                                                           │
  │         ▼                                                           │
  │  TBEP ──► creates task packet ──► returns to CO                     │
  │         │                                                           │
  │         ▼                                                           │
  │  CO ──► approves packet ──► assigns to specialist                   │
  │         │                                                           │
  │         ▼                                                           │
  │  SPECIALIST ──► executes (skills + hooks) ──► completion report     │
  │         │                                                           │
  │         ▼                                                           │
  │  CO ──► receives report ──► assigns review (if needed)              │
  │         │                                                           │
  │         ▼                                                           │
  │  REVIEW AGENT ──► evaluates ──► results to CO                       │
  │         │                                                           │
  │         ▼                                                           │
  │  CO ──► wiki update packet ──► WKC updates wiki                     │
  │         │                                                           │
  │         ▼                                                           │
  │  CO ──► selects next task ──► LOOP or COMPLETE                      │
  │                                                                     │
  │  [CLARIFICATION BRANCH]                                             │
  │  Specialist ──► CO ──► RDAG ──► User ──► RDAG ──► CO ──► continue  │
  │                                                                     │
  │  [USER ACTION BRANCH]                                               │
  │  Specialist ──► CO ──► RDAG ──► User acts ──► RDAG ──► CO          │
  └────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
  ┌────────────────────────────────────────────────────────────────────┐
  │ PHASE 9: PROJECT COMPLETION                                        │
  │                                                                     │
  │  CO ──► verifies all requirements met                               │
  │  CO ──► final wiki update ──► WKC records completion                │
  │  CO ──► notifies RDAG                                               │
  │  RDAG ──► informs user: PROJECT COMPLETE                            │
  └────────────────────────────────────────────────────────────────────┘
```

# Visible Progress Feed Flow Diagram

```
  EVERY STATUS CHANGE produces a feed entry:

  ┌──────────────────────────────────────────────────────────────┐
  │  USER-VISIBLE WORKFLOW FEED                                   │
  │                                                               │
  │  [timestamp] Task TP-001 QUEUED                               │
  │    Agent: Frontend Web Agent (FWA)                            │
  │    Reason: Implement login page per approved requirements     │
  │                                                               │
  │  [timestamp] Task TP-001 PLANNING                             │
  │    TBEP preparing detailed task packet                        │
  │                                                               │
  │  [timestamp] Task TP-001 ASSIGNED                             │
  │    Agent: Frontend Web Agent (FWA)                            │
  │    Selection: Best match for React component implementation   │
  │    Expected: Build login form with validation                 │
  │                                                               │
  │  [timestamp] Task TP-001 IN PROGRESS                          │
  │    FWA executing task packet                                  │
  │                                                               │
  │  [timestamp] Task TP-001 WAITING FOR CLARIFICATION            │
  │    FWA needs: OAuth provider preference (Google vs GitHub)    │
  │    User must respond                                          │
  │                                                               │
  │  [timestamp] Task TP-001 IN PROGRESS                          │
  │    Clarification resolved, FWA continuing                     │
  │                                                               │
  │  [timestamp] Task TP-001 HANDED BACK TO ORCHESTRATOR          │
  │    FWA returned completion report                             │
  │                                                               │
  │  [timestamp] Task TP-001 UNDER REVIEW                         │
  │    Reviewer: Code Review Agent (CRV)                          │
  │                                                               │
  │  [timestamp] Task TP-001 COMPLETED                            │
  │    Review passed. Login page implemented.                     │
  │                                                               │
  │  [timestamp] Task TP-001 SENT TO WIKI                         │
  │    WKC updating task history and decisions                    │
  │                                                               │
  │  [timestamp] Next: Task TP-002 QUEUED                         │
  │    Agent: Backend Agent (BEA)                                 │
  │    Reason: Implement authentication API endpoints             │
  └──────────────────────────────────────────────────────────────┘
```

# Built-in vs Custom Agent Selection Flow Diagram

```
  CO needs to assign a task
       │
       ▼
  ┌──────────────────────────────────┐
  │  Identify required specialization │
  └──────────────┬───────────────────┘
                 │
                 ▼
  ┌──────────────────────────────────┐
  │  Search built-in agents           │
  │  (AGENTS/ + agent-registry.json)  │
  └──────────────┬───────────────────┘
                 │
                 ├──► Exact match found
                 │    │
                 │    ▼
                 │    Search custom agents for more specific match
                 │    │
                 │    ├──► Custom agent is more specific → USE CUSTOM
                 │    │    (e.g., client-specific variant)
                 │    │
                 │    └──► No better custom match → USE BUILT-IN
                 │
                 └──► No exact match
                      │
                      ▼
                      Search custom agents
                      │
                      ├──► Custom match found → USE CUSTOM
                      │
                      └──► No match → CO flags gap, may request
                           user to create custom agent or adjust plan

  OVERRIDE RULES:
  If a rule override exists that prefers custom over built-in
  for a specific domain or client → honor the override
```

# Error Prevention / Gating Model Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│              ERROR PREVENTION GATING MODEL                        │
└─────────────────────────────────────────────────────────────────┘

  GATE 1: REQUIREMENT CLARITY (RDAG)
  ├── Prevents: ambiguous requirements entering the system
  ├── How: iterative clarification + explicit approval
  └── Result: only validated, approved requirements proceed

  GATE 2: ORCHESTRATION INTEGRITY (CO)
  ├── Prevents: misrouting, wrong agent selection, sequencing errors
  ├── How: complete state awareness + rule-based decisions
  └── Result: correct agent gets correct task in correct order

  GATE 3: TASK PRECISION (TBEP)
  ├── Prevents: vague execution, scope creep, missing criteria
  ├── How: detailed task packets with explicit scope and criteria
  └── Result: specialist knows exactly what to do and not do

  GATE 4: EXECUTION GOVERNANCE (Hooks + Rules)
  ├── Prevents: process drift, unauthorized actions, skipped steps
  ├── How: mandatory hooks enforced, rules applied, skills approved
  └── Result: execution follows governed process

  GATE 5: QUALITY ASSURANCE (Review Agents)
  ├── Prevents: defective output propagating to next phase
  ├── How: specialized review agents evaluate against criteria
  └── Result: only quality-approved work proceeds

  GATE 6: KNOWLEDGE INTEGRITY (WKC)
  ├── Prevents: inconsistent project knowledge, lost decisions
  ├── How: single wiki owner, structured update packets
  └── Result: wiki is always accurate and complete

  GATE 7: COMMUNICATION INTEGRITY (RDAG only)
  ├── Prevents: user confusion from multiple agent voices
  ├── How: single communication owner for all user interaction
  └── Result: user gets consistent, clear communication

  GATE 8: ENFORCEMENT (Enforcement Agents)
  ├── Prevents: governance violations, standard deviations
  ├── How: 18 enforcement agents checking compliance
  └── Result: standards are maintained across all work
```
