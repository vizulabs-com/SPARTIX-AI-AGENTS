# End-to-End Dataflow

## Complete Dataflow: User Request to Project Completion

### Phase 1: Session Initialization

1. **New session begins**
2. **SRL activates** and loads rules in priority order:
   - System rules (`RULES/system/`) — immutable base constraints
   - User custom rules (`RULES/user/`) — loaded before project rules
   - Project rules (`RULES/project/`) — project-specific governance
   - Agent rules (`RULES/agents/`) — agent-specific behavior rules
   - Skill rules (`RULES/skills/`) — skill usage constraints
   - Hook rules (`RULES/hooks/`) — hook trigger rules
   - Session rules (`RULES/sessions/`) — session-specific overrides
   - Override declarations (`RULES/overrides/`) — explicit overrides
3. **SRL resolves conflicts** using `RULES/rule-priority-map.json`
4. **SRL builds active rule context** and passes it to CO
5. **CO initializes**:
   - Loads active rule context
   - Discovers built-in agents from `AGENTS/` and `SYSTEM/agent-registry.json`
   - Discovers custom agents from `custom-agents/` and `SYSTEM/custom-agent-registry.json`
   - Discovers skills from `SKILLS/` and `custom-skills/`
   - Discovers hooks from `HOOKS/` and `custom-hooks/`
   - Reads current wiki state from `WIKI/`
   - Builds complete project state
6. **CO signals readiness** to RDAG
7. **RDAG greets the user** and begins requirement collection

### Phase 2: Requirements Collection

8. **User submits a request** to RDAG
9. **RDAG analyzes the request** for completeness
10. **RDAG asks clarification questions** if needed
11. **User provides clarifications**
12. **RDAG validates responses** for completeness and consistency
13. **RDAG proposes a requirements summary** to the user
14. **User approves** the requirements
15. **RDAG passes approved requirements** to CO

### Phase 3: Orchestration Planning

16. **CO receives approved requirements**
17. **CO analyzes project-wide state** including:
    - Current wiki state
    - Active rules
    - Available agents and their capabilities
    - Available skills
    - Active hooks
    - Any existing work in progress
18. **CO decides the execution strategy**:
    - Which domains are involved
    - What sequence of work is needed
    - Which agents are best suited
    - What dependencies exist between tasks
19. **CO selects the first task** and the responsible agent

### Phase 4: Task Preparation

20. **CO sends execution intent** to TBEP
21. **TBEP receives the intent** and creates a detailed task packet:
    - Task ID and description
    - Assigned agent
    - In-scope work
    - Out-of-scope work
    - Required inputs
    - Expected outputs
    - Testing requirements
    - Review requirements
    - Completion criteria
    - Mandatory hooks to obey
    - Approved skills to use
    - Return requirements
22. **TBEP returns the prepared packet** to CO
23. **CO reviews and approves** the task packet

### Phase 5: Specialist Execution

24. **CO assigns the task packet** to the selected specialist agent
25. **CO updates the user-visible workflow feed**: status = "assigned"
26. **Specialist agent receives the task packet**
27. **Specialist agent validates inputs** and checks for blockers
28. **If blockers exist**:
    - Specialist sends a blocker report to CO
    - CO determines if user input is needed
    - If yes: CO routes to RDAG → RDAG asks user → user responds → RDAG validates → RDAG returns to CO
    - If no: CO resolves internally and re-routes
29. **Specialist agent executes** the task:
    - Uses approved skills only
    - Obeys mandatory hooks (pre-action, mid-process, post-action)
    - Stays within declared specialization
    - CO updates workflow feed: status = "in progress"
30. **Specialist agent completes** and prepares a structured completion report

### Phase 6: Report and Review

31. **Specialist agent returns completion report** to CO only
32. **CO receives the completion report**
33. **CO updates workflow feed**: status = "under review" (if review is required)
34. **CO assigns review** to the appropriate Review-Only Specialist if required
35. **Review agent evaluates** the work and returns review results to CO
36. **If review fails**: CO may re-assign to the specialist with feedback, or escalate
37. **If review passes**: CO marks the task as complete

### Phase 7: Wiki Update

38. **CO prepares a wiki update packet** containing:
    - Task completion summary
    - Decisions made
    - Outputs produced
    - Review results
    - Any blockers encountered and how they were resolved
39. **CO sends the wiki update packet** to WKC
40. **WKC receives the packet** and updates the relevant wiki pages:
    - `WIKI/tasks.md` — task history
    - `WIKI/decisions.md` — decision history
    - `WIKI/requirements.md` — requirements traceability
    - `WIKI/reviews.md` — review results
    - `WIKI/blockers.md` — blocker history
    - `WIKI/milestones.md` — milestone tracking
    - `WIKI/changelog.md` — change history
41. **WKC confirms update** to CO

### Phase 8: Next Task Selection

42. **CO updates workflow feed**: status = "completed" for the finished task
43. **CO re-evaluates project state** with updated wiki
44. **CO decides the next task** based on:
    - Remaining requirements
    - Dependencies
    - Priority ordering
    - Active rules
45. **If more tasks remain**: Return to Phase 4 (Task Preparation)
46. **If all tasks are complete**: Proceed to Phase 9

### Phase 9: Project Completion

47. **CO verifies all requirements are met**
48. **CO sends final wiki update packet** to WKC with project completion state
49. **WKC updates** `WIKI/project-status.md` to "COMPLETED"
50. **CO updates workflow feed**: project status = "completed"
51. **CO notifies RDAG** of project completion
52. **RDAG informs the user** that the project is complete with a summary

## Clarification Flow (Mid-Execution)

When a specialist agent encounters missing information during execution:

1. Specialist detects missing information or ambiguity
2. Specialist sends a clarification request to CO (not to the user)
3. CO determines that user input is required
4. CO routes the issue to RDAG with context
5. RDAG formulates a clear question for the user
6. RDAG asks the user for clarification, approval, or action
7. User responds or updates the required file/configuration
8. RDAG validates and confirms the response
9. RDAG returns the resolved information to CO
10. CO updates the plan if needed
11. CO continues routing work (may re-assign to the same specialist or adjust)

## User Action Required Flow

When the system needs the user to perform an external action:

1. Agent detects that a user-managed configuration, file, or external action is needed
2. Agent sends a User Action Required packet to CO
3. CO routes to RDAG
4. RDAG presents the action request to the user with:
   - What needs to be done
   - Why it is needed
   - What file or configuration to update
   - Expected format or values
5. User performs the action
6. RDAG validates the action was completed
7. RDAG returns confirmation to CO
8. CO continues routing work
