# Clarification Workflow

## When a Specialist Needs User Input

This workflow is triggered when a specialist agent encounters missing information, ambiguity, or a need for user-managed configuration during task execution.

### Flow

1. **Specialist detects issue**: Missing information, ambiguity, or user-managed configuration needed
2. **Specialist creates Clarification Request Packet**: Documents what is missing and why
3. **Specialist sends packet to CO**: Never directly to the user
4. **CO receives the request**: Evaluates whether user input is truly required
5. **CO determines routing**:
   - If CO can resolve internally (e.g., from wiki or rules): resolve and continue
   - If user input is required: route to RDAG
6. **CO sends to RDAG**: Includes context about what is needed and why
7. **RDAG formulates question**: Creates a clear, unambiguous question for the user
8. **RDAG asks the user**: Presents the question with context and options if applicable
9. **User responds**: Provides the requested information or makes a decision
10. **RDAG validates response**: Checks completeness and consistency
11. **RDAG returns to CO**: Passes validated response with confirmation
12. **CO updates plan**: Adjusts if the response changes the approach
13. **CO continues routing**: Re-assigns to the specialist or adjusts the workflow

### Workflow Status During Clarification
- Task status changes to: **"waiting for clarification"**
- Workflow feed shows: which agent requested clarification, what is being asked, and that the user must respond
- Once resolved: status returns to **"in progress"** or **"assigned"**

### Rules
- Specialist agents must never ask the user directly
- All clarification requests must go through CO
- CO must evaluate whether the request truly requires user input
- RDAG must validate all user responses before returning to CO
- The workflow feed must reflect the clarification state at all times
