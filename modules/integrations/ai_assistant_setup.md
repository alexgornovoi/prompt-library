# AI Assistant Integration Setup

Guidance for wiring shared instructions into common coding assistants.

## Repository-Level Instruction Files

- Cursor: `.cursor/rules/` (markdown rule files, optional metadata/frontmatter by tool format).
- Copilot: `.github/copilot-instructions.md` and optional `.github/instructions/*.instructions.md`.
- Codex-style agents: project-level rules file as expected by the runner.

## Integration Principles

- Keep canonical guidance in this pack, then render/sync to tool-specific file locations.
- Separate always-on rules from task-invoked rules.
- Use path-scoped targeting only for language/framework-specific guidance.
- Avoid duplicating the same instruction text across tools.

## Operational Notes

- Prefer generated outputs over hand-maintained duplicated files.
- When a tool requires unique metadata (for example glob frontmatter), encode that at render time.
