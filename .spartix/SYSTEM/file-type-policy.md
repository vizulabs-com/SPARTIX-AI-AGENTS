# File Type Policy

This document defines which folders use `.md`, `.json`, or mixed formats throughout the `.spartix` system.

## Markdown-Primary Folders (.md)

These folders primarily contain Markdown files for human-readable definitions, documentation, and governance:

| Folder | Content Type | Format |
|--------|-------------|--------|
| `AGENTS/**/*.md` | Built-in agent definitions | `.md` only |
| `custom-agents/**/*.md` | Custom agent definitions | `.md` only |
| `SKILLS/*.md` | Skill documentation and definitions | `.md` primary |
| `custom-skills/*.md` | Custom skill documentation | `.md` primary |
| `HOOKS/*.md` | Hook documentation and definitions | `.md` primary |
| `custom-hooks/*.md` | Custom hook documentation | `.md` primary |
| `RULES/**/*.md` | Rule definitions and documentation | `.md` primary |
| `WIKI/**/*.md` | Wiki pages and project history | `.md` only |
| `SYSTEM/*.md` | System architecture documentation | `.md` only |
| `WORKFLOWS/*.md` | Workflow definitions | `.md` only |
| `DIAGRAMS/*.md` | Diagram documentation | `.md` only |
| `PACKETS/*.md` | Packet and report templates | `.md` primary |

## JSON-Primary or Mixed Folders (.json or .md + .json)

These folders may contain JSON files for machine-readable configuration, registries, and metadata:

| Folder | Content Type | Format | Reason for JSON |
|--------|-------------|--------|-----------------|
| `SKILLS/` | Skill metadata and registry | `.json` alongside `.md` | Machine-readable skill discovery, parameter schemas, and dependency declarations |
| `custom-skills/` | Custom skill metadata | `.json` alongside `.md` | Same as SKILLS — enables automated discovery and validation |
| `HOOKS/` | Hook metadata and trigger config | `.json` alongside `.md` | Machine-readable trigger conditions, event bindings, and execution parameters |
| `custom-hooks/` | Custom hook metadata | `.json` alongside `.md` | Same as HOOKS — enables automated trigger registration |
| `RULES/` | Rule priority maps and metadata | `.json` alongside `.md` | Machine-readable priority ordering, conflict resolution maps, and override chains |
| `PACKETS/` | Packet schemas | `.json` alongside `.md` | Machine-readable packet validation schemas for structured data exchange |
| `SYSTEM/` | Registry and index files | `.json` alongside `.md` | Agent registry, skill index, hook index for automated discovery |

## When to Use JSON Instead of Markdown

JSON is used when:

1. **Machine-readable discovery is required**: Agent registries, skill indexes, and hook indexes must be parseable by the orchestrator without natural language processing.
2. **Validation schemas are needed**: Packet definitions require JSON Schema for structural validation of task packets, completion reports, and wiki update packets.
3. **Priority ordering must be unambiguous**: Rule priority maps use JSON to define exact numeric ordering and override chains.
4. **Metadata must be structured**: Skill parameters, hook trigger conditions, and agent capabilities need structured key-value representation.
5. **Configuration is runtime-dependent**: Session rules, workflow state, and visibility status models use JSON for runtime state management.

## When to Use Markdown Instead of JSON

Markdown is used when:

1. **Human readability is the primary goal**: Agent definitions, governance documents, and wiki pages are written for human consumption.
2. **Rich formatting is needed**: Descriptions, instructions, and documentation benefit from headers, lists, and emphasis.
3. **The content is primarily instructional**: Agent identity, purpose, rules, and responsibilities are best expressed in natural language.
4. **Version control diffing matters**: Markdown diffs are more readable than JSON diffs for documentation changes.

## Registry and Index Files

The following JSON files serve as machine-readable indexes:

| File | Location | Purpose |
|------|----------|---------|
| `agent-registry.json` | `SYSTEM/` | Master index of all built-in agents with paths, categories, and capabilities |
| `custom-agent-registry.json` | `SYSTEM/` | Index of discovered and validated custom agents |
| `skill-index.json` | `SKILLS/` | Index of all built-in skills with metadata |
| `custom-skill-index.json` | `custom-skills/` | Index of custom skills |
| `hook-index.json` | `HOOKS/` | Index of all built-in hooks with trigger conditions |
| `custom-hook-index.json` | `custom-hooks/` | Index of custom hooks |
| `rule-priority-map.json` | `RULES/` | Master rule priority ordering and conflict resolution |
| `workflow-state.json` | `SYSTEM/` | Current workflow state model |
| `visibility-status.json` | `SYSTEM/` | User-visible status model configuration |
