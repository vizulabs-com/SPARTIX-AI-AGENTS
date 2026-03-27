# User-Visible Workflow Transparency Model

## Purpose
The user must be able to see what is happening at every operational step. This document defines the visibility model, status labels, and progress behavior.

## Workflow Status Labels

| Status | Description | Triggered When |
|--------|-------------|----------------|
| `queued` | Task is waiting to be assigned | CO has identified the task but not yet assigned it |
| `assigned` | Task has been assigned to a specialist | CO assigns the task packet to an agent |
| `planning` | Task packet is being prepared | CO sends execution intent to TBEP |
| `in progress` | Specialist is actively executing | Specialist begins work |
| `waiting for clarification` | User input is needed | Clarification request routed to RDAG |
| `waiting for user action` | User must perform an external action | User action request routed to RDAG |
| `under review` | Output is being reviewed | CO assigns to a review specialist |
| `completed` | Task is finished and approved | Review passes or CO marks complete |
| `blocked` | Task cannot proceed | Blocker identified that cannot be resolved |
| `handed back to orchestrator` | Specialist returned work to CO | Specialist reports completion or blocker |
| `sent to wiki` | Results are being recorded | CO sends wiki update packet to WKC |

## Workflow Feed Entries

Each entry in the user-visible workflow feed contains:

- **Timestamp**: When the event occurred
- **Task ID**: Reference to the task packet
- **Agent**: Which agent is involved
- **Status**: Current status label
- **Description**: What is happening
- **Selection Rationale**: Why this agent was chosen (on assignment)
- **Expected Action**: What the agent is expected to do
- **Blocker Info**: If blocked, what is blocking and what is needed
- **Next Agent**: If known, who works next

## Visibility Rules

1. Every status change must produce a workflow feed entry
2. The user must see which agent received the work and why
3. The user must see what the agent is expected to do
4. The user must see whether clarification or user action is needed
5. The user must see review status and results
6. The user must see what was returned to CO
7. The user must see what was sent to WKC
8. The user must see which agent is next (when known)
9. Blocked tasks must show the blocker reason and required resolution
10. The workflow feed must be chronologically ordered

## Progress Visibility Behavior

- **Real-time updates**: Status changes are reflected immediately in the feed
- **Contextual detail**: Each entry includes enough context for the user to understand what is happening without needing to read internal packets
- **Escalation visibility**: If a task is re-assigned or escalated, the feed shows why
- **Completion summary**: When a task completes, the feed shows a brief summary of what was accomplished
