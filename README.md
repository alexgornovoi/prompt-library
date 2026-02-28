# Prompt Library

A repo for reusable prompts, rules, and agents organized by concern (tool-agnostic first).

## Module Collections

- **foundation/** - Shared baseline guidance.
- **standards/** - Naming and style conventions.
- **languages/** - Language-specific patterns.
- **tasks/** - Task-invoked agents (setup, docs, cleanup).
- **integrations/** - Platform integration notes.

## Use with rulepack

Use this prompt-library from git:

```bash
rulepack deps add https://github.com/alexgornovoi/prompt-library --export default --ref main
rulepack deps install
rulepack build
```

Use this prompt-library locally (from the `rule-pack` repo root):

```bash
rulepack deps add --local ./prompt-library --export default
rulepack deps install
rulepack build
```

Use only the core export:

```bash
rulepack deps add --local ./prompt-library --export core
rulepack deps install
rulepack build
```

Use only Python + shared repo standards:

```bash
rulepack deps add --local ./prompt-library --export python
rulepack deps install
rulepack build
```

Exports in this repo:

- `default`: all modules
- `core`: `foundation.*`, `standards.*`, `languages.*`
- `python`: `foundation.*`, `standards.*`, `languages.python.*`

If `--export` is omitted, `default` is used.
