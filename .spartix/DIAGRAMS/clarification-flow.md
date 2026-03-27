# User Clarification Flow Diagram

```
┌──────────────┐
│  SPECIALIST   │  Detects missing info / ambiguity
│  AGENT        │
└──────┬───────┘
       │ Clarification Request Packet
       ▼
┌──────────────┐
│     CO       │  Evaluates: Is user input truly needed?
│              │
└──────┬───────┘
       │
       ├──── NO: CO resolves internally (from wiki/rules) → continues
       │
       ▼ YES
┌──────────────┐
│    RDAG      │  Formulates clear question for user
│              │
└──────┬───────┘
       │ Question with context
       ▼
┌──────────────┐
│    USER      │  Provides answer / makes decision
│              │
└──────┬───────┘
       │ Response
       ▼
┌──────────────┐
│    RDAG      │  Validates response for completeness
│              │
└──────┬───────┘
       │ Validated response
       ▼
┌──────────────┐
│     CO       │  Updates plan if needed
│              │  Continues routing work
└──────────────┘

WORKFLOW FEED STATUS DURING CLARIFICATION:
  Task status: "waiting for clarification"
  Shows: which agent asked, what is being asked, user must respond
  On resolution: status returns to "in progress"
```

# User Action Required Flow Diagram

```
┌──────────────┐
│  SPECIALIST   │  Detects need for user-managed action
│  AGENT        │  (file update, config, external setup)
└──────┬───────┘
       │ User Action Required Packet
       ▼
┌──────────────┐
│     CO       │  Validates need for user action
│              │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    RDAG      │  Presents action request to user:
│              │  • What needs to be done
│              │  • Step-by-step instructions
│              │  • Expected format/values
│              │  • Why it is needed
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    USER      │  Performs the action
│              │  (updates file, provides config, etc.)
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    RDAG      │  Validates action was completed correctly
│              │
└──────┬───────┘
       │ Confirmation
       ▼
┌──────────────┐
│     CO       │  Continues routing work
│              │
└──────────────┘

WORKFLOW FEED STATUS DURING USER ACTION:
  Task status: "waiting for user action"
  Shows: what action is needed, instructions, user must act
  On completion: status returns to "in progress"
```
