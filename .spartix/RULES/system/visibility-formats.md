# System Rule: Visibility Formats

**Rule ID**: SYS-004
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
Defines the mandatory structured formats for all visible workflow updates shown to the user.

---

## Rule 11: Required Visible Workflow Update Formats

### Workflow Transition:
```
## Workflow Update
- Current Owner: [Agent Name]
- Action: [What is happening now]
- Reason: [Why this step is needed]
- Input: [What this agent received]
- Expected Output: [What this agent must return]
- Next Planned Owner: [Next Agent]
```

### Step Completion:
```
## Step Completed
- Agent: [Agent Name]
- Result: [What was completed]
- Output Produced: [Summary of output]
- Returned To: Chief Orchestrator (CO)
- Next Step: [What happens next]
```

### Clarification Routing:
```
## Clarification Routing
- Source Agent: [Specialist Agent]
- Returned To: Chief Orchestrator (CO)
- Routed To: Requirements Discovery and Approval Gate Agent (RDAG)
- Waiting For: User clarification / approval / action
```

### Task Packet Prepared:
```
## Task Packet Prepared
- Prepared By: Task Breakdown and Execution Packet Agent (TBEP)
- Assigned To: [Specialist Agent]
- Objective: [Short summary]
- Scope: [Short summary]
- Expected Result: [Short summary]
```

### Task Packet Review:
```
## Task Packet Review
- Reviewed By: Chief Orchestrator (CO)
- Check: Completeness, clarity, scope, and step-by-step readiness
- Result: Approved or returned for correction
```

### Wiki Update Before Execution:
```
## Wiki Update Before Execution
- Sent By: Chief Orchestrator (CO)
- Received By: Wiki Custodian (WKC)
- Purpose: Record the approved task packet, workflow transition, and planned execution state
- Status: Execution is blocked until wiki update is completed
```

### Execution Unlock:
```
## Execution Unlock
- Trigger: Wiki Custodian (WKC) completed the wiki update
- Approved By: Chief Orchestrator (CO)
- Result: Assigned specialist agent may now begin execution
```

### Review Step:
```
## Review Step
- Reviewing Agent: [Review Agent Name]
- Review Type: [Architecture / Security / QA / Performance / etc.]
- Target: [What is being reviewed]
- Result: [Passed / Failed / Needs fixes]
```

### Wiki Update:
```
## Wiki Update
- Sent By: Chief Orchestrator (CO)
- Received By: Wiki Custodian (WKC)
- Purpose: Update project history / decisions / task progress / completion state
```

## Rule 12: Visible Workflow Timeline Statuses
Maintain continuous visible timeline using: queued, assigned, planning, task packet being prepared, task packet under review, waiting for wiki update, execution unlocked, in progress, waiting for clarification, waiting for user action, under review, completed, returned to orchestrator, sent to wiki, next step assigned.

## Override Policy
These formats cannot be overridden by any other rule at any level.
