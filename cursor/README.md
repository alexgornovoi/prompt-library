# Cursor Rules

Cursor-specific rules and agents. Symlink into your project to use.

## Setup

From your project root:

```bash
ln -s ~/path/to/prompt-library/cursor .cursor
```

All rules in `cursor/rules/` will be active, and they stay synced when you `git pull` the library.

## Structure

```
cursor/
└── rules/
    ├── global/
    │   └── style_guide.mdc   # snake_case, whitespace, always-on
    ├── python/
    │   └── python_patterns.mdc   # General Python (*.py)
    └── task/
        ├── cleanup.md        # Clean & Streamline agent
        ├── omscs_study.md    # Explain CS concepts
        └── docs_generator.md # Documentation agent
```

## Rule Types

| Folder   | Purpose                               |
|----------|----------------------------------------|
| global/  | Always-on (naming, whitespace, style) |
| python/  | File-specific (`**/*.py`)             |
| task/    | Task agents (invoke as needed)        |

Add more language folders as needed (e.g., `javascript/`, `rust/`) with `.mdc` files using `globs` for file patterns.
