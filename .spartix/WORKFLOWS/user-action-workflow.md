# User Action Required Workflow

## When the User Must Perform an External Action

This workflow is triggered when the system needs the user to update files, provide configuration, set up external services, or perform any action that cannot be automated.

### Flow

1. **Agent detects need**: A user-managed configuration, file, or external action is required
2. **Agent creates User Action Required Packet**: Documents what needs to be done and why
3. **Agent sends packet to CO**: Never directly to the user
4. **CO receives the request**: Validates the need for user action
5. **CO routes to RDAG**: Includes full context and instructions
6. **RDAG presents to user**: Shows what needs to be done with:
   - Clear description of the required action
   - Step-by-step instructions
   - Expected format or values
   - Why it is needed
7. **User performs the action**: Updates files, provides configuration, etc.
8. **RDAG validates completion**: Checks that the action was performed correctly
9. **RDAG returns confirmation to CO**: With validation results
10. **CO continues routing**: Resumes the workflow

### Workflow Status During User Action
- Task status changes to: **"waiting for user action"**
- Workflow feed shows: what action is needed, instructions, and that the user must act
- Once completed: status returns to **"in progress"** or **"assigned"**

### Rules
- Agents must never instruct the user directly
- All user action requests must go through CO → RDAG
- RDAG must provide clear, actionable instructions
- RDAG must validate that the action was completed correctly
- The workflow feed must reflect the user action state at all times
