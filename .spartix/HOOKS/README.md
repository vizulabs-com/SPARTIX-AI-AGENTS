# Hooks Ecosystem

## What Is a Hook?

A hook is an automated trigger that fires at specific points in the task execution lifecycle. Hooks enforce process governance, logging, validation, and compliance without requiring agents to manually invoke them. They are event-driven, not intention-driven.

## What Is a Custom Hook?

A custom hook is a user-defined hook placed in `custom-hooks/` that follows the same format as built-in hooks. Custom hooks are discovered and registered by CO during session initialization.

## How Hooks Differ from Agents

| Aspect | Agent | Hook |
|--------|-------|------|
| Has identity and purpose | Yes | No |
| Makes decisions | Yes | No |
| Receives task packets | Yes | No |
| Is triggered by events | No | Yes |
| Enforces process rules | No | Yes |

## How Hooks Differ from Skills

| Aspect | Hook | Skill |
|--------|------|-------|
| Triggered automatically | Yes | No |
| Invoked intentionally | No | Yes |
| Mandatory enforcement | Yes (if mandatory) | No |
| Used for governance | Yes | No |
| Used for capability | No | Yes |

## Hook Types

### Pre-Action Hooks
Triggered BEFORE a specialist agent begins work.
- Validate inputs
- Check permissions
- Log start events
- Enforce pre-conditions

### Mid-Process Hooks
Triggered DURING execution at defined checkpoints.
- Progress logging
- Intermediate validation
- Resource usage checks
- Compliance checkpoints

### Post-Action Hooks
Triggered AFTER a specialist agent completes work.
- Validate outputs
- Log completion events
- Trigger notifications
- Enforce post-conditions

### Global Hooks
Always active regardless of task type.
- Audit logging
- Security monitoring
- Performance tracking

## Mandatory vs Optional Hooks

**Mandatory hooks** are always enforced. CO includes them in every task packet. No agent may skip them.

**Optional hooks** are included based on task context and active rules. CO decides which optional hooks apply per task.

## Hook Documentation Format (.md)

Each hook has a Markdown file describing its trigger, behavior, and enforcement rules.

## Hook Metadata Format (.json)

Each hook may have a companion JSON metadata file:

```json
{
  "name": "hook-name",
  "version": "1.0.0",
  "type": "pre-action | mid-process | post-action | global",
  "mandatory": true,
  "triggerConditions": [...],
  "description": "What this hook does",
  "enforcement": "How this hook is enforced"
}
```

## How Hooks Interact with Task Flow

1. CO includes mandatory hooks in every task packet
2. CO includes relevant optional hooks based on context
3. Pre-action hooks fire before specialist begins
4. Mid-process hooks fire at checkpoints during execution
5. Post-action hooks fire after specialist completes
6. Global hooks fire regardless of task type
7. Hook results are included in the completion report

## How Hooks Interact with Rule Enforcement

- Hook rules in `RULES/hooks/` define which hooks are mandatory
- Rules can promote optional hooks to mandatory for specific contexts
- Rules can define hook trigger conditions

## How Hooks Interact with Reports and Wiki Updates

- Hook execution results are included in completion reports
- CO includes hook compliance status in wiki update packets
- WKC records hook compliance in task history
