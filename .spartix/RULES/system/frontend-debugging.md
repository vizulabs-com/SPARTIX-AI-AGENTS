# System Rule: Frontend Self-Debugging and Quality

**Rule ID**: SYS-007
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
Rules for proactive frontend issue detection, classification, self-validation, workspace debug awareness, auto-fix boundaries, validation requirements, escalation, and quality gates.

---

## Rule 38: Frontend Self-Debugging
AI agents must not wait for the user to identify frontend problems. They must proactively inspect, locate, diagnose, and attempt to resolve issues inside the approved workflow. The user is not expected to know where the issue is, which file caused it, or what type of problem it is.

## Rule 39: Frontend Issue Investigation
Investigate at minimum: affected page/component, related templates/UI files, related styles, related scripts, related assets, related event handlers, related state logic, related API/backend responses, related routes, related browser/runtime errors, related console errors, related configuration. Goal: locate actual source, not guess.

## Rule 40: Frontend Error Classification
Classify before fixing. Issue may be: rendering, layout, styling, responsiveness, interaction, event binding, state management, data binding, undefined variable/function, API integration, routing, asset loading, configuration, dependency, browser/runtime error, validation. Fix must be based on real class, not random edits.

## Rule 41: Frontend Self-Validation Loop
1. Inspect the visible issue
2. Identify likely affected files and dependencies
3. Inspect runtime or logical cause
4. Classify the issue
5. Apply minimal justified fix
6. Validate the fix
7. Re-check the affected flow
8. Confirm resolved or partially resolved
9. Report clearly to CO

Do not stop at first guess. Do not apply blind fixes without re-validation.

## Rule 42: Frontend Workspace Debug Awareness
For every frontend issue, know: where the page/component lives, files controlling structure, files controlling styling, files controlling behavior, files providing data, routes leading to it, dependencies that may break it, commands/checks for validation, tests/manual validations needed after fix.

## Rule 43: Frontend Auto-Fix Boundaries
May attempt auto-fix only when: issue inside approved scope, affected area identifiable, fix doesn't violate rules, fix doesn't introduce unsafe architectural changes, fix can be validated. Prefer: minimal change, localized diagnosis, validated correction, safe rollback reasoning. No broad speculative rewrites.

## Rule 44: Frontend Validation Requirement
Not fixed until validated: affected UI renders correctly, interaction works, layout not broken, state/data flow correct, no new errors introduced, impacted flow works. Validation may include: render, route, interaction, state, console/runtime error, asset load, API response binding, responsive checks.

## Rule 45: Frontend Escalation
If cannot confidently isolate or fix, return to CO with: suspected issue class, affected area, files inspected, attempted fixes, validation results, remaining uncertainty, blocker status, recommended next step. If user clarification needed, route through RDAG.

## Rule 46: Frontend Quality Gate
Before marking frontend task complete, confirm: issue location investigated, issue classified, affected files identified, fix applied inside scope, fix validated, no obvious regression, result reported clearly. If any missing, task not complete.

## Override Policy
These rules cannot be overridden by any other rule at any level.
