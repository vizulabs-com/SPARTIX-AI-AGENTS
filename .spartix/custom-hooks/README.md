# Custom Hooks Ecosystem

Custom hooks follow the same format as built-in hooks. Place custom hook `.md` files and optional `.json` metadata files in this directory. CO discovers and validates custom hooks during session initialization by reading `custom-hook-index.json`.

## Creating a Custom Hook

1. Create a `.md` file describing the hook (name, type, trigger conditions, behavior, enforcement)
2. Optionally create a companion `.json` metadata file for machine-readable registration
3. Update `custom-hook-index.json` to register the hook
4. CO will discover and validate the hook at next session start

## Hook Types
- `pre-action` — fires before specialist begins work
- `mid-process` — fires during execution at checkpoints
- `post-action` — fires after specialist completes
- `global` — always active regardless of task
