# User Action Required Packet Definition

## Purpose
A User Action Required Packet is used when the system needs the user to perform an external action such as updating a file, providing configuration values, setting up an external service, or making a decision that cannot be automated.

## Required Sections

### Header
- **Packet ID**: Unique identifier (e.g., `UAR-2024-001`)
- **Requesting Agent**: Name and code of the agent that needs user action
- **Related Task Packet ID**: Reference to the task being executed
- **Created At**: Timestamp
- **Urgency**: blocking | non-blocking

### Action Details
- **What Needs to Be Done**: Clear description of the required action
- **Why It Is Needed**: Why the system cannot perform this action automatically
- **Step-by-Step Instructions**: Detailed steps for the user to follow
- **Expected Outcome**: What the result should look like after the action

### File or Configuration Details (if applicable)
- **Target File**: Path to the file that needs to be updated
- **Expected Format**: Format or schema the file should follow
- **Example Values**: Example of what valid values look like
- **Current State**: What the file currently contains (if relevant)

### Validation
- **How to Verify**: How RDAG will verify the action was completed
- **Success Criteria**: What constitutes successful completion
- **Common Mistakes**: Common errors to avoid

### Routing
- **From**: Specialist agent → CO
- **To**: CO → RDAG → User
- **Return Path**: User completes action → RDAG validates → CO continues
