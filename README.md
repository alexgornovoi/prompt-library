# Prompt Library

A repo for reusable prompts, rules, and agents organized by concern (tool-agnostic first).

## Module Collections

- **foundation/** - Shared baseline guidance.
- **standards/** - Naming and style conventions.
- **languages/** - Language-specific patterns.
- **tasks/** - Task-invoked agents (setup, docs, cleanup).
- **integrations/** - Platform integration notes.

## Install with rulepack

Use this repo as a Rule Pack source dependency:

```bash
rulepack add <git-url-to-this-repo> --export default --ref <tag-or-commit>
rulepack install
rulepack build
```

Named exports:

- `default` - all modules
- `core` - `foundation.*`, `standards.*`, `languages.*`
- `standards`, `tasks`, `integrations`, etc. - implicit folder exports (no explicit export needed)
