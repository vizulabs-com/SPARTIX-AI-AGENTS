# Hook: Post-Execution Validation

## Name
post-execution-validation

## Type
post-action

## Mandatory
Yes — fires after every specialist agent completes work.

## Description
Validates that the completion report is well-formed, contains all required sections, and that all deliverables specified in the task packet have been produced. Prevents incomplete or malformed reports from reaching CO.

## Trigger Conditions
- A specialist agent has completed execution and is about to return the completion report to CO

## Behavior
1. Verify the completion report contains all required sections (header, execution summary, deliverables, testing, issues, verification)
2. Verify all deliverables listed in the task packet's expected outputs are accounted for in the report
3. Verify completion criteria from the task packet are addressed with pass/fail status
4. Verify skills used and hooks obeyed are documented
5. If validation passes: report may be sent to CO
6. If validation fails: agent must fix the report before sending, or report the inability to CO

## Enforcement
- This hook fires automatically after every specialist completes work
- Agents must not send incomplete reports to CO
- Missing deliverables must be explicitly documented with explanation
