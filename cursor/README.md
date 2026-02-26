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

## AGENTS.md

Plain markdown alternative to `.cursor/rules`. No frontmatter or metadata. Place in project root or subdirectories; nested files combine with parents, with more specific instructions taking precedence.

## Structure (this library)

| Folder | Purpose |
|--------|---------|
| global/ | Always-on (style, naming, whitespace) |
| python/ | File-specific (`**/*.py`) |
| task/ | Task agents (invoke as needed via @mention) |

Add more language folders (e.g., `javascript/`, `rust/`) with `.mdc` files using `globs` for file patterns.
