# Spec-driven development

A repeatable process that ties milestones, decisions, and enforcement together so implementation stays deliberate and traceable.

## Standard file layout

Every project using spec-driven development maintains these living documents under `docs/`:

| File | Role | Living document? |
| --- | --- | --- |
| `docs/ARCHITECTURE.md` | System design: boundaries, invariants, data models, major flows. | Yes — updated whenever implementation changes the design. |
| `docs/ATTENTION.md` | Decision log: open questions, known issues, security decisions, and their resolutions. | Yes — reconciled at every session and sprint boundary. |
| `docs/BOUNDARIES.md` | Confirmed security and correctness constraints, stated as enforceable rules. | Yes — grows as decisions produce hard constraints; entries are never removed without a new decision. |
| `docs/M<N>_<NAME>.md` | Sprint files (e.g. `docs/M1_CORE_LOOP.md`, `docs/M2_GRAPH_RAG.md`). One per milestone. | Yes — checklist updates throughout the sprint; `## Sprint Notes` added at completion. Kept as-is afterward (historical record). |

All four are living documents. They are updated in the normal course of work, not written once and forgotten. If a file does not exist yet, create it the first time the workflow calls for it.

## Session start

At the beginning of every session (or when resuming work):

1. Read the **current sprint file** (`docs/M<N>_<NAME>.md`) to re-establish scope and see what is checked off.
2. Scan **`docs/ATTENTION.md`** for any items still under `## Needs Decision` — do not start work that depends on an unresolved question.
3. Read **`docs/BOUNDARIES.md`** (if it exists) so confirmed constraints are loaded before coding begins.

## Flow

```
Sprint file (what to build)
    ↓
Encounter ambiguity or tradeoff
    ↓
Surface in docs/ATTENTION.md → ## Needs Decision (stop, do not proceed)
    ↓
User confirms choice
    ↓
Move to ## Resolved Decisions in docs/ATTENTION.md
    ↓
If security/correctness boundary → also add to docs/BOUNDARIES.md
    ↓
Mark sprint checklist item [x] · add ## Sprint Notes at completion
```

1. The **sprint file** defines what to build.
2. On **ambiguity or a real tradeoff**, add to `## Needs Decision` in `docs/ATTENTION.md` and **stop** until approved.
3. After confirmation, move the entry to `## Resolved Decisions`.
4. If the decision creates a **security or correctness boundary**, promote it to `docs/BOUNDARIES.md` so future sessions enforce it.
5. **Checklist** and **`## Sprint Notes`** stay accurate through the sprint.
6. When implementation changes system design, update **`docs/ARCHITECTURE.md`** in the same change set.

## Key properties

- **Decisions are explicit and approved before code.** State a recommendation; do **not** treat the recommendation as permission. Approval is required. The codebase reflects deliberate choices, not convenience.

- **History and enforcement are separate.** `docs/ATTENTION.md` records what was decided and why. `docs/BOUNDARIES.md` states what must hold going forward. History can be archived; boundaries stay visible until explicitly revised.

- **Sprint files stay honest.** Checklists reflect completed work, deviations are noted, `## Sprint Notes` captures friction and lessons so the next milestone starts from truth.

- **Issues are logged, not suppressed.** Anything spotted during implementation that is not immediately fixable goes under `## Known Issues` in `docs/ATTENTION.md` with affected area and suggested mitigation.

- **Architecture stays current.** `docs/ARCHITECTURE.md` is updated together with code when boundaries, invariants, or major flows change. Prefer explicit module and layer boundaries over tacit coupling.
