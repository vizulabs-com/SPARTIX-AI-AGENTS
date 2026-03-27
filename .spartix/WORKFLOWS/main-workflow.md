# Main Workflow Definition

## End-to-End Project Workflow

### Phase 1: Session Bootstrap
1. New session begins
2. SRL loads rules in priority order (system → user → project → agents → skills → hooks → sessions → overrides)
3. SRL resolves conflicts using `rule-priority-map.json`
4. SRL passes active rule context to CO
5. CO initializes: discovers agents, skills, hooks; reads wiki state
6. CO signals readiness to RDAG
7. RDAG greets the user

### Phase 2: Requirements Collection
8. User submits request to RDAG
9. RDAG analyzes for completeness
10. RDAG asks clarification questions (iterative until complete)
11. RDAG analyzes the request context and prepares proactive recommendations (SYS-009)
12. RDAG presents recommendations categorized by type (features, UX, security, performance, accessibility) with priority levels
13. User reviews recommendations — accepts, rejects, or modifies freely
14. RDAG incorporates accepted recommendations into the requirements summary
15. RDAG proposes final requirements summary (user's explicit requirements + accepted recommendations)
16. User approves requirements
17. RDAG passes approved requirements to CO

### Phase 3: Orchestration Planning
14. CO receives approved requirements
15. CO analyzes project-wide state (wiki, rules, agents, skills, hooks)
16. CO determines execution strategy and task sequence
17. CO selects first task and responsible agent

### Phase 4: Task Preparation
18. CO sends execution intent to TBEP
19. TBEP creates detailed step-by-step task packet (including workspace definition, file scope, dependency impact, command plan, testing plan)
20. TBEP returns packet to CO
21. CO reviews packet for completeness, clarity, step-by-step readiness, and alignment with active rules
22. If packet is incomplete or vague: CO returns to TBEP for correction
23. CO approves packet

### Phase 4b: Wiki-Before-Execution Gate
24. CO sends approved task packet to WKC
25. WKC updates wiki with: approved task packet, workflow transition, planned execution state
26. WKC confirms wiki update to CO
27. CO confirms execution is now unlocked (execution blocked until this point)

### Phase 5: Specialist Execution
28. CO assigns task packet to specialist
29. CO updates workflow feed: status = "execution unlocked → assigned"
30. Specialist validates inputs and confirms execution readiness
31. Specialist executes (using approved skills, obeying hooks, following step-by-step packet)
32. CO updates workflow feed: status = "in progress"
33. Specialist completes and prepares completion report (including enhanced workspace reporting)

### Phase 6: Report and Review
34. Specialist returns completion report to CO
35. CO evaluates report
36. If review required: CO assigns to review specialist
37. Review specialist evaluates and returns results to CO
38. If review passes: proceed; if fails: re-assign or escalate

### Phase 7: Wiki Update
39. CO prepares wiki update packet
40. CO sends packet to WKC
41. WKC updates relevant wiki pages
42. WKC confirms update to CO

### Phase 8: Next Task
43. CO updates workflow feed: status = "completed"
44. CO re-evaluates project state
45. If more tasks: return to Phase 4
46. If all complete: proceed to Phase 9

### Phase 9: Project Completion
47. CO verifies all requirements met
48. CO sends final wiki update to WKC
49. WKC records project completion
50. CO notifies RDAG
51. RDAG informs user of completion

---

## Visibility Requirement
All phase transitions must be shown to the user using the structured formats defined in `.spartix/RULES/system/visibility-formats.md` (SYS-004).

## Historical Context Requirement
Phase 1 (Session Bootstrap) must include checking for historical project context before proceeding. See `.spartix/RULES/system/wiki-governance.md` (SYS-005), Rules 22-26.

## Frontend Quality Requirement
Phase 5 (Specialist Execution) for frontend tasks must include the self-debugging loop, classification, and quality gate defined in `.spartix/RULES/system/frontend-debugging.md` (SYS-007).
