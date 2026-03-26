# Requirements

> This section tracks the full lifecycle of requirements for SPARTIX -- from initial request through clarification, specification, implementation, and evolution.

---

## How Requirements Flow

```
Original Request --> Clarification --> Brief --> User Stories --> Implementation --> Evolution
```

1. A stakeholder or agent submits an **original request**.
2. The request goes through **clarification** to resolve ambiguities.
3. A **brief** is produced summarizing the validated requirement.
4. The brief is broken into **user stories** for implementation.
5. As the project evolves, requirements are tracked in the **evolution** log.

---

## Sub-folders

### `original-requests/`
Raw, unprocessed requests as they were originally submitted. These are preserved exactly as received for traceability.

- **Naming convention:** `REQ-XXXX-short-description.md`
- **Contents:** Original text, submitter, date received, source channel

### `clarification-logs/`
Records of questions asked, answers received, and assumptions validated during requirement clarification.

- **Naming convention:** `CLR-XXXX-short-description.md`
- **Contents:** Original request reference, questions, answers, assumptions, sign-off

### `briefs/`
Finalized requirement specifications ready for implementation. These are the authoritative source of what needs to be built.

- **Naming convention:** `BRF-XXXX-short-description.md`
- **Contents:** Summary, acceptance criteria, constraints, dependencies, priority, linked original request

### `user-stories/`
Implementation-ready user stories derived from briefs. Written in standard user story format.

- **Naming convention:** `US-XXXX-short-description.md`
- **Contents:** As a [user], I want [goal], so that [reason]. Acceptance criteria, story points, linked brief

### `evolution/`
Tracks how requirements change over time. Every modification to an approved brief or user story is logged here.

- **Naming convention:** `EVO-XXXX-short-description.md`
- **Contents:** Original requirement reference, change description, reason, impact assessment, approval

---

## Requirement States

| State | Description |
|-------|-------------|
| **Draft** | Initial submission, not yet reviewed |
| **In Clarification** | Questions outstanding, awaiting answers |
| **Specified** | Brief complete, ready for story breakdown |
| **Ready** | User stories written, ready for sprint planning |
| **In Progress** | Currently being implemented |
| **Done** | Implemented and verified |
| **Deferred** | Postponed to a future phase |
| **Rejected** | Will not be implemented (with documented reason) |

---

## Quick Reference

- Start a new requirement: Create a file in `original-requests/`
- Check requirement status: See the state field in each brief
- Understand a requirement change: Check `evolution/`
- Find acceptance criteria: Look in the corresponding `briefs/` file

---

*Last updated: YYYY-MM-DD*
*Maintained by Nabil Mansour [Wiki Builder]*
