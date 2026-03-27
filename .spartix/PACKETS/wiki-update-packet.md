# Wiki Update Packet Definition

## Purpose
A Wiki Update Packet is the structured document sent by CO to WKC to record project events, decisions, task results, and state changes in the wiki. Only CO may send these packets, and only WKC may process them.

## Required Sections

### Header
- **Packet ID**: Unique identifier (e.g., `WU-2024-001`)
- **Sent By**: CO (always)
- **Sent At**: Timestamp
- **Update Type**: requirements | decision | task | blocker | milestone | review | change | completion

### Update Content
- **Target Wiki Page**: Which wiki page to update (e.g., `WIKI/tasks.md`)
- **Update Action**: append | update-status | create-entry
- **Entry Title**: Title for the new entry or update
- **Entry Content**: Full content to be recorded
- **Related Task Packet ID**: Reference to the originating task packet (if applicable)
- **Related Agent**: Which agent produced the content being recorded

### Context
- **Trigger Event**: What caused this wiki update (task completion, decision, blocker, etc.)
- **Previous State**: What the relevant state was before this update
- **New State**: What the state is after this update

### Metadata
- **Tags**: Categorization tags for the entry
- **Priority**: Informational / Important / Critical
- **Cross-References**: Links to related wiki entries
