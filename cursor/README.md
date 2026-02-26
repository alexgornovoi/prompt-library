# Cursor Rules

Cursor-specific rules and agents. Symlink into your project to use.

Reference: [Rules | Cursor Docs](https://cursor.com/docs/context/rules)

## Setup

From your project root:

```bash
ln -s ~/path/to/prompt-library/cursor .cursor
```

All rules in `cursor/rules/` will be active, and they stay synced when you `git pull` the library.

## Project rules

Project rules live in `.cursor/rules` as markdown files and are version-controlled. They provide persistent, reusable context at the prompt level.

Use `.md` or `.mdc` extensions. Use `.mdc` with frontmatter for `description`, `globs`, and `alwaysApply` to control when rules are applied.

```bash
.cursor/rules/
  style_guide.mdc       # Rule with frontmatter
  api-guidelines.md     # Simple markdown rule
  global/               # Always-on rules
  python/               # File-specific rules
  task/                 # Task agents (invoke manually)
```

## Rule types

Configure how a rule is applied via frontmatter:

| Type | Frontmatter | Behavior |
|------|-------------|----------|
| Always Apply | `alwaysApply: true` | Apply to every chat session |
| Apply Intelligently | `alwaysApply: false` + `description` | Agent decides relevance from description |
| Apply to Specific Files | `globs: "**/*.py"` | When file matches the pattern |
| Apply Manually | `alwaysApply: false`, no globs | When @-mentioned in chat (e.g., `@cleanup`) |

## Rule anatomy

```markdown
---
description: "Standards for frontend components and API validation"
globs: "**/*.tsx"
alwaysApply: false
---

...rule content in markdown
```

- **description** – Used for Apply Intelligently; helps Agent decide relevance.
- **globs** – File patterns for Apply to Specific Files. Multiple patterns: `"**/*.ts,**/*.tsx"`.
- **alwaysApply** – `true` = every chat; `false` = intelligently, by file, or manually.

Reference files in rules with `@filename.ts` to include them in context.

## Rule semantics: hints vs strict constraints

- **Without run:** The AI treats rules as hints or contextual knowledge about your style. It may follow them but not always (statistical probability).
- **With run:** Use `run:` to mark a strict constraint—a command or action that must be followed precisely. Example: `run: npm run lint before committing`.

## Glob examples

| Pattern | Matches |
|---------|---------|
| `*` | All files in current directory |
| `**` or `**/*` | All files in all directories |
| `*.py` | All `.py` in current directory |
| `**/*.py` | All `.py` recursively |
| `src/*.py` | `src/foo.py`, `src/bar.py` (not `src/foo/bar.py`) |
| `src/**/*.py` | All `.py` in `src/` recursively |

## Rule precedence

1. Team Rules (dashboard)
2. Project Rules (`.cursor/rules/`)
3. User Rules (global settings)
4. Legacy `.cursorrules`

## Best practices

Good rules are focused, actionable, and scoped.

- Keep rules under 500 lines
- Split large rules into multiple, composable rules
- Provide concrete examples or referenced files
- Avoid vague guidance. Write rules like clear internal docs
- Reuse rules when repeating prompts in chat
- Reference files instead of copying their contents—this keeps rules short and prevents them from becoming stale as code changes

### What to avoid

- **Copying entire style guides:** Use a linter instead. Agent already knows common style conventions.
- **Documenting every possible command:** Agent knows common tools like npm, git, and pytest.
- **Adding instructions for edge cases that rarely apply:** Keep rules focused on patterns you use frequently.
- **Duplicating what's already in your codebase:** Point to canonical examples instead of copying code.

## AGENTS.md

Plain markdown alternative to `.cursor/rules`. No frontmatter or metadata. Place in project root or subdirectories; nested files combine with parents, with more specific instructions taking precedence.

## Structure (this library)

| Folder | Purpose |
|--------|---------|
| global/ | Always-on (style, naming, whitespace) |
| python/ | File-specific (`**/*.py`) |
| task/ | Task agents (invoke as needed via @mention) |

Add more language folders (e.g., `javascript/`, `rust/`) with `.mdc` files using `globs` for file patterns.
