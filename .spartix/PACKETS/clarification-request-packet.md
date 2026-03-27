# Clarification Request Packet Definition

## Purpose
A Clarification Request Packet is used when a specialist agent or CO determines that user input is needed to proceed. The packet flows from the specialist to CO, then CO routes it to RDAG, who presents it to the user.

## Required Sections

### Header
- **Packet ID**: Unique identifier (e.g., `CLR-2024-001`)
- **Requesting Agent**: Name and code of the agent that needs clarification
- **Related Task Packet ID**: Reference to the task being executed
- **Created At**: Timestamp
- **Urgency**: blocking | non-blocking

### Clarification Details
- **What Is Missing**: Clear description of the missing information
- **Why It Is Needed**: Why the agent cannot proceed without this information
- **Impact of Not Resolving**: What happens if the clarification is not provided
- **Suggested Options**: If applicable, options for the user to choose from
- **Context for User**: Background information to help the user understand the question

### Expected Response
- **Response Format**: What format the answer should take
- **Response Constraints**: Any constraints on valid answers
- **Default Value**: If applicable, a suggested default if the user has no preference

### Routing
- **From**: Specialist agent → CO
- **To**: CO → RDAG → User
- **Return Path**: User → RDAG → CO → (back to specialist or plan adjustment)
