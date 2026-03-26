# Technical Debt Registry

> Tracks known technical debt in SPARTIX. Each item represents a compromise made for speed, a known shortcut, or an area that needs improvement.

---

## How to Use This Registry

- Add entries when you identify or introduce technical debt.
- Assign an owner responsible for eventual remediation.
- Review this registry during sprint planning to schedule debt paydown.
- Update status as items are addressed.

---

## Debt Items

| ID | Description | Impact | Priority | Estimated Effort | Owner | Status | Created Date |
|----|-------------|--------|----------|-----------------|-------|--------|--------------|
| *TD-001* | *[What the debt is and where it lives]* | *[How it affects the system: performance, maintainability, reliability, developer experience, etc.]* | *[Critical / High / Medium / Low]* | *[Hours / Days / Weeks]* | *[Person responsible]* | *[Open / In Progress / Resolved / Accepted]* | *YYYY-MM-DD* |
| *TD-002* | *[What the debt is and where it lives]* | *[How it affects the system]* | *[Critical / High / Medium / Low]* | *[Hours / Days / Weeks]* | *[Person responsible]* | *[Open / In Progress / Resolved / Accepted]* | *YYYY-MM-DD* |
| *TD-003* | *[What the debt is and where it lives]* | *[How it affects the system]* | *[Critical / High / Medium / Low]* | *[Hours / Days / Weeks]* | *[Person responsible]* | *[Open / In Progress / Resolved / Accepted]* | *YYYY-MM-DD* |

---

## Priority Definitions

| Priority | Definition | Action |
|----------|-----------|--------|
| **Critical** | Actively causing issues in production or blocking development | Address in current sprint |
| **High** | Significant impact on maintainability, performance, or reliability | Schedule within next 2 sprints |
| **Medium** | Noticeable impact but manageable with workarounds | Schedule within next quarter |
| **Low** | Minor inconvenience, no functional impact | Address opportunistically |

---

## Status Definitions

| Status | Definition |
|--------|-----------|
| **Open** | Identified but not yet being worked on |
| **In Progress** | Actively being remediated |
| **Resolved** | Debt has been paid down; item closed |
| **Accepted** | Consciously accepted as-is with documented reasoning |

---

## Debt Categories

| Category | Description | Examples |
|----------|-------------|---------|
| **Code Quality** | Poor structure, duplication, complexity | Duplicated logic, god classes, magic numbers |
| **Testing** | Insufficient or brittle tests | Missing unit tests, flaky integration tests |
| **Architecture** | Structural compromises | Tight coupling, missing abstractions, layering violations |
| **Dependencies** | Outdated or risky dependencies | Unpatched libraries, deprecated APIs |
| **Documentation** | Missing or outdated documentation | Undocumented APIs, stale setup guides |
| **Infrastructure** | Build, deploy, or tooling issues | Slow CI, manual deployment steps |
| **Performance** | Known performance bottlenecks | Unoptimized queries, missing caching |
| **Security** | Known security weaknesses | Incomplete input validation, weak auth |

---

## Summary Dashboard

| Category | Open | In Progress | Resolved | Accepted | Total |
|----------|------|-------------|----------|----------|-------|
| Code Quality | *0* | *0* | *0* | *0* | *0* |
| Testing | *0* | *0* | *0* | *0* | *0* |
| Architecture | *0* | *0* | *0* | *0* | *0* |
| Dependencies | *0* | *0* | *0* | *0* | *0* |
| Other | *0* | *0* | *0* | *0* | *0* |
| **Total** | **0** | **0** | **0** | **0** | **0** |

---

## Resolution Log

| ID | Resolved Date | Resolution Summary | Resolved By |
|----|---------------|-------------------|-------------|
| *TD-XXX* | *YYYY-MM-DD* | *[How the debt was addressed]* | *[Person]* |

---

*Last updated: YYYY-MM-DD*
*Maintained by Nabil Mansour [Wiki Builder]*
