# Prompt Library

A repo for storing reusable prompts, rules, and agents. May include Cursor rules, system prompts, templates, and other prompt formats.

## Cursor rules

To use the Cursor rules in a project, symlink from your project root:

```bash
ln -s ~/path/to/prompt-library/cursor .cursor
```

Rules stay synced when you `git pull`. See [cursor/README.md](cursor/README.md) for layout.

## Structure

- **cursor/** – Cursor rules and agents (symlink as `.cursor` in projects)
- **.cursor/** – Repo instructions for editing this library
- Other prompt collections can be added alongside `cursor/` as needed
