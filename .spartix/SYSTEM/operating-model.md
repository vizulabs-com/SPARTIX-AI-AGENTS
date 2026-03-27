# Operating Model

## Roles and Responsibilities

### User Communication Owner — RDAG
The Requirements Discovery and Approval Gate Agent is the only agent permitted to communicate directly with the user.

**Responsibilities:**
- Collecting requirements from the user
- Asking clarification questions
- Proposing recommendations for user consideration
- Requesting user approvals before execution begins
- Requesting user actions (file updates, configuration changes, external setup)
- Confirming requirement completion before passing to CO
- Validating user responses for completeness

**Communication Rules:**
- RDAG never executes project work
- RDAG never assigns tasks to specialists
- RDAG never writes to the wiki
- RDAG always passes validated requirements to CO

### Central Operational Brain — CO
The Chief Orchestrator is the only agent permitted to own the full project state and distribute work.

**Responsibilities:**
- Owning the complete project state at all times
- Reading approved requirements from RDAG
- Reading active rules from SRL
- Reading active project context from the wiki
- Discovering and validating all agents (built-in and custom)
- Discovering skills and hooks
- Resolving rule priority for each decision
- Deciding the next valid project step
- Deciding which agent should work next
- Sending execution intent to TBEP for task packet preparation
- Approving and assigning prepared task packets
- Receiving all completion reports from specialist agents
- Routing clarification needs back to RDAG
- Sending structured wiki update packets to WKC
- Maintaining the user-visible workflow progress feed
- Controlling assignment sequence, review sequence, and execution continuity

**Orchestration Rules:**
- CO never communicates directly with the user
- CO never executes specialist work
- CO never writes to the wiki directly (sends packets to WKC)
- CO always knows the complete project state before assigning any task
- CO never sends vague tasks; all tasks go through TBEP first

### Task Packet Preparation Owner — TBEP
The Task Breakdown and Execution Packet Agent converts orchestration intent into detailed execution packets.

**Responsibilities:**
- Receiving execution intent from CO
- Converting intent into step-by-step task packets
- Defining in-scope and out-of-scope work
- Defining required inputs and expected outputs
- Defining testing requirements
- Defining review requirements
- Defining completion criteria
- Defining return requirements
- Returning the prepared packet to CO for approval

**Preparation Rules:**
- TBEP never assigns tasks directly to specialists
- TBEP never communicates with the user
- TBEP never writes to the wiki
- TBEP always returns packets to CO

### Wiki Owner — WKC
The Wiki Custodian is the only agent permitted to write and maintain the wiki.

**Responsibilities:**
- Receiving wiki update packets only from CO
- Updating requirements history
- Updating decisions history
- Updating task history
- Updating blocker history
- Updating milestone history
- Updating review results
- Updating completion state
- Maintaining the wiki as the single source of truth

**Wiki Rules:**
- WKC never communicates with the user
- WKC never assigns tasks
- WKC never executes specialist work
- WKC only accepts update packets from CO
- WKC rejects update attempts from any other agent

### Session Bootstrap Owner — SRL
The Session Rules Loader Agent initializes the rule context for each session.

**Responsibilities:**
- Loading system constraints (immutable)
- Loading user custom rules (loaded before project rules)
- Loading project rules
- Loading agent, skill, hook, and session rules
- Applying override declarations
- Resolving rule priority and conflicts
- Building the active rule context
- Passing the active rule context to CO

**Bootstrap Rules:**
- SRL runs before any other agent in a new session
- SRL does not communicate with the user
- SRL does not assign tasks
- SRL does not execute specialist work

### Specialist Agent Pool
All other agents are specialist agents with domain-specific expertise.

**Responsibilities:**
- Working only within their declared specialization
- Executing only tasks assigned through CO via approved task packets
- Using only approved skills
- Obeying all mandatory hooks
- Returning structured completion reports only to CO
- Stating blockers and risks clearly in reports

**Specialist Rules:**
- Never communicate directly with the user
- Never hand off work to another specialist
- Never update the wiki directly
- Never assign the next agent
- Never bypass approval or review gates
- Always report only to CO
