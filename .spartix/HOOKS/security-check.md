# Hook: Security Check

## Name
security-check

## Type
pre-action

## Mandatory
Yes — fires before execution of any task that involves code, configuration, or infrastructure changes.

## Description
Checks that the task packet and execution context comply with security policies before the specialist begins work. Validates that security-sensitive operations have appropriate authorization, that secrets are not exposed, and that security standards are referenced.

## Trigger Conditions
- A specialist agent is about to execute a task that involves code generation, configuration changes, infrastructure modifications, or data access

## Behavior
1. Verify the task packet references applicable security standards from the active rule context
2. Verify no secrets, credentials, or sensitive data are embedded in the task packet inputs
3. Verify the assigned agent has the appropriate security clearance for the task domain
4. Verify security-related mandatory hooks (audit-log) are included in the packet
5. If check passes: agent may proceed
6. If check fails: agent must report the security concern to CO and halt execution

## Enforcement
- This hook cannot be skipped for any task involving code, config, or infrastructure
- Security failures must be reported to CO immediately
- CO must resolve security concerns before re-assigning the task
