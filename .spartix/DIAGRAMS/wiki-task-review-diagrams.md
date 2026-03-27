# Wiki Update Flow Diagram

```
  TASK COMPLETES (or decision made, blocker found, milestone reached)
       │
       ▼
  ┌─────────┐
  │   CO    │ ──► Prepares wiki update packet:
  │         │     • Update type (task/decision/blocker/milestone/review/change)
  │         │     • Target wiki page
  │         │     • Entry content
  │         │     • Related task packet ID
  │         │     • Context and metadata
  └────┬────┘
       │ wiki update packet
       ▼
  ┌─────────┐
  │   WKC   │ ──► Validates packet structure
  │         │ ──► Identifies target wiki page
  │         │ ──► Appends entry (preserves history)
  │         │ ──► Updates cross-references
  │         │ ──► Confirms update to CO
  └────┬────┘
       │ confirmation
       ▼
  ┌─────────┐
  │   CO    │ ──► Records confirmation
  │         │ ──► Continues to next task
  └─────────┘

  WIKI PAGES UPDATED:
  ├── WIKI/requirements.md  ← requirements history
  ├── WIKI/decisions.md     ← decision history
  ├── WIKI/tasks.md         ← task history
  ├── WIKI/blockers.md      ← blocker history
  ├── WIKI/milestones.md    ← milestone tracking
  ├── WIKI/reviews.md       ← review results
  ├── WIKI/changelog.md     ← change history
  └── WIKI/project-status.md ← completion state
```

# Task Lifecycle Diagram

```
  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
  │  QUEUED  │───►│ PLANNING │───►│ ASSIGNED │───►│   IN     │
  │          │    │ (TBEP)   │    │          │    │ PROGRESS │
  └──────────┘    └──────────┘    └──────────┘    └────┬─────┘
                                                       │
                       ┌───────────────────────────────┤
                       │               │               │
                       ▼               ▼               ▼
                ┌────────────┐  ┌────────────┐  ┌──────────┐
                │ WAITING    │  │ WAITING    │  │ BLOCKED  │
                │ FOR        │  │ FOR USER   │  │          │
                │ CLARIFIC.  │  │ ACTION     │  │          │
                └──────┬─────┘  └──────┬─────┘  └──────┬───┘
                       │               │               │
                       └───────┬───────┘               │
                               │                       │
                               ▼                       │
                        ┌──────────┐                   │
                        │   IN     │◄──────────────────┘
                        │ PROGRESS │   (if unblocked)
                        └────┬─────┘
                             │
                             ▼
                      ┌──────────┐
                      │  HANDED  │
                      │  BACK TO │
                      │    CO    │
                      └────┬─────┘
                             │
                      ┌──────┴──────┐
                      │             │
                      ▼             ▼
               ┌──────────┐  ┌──────────┐
               │  UNDER   │  │ COMPLETED│
               │  REVIEW  │  │ (no      │
               │          │  │  review  │
               └────┬─────┘  │  needed) │
                    │        └────┬─────┘
                    ▼             │
             ┌──────────┐        │
             │ COMPLETED│        │
             └────┬─────┘        │
                  │              │
                  └──────┬───────┘
                         │
                         ▼
                  ┌──────────┐
                  │ SENT TO  │
                  │   WIKI   │
                  └──────────┘
```

# Completion Report Return Flow Diagram

```
  ┌──────────────┐
  │  SPECIALIST   │  Completes task execution
  │  AGENT        │
  └──────┬───────┘
         │ Structured Completion Report:
         │ • Report ID
         │ • Execution summary
         │ • Deliverables
         │ • Testing results
         │ • Issues/blockers
         │ • Risks/recommendations
         │ • Completion verification
         ▼
  ┌──────────────┐
  │     CO       │  Receives and evaluates report
  │              │
  └──────┬───────┘
         │
         ├──► All criteria met, no review needed
         │    └──► Mark COMPLETED → Wiki update → Next task
         │
         ├──► Review required
         │    └──► Assign to Review Agent
         │         │
         │         ▼
         │    ┌──────────────┐
         │    │ REVIEW AGENT │  Evaluates output
         │    └──────┬───────┘
         │           │
         │           ├──► PASS → CO marks COMPLETED → Wiki update
         │           │
         │           └──► FAIL → CO re-assigns with feedback
         │                       OR escalates
         │
         └──► Criteria not met / issues found
              └──► CO decides: re-assign, adjust plan, or escalate
```

# Review Gate Flow Diagram

```
  ┌──────────────┐
  │     CO       │  Determines review is required
  └──────┬───────┘
         │ Review assignment
         ▼
  ┌──────────────────────────────────────────────────┐
  │              REVIEW GATE                          │
  │                                                    │
  │  ┌──────────────┐                                 │
  │  │ REVIEW AGENT │  From category 30:              │
  │  │              │  • Architecture Review (ARV)     │
  │  │              │  • Code Review (CRV)             │
  │  │              │  • UX Review (UXRV)              │
  │  │              │  • Security Review (SRV)         │
  │  │              │  • Performance Review (PRV)      │
  │  │              │  • Compliance Review (CORV)      │
  │  │              │  • etc.                          │
  │  └──────┬───────┘                                 │
  │         │                                          │
  │         ├──► PASS                                  │
  │         │    • Quality criteria met                │
  │         │    • No critical issues                  │
  │         │    • Recommendations (optional)          │
  │         │                                          │
  │         └──► FAIL                                  │
  │              • Critical issues found               │
  │              • Quality below threshold             │
  │              • Specific feedback for improvement   │
  │                                                    │
  └──────────────────────────────────────────────────┘
         │
         ▼
  ┌──────────────┐
  │     CO       │  Processes review results
  │              │  PASS → complete task → wiki update
  │              │  FAIL → re-assign or escalate
  └──────────────┘
```
