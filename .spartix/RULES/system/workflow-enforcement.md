# System Rule: Workflow Enforcement

**Rule ID**: SYS-003
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
Comprehensive enforcement of the `.spartix` governed workflow. Covers transparency, communication ownership, orchestration ownership, task preparation, wiki-before-execution, and execution control.

---

## Rule 1: Core Transparency
The user must see the workflow progression step by step. For every important workflow transition, show: which agent received the work, why selected, what it will do, inputs, expected output, when finished, what returned, what sent to CO, what sent to WKC, and who is next. Do not hide the operational chain.

## Rule 2: Communication Ownership
The user sees all workflow steps, but direct clarification, approval, and user-action requests go only through RDAG. No other agent may directly ask the user for clarification, approval, configuration, credentials, or file updates.

## Rule 3: Orchestration Ownership
Only CO may: receive reports from specialists, decide the next valid step, select the next responsible agent, receive/approve task packets, send approved packets to WKC, unlock execution after wiki confirmation, maintain visible workflow progress. No specialist may assign the next agent or hand off directly to another specialist.

## Rule 4: Task Preparation Before Execution
No execution from vague instructions. Required order:
1. CO decides the next valid step
2. TBEP prepares the full detailed task packet
3. Task packet is reviewed for quality, completeness, clarity, and step-by-step readiness
4. CO reviews and accepts only after confirming completeness
5. CO sends approved packet to WKC
6. WKC updates wiki with task state, planned execution state, workflow transition
7. Only after wiki update is confirmed may the specialist begin execution

## Rule 5: Task Review
Before approval, the task packet must be confirmed as: complete, unambiguous, scoped correctly, aligned with current step, aligned with active rules, aligned with approved requirements, written step-by-step, explicit about inputs/outputs/constraints/validation, clear on workspace location, file scope, dependency impact, command plan, command location, testing and validation path. If vague or incomplete, return for correction.

## Rule 6: Step-by-Step Task Packet
Every task packet must contain detailed execution steps describing: what to do first, what comes next, files/folders involved, expected changes, what must not change, validations required, testing required, what completion looks like. No high-level summaries only.

## Rule 7: Wiki-Before-Execution
Implementation may begin only after: task packet fully prepared, reviewed, accepted by CO, approved packet sent to WKC, wiki updated with official task state and planned execution state, CO confirms execution is unlocked. If wiki update not completed, execution remains blocked.

## Rule 8: Specialist Execution
Once unlocked, the specialist must: execute only within specialization, follow the step-by-step packet, stay inside scope, avoid modifying unrelated files, avoid talking to user, avoid handing off to another specialist, return completion/blockers/missing info only to CO.

## Rule 9: Clarification and User Action Routing
Route: Specialist → CO → RDAG → User → RDAG → CO → Workflow continues. This route is mandatory.

## Rule 10: Wiki Ownership
Only WKC may update the wiki. When CO sends an approved packet to WKC, the user must see it. Wiki update must record: approved task packet, workflow transition, planned execution state, official project state update. No specialist may write directly to the wiki.

## Rule 13: Strict Block Rule
Execution must be blocked if missing: task packet, task packet review, step-by-step detail, orchestrator acceptance, wiki update, clear scope, clear validation requirements, clear completion criteria.

## Rule 14: Final Enforcement
Every major transition must be visible. Every task prepared before execution. Every task reviewed before approval. Every approved task recorded in wiki before execution starts. Execution blocked until wiki update complete. Only RDAG talks to user. Only CO orchestrates. Only TBEP prepares packets. Only WKC writes to wiki. Mandatory and cannot be bypassed.

## Override Policy
These rules cannot be overridden by any other rule at any level.
