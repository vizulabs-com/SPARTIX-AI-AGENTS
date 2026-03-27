# Override Declarations

This directory contains explicit override declarations that take highest user-level priority in the rule resolution chain.

## Purpose
Override declarations allow explicit, intentional overrides of lower-priority rules. They are applied last in the loading sequence and take precedence over all rules except immutable system constraints. Use overrides sparingly and document the rationale clearly.

## Loading Order
Overrides are loaded at priority level 8 (last) by SRL during session initialization. They cannot override system rules (priority level 1), which are immutable.

## Format
Each override file is a Markdown document with:
- Override ID
- Target rule(s) being overridden
- Override behavior
- Rationale for the override
- Expiration (if temporary)

## Important
- Overrides CANNOT override system rules — system constraints are immutable
- Every override MUST include a clear rationale
- Overrides should be reviewed periodically and removed when no longer needed

Place your override declarations here as `.md` files.
