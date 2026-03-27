# Agent Rules

This directory contains agent-specific behavior rules that constrain how individual agents or agent categories operate.

## Purpose
Agent rules define additional constraints beyond the system rules that apply to specific agents or categories. For example, a rule might restrict which skills a particular agent category can use, or enforce additional reporting requirements for security-related agents.

## Loading Order
Agent rules are loaded at priority level 4 (after system, user, and project rules) by SRL during session initialization.

## Format
Each rule file is a Markdown document with:
- Rule ID
- Target agent(s) or category
- Constraint description
- Enforcement behavior

## Example

```markdown
# Agent Rule: Security Agents Must Log All Actions

**Rule ID**: AGT-001
**Target**: 11_SECURITY_PRIVACY_AND_COMPLIANCE, 23_ADVANCED_SECURITY_SPECIALISTS
**Constraint**: All agents in security categories must include detailed action logs in their completion reports.
**Enforcement**: Post-execution validation hook checks for action log section in completion report.
```

Place your agent-specific rules here as `.md` files.
