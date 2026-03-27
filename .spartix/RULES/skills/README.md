# Skill Rules

This directory contains rules that govern how skills are used, which agents may use which skills, and any constraints on skill invocation.

## Purpose
Skill rules define constraints on skill usage beyond what is specified in the skill metadata. For example, a rule might restrict the `code-generation` skill to only produce code in approved languages, or require the `security-scanning` skill to always scan for OWASP Top 10.

## Loading Order
Skill rules are loaded at priority level 5 by SRL during session initialization.

## Format
Each rule file is a Markdown document with Rule ID, target skill(s), constraint description, and enforcement behavior.

Place your skill-specific rules here as `.md` files.
