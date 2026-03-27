# System Rule: Core Constraints

**Rule ID**: SYS-001
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
These are the immutable core constraints of the .spartix system. No other rule may override these.

## Constraints

1. Only RDAG may communicate directly with the user.
2. Only CO may own the full project state and distribute work.
3. Only WKC may write to the wiki.
4. Only TBEP may prepare task packets from CO's execution intent.
5. Only SRL may load and resolve rules at session start.
6. No specialist agent may hand off work directly to another specialist.
7. No specialist agent may update the wiki directly.
8. No execution may begin before requirements are clarified and approved.
9. No execution may begin before a detailed task packet is prepared.
10. Every specialist must report only to CO.
11. The wiki is the single source of truth.
12. All agent files must follow the required unified format.
13. Every agent must be a specialist with domain expertise, not a generalist.
14. User custom rules must be loaded before project rules.
15. System rules cannot be overridden.

## Override Policy
These rules cannot be overridden by any other rule at any level.
