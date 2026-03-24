# Decision protocol

Rules for surfacing, recording, and resolving decisions within the spec-driven workflow.

## What counts as a decision point

Stop and surface a decision **before** writing code when:

- Two or more reasonable approaches exist with meaningfully different tradeoffs.
- The spec is ambiguous or silent on something that affects design or behavior.
- You are about to assume something that would be hard to reverse.
- The change touches a security boundary, persistence layer, or public contract.
- Work would expand beyond the scope of the current sprint file.
- Choosing one path would foreclose or seriously complicate another.

These are **not** decision points:

- Naming, formatting, or stylistic choices with no architectural consequence.
- Details explicitly resolved in an existing decision or in `docs/BOUNDARIES.md`.
- Trivial implementation choices within an already-decided approach.

## Decision block format

Number decisions sequentially so sprint files and `docs/ATTENTION.md` can cross-reference them. Use **one block per decision**:

```
[DECISION-XX] OPEN — Short title
─────────────────────────────────
Context: Why this matters now.

Option A — name
  Tradeoffs.

Option B — name
  Tradeoffs.

Recommendation: One–two sentences.
Blocks: What cannot proceed until resolved.
Touches: Sprint file, packages, or spec sections affected.
```

When resolved, update the tag to `RESOLVED` and note which option was chosen.

## Approval rules

- Do not implement a chosen option until the user has **explicitly approved** it.
- Do not batch unrelated decisions into one block — one block per decision.
- Do not hide decisions inside implementation detail or commit messages.
- Always state a recommendation; do not dump the problem without analysis.
- After approval, restate the chosen option before coding.
- If the chosen option unlocks further decisions, surface those before proceeding.

## Boundaries promotion

`docs/BOUNDARIES.md` holds confirmed security and correctness constraints as enforceable rules — not narrative history.

- **Create** `docs/BOUNDARIES.md` the first time a decision produces a hard constraint. It does not need to exist on day one.
- **Promote** a decision when it cements a rule that must survive beyond the current session. State the constraint and reference the decision ID (e.g. `DECISION-04`). Do not duplicate the full rationale — `docs/ATTENTION.md` keeps the history.
- **Do not weaken or remove** an existing boundary without surfacing a new decision through the normal protocol.
- **Security-sensitive changes** go into `## Security Decisions` in `docs/ATTENTION.md` and require sign-off **before** implementation. Once confirmed, promote any resulting constraint to `docs/BOUNDARIES.md`.

Safety principles (subprocess hygiene, path confinement, least-privilege defaults, etc.) are standing policy that lives in separate modules or project-level files. This protocol defines how decisions about safety surface, get approved, and become enforceable constraints.
