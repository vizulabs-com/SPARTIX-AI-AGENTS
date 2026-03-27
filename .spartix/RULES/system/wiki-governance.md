# System Rule: Wiki Governance

**Rule ID**: SYS-005
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
Comprehensive governance for wiki structure, categorization, reading priority, writing discipline, state clarity, and historical context management.

---

## Rule 15: Wiki Categorization
The wiki must be structured, categorized, and consistently organized. Not a flat collection of notes or random history dump. It is the primary reference and official project memory.

## Rule 16: Mandatory Wiki Structure
At minimum, categorized sections for: project overview, approved requirements, requirement history, clarification history, decisions, task backlog, active tasks, completed tasks, blockers and risks, reviews and validations, architecture and technical notes, configuration and environment notes, workflow transitions, milestones and progress, final completion state.

## Rule 17: Wiki Read Priority
Read the relevant category based on current need first:
- Scope issues → approved requirements
- What was done → completed tasks
- Blocked execution → blockers and risks
- Past decisions → decisions
- What happens next → active tasks, workflow transitions, progress state

## Rule 18: Wiki Writing
Updates must be written into the correct category. No generic mixed updates. No unrelated info in wrong sections. No merging tasks/requirements/decisions/blockers into one undifferentiated note.

## Rule 19: Wiki Navigation
Categories must be clearly named, unambiguous, historically traceable. Current official state must be distinguishable from older history. Must support both historical and current-state understanding.

## Rule 20: Wiki State Clarity
Clearly separate: current active state, approved state, historical state, completed state, blocked state, deferred state. Do not mix past and present without clear labeling.

## Rule 21: Wiki as Primary Reference
Always prefer categorized wiki understanding before making assumptions from scattered project files. Wiki provides official understanding of: why something exists, whether approved, whether completed, whether current, whether blocked, what should happen next.

## Rule 22: Historical Context Check
At session start, check whether old project history exists in: wiki, task records, workflow transitions, completion records, decisions, clarification logs, blockers, reviews. If exists, read first before continuing.

## Rule 23: Mandatory History Reading
If old history available, determine: what completed, what approved, what blocked, what deferred, what decided, what still active, what must not be duplicated. Do not treat new session as fresh empty start when valid history exists.

## Rule 24: Missing History Fallback
If no old history found: continue using current workspace state, current `.spartix` structure, active rules, approved workflow. Treat as no recoverable prior history. Begin building valid history from current point. Missing history must not block work unless another rule explicitly requires it.

## Rule 25: History Priority
Prefer: official wiki history, task history, decision history, workflow history — before assumptions from raw code or isolated files. If code and history appear inconsistent, handle through approved workflow.

## Rule 26: Session Start History Check
At session start: (1) check historical records exist, (2) check wiki exists, (3) read relevant historical context, (4) determine what already happened, (5) determine continuation or fresh start, (6) continue per approved workflow.

## Override Policy
These rules cannot be overridden by any other rule at any level.
