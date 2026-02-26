# Copilot Prompts

GitHub Copilot custom instructions. Copilot uses files in `.github/` and optional `AGENTS.md` files. Copilot is the agent whether you use it in VS Code, GitHub.com, or elsewhere.

Reference: [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)

## Repository-wide instructions

- Create `.github/copilot-instructions.md` (create the `.github` directory if it doesn't exist).
- Add natural language instructions in Markdown format.
- Whitespace between instructions is ignored.

## Path-specific instructions

- Create `.github/instructions/` (optionally with subdirectories to organize).
- Create files named `NAME.instructions.md` — the filename **must** end with `.instructions.md`.
- Add frontmatter at the start of each file:

```yaml
---
applyTo: "app/models/**/*.rb"
# optionally: excludeAgent: "code-review" or "coding-agent"
---
```

- **applyTo**: Glob syntax. Multiple patterns: `"**/*.ts,**/*.tsx"`.
- **excludeAgent**: Optional. Use `"code-review"` or `"coding-agent"` to restrict which agent reads the file. If omitted, both use the instructions.

### Glob examples

| Pattern | Matches |
|---------|---------|
| `*` | All files in current directory |
| `**` or `**/*` | All files in all directories |
| `*.py` | All `.py` in current directory |
| `**/*.py` | All `.py` recursively |
| `src/*.py` | `src/foo.py`, `src/bar.py` (not `src/foo/bar.py`) |
| `src/**/*.py` | All `.py` in `src/` recursively |
| `**/subdir/**/*.py` | All `.py` in any `subdir` at any depth |

## Agent instructions

- `AGENTS.md` (anywhere in repo) — used by AI agents; nearest file in directory tree wins.

## Prompt Files (Copilot in VS Code)

Stored in `.github/prompts/`. Enable with `"chat.promptFiles": true` in workspace settings. Attach via **Prompt...** in Copilot Chat.

## Contents

- **project_setup.md** – Project setup (gitignore, README). Optionally fetches `VisualStudioCode.gitignore` when the project uses Copilot in VS Code.
