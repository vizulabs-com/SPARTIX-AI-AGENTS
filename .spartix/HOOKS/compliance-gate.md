# Hook: Compliance Gate

## Name
compliance-gate

## Type
post-action

## Mandatory
No — included by CO when the task involves regulated domains or compliance-sensitive work.

## Description
Validates that task outputs comply with applicable regulatory, organizational, and project compliance requirements before the completion report is accepted. Covers GDPR, PCI-DSS, SOC2, HIPAA, accessibility standards, and project-specific compliance rules.

## Trigger Conditions
- A specialist agent has completed a task in a compliance-sensitive domain
- The task packet specifies compliance validation as a post-action requirement
- The deliverables involve personal data, payment data, security controls, or regulated content

## Behavior
1. Identify applicable compliance frameworks from the task packet and active rule context
2. Validate deliverables against each applicable compliance requirement
3. Document compliance status for each requirement (compliant, non-compliant, not-applicable)
4. Flag any non-compliance findings with severity, evidence, and remediation guidance
5. If compliant: completion report may proceed to CO
6. If non-compliant: findings must be included in the completion report for CO review

## Enforcement
- This hook is optional — CO decides whether to include it based on task domain
- When included, non-compliance findings must be documented even if the task is otherwise complete
- Critical compliance violations must block task completion until resolved
