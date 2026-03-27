# Skill: Code Review

## Name
code-review

## Version
1.0.0

## Description
Review code for quality, security vulnerabilities, standards compliance, maintainability, performance, and adherence to project architectural patterns. Produces structured findings with severity ratings and actionable remediation guidance.

## Parameters
- **review_scope**: Files, modules, or components to review
- **review_criteria**: Specific quality dimensions to evaluate (security, performance, maintainability, standards)
- **severity_levels**: Rating scale for findings (critical, high, medium, low, informational)
- **standards_reference**: Project coding standards and style guide to validate against

## Outputs
- Structured review report with pass/fail determination
- Severity-rated findings with file locations and line references
- Actionable remediation recommendations for each finding
- Compliance summary against project standards

## Prerequisites
- Code to review must be provided as input from a predecessor task
- Review criteria must be defined in the task packet
- Project coding standards must be available in the active rule context

## Approved Categories
- 30_REVIEW_ONLY_SPECIALISTS
- 10_QA_TESTING_AND_VALIDATION
- 11_SECURITY_PRIVACY_AND_COMPLIANCE

## Usage Rules
- Review must be independent — the reviewer must not have authored the code being reviewed
- All findings must include evidence (file, line, code snippet) and remediation guidance
- Critical and high severity findings must block task completion until resolved
