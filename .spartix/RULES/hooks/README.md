# Hook Rules

This directory contains rules that govern hook behavior, trigger conditions, and enforcement policies.

## Purpose
Hook rules define additional constraints on how hooks operate. For example, a rule might promote an optional hook to mandatory for specific task types, or define custom trigger conditions for hooks in certain domains.

## Loading Order
Hook rules are loaded at priority level 6 by SRL during session initialization.

## Format
Each rule file is a Markdown document with Rule ID, target hook(s), constraint description, and enforcement behavior.

Place your hook-specific rules here as `.md` files.
