# Incidents

> This section documents production incidents, post-mortems, and operational runbooks for SPARTIX.

---

## Purpose

- Provide a structured process for responding to and learning from incidents.
- Maintain runbooks so that common issues can be resolved quickly.
- Build institutional memory to prevent recurring problems.

---

## Post-Mortem Format

All incidents that reach production or significantly impact development must have a post-mortem. Use the following structure.

### Post-Mortem Template

Save post-mortems as: `INC-XXXX-short-description.md`

```markdown
# INC-XXXX: [Incident Title]

> **Severity:** [SEV-1 / SEV-2 / SEV-3 / SEV-4]
> **Date:** YYYY-MM-DD
> **Duration:** [How long the incident lasted]
> **Impact:** [Who and what was affected]
> **Responders:** [Who was involved in resolution]
> **Status:** [Resolved / Monitoring / Open]

## Summary
[2-3 sentence summary of what happened]

## Timeline
| Time (UTC) | Event |
|------------|-------|
| HH:MM | [Event description] |
| HH:MM | [Event description] |
| HH:MM | [Event description] |

## Root Cause
[What caused the incident at its root]

## Contributing Factors
- [Factor 1]
- [Factor 2]

## Resolution
[What was done to resolve the incident]

## Impact Assessment
- **Users affected:** [Number or scope]
- **Data impact:** [Any data loss or corruption]
- **Revenue impact:** [If applicable]
- **Reputation impact:** [If applicable]

## Lessons Learned
- [Lesson 1]
- [Lesson 2]

## Action Items
| Action | Owner | Due Date | Status |
|--------|-------|----------|--------|
| [Action description] | [Person] | YYYY-MM-DD | [Open / Done] |

## Prevention
[What changes will prevent this from happening again]
```

---

## Severity Levels

| Severity | Definition | Response Time | Notification |
|----------|-----------|---------------|--------------|
| **SEV-1** | Complete system outage or data loss | Immediate | All stakeholders |
| **SEV-2** | Major feature broken, significant user impact | Within 1 hour | Team lead + affected stakeholders |
| **SEV-3** | Minor feature broken, workaround available | Within 4 hours | Team lead |
| **SEV-4** | Cosmetic issue or minor degradation | Next business day | Team channel |

---

## Runbook Structure

Runbooks document step-by-step procedures for handling known operational scenarios. Save runbooks as: `RB-XXXX-short-description.md`

### Runbook Template

```markdown
# RB-XXXX: [Runbook Title]

> **Last tested:** YYYY-MM-DD
> **Owner:** [Person responsible for keeping this current]

## When to Use
[Describe the scenario that triggers this runbook]

## Symptoms
- [Observable symptom 1]
- [Observable symptom 2]

## Prerequisites
- [Access or tools needed]

## Steps

### 1. [Step Title]
[Detailed instructions]

### 2. [Step Title]
[Detailed instructions]

### 3. [Step Title]
[Detailed instructions]

## Verification
[How to confirm the issue is resolved]

## Escalation
[When and how to escalate if these steps don't resolve the issue]
```

---

## Incident Index

| ID | Date | Title | Severity | Status | Post-Mortem |
|----|------|-------|----------|--------|-------------|
| *INC-001* | *YYYY-MM-DD* | *[Incident title]* | *[SEV-X]* | *[Resolved / Open]* | *[Link]* |

---

## Runbook Index

| ID | Title | Last Tested | Owner |
|----|-------|-------------|-------|
| *RB-001* | *[Runbook title]* | *YYYY-MM-DD* | *[Person]* |

---

*Last updated: YYYY-MM-DD*
*Maintained by Nabil Mansour [Wiki Builder]*
