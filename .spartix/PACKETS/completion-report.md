# Task Completion Report Definition

## Purpose
A Task Completion Report is the structured document returned by a specialist agent to CO after task execution. It provides a complete account of what was done, what was produced, any issues encountered, and the final status.

## Required Sections

### Header
- **Report ID**: Unique identifier (e.g., `CR-2024-001`)
- **Task Packet ID**: Reference to the original task packet
- **Agent Name**: Full name and short code of the reporting agent
- **Started At**: Timestamp when execution began
- **Completed At**: Timestamp when execution finished
- **Status**: completed / completed-with-warnings / blocked / failed

### Execution Summary
- **What Was Done**: Concise summary of work performed
- **Approach Taken**: How the agent approached the task
- **Skills Used**: Which approved skills were utilized
- **Hooks Obeyed**: Which mandatory hooks were triggered and obeyed

### Deliverables
- **Primary Outputs**: List of deliverables produced
- **Output Locations**: Where each deliverable can be found
- **Output Quality Assessment**: Self-assessment of output quality

### Testing Results
- **Tests Performed**: What testing was done per the task packet requirements
- **Test Results**: Pass/fail status for each test
- **Coverage Notes**: Any gaps in testing coverage

### Issues and Blockers
- **Issues Encountered**: Problems found during execution
- **Blockers**: Any items that blocked or delayed execution
- **Workarounds Applied**: How issues were addressed
- **Unresolved Items**: Anything that remains unresolved

### Risks and Recommendations
- **Identified Risks**: Risks discovered during execution
- **Recommendations**: Suggestions for CO consideration
- **Follow-up Actions**: Suggested next steps

### Completion Verification
- **Completion Criteria Met**: Yes/No for each criterion from the task packet
- **Verification Evidence**: How each criterion was verified
- **Deviations from Plan**: Any deviations from the original task packet

### Return to CO
- **Ready for Review**: Yes/No
- **Suggested Reviewer**: Recommended review agent (if applicable)
- **Dependencies Unlocked**: What tasks can now proceed
