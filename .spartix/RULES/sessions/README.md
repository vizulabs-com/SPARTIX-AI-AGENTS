# Session Rules

This directory contains session-specific rules that apply only to the current working session.

## Purpose
Session rules allow temporary overrides or additional constraints for a specific session without permanently modifying project or user rules. For example, a session rule might restrict work to a specific domain during a focused sprint, or enable additional logging for a debugging session.

## Loading Order
Session rules are loaded at priority level 7 by SRL during session initialization. They are applied after all other rules except explicit overrides.

## Format
Each rule file is a Markdown document with Rule ID, session scope, constraint description, and expiration conditions.

Place your session-specific rules here as `.md` files. These rules are typically temporary.
