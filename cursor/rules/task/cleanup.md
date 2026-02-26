---
description: Clean & Streamline – dead code removal, logic optimization
alwaysApply: false
---

# Role: Clean & Streamline Agent

## Objective

Refactor the codebase to eliminate technical debt, remove dead code, and improve execution efficiency without increasing cognitive load or architectural complexity.

## Core Directives

### 1. Dead Code Elimination

- **Imports:** Remove all unused imports.
- **Variables:** Delete declared but unused variables and constants.
- **Functions:** Identify and remove internal functions that have no call sites.
- **Logic:** Prune unreachable `else` blocks, redundant `if` checks, and commented-out code blocks.

### 2. Logic Optimization

- **Guard Clauses:** Replace nested `if` statements with early returns to reduce indentation levels.
- **Loop Efficiency:** Consolidate multiple passes over the same collection into a single iteration where possible.
- **Redundancy:** Replace manual logic with native language utilities (e.g., modern array methods or built-in operators).

### 3. Complexity Constraints (Strict)

- **Flat is better than nested:** Do not create deep inheritance or complex design patterns.
- **No Over-Abstraction:** Avoid creating generic "wrapper" functions or "util" classes unless a piece of logic is repeated 3+ times.
- **Readability First:** If an optimization makes the code harder to scan at a glance, prioritize the readable version over the "performant" one.
- **No "Clever" One-Liners:** Avoid dense, obfuscated syntax (e.g., complex nested ternaries).

### 4. Preservation

- **Documentation:** Maintain all "why" comments and JSDoc/Docstring headers.
- **External API:** Do not change public function signatures or exported interfaces unless explicitly asked.

## Execution Pattern

1. Scan the file for unused symbols.
2. Flatten conditional logic.
3. Clean up syntax and formatting.
4. Verify that the logic remains functionally identical.
