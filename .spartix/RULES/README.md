# Rules Ecosystem

## What Are Rules?

Rules are governance directives that constrain and guide the behavior of agents, skills, hooks, and the orchestration process. Rules are above agents, skills, and hooks in the governance hierarchy because they define the boundaries within which everything else operates.

## Why Rules Are Above Agents, Skills, and Hooks

- Rules define what agents can and cannot do
- Rules define which skills are approved for which contexts
- Rules define which hooks are mandatory
- Rules define orchestration constraints
- Rules define priority and conflict resolution
- Without rules, agents, skills, and hooks have no governance framework

## Rule Loading Order for New Sessions

SRL loads rules in this exact order:

1. **System rules** (`RULES/system/`) — Immutable base constraints. Cannot be overridden by any other rule.
2. **User custom rules** (`RULES/user/`) — User-defined preferences. Loaded BEFORE project rules. Can override project rules but not system rules.
3. **Project rules** (`RULES/project/`) — Project-specific governance. Cannot override system or user rules.
4. **Agent rules** (`RULES/agents/`) — Agent-specific behavior constraints.
5. **Skill rules** (`RULES/skills/`) — Skill usage constraints.
6. **Hook rules** (`RULES/hooks/`) — Hook trigger and enforcement rules.
7. **Session rules** (`RULES/sessions/`) — Session-specific overrides.
8. **Override declarations** (`RULES/overrides/`) — Explicit overrides applied last. Cannot override system rules.

## How Rule Priority Is Resolved

Priority is resolved using `RULES/rule-priority-map.json`:

- System rules have the highest priority (immutable)
- User custom rules override project rules when they conflict
- Explicit overrides apply last but cannot override system rules
- Unresolvable conflicts are flagged for CO attention

## How Conflicts Are Handled

1. SRL detects conflicting rules during loading
2. SRL consults `rule-priority-map.json` for resolution
3. Higher-priority rules win
4. If priority is equal, the more specific rule wins
5. If still unresolvable, SRL flags the conflict for CO
6. CO may route to RDAG for user decision

## How Rules Affect the System

- **Agents**: Rules constrain agent behavior, define forbidden actions, and set quality standards
- **Skills**: Rules define which skills are approved for which contexts
- **Hooks**: Rules define which hooks are mandatory and their trigger conditions
- **Orchestration**: Rules constrain CO's routing decisions and sequencing
- **Wiki**: Rules define what must be recorded and how

## Rule File Format (.md)

Each rule is a Markdown file with:
- Rule ID
- Rule name
- Priority level
- Scope (system/user/project/agent/skill/hook/session)
- Description
- Conditions
- Actions
- Exceptions
- Override policy

## Rule Metadata (.json)

`rule-priority-map.json` provides machine-readable priority ordering:

```json
{
  "priorityOrder": [
    "system",
    "user",
    "project",
    "agents",
    "skills",
    "hooks",
    "sessions",
    "overrides"
  ],
  "conflictResolution": "higher-priority-wins",
  "tieBreaker": "more-specific-wins",
  "unresolvable": "flag-for-co"
}
```
