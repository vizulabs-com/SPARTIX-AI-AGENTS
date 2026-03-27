# User Custom Rules

This directory contains user-defined custom rules that reflect personal preferences, team standards, and individual workflow constraints.

## Purpose
User custom rules allow individual users or teams to define governance preferences that are loaded BEFORE project rules during session initialization. This means user rules take priority over project rules when conflicts arise, while still respecting immutable system constraints.

## Loading Order
User rules are loaded at priority level 2 by SRL — after system rules (level 1) but before project rules (level 3). This ensures user preferences are honored over project defaults.

## Priority Behavior
- User rules CANNOT override system rules (system rules are immutable)
- User rules CAN override project rules when conflicts exist
- User rules are overridden by explicit override declarations (level 8)

## Format
Each rule file is a Markdown document with:
- **Rule ID**: Unique identifier (e.g., USR-001)
- **Rule Name**: Descriptive name
- **Priority Level**: 2 (user)
- **Scope**: user
- **Description**: What this rule constrains or enables
- **Conditions**: When this rule applies
- **Actions**: What behavior is enforced
- **Override Policy**: What this rule can and cannot override

## Example

```markdown
# User Rule: Prefer TypeScript Over JavaScript

**Rule ID**: USR-001
**Priority Level**: 2
**Scope**: user
**Description**: All frontend code generation must use TypeScript. JavaScript is not permitted for new code.
**Conditions**: When code-generation skill is invoked for frontend categories.
**Actions**: Enforce TypeScript as the target language. Reject JavaScript output.
**Override Policy**: Can override project rules that allow JavaScript. Cannot override system constraints.
```

Place your custom rules here as `.md` files. They will be discovered and loaded by SRL at session start.
