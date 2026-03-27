# System Rule: Workspace Execution Awareness

**Rule ID**: SYS-006
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
Comprehensive rules for workspace awareness, file targeting, dependency awareness, change definition, command execution, testing, and workspace safety during agent execution.

---

## Rule 27: Workspace Execution Awareness
Every agent must know before starting: where it will work, relevant folders, files allowed to read, files allowed to modify, files not to touch, related dependencies, affected components, exact expected change, commands to execute, command locations, tests/validations to run, expected output, what to report back.

## Rule 28: Mandatory Workspace Definition in Every Task
Every task packet must include: working directory, relevant folders, relevant files, read scope, write scope, no-touch scope, affected dependencies, affected configurations, related tests, related commands, expected command execution location, expected validation path, expected resulting changes. Incomplete if any missing.

## Rule 29: File Awareness
Every agent must know: files for reading, files for editing, related but not to modify, files indirectly affected, files to validate after change. No assumed file targeting. No modifications outside approved write scope.

## Rule 30: Dependency Awareness
Understand dependency impact before changes: code, module, template, configuration, service, database, build, runtime, test dependencies. Understand what may break. No isolated file work if part of dependent chain.

## Rule 31: Change Definition
Before execution, understand: what change required, why required, where it happens, how to apply, what remains unchanged, intended result, side effects to avoid. No vague execution.

## Rule 32: Command Execution Location
Task packet must define: which commands required, why each needed, where each executed (project root, app folder, service folder, container, etc.), expected result, failure conditions. No guessing command location.

## Rule 33: Testing and Validation
Know: what to test, where test runs, affected files/components, command/validation method, success criteria, failure criteria, validation type (local, runtime, build, config, UI, backend, database, integration, responsive, interaction, console error). No completion without known validation path.

## Rule 34: Workspace Change Boundaries
Must not: modify unrelated folders, update unrelated files, rename/move/delete files without approval, touch dependencies outside scope, perform extra cleanup outside scope, add unexpected files. Every change must be minimal, justified, traceable.

## Rule 35: Execution Readiness
Not execution-ready unless agent knows: exact working area, exact files, exact dependencies, exact expected changes, exact allowed edits, exact restricted areas, exact commands, exact command locations, exact tests/validations, exact completion evidence. If unclear, execution blocked.

## Rule 36: Workspace Reporting
When returning to CO, report: where worked, files read, files modified, files intentionally not touched, dependencies involved, commands run, command locations, tests/validations run, what changed, what remains, risks/blockers, frontend issue class if relevant, files inspected, validation method, resolution status.

## Rule 37: Workspace Safety Enforcement
Before execution unlock, confirm task packet defines: workspace location, file targeting, dependency awareness, command plan, testing plan, validation path, safe change boundaries. If missing, reject or return for correction.

## Override Policy
These rules cannot be overridden by any other rule at any level.
