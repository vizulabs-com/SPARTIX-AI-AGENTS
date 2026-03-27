# Custom Skills Ecosystem

Custom skills follow the same format as built-in skills. Place custom skill `.md` files and optional `.json` metadata files in this directory. CO discovers and validates custom skills during session initialization by reading `custom-skill-index.json`.

## Creating a Custom Skill

1. Create a `.md` file describing the skill (name, description, parameters, outputs, prerequisites, approved categories)
2. Optionally create a companion `.json` metadata file for machine-readable discovery
3. Update `custom-skill-index.json` to register the skill
4. CO will discover and validate the skill at next session start
