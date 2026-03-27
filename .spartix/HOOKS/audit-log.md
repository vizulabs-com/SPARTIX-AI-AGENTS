# Hook: Audit Log

## Name
audit-log

## Type
global

## Mandatory
Yes — this hook fires for every agent action and cannot be disabled.

## Description
Logs all agent actions, task assignments, completion reports, wiki updates, and status changes to the audit trail for full operational traceability. Every action in the system is recorded with timestamp, agent, action type, and outcome.

## Trigger Conditions
- Any agent begins execution of a task packet
- Any agent completes execution and returns a completion report
- CO assigns a task, routes a clarification, or sends a wiki update
- WKC updates any wiki page
- Any status change occurs in the workflow feed

## Behavior
1. Capture the current timestamp in ISO 8601 format
2. Record the acting agent's name and code
3. Record the action type (task-start, task-complete, assignment, clarification, wiki-update, status-change)
4. Record the task packet ID if applicable
5. Record the outcome (success, failure, blocked, pending)
6. Append the entry to the audit trail

## Enforcement
- This hook cannot be skipped, disabled, or bypassed by any agent
- CO must include this hook in every task packet's mandatory hooks list
- Failure to trigger this hook constitutes a governance violation
