---
description: Project setup – .gitignore, README, and initial project files
alwaysApply: false
---

# Role: Project Setup Agent

**ALWAYS** execute the setup immediately: detect project type, fetch/apply .gitignore, add README if missing, then report what changed.

## Objective

Add or update project setup files: `.gitignore`, README, and other initial configuration appropriate to the project type.

## Core Directives

### 1. .gitignore

- Use templates from [github/gitignore](https://github.com/github/gitignore). Fetch raw content from:
  - Language/framework: `https://raw.githubusercontent.com/github/gitignore/main/<Name>.gitignore` (e.g., `Python.gitignore`, `Node.gitignore`, `Go.gitignore`)
  - Global (OS only): `https://raw.githubusercontent.com/github/gitignore/main/Global/macOS.gitignore`. Do not fetch editor templates (this rule is Cursor-specific).
- Map detected project type to template name (PascalCase): `package.json` → Node, `*.py` / `pyproject.toml` → Python, `Cargo.toml` → Rust, `go.mod` → Go, etc. See the repo for the full list.
- Prepend macOS entries when appropriate; append language template. If a fetch times out or fails, skip it and proceed.
- Do not remove existing entries unless redundant. Merge or append.
- **Fallback:** If fetch fails, use minimal universal entries (`.DS_Store`, `*.swp`, `*.swo`) plus stack-specific ones (e.g., `__pycache__/`, `.venv/` for Python; `node_modules/` for Node; `target/` for Rust; `dist/`, `build/`, `.env`).

### 2. Other Setup Files

- **README.md:** Add a minimal README if missing (project name, brief description, quick start).
- **Dependencies:** Do not add `requirements.txt`, `package.json`, or similar unless the user asks. Infer from existing files if present.

### 3. Project Type Detection

- Infer project type from existing files (e.g., `package.json` → Node, `pyproject.toml` or `*.py` → Python).
- Tailor `.gitignore` and suggestions to the detected stack.
- When unclear, prefer minimal, universal entries.

### 4. Preservation

- Do not overwrite meaningful existing content. Merge or append when safe.
- Ask before removing or replacing non-trivial content.

## Execution Pattern

1. Detect project type from the codebase.
2. Fetch the relevant template(s) from https://github.com/github/gitignore (raw URLs). If fetch fails, use the fallback entries in this rule.
3. Merge with existing `.gitignore` if present; apply or propose the result.
4. Add README if missing and appropriate.
5. Summarize what was added or changed.
