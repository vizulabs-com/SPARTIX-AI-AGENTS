# SPARTIX Wiki

> **This folder is intentionally empty in the base framework.**

## What is this?

The `WIKI/` folder is the **single source of truth** for your project's memory. It is automatically populated by the SPARTIX workflow during active project execution.

## When does it get populated?

When you use SPARTIX to govern a real project, the **Wiki Custodian (WKC)** agent creates and maintains wiki entries here as work progresses. You do not need to create anything manually.

## What goes here?

During active project execution, the wiki will contain categorized sections for:

- Project overview
- Approved requirements and requirement history
- Clarification history
- Decisions
- Task backlog, active tasks, and completed tasks
- Blockers and risks
- Reviews and validations
- Architecture and technical notes
- Configuration and environment notes
- Workflow transitions
- Milestones and progress
- Final completion state

## Important rules

- **Only the Wiki Custodian (WKC) agent may write to this folder.** No other agent or manual edit should modify wiki content during governed execution.
- The wiki is the primary reference the AI agents consult before making assumptions from code or other files.
- Current state is always kept separate from historical state for clarity.

## For users cloning this repo

If you are setting up SPARTIX for a new project, leave this folder as-is. The workflow will initialize it when you begin your first governed session.
