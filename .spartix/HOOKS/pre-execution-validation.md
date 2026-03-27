# Hook: Pre-Execution Validation

## Name
pre-execution-validation

## Type
pre-action

## Mandatory
Yes — fires before every specialist agent begins work.

## Description
Validates that the task packet is complete, well-formed, and contains all required sections before the specialist agent begins execution. Prevents agents from starting work on incomplete or malformed task packets.

## Trigger Conditions
- A specialist agent receives a task packet and is about to begin execution

## Behavior
1. Verify the task packet contains all required sections (assignment, scope, inputs, outputs, criteria, hooks, skills)
2. Verify the assigned agent matches the receiving agent
3. Verify all required inputs are present and accessible
4. Verify mandatory hooks are listed in the packet
5. Verify approved skills are listed in the packet
6. If validation passes: agent may proceed with execution
7. If validation fails: agent must report the validation failure to CO and halt execution

## Enforcement
- This hook fires automatically before any specialist begins work
- Agents must not bypass this validation under any circumstances
- Validation failures must be reported to CO immediately with specific details about what is missing
