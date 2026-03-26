# Frequently Asked Questions

> Answers to common questions about SPARTIX. If your question isn't here, check the relevant wiki section or ask in the team channel.

---

## General

### What is SPARTIX?
*[One-paragraph project description]*

### Who is the target audience?
*[Description of primary users and use cases]*

### Where can I find the project roadmap?
See the [Timeline](../project/timeline.md) for milestones and the [Vision](../project/vision.md) for long-term goals.

### How do I report a bug or request a feature?
*[Describe the process: issue tracker, template to use, who to tag]*

### Where are project decisions documented?
See the [Decision Log](../decisions/decision-log.md) for all decisions and the [ADR directory](../architecture/adr/) for architectural decisions.

---

## Technical

### What is the technology stack?
See [Technology Stack](../architecture/tech-stack.md) for the complete inventory.

### What version of Node.js should I use?
*[Specify version and link to setup guide]*. See [Setup Guide](../development/setup-guide.md) for details.

### How is the project structured?
See [Architecture Overview](../architecture/overview.md) for the high-level structure.

### Where do I find API documentation?
*[Location of API docs, or "not yet available"]*

### How do I add a new dependency?
*[Process for proposing and adding dependencies]*

---

## Process

### What is the Git branching strategy?
See [Coding Conventions](../development/conventions.md) for branch naming and workflow details.

### How does code review work?
*[Describe the review process, who reviews, turnaround expectations]*

### How are tasks assigned to agents?
See [Agent Routing Log](../development/agent-routing-log.md) for routing rules and history.

### What is the release process?
See [Build & Deploy](../development/build-deploy.md) for the full release workflow.

### How do I update the wiki?
*[Describe the process: edit directly, submit PR, who reviews wiki changes]*

---

## Troubleshooting

### Build is failing -- what do I check first?
1. Verify your Node.js version matches the requirement.
2. Delete `node_modules` and run `npm install` again.
3. Check the [Common Issues](../development/setup-guide.md#common-issues) section.
4. *[Additional project-specific steps]*

### Tests are failing locally but pass in CI (or vice versa)
1. *[Check environment differences]*
2. *[Check for time-dependent or order-dependent tests]*
3. *[Describe any known flaky tests]*

### I'm getting permission errors
1. *[Common permission issue and fix]*
2. *[Platform-specific guidance]*

### Where do I find logs?
*[Describe log locations for development and production environments]*

---

## Adding to This FAQ

When you encounter a question that gets asked more than once:

1. Add it under the appropriate section above.
2. Provide a clear, concise answer.
3. Link to detailed documentation where applicable.
4. Keep answers current -- update them when things change.

---

*Last updated: YYYY-MM-DD*
*Maintained by Nabil Mansour [Wiki Builder]*
