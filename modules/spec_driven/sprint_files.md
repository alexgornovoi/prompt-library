# Sprint files

Rules for creating, maintaining, and completing sprint files within the spec-driven workflow.

## File naming

Sprint files live at `docs/M<N>_<NAME>.md` where `<N>` is a sequential number and `<NAME>` is a short uppercase descriptor (e.g. `docs/M1_CORE_LOOP.md`, `docs/M2_GRAPH_RAG.md`).

## Required sections

Every sprint file contains:

- **Checklist** — each work item as a markdown checkbox (`- [ ]` / `- [x]`).
- **Acceptance criteria** — what "done" looks like for the sprint as a whole.
- **`## Sprint Notes`** — filled in at completion (see below). Leave this section empty or absent until the sprint is done.

## Checklist discipline

- Mark items `[x]` only when done. Partial work stays unchecked with a short note on status.
- If implementation diverges from the written spec, update the spec or add an explicit **`## Deviations`** note in the sprint file — do not let plan and code drift silently apart.
- Do not remove or rewrite checklist items to hide original intent; add notes alongside them instead.

## Completion

When all checklist items are done (or the sprint is otherwise closed), add a **`## Sprint Notes`** section covering:

- What was harder than expected.
- Which spec sections or assumptions were wrong.
- Unresolved issues or risks that carry forward.
- What the next sprint needs to know before starting.

## Lifecycle

- **Create** a new sprint file when scope is large enough to warrant its own checklist and acceptance criteria.
- **Handoff**: `## Sprint Notes` in the finishing sprint is the bridge to the next one. Unresolved issues, changed assumptions, and open risks carry forward explicitly — do not rely on memory.
- **Preserve**: old sprint files are kept as-is after completion. They are the historical record of what was planned, what changed, and what was learned.

## Architecture updates

- Scope work to the current sprint file. If you must reach outside scope, treat it as a decision point.
- When a sprint changes boundaries, invariants, or major flows, update `docs/ARCHITECTURE.md` in the same change set.
- When a decision changes architectural truth, reflect it in both `## Resolved Decisions` in `docs/ATTENTION.md` and in `docs/ARCHITECTURE.md`.
