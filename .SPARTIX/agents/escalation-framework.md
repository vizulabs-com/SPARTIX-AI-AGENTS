# Escalation Framework

## Agent System Escalation Policy and Procedures

---

## Escalation Philosophy

Escalation is not failure. Escalation is the system working correctly.

A well-designed agent system recognizes the boundaries of each component's competence and acts decisively when those boundaries are reached. The cost of a false escalation (unnecessary human involvement) is always lower than the cost of a missed escalation (incorrect output delivered with false confidence, silent failure, or compounding errors).

### Core Principles

1. **Escalate early, not late.** The moment uncertainty crosses a threshold, escalate. Do not attempt to "power through" ambiguity.
2. **Escalate with context.** Every escalation carries the full chain of reasoning, partial outputs, and the specific trigger that caused it. The recipient of an escalation should never need to ask "why am I seeing this?"
3. **Escalation is bidirectional.** Any layer can escalate upward (toward the human) or backward (toward clarification/requirements). The direction depends on the nature of the issue.
4. **Escalation has a chain.** Steps are not skipped except under critical risk conditions. The chain exists to maximize automated resolution before involving the human.
5. **Escalation is logged.** Every escalation event is recorded in the task envelope's audit trail with timestamp, trigger, severity, and resolution.
6. **De-escalation is active.** When conditions improve, the system actively reduces the escalation level rather than leaving tasks in an elevated state.

---

## Complexity Tiers

Every task in the system is classified into one of four complexity tiers. The tier determines timeout policies, checkpoint frequency, escalation thresholds, review requirements, and quality gates.

### T1 -- Routine

**Definition:** A well-defined task in a single domain with no ambiguity, low risk, and a single agent sufficient to complete it.

**Criteria:**
- Single domain involvement
- Clear, unambiguous requirements
- No cross-cutting concerns
- Low risk (no security, data-loss, or compliance implications)
- Estimated effort: small (minutes to low hours)
- No dependency on other active tasks

**Examples:**
- Fix a typo in documentation
- Add a configuration field with a known schema
- Write a single unit test for an existing function
- Update a color token in a theme file
- Rename a variable across a single module

**Timeout:** 15 minutes
**Checkpoint frequency:** Completion only
**Confidence threshold for escalation:** < 0.7
**Review requirement:** None (ORCH validates directly)

---

### T2 -- Standard

**Definition:** A task with moderate complexity, clear requirements, possibly spanning two domains, that may benefit from a review step.

**Criteria:**
- One or two domains involved
- Requirements are clear but may have minor interpretation choices
- Moderate risk (localized impact if incorrect)
- Estimated effort: hours
- May have lightweight dependencies on other components

**Examples:**
- Implement a new REST API endpoint with validation
- Design a UI component based on a wireframe
- Write a technical document with code examples
- Add a new CI/CD pipeline stage
- Create a data transformation script with tests

**Timeout:** 60 minutes
**Checkpoint frequency:** Start, midpoint, completion
**Confidence threshold for escalation:** < 0.7
**Review requirement:** Optional (ORCH may request peer review for borderline cases)

---

### T3 -- Complex

**Definition:** A multi-domain task with significant scope, cross-cutting concerns, and a requirement for coordination between multiple agents.

**Criteria:**
- Three or more domains involved
- Cross-cutting concerns (e.g., code changes that affect UI, API, database, and tests)
- Moderate-to-high risk
- Estimated effort: hours to days
- Dependencies between sub-tasks
- Requires aggregation of multiple agent outputs

**Examples:**
- Build a feature end-to-end (backend, frontend, tests, documentation)
- Migrate a service from one framework to another
- Implement a data pipeline with ingestion, transformation, and visualization
- Design and implement a new authentication flow
- Refactor a core module with ripple effects across the codebase

**Timeout:** 4 hours
**Checkpoint frequency:** Start, 25%, 50%, 75%, completion
**Confidence threshold for escalation:** < 0.8
**Review requirement:** Mandatory senior review before delivery

---

### T4 -- Critical

**Definition:** An enterprise-scale task with high risk, regulatory implications, novel architecture decisions, or multi-team impact.

**Criteria:**
- System-wide or organization-wide impact
- High risk (security, data integrity, compliance, financial)
- Novel or unprecedented requirements (no existing pattern to follow)
- Regulatory or legal implications
- Estimated effort: days to weeks
- Requires human checkpoints during execution
- Rollback planning is mandatory

**Examples:**
- Full system architecture redesign
- Security incident response and remediation
- Compliance audit preparation and execution
- Major version migration affecting all users
- Implementation of a new encryption or data-handling standard
- Merging two codebases or systems

**Timeout:** 24 hours (with mandatory human checkpoints every 4 hours)
**Checkpoint frequency:** Start, every 10% increment, completion
**Confidence threshold for escalation:** < 0.8
**Review requirement:** Mandatory senior review AND human approval before delivery

---

## Escalation Triggers

Each trigger has a defined condition, severity, and default action.

### Trigger 1: Confidence Drop

| Field      | Value                                                           |
| ---------- | --------------------------------------------------------------- |
| Condition  | Agent's self-reported confidence falls below the tier threshold |
| Thresholds | T1/T2: < 0.7, T3/T4: < 0.8                                      |
| Severity   | Medium                                                          |
| Action     | Step 1 (Specialist Re-attempt with adjusted parameters)         |

### Trigger 2: Scope Exceeded

| Field     | Value                                                                |
| --------- | -------------------------------------------------------------------- |
| Condition | Agent reports that work exceeds the scoped envelope by more than 20% |
| Severity  | Medium                                                               |
| Action    | Pause task, re-scope with Requirements Layer, then re-route          |

### Trigger 3: Conflict Between Agents

| Field     | Value                                                                  |
| --------- | ---------------------------------------------------------------------- |
| Condition | Two or more agents produce contradictory outputs for related sub-tasks |
| Severity  | High                                                                   |
| Action    | Trigger conflict resolution protocol (see below)                       |

### Trigger 4: Blocker (No Workaround)

| Field     | Value                                               |
| --------- | --------------------------------------------------- |
| Condition | Agent cannot proceed and no alternative path exists |
| Severity  | High                                                |
| Action    | Escalation chain starting at Step 1                 |

### Trigger 5: Risk Detected

| Field     | Value                                                                                |
| --------- | ------------------------------------------------------------------------------------ |
| Condition | Agent identifies a security vulnerability, data-loss vector, or compliance violation |
| Severity  | Critical                                                                             |
| Action    | Immediate jump to Step 4 (Human Decision Point), pause all related tasks             |

### Trigger 6: Time Exceeded

| Field     | Value                                                         |
| --------- | ------------------------------------------------------------- |
| Condition | Task exceeds its tier timeout without completion              |
| Severity  | Medium (T1/T2), High (T3/T4)                                  |
| Action    | Step 2 (Re-route) for T1/T2, Step 3 (Senior Review) for T3/T4 |

### Trigger 7: Repeated Failure

| Field     | Value                                             |
| --------- | ------------------------------------------------- |
| Condition | Agent fails the same sub-task twice consecutively |
| Severity  | High                                              |
| Action    | Step 2 (Re-route to alternate agent)              |

### Trigger 8: Ambiguity Discovered During Execution

| Field     | Value                                                                  |
| --------- | ---------------------------------------------------------------------- |
| Condition | Agent encounters undefined or contradictory requirements mid-execution |
| Severity  | Medium                                                                 |
| Action    | Back-escalation to Clarifier or Requirements Layer                     |

### Trigger 9: Resource Exhaustion

| Field     | Value                                                                |
| --------- | -------------------------------------------------------------------- |
| Condition | Agent reports that the task requires resources beyond its allocation |
| Severity  | Medium                                                               |
| Action    | ORCH re-evaluates tier assignment and re-routes if necessary         |

---

## Escalation Chain

The escalation chain is a four-step sequence. Each step attempts resolution before advancing to the next. Steps are not skipped except under the Critical Risk Override rule.

### Step 1: Specialist Re-attempt

**Who acts:** The originally assigned specialist agent.
**What happens:**
- ORCH provides the agent with additional context, adjusted parameters, or clarified constraints.
- The agent re-attempts the task or the specific sub-task that triggered the escalation.
- Maximum one re-attempt per trigger event.

**Outcome:**
- If successful: task resumes normal flow. Escalation is logged but resolved.
- If unsuccessful: advance to Step 2.

**Time budget:** 50% of the original tier timeout.

---

### Step 2: Re-route

**Who acts:** ORCH selects an alternate agent in the same domain.
**What happens:**
- ORCH creates a new task envelope version with:
	- The original task context
	- The first agent's partial output (if any)
	- The escalation trigger details
	- A note that this is a re-routed task
- The alternate agent receives the full context and begins work.

**Outcome:**
- If successful: task resumes normal flow. Both agents' work is preserved in the audit trail.
- If unsuccessful: advance to Step 3.

**Time budget:** 75% of the original tier timeout.

---

### Step 3: Senior Review

**Who acts:** A designated senior reviewer agent (or a senior specialist in the relevant domain).
**What happens:**
- ORCH dispatches a review envelope containing:
	- The original task and requirements
	- All partial outputs from Steps 1 and 2
	- Escalation history
	- Specific questions for the reviewer
- The senior reviewer evaluates the situation and provides one of:
	- A corrected output (resolving the issue)
	- A revised approach recommendation (ORCH re-routes with new instructions)
	- A recommendation to escalate to the human

**Outcome:**
- If resolved: task resumes with the reviewer's output or revised approach.
- If not resolved: advance to Step 4.

**Time budget:** 100% of the original tier timeout.

---

### Step 4: Human Decision Point

**Who acts:** The human user.
**What happens:**
- ORCH presents the user with a structured escalation report:
	- **Summary:** One-paragraph description of the task and the issue.
	- **Work completed:** What has been accomplished so far.
	- **Blocker/Conflict:** Specific description of what cannot be resolved automatically.
	- **Options:** Enumerated choices the user can make (e.g., "Accept partial output", "Provide additional guidance", "Abort task", "Override with manual input").
	- **Recommendation:** ORCH's suggested path forward based on all available information.

**Outcome:**
- The user's decision is final. ORCH executes accordingly.
- If the user provides new information, ORCH may restart from the appropriate layer (Clarification, Requirements, or Execution).

---

## Back-Escalation Rules

Back-escalation is the mechanism by which any layer in the system can push an issue upstream (toward clarification or requirements) rather than downstream (toward the human).

### When to Back-Escalate

| Condition                                         | Back-Escalate To   |
| ------------------------------------------------- | ------------------ |
| User intent is ambiguous or multi-interpretable   | Clarifier Agent    |
| Acceptance criteria are incomplete                | Requirements Agent |
| Acceptance criteria are contradictory             | Requirements Agent |
| Requirements are technically infeasible as stated | Requirements Agent |
| Scope is undefined for a discovered sub-task      | Requirements Agent |
| User's terminology is unclear or domain-specific  | Clarifier Agent    |

### Back-Escalation Protocol

1. The detecting agent (or ORCH) sets the task state to `blocked`.
2. A back-escalation envelope is created with:

	- `message_type: escalate`
	- `escalation_reason: ambiguity | incomplete_requirements | contradictory_requirements | infeasible_requirements`
	- The specific issue description
	- Suggested questions or modifications
3. The target layer (Clarifier or Requirements) processes the envelope.
4. If user interaction is needed, the target layer engages the user.
5. The resolved context is returned to ORCH.
6. ORCH updates the task envelope and resumes execution.

### Limits

- A task may back-escalate a maximum of **two times** before ORCH escalates to Human Decision Point (Step 4).
- Each back-escalation resets the tier timeout for the affected sub-task (but not for the overall task).

---

## Human Checkpoint Rules

Certain conditions require MANDATORY human involvement, regardless of the escalation chain's current step.

### Always Involve the Human When:

1. **The task is T4 (Critical).** Human checkpoints every 4 hours are mandatory.
2. **Risk is detected.** Any security, data-loss, or compliance risk triggers immediate human notification.
3. **Scope change exceeds 30%.** If the re-scoped task is more than 30% larger or fundamentally different from the original, the human must approve the new scope.
4. **Irreversible action.** Any action that cannot be undone (deletion of data, deployment to production, sending external communications) requires human approval.
5. **Financial or legal impact.** Any task with direct financial or legal consequences requires human sign-off.
6. **Agent disagreement after conflict resolution.** If the conflict resolution protocol fails to reach consensus, the human decides.
7. **Third back-escalation.** If a task has been back-escalated twice and a third ambiguity arises, the human is involved.

---

## Escalation Message Format

Every escalation message follows a standardized format to ensure clarity and actionability.

```yaml
escalation:
	id: "esc-<uuid>"
	timestamp: "<ISO-8601>"
	task_id: "<parent task envelope ID>"
	trigger: "<trigger name>"
	severity: "<critical | high | medium | low>"
	tier: "<T1 | T2 | T3 | T4>"
	chain_step: <1 | 2 | 3 | 4>
	source_agent: "<agent ID that triggered the escalation>"
	target: "<agent ID | human>"

	summary: |
		<One-paragraph description of the issue.>

	context:
		original_task: "<brief task description>"
		work_completed: |
			<Summary of work done before the escalation.>
		partial_output_ref: "<artifact reference, if any>"
		blocker_description: |
			<Specific description of the blocker, conflict, or ambiguity.>

	options:
		- id: "opt-1"
		  description: "<Option description>"
		- id: "opt-2"
		  description: "<Option description>"
		- id: "opt-3"
		  description: "<Option description>"

	recommendation:
		option_id: "opt-<N>"
		reasoning: |
			<Why ORCH recommends this option.>

	audit:
		escalation_history:
			- step: 1
			  timestamp: "<ISO-8601>"
			  agent: "<agent ID>"
			  outcome: "<resolved | failed | skipped>"
			- step: 2
			  timestamp: "<ISO-8601>"
			  agent: "<agent ID>"
			  outcome: "<resolved | failed | skipped>"
```

---

## De-Escalation Rules

De-escalation occurs when conditions improve and a task no longer requires elevated handling.

### De-Escalation Triggers

1. **Blocker resolved.** The condition that caused the escalation has been addressed.
2. **Confidence restored.** Agent confidence returns above the tier threshold.
3. **Scope reduced.** Re-scoping brings the task back within original boundaries.
4. **Conflict resolved.** Agents reach consensus or the conflict resolution protocol succeeds.
5. **Human provides clarity.** The human's input resolves the ambiguity or approves a path forward.

### De-Escalation Protocol

1. ORCH verifies that the de-escalation trigger is genuine (not a false positive).
2. ORCH updates the task envelope:

	- State returns to `in_progress`
	- Escalation record is closed with resolution details
	- Tier may be re-assessed (a T3 task whose scope was reduced may become T2)
3. ORCH resumes normal routing and monitoring.
4. The de-escalation is logged in the audit trail.

### Tier Re-Assessment

When de-escalating, ORCH may re-classify the task to a lower tier if:

- The resolved scope is significantly smaller than originally assessed
- Risk factors have been mitigated
- Cross-domain concerns have been eliminated

Tier re-assessment adjusts timeout policies, checkpoint frequency, and review requirements accordingly.

---

## Timeout Policies Per Tier

| Tier | Initial Timeout | Re-attempt Budget (Step 1) | Re-route Budget (Step 2) | Senior Review Budget (Step 3) | Total Maximum |
| ---- | --------------- | -------------------------- | ------------------------ | ----------------------------- | ------------- |
| T1   | 15 minutes      | 7 minutes                  | 15 minutes               | 15 minutes                    | 52 minutes    |
| T2   | 60 minutes      | 30 minutes                 | 45 minutes               | 60 minutes                    | 3.25 hours    |
| T3   | 4 hours         | 2 hours                    | 3 hours                  | 4 hours                       | 13 hours      |
| T4   | 24 hours        | 12 hours                   | 18 hours                 | 24 hours                      | 78 hours      |

### Timeout Behavior

- When a timeout fires, ORCH immediately advances to the next escalation chain step.
- The total maximum is the sum of all steps. If the total maximum is exceeded without resolution, ORCH escalates to Human Decision Point (Step 4) regardless of the current chain step.
- Human Decision Point (Step 4) has no automated timeout. The user responds at their own pace.

---

## Conflict Resolution Protocol

When two or more agents produce contradictory outputs for related sub-tasks, ORCH initiates the conflict resolution protocol.

### Step 1: Identify the Conflict

- ORCH compares the outputs and identifies the specific points of contradiction.
- ORCH documents the conflict in a structured format:

   Agent A's position and reasoning
   Agent B's position and reasoning
   The specific data, logic, or design point in disagreement

### Step 2: Request Justification

- ORCH sends a `query` envelope to each conflicting agent asking for:

   The reasoning behind their output
   The sources, assumptions, or constraints that led to their decision
   Whether they can accommodate the other agent's position without violating their domain constraints

### Step 3: Automated Resolution Attempt

- If one agent can accommodate the other without violating constraints, ORCH adopts the compatible solution.
- If both agents can justify their positions equally, ORCH applies the following priority rules:

  . **Security over convenience.** The more secure option wins.
  . **Correctness over performance.** The correct option wins even if slower.
  . **Consistency over novelty.** The option that aligns with existing codebase patterns wins.
  . **User-facing impact.** The option with better user experience wins, all else being equal.

### Step 4: Senior Arbiter

- If automated resolution fails, ORCH dispatches the conflict to a senior reviewer agent.
- The senior reviewer has authority to override either agent's output.
- The reviewer's decision is final at the automated level.

### Step 5: Human Arbiter

- If the senior reviewer cannot resolve the conflict (e.g., it involves a business decision or policy choice), ORCH escalates to the human.
- The human is presented with both positions, the reviewer's analysis, and ORCH's recommendation.

---

## Priority Override Rules

Certain situations require immediate priority escalation, bypassing normal queue ordering.

### Priority Levels

| Level    | Description                                                  | Override Behavior                                |
| -------- | ------------------------------------------------------------ | ------------------------------------------------ |
| Critical | Security breach, data loss in progress, system outage        | Preempts ALL other tasks. All agents redirect.   |
| Urgent   | Production bug affecting users, compliance deadline imminent | Preempts T1/T2 tasks. T3/T4 tasks are paused.    |
| High     | Important feature deadline, significant user-reported issue  | Queued ahead of medium/low tasks. No preemption. |
| Medium   | Standard work with normal timelines                          | Normal queue ordering.                           |
| Low      | Nice-to-have improvements, exploratory work                  | Processed after all higher-priority tasks.       |

### Critical Priority Protocol

When a task is classified as Critical priority:

1. ORCH broadcasts a priority override to all active agents.
2. Non-essential active tasks are paused (state: `blocked` with reason `priority_override`).
3. All available agent capacity is redirected to the critical task.
4. Human is immediately notified.
5. Timeout policies are halved (faster escalation).
6. Checkpoints are required at every 5% progress increment.

### Urgent Priority Protocol

When a task is classified as Urgent priority:

1. ORCH pauses all T1 and T2 tasks (state: `blocked` with reason `priority_override`).
2. T3 and T4 tasks continue but do not receive additional agent allocation.
3. Available capacity is directed to the urgent task.
4. Human is notified within the first checkpoint.
5. Timeout policies are reduced by 25%.

### Priority Re-Assessment

ORCH re-assesses priority at every checkpoint. A task that was initially Critical may be de-prioritized to Urgent or High once the immediate danger is contained. Conversely, a Medium task may be escalated to High or Urgent if new information emerges.

---

## Summary

This escalation framework ensures that:

- Every task is handled at the appropriate level of rigor.
- No task silently fails or delivers incorrect output.
- Automated resolution is maximized before involving the human.
- The human is always informed and always has the final say.
- Every escalation is documented, traceable, and auditable.
- The system degrades gracefully under pressure, prioritizing the most critical work.

---

*Escalation Framework v1.0 -- Governing document for all agent escalation behavior.*
