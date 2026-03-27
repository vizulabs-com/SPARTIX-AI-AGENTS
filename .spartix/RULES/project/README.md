# Project Rules

This directory contains project-specific governance rules that define standards, constraints, and policies for the current project.

## Purpose
Project rules establish the governance framework for a specific project including coding standards, architecture constraints, naming conventions, review requirements, and compliance policies. They apply to all agents working on this project.

## Loading Order
Project rules are loaded at priority level 3 by SRL — after system rules (level 1) and user rules (level 2). This means project rules are overridden by user preferences when conflicts exist.

## Priority Behavior
- Project rules CANNOT override system rules (system rules are immutable)
- Project rules CANNOT override user custom rules (user rules have higher priority)
- Project rules CAN be overridden by explicit override declarations (level 8)
- Project rules take precedence over agent, skill, hook, and session rules (levels 4-7)

## Format
Each rule file is a Markdown document with:
- **Rule ID**: Unique identifier (e.g., PRJ-001)
- **Rule Name**: Descriptive name
- **Priority Level**: 3 (project)
- **Scope**: project
- **Description**: What this rule constrains or enables
- **Conditions**: When this rule applies
- **Actions**: What behavior is enforced
- **Override Policy**: What this rule can and cannot override

## Example

```markdown
# Project Rule: All APIs Must Follow RESTful Conventions

**Rule ID**: PRJ-001
**Priority Level**: 3
**Scope**: project
**Description**: All API endpoints must follow RESTful conventions including proper HTTP methods, resource naming, and status codes.
**Conditions**: When API Design Agent or Backend Agent creates or modifies API endpoints.
**Actions**: Enforce RESTful naming, proper HTTP method usage, and standard status codes. Reject non-RESTful patterns.
**Override Policy**: Can be overridden by user rules. Cannot override system constraints.
```

Place your project-specific rules here as `.md` files. They will be discovered and loaded by SRL at session start.
