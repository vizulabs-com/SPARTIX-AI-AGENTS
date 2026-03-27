# Hook: Progress Checkpoint

## Name
progress-checkpoint

## Type
mid-process

## Mandatory
No — included by CO based on task complexity and duration.

## Description
Logs execution progress at defined checkpoints during long-running or complex tasks. Enables CO to track progress, detect stalls, and update the user-visible workflow feed with intermediate status.

## Trigger Conditions
- A specialist agent reaches a defined checkpoint during execution (e.g., 25%, 50%, 75% completion)
- A significant sub-deliverable is completed within a complex task
- A predefined time interval has elapsed during execution

## Behavior
1. Record the current progress percentage or milestone reached
2. Document what has been completed so far
3. Document what remains to be done
4. Flag any emerging risks or blockers discovered since the last checkpoint
5. Send the checkpoint data to CO for workflow feed update

## Enforcement
- This hook is optional — CO decides whether to include it based on task complexity
- When included, agents must honor checkpoint intervals as specified in the task packet
- Checkpoint data must be accurate and honest — never inflate progress
