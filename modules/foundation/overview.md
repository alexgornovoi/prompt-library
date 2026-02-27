# Prompt Library Overview

Reusable instructions for coding assistants, organized by concern instead of tool.

## Collections

- `foundation/` - shared orientation and operating model
- `standards/` - coding style and naming conventions
- `languages/` - language-specific guidance
- `tasks/` - reusable task agents
- `integrations/` - platform setup notes when needed

## Usage

Compose modules by scope:

- Include `foundation.*` and `standards.*` as baseline guidance.
- Add language modules only for stacks in the repo.
- Invoke task modules when doing scoped workflows (setup, docs, cleanup).

This keeps rules portable across Cursor, Copilot, Codex, and other agents.
