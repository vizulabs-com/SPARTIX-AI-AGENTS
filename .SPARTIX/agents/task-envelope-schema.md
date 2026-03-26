# Task Envelope Schema

## Standardized Inter-Agent Communication Format

---

## Overview

The Task Envelope is the atomic unit of communication in the agent system. Every instruction, result, escalation, handoff, and query between ORCH and specialist agents is transmitted as a Task Envelope. Envelopes are immutable once dispatched -- updates produce new versions, preserving a complete audit trail.

This document defines the full schema, field specifications, lifecycle states, and usage examples.

---

## Full YAML Schema

```yaml
envelope:
	# === IDENTITY ===
	id: "<uuid-v4>"                          # Unique envelope identifier
	version: <integer>                       # Envelope version (starts at 1, increments on updates)
	parent_id: "<uuid-v4 | null>"            # ID of the parent envelope (for sub-tasks and chains)
	root_id: "<uuid-v4>"                     # ID of the root envelope (top-level task)
	chain_position: <integer>                # Position in a sequential chain (1-indexed, 0 if standalone)

	# === CLASSIFICATION ===
	message_type: "<execute | review | escalate | handoff | inform | query>"
	priority: "<critical | high | medium | low>"
	tier: "<T1 | T2 | T3 | T4>"
	domain: "<string>"                       # Primary domain (e.g., "software", "infrastructure")
	sub_domain: "<string | null>"            # Sub-domain if applicable (e.g., "frontend", "ci-cd")

	# === ROUTING ===
	source_agent: "<agent-id>"               # Agent that created/dispatched this envelope
	target_agent: "<agent-id>"               # Agent that should process this envelope
	routing_pattern: "<single | parallel | sequential | chain>"
	execution_plan:                          # Only for chain/parallel patterns
		phases:
			- phase_id: <integer>
			  parallel: <boolean>
			  agents:
				  - agent_id: "<agent-id>"
				    sub_task_ref: "<uuid-v4>"
			- phase_id: <integer>
			  parallel: <boolean>
			  depends_on: [<phase_id>, ...]
			  agents:
				  - agent_id: "<agent-id>"
				    sub_task_ref: "<uuid-v4>"

	# === TASK DEFINITION ===
	task:
		title: "<string>"                    # Short task title (under 100 characters)
		description: |                       # Full task description (markdown supported)
			<Detailed description of the work to be performed.>
		acceptance_criteria:                 # List of criteria that must be met for completion
			- criterion: "<string>"
			  met: <boolean | null>           # null = not yet evaluated
		constraints:                         # Boundaries and limitations
			- "<string>"
		scope:
			in_scope:                        # Explicitly in scope
				- "<string>"
			out_of_scope:                    # Explicitly excluded
				- "<string>"
		estimated_effort: "<string>"         # Human-readable estimate (e.g., "2 hours", "30 minutes")

	# === CONTEXT ===
	context:
		prior_outputs:                       # Outputs from preceding agents in the chain
			- envelope_id: "<uuid-v4>"
			  agent_id: "<agent-id>"
			  summary: "<string>"            # Brief summary of the output
			  artifact_ref: "<string | null>" # Reference to the full output artifact
		requirements_ref: "<uuid-v4 | null>" # Reference to the requirements envelope
		clarification_ref: "<uuid-v4 | null>" # Reference to the clarification envelope
		additional_context: |                # Free-form additional context
			<Any additional information the agent needs.>
		environment:                         # Runtime environment details
			platform: "<string>"
			runtime: "<string>"
			dependencies:
				- name: "<string>"
				  version: "<string>"

	# === STATE ===
	state: "<pending | in_progress | done | blocked | escalated>"
	progress:
		percentage: <float>                  # 0.0 to 100.0
		checkpoint: "<string>"               # Current checkpoint label
		last_update: "<ISO-8601>"
	confidence: <float>                      # Agent's self-reported confidence (0.0 to 1.0)

	# === RESULT ===
	result:
		status: "<success | partial | failed | null>"
		output: |                            # The agent's output (markdown supported)
			<Agent's work product.>
		artifacts:                           # List of produced artifacts
			- id: "<uuid-v4>"
			  type: "<code | document | design | data | config | test | other>"
			  name: "<string>"
			  path: "<string | null>"        # File path if applicable
			  content_ref: "<string>"        # Reference to content storage
			  checksum: "<sha256>"
		validation:
			passed: <boolean | null>
			details: |
				<Validation results.>
		notes: |                             # Agent's notes on the work
			<Any observations, warnings, or recommendations.>

	# === ESCALATION ===
	escalation:
		is_escalated: <boolean>
		reason: "<confidence_drop | scope_exceeded | conflict | blocker | risk_detected | timeout | repeated_failure | ambiguity | null>"
		severity: "<critical | high | medium | low | null>"
		chain_step: <1 | 2 | 3 | 4 | null>
		description: |
			<Detailed description of the escalation.>
		suggested_resolution: |
			<Agent's suggested path forward.>
		options:
			- id: "<string>"
			  description: "<string>"
		recommendation:
			option_id: "<string | null>"
			reasoning: |
				<Why this option is recommended.>

	# === AUDIT TRAIL ===
	audit:
		created_at: "<ISO-8601>"
		created_by: "<agent-id>"
		updated_at: "<ISO-8601>"
		updated_by: "<agent-id>"
		history:
			- timestamp: "<ISO-8601>"
			  agent: "<agent-id>"
			  action: "<created | dispatched | started | checkpoint | completed | blocked | escalated | re-routed | resumed | de-escalated | closed>"
			  state_before: "<state>"
			  state_after: "<state>"
			  details: "<string>"
		version_history:
			- version: <integer>
			  timestamp: "<ISO-8601>"
			  changed_by: "<agent-id>"
			  change_summary: "<string>"

	# === METADATA ===
	metadata:
		schema_version: "1.0"
		tags:
			- "<string>"
		labels:
			"<key>": "<value>"
		ttl: "<ISO-8601-duration | null>"    # Time-to-live for the envelope
		retry_count: <integer>               # Number of retries attempted
		max_retries: <integer>               # Maximum allowed retries
```

---

## Field Descriptions

### Identity Fields

| Field            | Type    | Required | Description                                                                                       |
| ---------------- | ------- | -------- | ------------------------------------------------------------------------------------------------- |
| `id`             | UUID v4 | Yes      | Globally unique identifier for this envelope instance.                                            |
| `version`        | Integer | Yes      | Version number. Starts at 1. Incremented each time the envelope is updated (new version created). |
| `parent_id`      | UUID v4 | No       | The ID of the envelope that spawned this one. Null for top-level tasks.                           |
| `root_id`        | UUID v4 | Yes      | The ID of the root-level envelope. For top-level tasks, this equals `id`.                         |
| `chain_position` | Integer | Yes      | Position in a sequential chain. 0 if the task is standalone (not part of a chain).                |

### Classification Fields

| Field          | Type   | Required | Allowed Values                                                |
| -------------- | ------ | -------- | ------------------------------------------------------------- |
| `message_type` | String | Yes      | `execute`, `review`, `escalate`, `handoff`, `inform`, `query` |
| `priority`     | String | Yes      | `critical`, `high`, `medium`, `low`                           |
| `tier`         | String | Yes      | `T1`, `T2`, `T3`, `T4`                                        |
| `domain`       | String | Yes      | Any registered domain name                                    |
| `sub_domain`   | String | No       | Any registered sub-domain name                                |

### Message Types

| Type       | Purpose                                                                          |
| ---------- | -------------------------------------------------------------------------------- |
| `execute`  | Instructs the target agent to perform work. The primary task dispatch type.      |
| `review`   | Requests the target agent to review another agent's output without modifying it. |
| `escalate` | Signals an escalation event. Contains escalation details and options.            |
| `handoff`  | Transfers ownership of a task from one agent to another. Includes full context.  |
| `inform`   | Notifies an agent of information relevant to their work. No action required.     |
| `query`    | Requests information or clarification from the target agent. Expects a response. |

### Priority Levels

| Level      | Description                                                 | SLA Expectation                     |
| ---------- | ----------------------------------------------------------- | ----------------------------------- |
| `critical` | Immediate threat: security breach, data loss, system outage | Response within minutes             |
| `high`     | Significant impact: production bug, approaching deadline    | Response within the hour            |
| `medium`   | Normal workflow: standard feature work, maintenance         | Response within tier timeout        |
| `low`      | Non-urgent: exploratory work, nice-to-have improvements     | Best-effort within expanded timeout |

### Task Lifecycle States

| State         | Description                                                                            | Transitions From         | Transitions To                   |
| ------------- | -------------------------------------------------------------------------------------- | ------------------------ | -------------------------------- |
| `pending`     | Envelope created but not yet dispatched to the target agent.                           | (initial)                | `in_progress`                    |
| `in_progress` | Target agent has acknowledged the envelope and is actively working.                    | `pending`                | `done`, `blocked`, `escalated`   |
| `done`        | Work is complete. Result section is populated.                                         | `in_progress`            | (terminal, unless re-opened)     |
| `blocked`     | Agent cannot proceed. Awaiting resolution (escalation, clarification, dependency).     | `in_progress`            | `in_progress`, `escalated`       |
| `escalated`   | Task has been escalated per the escalation framework. Escalation section is populated. | `in_progress`, `blocked` | `in_progress`, `blocked`, `done` |

### State Transition Diagram

```
                    +---> done
                    |
pending ---> in_progress ---> blocked ---> in_progress (resumed)
                    |              |
                    |              +---> escalated ---> in_progress (de-escalated)
                    |                        |
                    +---> escalated           +---> done
                             |
                             +---> blocked
                             +---> done
```

### Routing Fields

| Field             | Type   | Required | Description                                                  |
| ----------------- | ------ | -------- | ------------------------------------------------------------ |
| `source_agent`    | String | Yes      | The agent that created or dispatched this envelope.          |
| `target_agent`    | String | Yes      | The agent designated to process this envelope.               |
| `routing_pattern` | String | Yes      | `single`, `parallel`, `sequential`, `chain`                  |
| `execution_plan`  | Object | No       | Required for `parallel`, `sequential`, and `chain` patterns. |

### Result Fields

| Field        | Type   | Required | Description                                                   |
| ------------ | ------ | -------- | ------------------------------------------------------------- |
| `status`     | String | No       | `success`, `partial`, `failed`, or null if not yet completed. |
| `output`     | String | No       | The agent's work product. Markdown supported.                 |
| `artifacts`  | Array  | No       | List of produced artifacts (code, documents, data, etc.).     |
| `validation` | Object | No       | Validation results from quality gates.                        |
| `notes`      | String | No       | Agent's observations, warnings, or recommendations.           |

### Artifact Types

| Type       | Description                                         |
| ---------- | --------------------------------------------------- |
| `code`     | Source code files, scripts, patches                 |
| `document` | Documentation, specifications, reports              |
| `design`   | Wireframes, mockups, design tokens                  |
| `data`     | Datasets, configurations, migrations                |
| `config`   | Configuration files, environment settings           |
| `test`     | Test files, test results, coverage reports          |
| `other`    | Any artifact that does not fit the above categories |

### Audit Action Types

| Action         | Description                                          |
| -------------- | ---------------------------------------------------- |
| `created`      | Envelope was created.                                |
| `dispatched`   | Envelope was sent to the target agent by ORCH.       |
| `started`      | Target agent acknowledged and began work.            |
| `checkpoint`   | Agent reported a progress checkpoint.                |
| `completed`    | Agent finished work and set state to `done`.         |
| `blocked`      | Agent set state to `blocked`.                        |
| `escalated`    | Escalation was triggered.                            |
| `re-routed`    | ORCH re-assigned the envelope to a different agent.  |
| `resumed`      | A blocked or escalated task was resumed.             |
| `de-escalated` | An escalated task was returned to normal processing. |
| `closed`       | Envelope is finalized. No further updates.           |

---

## Context Passing: How Prior Outputs Chain to the Next Agent

In sequential and chain routing patterns, each agent's output becomes part of the context for the next agent. This is achieved through the `context.prior_outputs` field.

### Chaining Rules

1. **ORCH manages the chain.** Agents do not pass envelopes to each other directly. ORCH receives each result and constructs the next envelope with accumulated context.
2. **Summaries are mandatory.** Each prior output entry includes a `summary` field so the receiving agent can quickly understand the upstream work without parsing the full artifact.
3. **Artifact references are used for large outputs.** The full output is stored as an artifact and referenced by ID. The receiving agent can access it if needed.
4. **Context is append-only.** Each new envelope in a chain contains ALL prior outputs, not just the immediately preceding one. This ensures any agent in the chain has full visibility.
5. **Context size management.** If the accumulated context exceeds a threshold, ORCH summarizes older entries and retains only artifact references for the full content.

### Chaining Example

```
Envelope 1 (Agent A: Research)
	context.prior_outputs: []
	result.output: "Research findings..."
	result.artifacts: [{id: "art-001", type: "document", ...}]

	|
	v (ORCH creates Envelope 2 with Agent A's output in context)

Envelope 2 (Agent B: Implementation)
	context.prior_outputs:
		- envelope_id: "<envelope-1-id>"
		  agent_id: "agent-a"
		  summary: "Research findings on X, Y, Z. Recommends approach B."
		  artifact_ref: "art-001"
	result.output: "Implementation code..."
	result.artifacts: [{id: "art-002", type: "code", ...}]

	|
	v (ORCH creates Envelope 3 with both prior outputs)

Envelope 3 (Agent C: Testing)
	context.prior_outputs:
		- envelope_id: "<envelope-1-id>"
		  agent_id: "agent-a"
		  summary: "Research findings on X, Y, Z. Recommends approach B."
		  artifact_ref: "art-001"
		- envelope_id: "<envelope-2-id>"
		  agent_id: "agent-b"
		  summary: "Implemented feature using approach B. 3 modules created."
		  artifact_ref: "art-002"
```

---

## Envelope Examples

### Example 1: Single Agent Task (T1 Routine)

```yaml
envelope:
	id: "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
	version: 1
	parent_id: null
	root_id: "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
	chain_position: 0

	message_type: "execute"
	priority: "medium"
	tier: "T1"
	domain: "software"
	sub_domain: "frontend"

	source_agent: "orch"
	target_agent: "software/frontend-01"
	routing_pattern: "single"
	execution_plan: null

	task:
		title: "Fix typo in login button label"
		description: |
			The login page button currently reads "Sing In" instead of "Sign In".
			Fix the typo in the button label component.
		acceptance_criteria:
			- criterion: "Button label reads 'Sign In'"
			  met: null
			- criterion: "No other text is changed"
			  met: null
		constraints:
			- "Change only the label text, not the component structure"
		scope:
			in_scope:
				- "Login button label in src/components/LoginButton.tsx"
			out_of_scope:
				- "Any other UI components"
				- "Styling changes"
		estimated_effort: "5 minutes"

	context:
		prior_outputs: []
		requirements_ref: "req-001-uuid"
		clarification_ref: null
		additional_context: null
		environment:
			platform: "web"
			runtime: "React 18"
			dependencies: []

	state: "pending"
	progress:
		percentage: 0.0
		checkpoint: "not_started"
		last_update: "2026-03-26T10:00:00Z"
	confidence: null

	result:
		status: null
		output: null
		artifacts: []
		validation: null
		notes: null

	escalation:
		is_escalated: false
		reason: null
		severity: null
		chain_step: null
		description: null
		suggested_resolution: null
		options: []
		recommendation:
			option_id: null
			reasoning: null

	audit:
		created_at: "2026-03-26T10:00:00Z"
		created_by: "orch"
		updated_at: "2026-03-26T10:00:00Z"
		updated_by: "orch"
		history:
			- timestamp: "2026-03-26T10:00:00Z"
			  agent: "orch"
			  action: "created"
			  state_before: null
			  state_after: "pending"
			  details: "Envelope created from requirements req-001-uuid"
		version_history:
			- version: 1
			  timestamp: "2026-03-26T10:00:00Z"
			  changed_by: "orch"
			  change_summary: "Initial creation"

	metadata:
		schema_version: "1.0"
		tags:
			- "bugfix"
			- "frontend"
		labels:
			component: "login"
			sprint: "2026-Q1-S6"
		ttl: "PT15M"
		retry_count: 0
		max_retries: 1
```

---

### Example 2: Multi-Agent Collaboration (T3 Complex)

```yaml
envelope:
	id: "b2c3d4e5-f6a7-8901-bcde-f12345678901"
	version: 1
	parent_id: null
	root_id: "b2c3d4e5-f6a7-8901-bcde-f12345678901"
	chain_position: 0

	message_type: "execute"
	priority: "high"
	tier: "T3"
	domain: "software"
	sub_domain: null

	source_agent: "orch"
	target_agent: "orch"
	routing_pattern: "chain"
	execution_plan:
		phases:
			- phase_id: 1
			  parallel: true
			  agents:
				  - agent_id: "research-strategy/architect-01"
				    sub_task_ref: "sub-001-uuid"
				  - agent_id: "product-design/ux-01"
				    sub_task_ref: "sub-002-uuid"
			- phase_id: 2
			  parallel: false
			  depends_on: [1]
			  agents:
				  - agent_id: "software/backend-01"
				    sub_task_ref: "sub-003-uuid"
			- phase_id: 3
			  parallel: true
			  depends_on: [2]
			  agents:
				  - agent_id: "software/frontend-01"
				    sub_task_ref: "sub-004-uuid"
				  - agent_id: "security-quality/qa-01"
				    sub_task_ref: "sub-005-uuid"
			- phase_id: 4
			  parallel: false
			  depends_on: [3]
			  agents:
				  - agent_id: "content/docs-01"
				    sub_task_ref: "sub-006-uuid"

	task:
		title: "Implement user notification preferences feature"
		description: |
			Build an end-to-end notification preferences feature that allows users
			to configure which notifications they receive and through which channels
			(email, in-app, push). Includes backend API, frontend UI, tests, and
			documentation.
		acceptance_criteria:
			- criterion: "Users can view their current notification preferences"
			  met: null
			- criterion: "Users can toggle individual notification types on/off"
			  met: null
			- criterion: "Users can select preferred channel per notification type"
			  met: null
			- criterion: "Changes persist across sessions"
			  met: null
			- criterion: "API is documented with OpenAPI spec"
			  met: null
			- criterion: "Unit and integration tests cover all new endpoints"
			  met: null
			- criterion: "UI is accessible (WCAG 2.1 AA)"
			  met: null
		constraints:
			- "Must integrate with existing notification service"
			- "Must not break existing notification delivery"
			- "Database migration must be backwards-compatible"
		scope:
			in_scope:
				- "Backend API for notification preferences CRUD"
				- "Frontend preferences panel UI"
				- "Database schema for preferences storage"
				- "Unit and integration tests"
				- "API documentation"
			out_of_scope:
				- "Notification delivery mechanism changes"
				- "Email template modifications"
				- "Mobile app changes"
		estimated_effort: "8 hours"

	context:
		prior_outputs: []
		requirements_ref: "req-042-uuid"
		clarification_ref: "clar-018-uuid"
		additional_context: |
			The existing notification service uses a pub/sub pattern.
			Current schema is in src/db/migrations/. The preferences
			table does not exist yet.
		environment:
			platform: "web"
			runtime: "Node.js 22, React 18"
			dependencies:
				- name: "notification-service"
				  version: "3.2.1"
				- name: "postgres"
				  version: "16"

	state: "pending"
	progress:
		percentage: 0.0
		checkpoint: "not_started"
		last_update: "2026-03-26T09:00:00Z"
	confidence: null

	result:
		status: null
		output: null
		artifacts: []
		validation: null
		notes: null

	escalation:
		is_escalated: false
		reason: null
		severity: null
		chain_step: null
		description: null
		suggested_resolution: null
		options: []
		recommendation:
			option_id: null
			reasoning: null

	audit:
		created_at: "2026-03-26T09:00:00Z"
		created_by: "orch"
		updated_at: "2026-03-26T09:00:00Z"
		updated_by: "orch"
		history:
			- timestamp: "2026-03-26T09:00:00Z"
			  agent: "orch"
			  action: "created"
			  state_before: null
			  state_after: "pending"
			  details: "Complex feature envelope created with 4-phase execution plan"
		version_history:
			- version: 1
			  timestamp: "2026-03-26T09:00:00Z"
			  changed_by: "orch"
			  change_summary: "Initial creation"

	metadata:
		schema_version: "1.0"
		tags:
			- "feature"
			- "notifications"
			- "multi-agent"
		labels:
			feature: "notification-preferences"
			sprint: "2026-Q1-S6"
			epic: "user-settings-overhaul"
		ttl: "PT4H"
		retry_count: 0
		max_retries: 2
```

---

### Example 3: Escalation Envelope

```yaml
envelope:
	id: "c3d4e5f6-a7b8-9012-cdef-123456789012"
	version: 2
	parent_id: "b2c3d4e5-f6a7-8901-bcde-f12345678901"
	root_id: "b2c3d4e5-f6a7-8901-bcde-f12345678901"
	chain_position: 2

	message_type: "escalate"
	priority: "high"
	tier: "T3"
	domain: "software"
	sub_domain: "backend"

	source_agent: "software/backend-01"
	target_agent: "orch"
	routing_pattern: "single"
	execution_plan: null

	task:
		title: "Implement notification preferences API endpoints"
		description: |
			Create CRUD API endpoints for user notification preferences.
			This is sub-task 3 of the notification preferences feature.
		acceptance_criteria:
			- criterion: "GET /api/users/:id/notification-preferences returns current preferences"
			  met: true
			- criterion: "PUT /api/users/:id/notification-preferences updates preferences"
			  met: null
			- criterion: "Database migration creates preferences table"
			  met: true
			- criterion: "Input validation rejects invalid channel types"
			  met: null
		constraints:
			- "Must integrate with existing notification service"
			- "Database migration must be backwards-compatible"
		scope:
			in_scope:
				- "Backend API endpoints"
				- "Database migration"
				- "Input validation"
			out_of_scope:
				- "Frontend changes"
				- "Notification delivery"
		estimated_effort: "3 hours"

	context:
		prior_outputs:
			- envelope_id: "sub-001-uuid"
			  agent_id: "research-strategy/architect-01"
			  summary: "Architecture recommends separate preferences table with foreign key to users. Event-driven sync with notification service."
			  artifact_ref: "art-arch-001"
			- envelope_id: "sub-002-uuid"
			  agent_id: "product-design/ux-01"
			  summary: "UX spec defines 3 notification channels and 8 notification types. Toggle-based UI with channel selector per type."
			  artifact_ref: "art-ux-002"
		requirements_ref: "req-042-uuid"
		clarification_ref: "clar-018-uuid"
		additional_context: |
			The existing notification service pub/sub contract does not
			include a preferences check. The agent discovered that the
			notification service fires events without consulting user
			preferences, which contradicts the requirements.
		environment:
			platform: "server"
			runtime: "Node.js 22"
			dependencies:
				- name: "notification-service"
				  version: "3.2.1"

	state: "escalated"
	progress:
		percentage: 45.0
		checkpoint: "database_migration_complete"
		last_update: "2026-03-26T11:30:00Z"
	confidence: 0.55

	result:
		status: "partial"
		output: |
			Completed:
			- Database migration for preferences table
			- GET endpoint for reading preferences

			Blocked:
			- PUT endpoint cannot enforce preferences without notification
			  service changes. The service does not check preferences
			  before dispatching notifications.
		artifacts:
			- id: "art-be-003"
			  type: "code"
			  name: "notification-preferences-migration.sql"
			  path: "src/db/migrations/20260326_notification_preferences.sql"
			  content_ref: "store://artifacts/art-be-003"
			  checksum: "sha256:a1b2c3d4..."
			- id: "art-be-004"
			  type: "code"
			  name: "get-preferences-endpoint.ts"
			  path: "src/api/notifications/getPreferences.ts"
			  content_ref: "store://artifacts/art-be-004"
			  checksum: "sha256:e5f6a7b8..."
		validation:
			passed: null
			details: |
				Partial validation. GET endpoint passes unit tests.
				PUT endpoint not yet testable due to service dependency.
		notes: |
			The notification service (v3.2.1) does not expose a
			preferences-aware dispatch API. Implementing the PUT
			endpoint without this would create a false sense of control --
			users would set preferences, but notifications would still
			be sent regardless.

	escalation:
		is_escalated: true
		reason: "blocker"
		severity: "high"
		chain_step: 1
		description: |
			The notification service does not check user preferences
			before dispatching. The PUT endpoint for preferences would
			be cosmetic only without a service-level change. This is
			an architectural blocker that exceeds the scope of this
			sub-task.
		suggested_resolution: |
			Option 1: Extend the notification service to check preferences
			before dispatch (scope increase, requires service team).
			Option 2: Implement preferences as a filter layer between
			the service and delivery channels (workaround, self-contained).
			Option 3: Ship GET endpoint now, defer PUT until service
			is updated (partial delivery).
		options:
			- id: "opt-1"
			  description: "Extend notification service to check preferences (scope increase)"
			- id: "opt-2"
			  description: "Implement preferences as a filter layer (workaround)"
			- id: "opt-3"
			  description: "Ship GET only, defer PUT (partial delivery)"
		recommendation:
			option_id: "opt-2"
			reasoning: |
				Option 2 is self-contained and does not require changes
				to the notification service team's roadmap. It can be
				implemented as a middleware layer that intercepts
				notification events and filters based on user preferences.
				This is a proven pattern and keeps the feature scope
				manageable.

	audit:
		created_at: "2026-03-26T10:00:00Z"
		created_by: "orch"
		updated_at: "2026-03-26T11:30:00Z"
		updated_by: "software/backend-01"
		history:
			- timestamp: "2026-03-26T10:00:00Z"
			  agent: "orch"
			  action: "created"
			  state_before: null
			  state_after: "pending"
			  details: "Sub-task envelope created for backend API work"
			- timestamp: "2026-03-26T10:02:00Z"
			  agent: "orch"
			  action: "dispatched"
			  state_before: "pending"
			  state_after: "pending"
			  details: "Dispatched to software/backend-01"
			- timestamp: "2026-03-26T10:03:00Z"
			  agent: "software/backend-01"
			  action: "started"
			  state_before: "pending"
			  state_after: "in_progress"
			  details: "Agent acknowledged and began work"
			- timestamp: "2026-03-26T10:45:00Z"
			  agent: "software/backend-01"
			  action: "checkpoint"
			  state_before: "in_progress"
			  state_after: "in_progress"
			  details: "Database migration complete (25%)"
			- timestamp: "2026-03-26T11:15:00Z"
			  agent: "software/backend-01"
			  action: "checkpoint"
			  state_before: "in_progress"
			  state_after: "in_progress"
			  details: "GET endpoint complete (45%)"
			- timestamp: "2026-03-26T11:30:00Z"
			  agent: "software/backend-01"
			  action: "escalated"
			  state_before: "in_progress"
			  state_after: "escalated"
			  details: "Blocker: notification service does not support preferences-aware dispatch"
		version_history:
			- version: 1
			  timestamp: "2026-03-26T10:00:00Z"
			  changed_by: "orch"
			  change_summary: "Initial creation"
			- version: 2
			  timestamp: "2026-03-26T11:30:00Z"
			  changed_by: "software/backend-01"
			  change_summary: "Escalation: blocker encountered, partial results included"

	metadata:
		schema_version: "1.0"
		tags:
			- "feature"
			- "backend"
			- "escalation"
			- "blocker"
		labels:
			feature: "notification-preferences"
			sub_task: "api-endpoints"
			sprint: "2026-Q1-S6"
		ttl: "PT4H"
		retry_count: 0
		max_retries: 2
```

---

### Example 4: Back-Escalation to Clarifier

```yaml
envelope:
	id: "d4e5f6a7-b8c9-0123-defa-234567890123"
	version: 1
	parent_id: "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
	root_id: "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
	chain_position: 0

	message_type: "escalate"
	priority: "medium"
	tier: "T2"
	domain: "clarification"
	sub_domain: null

	source_agent: "orch"
	target_agent: "clarification/clarifier-01"
	routing_pattern: "single"
	execution_plan: null

	task:
		title: "Resolve ambiguity in notification preferences scope"
		description: |
			During execution of the notification preferences feature,
			the backend agent discovered that the requirements do not
			specify behavior for the following scenario:

			What happens when a user disables all channels for a
			notification type that is marked as "mandatory" by the
			system (e.g., security alerts, billing notifications)?

			The requirements state users can "toggle individual
			notification types on/off" but also reference "mandatory
			notifications" in the constraints without defining the
			interaction between these two rules.
		acceptance_criteria:
			- criterion: "User intent regarding mandatory notification override is clarified"
			  met: null
			- criterion: "Updated requirements are returned to ORCH"
			  met: null
		constraints:
			- "Must resolve without assuming user intent"
			- "Must present the ambiguity clearly to the user"
		scope:
			in_scope:
				- "Clarification of mandatory vs. user-togglable notifications"
			out_of_scope:
				- "Implementation decisions"
				- "Technical architecture"
		estimated_effort: "10 minutes"

	context:
		prior_outputs:
			- envelope_id: "sub-003-uuid"
			  agent_id: "software/backend-01"
			  summary: "Backend agent identified ambiguity: mandatory notification types conflict with user toggle capability. Partial implementation paused."
			  artifact_ref: null
		requirements_ref: "req-042-uuid"
		clarification_ref: "clar-018-uuid"
		additional_context: |
			The original clarification (clar-018) did not address
			mandatory notifications. The requirements (req-042)
			mention "mandatory notifications" in constraint 4 but
			the acceptance criteria allow toggling all types.

			Suggested questions for the user:
			1. Should mandatory notifications (security alerts, billing)
			   be exempt from user toggle controls?
			2. If yes, should they be visible in the preferences UI
			   but grayed out, or hidden entirely?
			3. If no, what happens if a user disables security alerts
			   and then a security event occurs?
		environment: null

	state: "pending"
	progress:
		percentage: 0.0
		checkpoint: "not_started"
		last_update: "2026-03-26T12:00:00Z"
	confidence: null

	result:
		status: null
		output: null
		artifacts: []
		validation: null
		notes: null

	escalation:
		is_escalated: true
		reason: "ambiguity"
		severity: "medium"
		chain_step: null
		description: |
			Back-escalation to Clarifier. The requirements contain
			a contradiction between user toggle capability and
			mandatory notification constraints. This cannot be
			resolved by the executing agent without user input.
		suggested_resolution: |
			Engage the user with the three questions listed in
			additional_context. Update the requirements based on
			the user's answers.
		options: []
		recommendation:
			option_id: null
			reasoning: null

	audit:
		created_at: "2026-03-26T12:00:00Z"
		created_by: "orch"
		updated_at: "2026-03-26T12:00:00Z"
		updated_by: "orch"
		history:
			- timestamp: "2026-03-26T12:00:00Z"
			  agent: "orch"
			  action: "created"
			  state_before: null
			  state_after: "pending"
			  details: "Back-escalation envelope for ambiguity resolution. Parent task paused."
		version_history:
			- version: 1
			  timestamp: "2026-03-26T12:00:00Z"
			  changed_by: "orch"
			  change_summary: "Initial creation for back-escalation to clarifier"

	metadata:
		schema_version: "1.0"
		tags:
			- "back-escalation"
			- "clarification"
			- "ambiguity"
		labels:
			feature: "notification-preferences"
			escalation_type: "back-escalation"
		ttl: "PT30M"
		retry_count: 0
		max_retries: 0
```

---

## Versioning and Audit Trail

### Envelope Versioning

Envelopes are immutable once dispatched. Any modification creates a new version.

| Rule                                                                                          |
| --------------------------------------------------------------------------------------------- |
| The `version` field starts at 1 and increments by 1 for each update.                          |
| The `id` remains the same across versions. The combination of `id` + `version` is unique.     |
| The `version_history` array records every version with timestamp, author, and change summary. |
| Previous versions are retained in storage and can be retrieved for audit purposes.            |
| Only the latest version is active. Agents always work with the latest version.                |

### Audit Trail Requirements

| Requirement                                                                                        |
| -------------------------------------------------------------------------------------------------- |
| Every state transition MUST be recorded in `audit.history`.                                        |
| Every routing decision by ORCH MUST be recorded.                                                   |
| Every escalation event MUST be recorded with trigger, severity, and outcome.                       |
| Timestamps MUST be in ISO-8601 format with timezone (UTC preferred).                               |
| The `created_by` and `updated_by` fields MUST always reflect the actual agent that acted.          |
| Audit trails are append-only. Entries are never deleted or modified.                               |
| For compliance-sensitive tasks (T4), the audit trail is the primary evidence of process adherence. |

---

## Attachment and Artifact Reference Format

Artifacts produced by agents are referenced in the `result.artifacts` array. The reference format ensures artifacts are traceable, verifiable, and retrievable.

### Artifact Reference Schema

```yaml
artifact:
	id: "<uuid-v4>"                          # Unique artifact identifier
	type: "<code | document | design | data | config | test | other>"
	name: "<human-readable-name>"            # File name or descriptive name
	path: "<relative-file-path | null>"      # Path within the project, if applicable
	content_ref: "<storage-uri>"             # URI to the artifact content
	checksum: "sha256:<hex-digest>"          # SHA-256 hash for integrity verification
	size_bytes: <integer>                    # Size in bytes
	mime_type: "<string>"                    # MIME type (e.g., "text/typescript", "application/json")
	created_at: "<ISO-8601>"                 # When the artifact was created
	created_by: "<agent-id>"                 # Which agent produced it
	metadata:                                # Optional key-value metadata
		"<key>": "<value>"
```

### Content Reference URI Schemes

| Scheme               | Description                                                      | Example                             |
| -------------------- | ---------------------------------------------------------------- | ----------------------------------- |
| `store://artifacts/` | Internal artifact storage                                        | `store://artifacts/art-001`         |
| `file://`            | Local file system reference                                      | `file:///src/api/endpoint.ts`       |
| `git://`             | Git reference (commit + path)                                    | `git://abc123:src/api/endpoint.ts`  |
| `inline://`          | Content embedded directly in the envelope (small artifacts only) | `inline://base64:<encoded-content>` |

### Checksum Verification

- Every artifact MUST include a SHA-256 checksum.
- ORCH verifies checksums when receiving artifacts from agents.
- If a checksum mismatch is detected, ORCH rejects the artifact and requests re-submission.
- Checksum verification is logged in the audit trail.

---

*Task Envelope Schema v1.0 -- Governing schema for all inter-agent communication.*
