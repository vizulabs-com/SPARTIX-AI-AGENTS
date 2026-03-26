# Coding Conventions

> Standards and practices for all development work on SPARTIX. All contributors must follow these conventions.

---

## Language Standards

### TypeScript
- **Target:** *[e.g., ES2022]*
- **Strict mode:** *[Enabled / Disabled]*
- **Key compiler options:** *[List critical tsconfig settings]*

### General Principles
- Prefer readability over cleverness.
- Write self-documenting code; add comments for "why", not "what".
- Keep functions small and focused on a single responsibility.
- Handle errors explicitly; never swallow exceptions silently.

---

## Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| **Classes** | PascalCase | `UserService`, `FileManager` |
| **Interfaces** | PascalCase (prefixed with I if project convention) | `IDisposable`, `ConfigOptions` |
| **Functions / Methods** | camelCase | `getUserById`, `parseConfig` |
| **Variables / Properties** | camelCase | `userName`, `isActive` |
| **Constants** | UPPER_SNAKE_CASE or camelCase (per context) | `MAX_RETRIES`, `defaultTimeout` |
| **Enums** | PascalCase (members: PascalCase) | `StatusCode.Success` |
| **Files** | *[camelCase / kebab-case / PascalCase -- specify]* | *[example.ts]* |
| **Directories** | *[camelCase / kebab-case -- specify]* | *[user-service/]* |

---

## File Structure

```
src/
	[layer]/
		[feature]/
			[feature].ts              -- Main implementation
			[feature].test.ts         -- Unit tests
			[feature].types.ts        -- Type definitions (if needed)
			[feature].utils.ts        -- Utility functions (if needed)
```

*[Adjust the structure above to match the actual project layout]*

---

## Git Workflow

### Branch Naming
- `feature/[ticket-id]-short-description` -- New features
- `fix/[ticket-id]-short-description` -- Bug fixes
- `refactor/[ticket-id]-short-description` -- Code refactoring
- `docs/short-description` -- Documentation changes
- `chore/short-description` -- Maintenance tasks

### Branching Strategy
*[Describe: trunk-based / GitFlow / GitHub Flow / other]*

### Pull Request Rules
- All changes require a pull request.
- PRs must be reviewed by at least *[N]* reviewer(s).
- All CI checks must pass before merge.
- Squash merge / merge commit / rebase -- *[specify strategy]*.

---

## Code Review Checklist

When reviewing code, verify:

- [ ] Code follows naming conventions and file structure
- [ ] No unnecessary code duplication
- [ ] Error handling is appropriate
- [ ] Tests cover new functionality and edge cases
- [ ] No hardcoded secrets or credentials
- [ ] Performance implications considered
- [ ] Accessibility requirements met (if UI changes)
- [ ] Documentation updated where needed
- [ ] Disposables are properly managed (no leaks)
- [ ] No new lint warnings or errors introduced

---

## Commit Message Format

```
<type>(<scope>): <short summary>

<optional body -- explain what and why, not how>

<optional footer -- breaking changes, issue references>
```

### Types
- `feat` -- New feature
- `fix` -- Bug fix
- `refactor` -- Code restructuring without behavior change
- `docs` -- Documentation only
- `test` -- Adding or updating tests
- `chore` -- Build, tooling, or maintenance
- `perf` -- Performance improvement
- `style` -- Formatting, whitespace (no logic change)

### Examples
```
feat(editor): add syntax highlighting for SPARQL

fix(auth): resolve token refresh race condition

refactor(storage): extract file operations into dedicated service
```

---

## Linting & Formatting

- **Linter:** *[e.g., ESLint]*
- **Formatter:** *[e.g., Prettier -- or "none, use EditorConfig"]*
- **Pre-commit hooks:** *[e.g., Husky + lint-staged]*
- Run `[command]` before committing to check compliance.

---

## Import Ordering

*[Specify the expected import order, e.g.:]*

1. Node.js built-in modules
2. Third-party dependencies
3. Internal modules (by layer: base, platform, editor, workbench)
4. Relative imports

---

*Last updated: YYYY-MM-DD*
*Maintained by Nabil Mansour [Wiki Builder]*
