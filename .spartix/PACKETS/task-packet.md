# Task Packet Definition

## Purpose
A Task Packet is the structured execution document prepared by TBEP and approved by CO before any specialist agent begins work. It ensures no specialist ever receives a vague task.

## Required Sections

### Header
- **Packet ID**: Unique identifier (e.g., `TP-2024-001`)
- **Created By**: TBEP
- **Approved By**: CO
- **Created At**: Timestamp
- **Approved At**: Timestamp
- **Priority**: Critical / High / Medium / Low

### Assignment
- **Assigned Agent**: Full agent name and short code
- **Agent Category**: Category folder (e.g., `04_FRONTEND_WEB_SPECIALISTS`)
- **Selection Rationale**: Why this agent was chosen over alternatives

### Task Definition
- **Task Title**: Clear, concise title
- **Task Description**: Detailed description of what must be accomplished
- **Business Context**: Why this task matters to the project
- **Dependencies**: What must be completed before this task
- **Predecessor Tasks**: List of completed tasks this depends on

### Scope
- **In-Scope Work**: Explicit list of what the specialist must do
- **Out-of-Scope Work**: Explicit list of what the specialist must NOT do
- **Boundaries**: Clear boundaries of responsibility

### Inputs
- **Required Inputs**: What the specialist needs to begin work
- **Reference Materials**: Links to wiki pages, previous outputs, or documentation
- **Context from Previous Tasks**: Relevant outputs from predecessor tasks

### Expected Outputs
- **Primary Deliverables**: What must be produced
- **Output Format**: Expected format for each deliverable
- **Quality Standards**: Minimum quality requirements

### Testing Requirements
- **Test Criteria**: How the output will be validated
- **Test Scenarios**: Specific scenarios to verify
- **Acceptance Thresholds**: Minimum pass criteria

### Review Requirements
- **Review Agent**: Which review specialist will evaluate the output
- **Review Criteria**: What the reviewer will assess
- **Review Gate**: Must pass review before task is marked complete

### Completion Criteria
- **Done When**: Explicit conditions that define task completion
- **Verification Method**: How completion is verified

### Return Requirements
- **Completion Report Format**: What the completion report must contain
- **Required Sections**: Mandatory sections in the report
- **Blocker Reporting**: How to report any blockers encountered

### Governance
- **Mandatory Hooks**: List of hooks that must be obeyed during execution
- **Approved Skills**: List of skills the agent may use
- **Active Rules**: Relevant rules that apply to this task
- **Constraints**: Any additional constraints from the active rule context
