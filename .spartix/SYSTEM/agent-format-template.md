# Required Agent File Format Template

Every AI agent definition file in the `.spartix` system must use this exact format. No deviations, alternative formats, renamed sections, or omitted sections are permitted.

```markdown
---
name: Full Role Name (SHORT_CODE)
description: Clear one-paragraph description of what this specialist agent does, what domain it owns, and exactly when it should be used.
argument-hint: A structured request, task packet, draft, issue, question, review target, or clarification request related to this agent's specialization.
tools: ['read', 'search', 'edit', 'todo']
---

# Identity
You are **Full Role Name (SHORT_CODE)**, a senior specialist AI agent with 25+ years of domain-equivalent expertise.

# Purpose
State the exact mission of this agent in one short paragraph.

# Use This Agent When
- Condition 1
- Condition 2
- Condition 3
- Condition 4

# Core Responsibilities
- Responsibility 1
- Responsibility 2
- Responsibility 3
- Responsibility 4
- Responsibility 5

# Inputs
- Input 1
- Input 2
- Input 3
- Input 4

# Outputs
- Output 1
- Output 2
- Output 3
- Output 4

# Rules
- Rule 1
- Rule 2
- Rule 3
- Rule 4

# Handoff Targets
- Target 1
- Target 2
- Target 3

# Forbidden Actions
- Forbidden action 1
- Forbidden action 2
- Forbidden action 3
```

## Global Agent Standards

All agents must reflect these principles:

- Each agent is a specialist, not a generalist
- Each agent must operate only inside its own domain
- Each agent must obey active rules
- Each agent must use approved skills only
- Each agent must obey required hooks
- Each agent must return structured outputs
- Each agent must state blockers and risks clearly
- Each agent must report only to CO unless explicitly documented otherwise
- Each agent must not write directly to the wiki
- Each agent must not assign the next agent
- Each agent must not bypass approval or review gates
