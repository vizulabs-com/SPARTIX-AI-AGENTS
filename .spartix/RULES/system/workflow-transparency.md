# System Rule: Workflow Transparency

**Rule ID**: SYS-002
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
The full `.spartix` workflow must be visibly transparent to the user at all times. The user must see the operational flow between agents step by step in a structured, readable way. This is mandatory and cannot be overridden.

## Transparency Requirement
For every important workflow step, always show the user:

- which agent received the work
- why this agent was selected
- what this agent is about to do
- what inputs this agent is using
- what output this agent is expected to produce
- when the agent finishes
- what the agent returned
- what was sent to the orchestrator
- what was sent to the wiki owner
- who the next responsible agent is

Do not hide the inter-agent workflow from the user.

## Visibility Format

### When work moves between agents, show:

```
### Workflow Update
- Current Owner: [Agent Name]
- Action: [What is happening now]
- Reason: [Why this step is needed]
- Input: [What this agent received]
- Expected Output: [What this agent must return]
- Next Planned Owner: [Next Agent]
```

### When an agent finishes, show:

```
### Step Completed
- Agent: [Agent Name]
- Result: [What was completed]
- Output Produced: [Summary of output]
- Returned To: Chief Orchestrator (CO)
- Next Step: [What happens next]
```

## Task Packet Visibility Rule
Whenever TBEP prepares a task packet, show:

```
### Task Packet Prepared
- Prepared By: Task Breakdown and Execution Packet Agent (TBEP)
- Assigned To: [Specialist Agent]
- Objective: [Short summary]
- Scope: [Short summary]
- Expected Result: [Short summary]
```

## Clarification Visibility Rule
If any specialist needs clarification, approval, credentials, config values, file updates, assets, or missing info:

```
### Clarification Routing
- Source Agent: [Specialist Agent]
- Returned To: Chief Orchestrator (CO)
- Routed To: Requirements Discovery and Approval Gate Agent (RDAG)
- Waiting For: User clarification / approval / action
```

## Wiki Visibility Rule
Whenever CO sends an update to WKC:

```
### Wiki Update
- Sent By: Chief Orchestrator (CO)
- Received By: Wiki Custodian (WKC)
- Purpose: [Update description]
```

## Review Visibility Rule
Whenever a review gate happens:

```
### Review Step
- Reviewing Agent: [Review Agent Name]
- Review Type: [Architecture / Security / QA / Performance / etc.]
- Target: [What is being reviewed]
- Result: [Passed / Failed / Needs fixes]
```

## Visible Workflow Timeline Statuses
Maintain a continuous visible workflow timeline using:
- queued
- assigned
- planning
- in progress
- waiting for clarification
- waiting for user action
- under review
- completed
- returned to orchestrator
- sent to wiki
- next step assigned

## Ownership Preservation
While showing all workflow steps visibly:
- RDAG remains the only direct user-facing clarification owner
- CO remains the only orchestration owner
- TBEP remains the task packet owner
- WKC remains the only wiki-writing owner

## Override Policy
This rule cannot be overridden by any other rule at any level. It is immutable.
