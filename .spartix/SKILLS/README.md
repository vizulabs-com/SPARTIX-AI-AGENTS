# Skills Ecosystem

## What Is a Skill?

A skill is a reusable, documented capability that specialist agents can invoke during task execution. Skills are discrete, well-defined operations that can be shared across multiple agents. Unlike agents, skills do not have identity, purpose, or decision-making authority. Unlike hooks, skills are invoked intentionally by agents rather than triggered automatically by events.

## How Skills Differ from Agents

| Aspect | Agent | Skill |
|--------|-------|-------|
| Has identity and purpose | Yes | No |
| Makes decisions | Yes | No |
| Receives task packets | Yes | No |
| Returns completion reports | Yes | No |
| Is assigned by CO | Yes | No |
| Is invoked by agents during execution | No | Yes |
| Is reusable across agents | N/A | Yes |

## How Skills Differ from Hooks

| Aspect | Skill | Hook |
|--------|-------|------|
| Invoked intentionally | Yes | No |
| Triggered by events | No | Yes |
| Agent chooses to use it | Yes | No |
| Mandatory enforcement possible | No | Yes |
| Used for process governance | No | Yes |

## Skill Structure

Each skill has:
- **Name**: Unique identifier
- **Description**: What the skill does
- **Parameters**: What inputs it accepts
- **Outputs**: What it produces
- **Prerequisites**: What must be true before use
- **Approved For**: Which agent categories may use it

## Skill Documentation Format (.md)

Each skill has a Markdown file describing its purpose, usage, parameters, and examples.

## Skill Metadata Format (.json)

Each skill may have a companion JSON metadata file for machine-readable discovery:

```json
{
  "name": "skill-name",
  "version": "1.0.0",
  "description": "What this skill does",
  "parameters": [...],
  "outputs": [...],
  "prerequisites": [...],
  "approvedCategories": [...],
  "tags": [...]
}
```

## How CO and Agents Discover Skills

1. CO reads `SKILLS/skill-index.json` for built-in skills
2. CO reads `custom-skills/custom-skill-index.json` for custom skills
3. CO builds a skill availability map
4. CO includes approved skills in each task packet
5. Specialist agents check the task packet for their approved skills
6. Agents invoke skills during execution as needed

## When Skills Should Be Markdown

- Skill documentation and usage guides are always `.md`
- Human-readable descriptions and examples are `.md`

## When Skills May Include JSON Metadata

- Machine-readable discovery indexes are `.json`
- Parameter schemas are `.json`
- Skill dependency declarations are `.json`

## Custom Skills

Custom skills follow the same format as built-in skills and are placed in `custom-skills/`. They are discovered and validated by CO during session initialization.
