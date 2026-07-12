# TRD: [Project Name]

**Date:** YYYY-MM-DD
**Revision:** 1

| Rev | Date | Summary |
|-----|------|---------|
| 1 | YYYY-MM-DD | Initial |

---

## 1. Product Overview

<!-- What is this? What problem does it solve? Who is it for?
     Be specific about the user and their context. -->

**v1 scope:** <!-- One sentence on what v1 includes and what is deferred. -->

### Features

| Feature | Status | Purpose |
|---------|--------|---------|
| **Feature A** | v1 | … |
| **Feature B** | deferred | … |

---

## 2. Architecture

<!-- High-level diagram or prose description.
     Include the key constraint that drove this choice.
     Name what is explicitly NOT used and why. -->

```
Layer A
    ↕
Layer B
    ├── Component 1
    └── Component 2
```

### Key design decisions

<!-- One paragraph per non-obvious decision.
     Decision / Why / What was rejected and why. -->

---

## 3. Data Model

<!-- Full schema. Every table, every column, types, constraints, foreign keys.
     This is the contract — the tasks below are derived from it. -->

```sql
table_name (
  id          INTEGER PRIMARY KEY,
  field       TEXT NOT NULL,
  ...
)
```

---

## 4. API Endpoints

<!-- Skip for CLI/library projects.
     Method, path, request body, response shape. -->

```
GET  /api/resource            → list
GET  /api/resource/:id        → single item
POST /api/resource/:id/action → {field: value}
```

---

## 5. UX / User Flows

<!-- Skip for CLI/library projects.
     Key screens and state transitions. ASCII wireframes are fine. -->

---

## 6. Tech Stack

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| **Server** | … | … |
| **Frontend** | … | … |
| **Database** | … | … |
| **Testing** | … | … |

---

## 7. Project Structure

```
project/
├── ...
```

---

## 8. Open Questions

<!-- Resolve ALL of these before writing the tasks below. -->

| # | Question | Decision |
|---|----------|----------|
| 1 | … | … |

---

## 9. Out of Scope (v1)

- …

---

## Implementation Tasks

Read the sections above before starting. Complete every task in order.
After completing a task, edit this file to replace `- [ ]` with `- [x]`, then stop for the iteration.
When all tasks are checked, output `<promise>DONE</promise>`.

### Rules

- **Phases must complete in order** — do not start a phase until all tasks in the previous phase are checked.
- **Within a phase, respect dependencies** — work top-to-bottom by default. Tasks marked `(independent)` can be done in any order. Tasks marked `(requires Task N)` must wait for that task.
- **Commit at the end of each phase** — the last task in every phase runs `make test` and commits. Only commit if tests pass.
- After completing a task, mark it `[x]` in this file and stop.
- If a task fails, add a comment line below it describing the error, fix the blocker, then complete it before moving on.

---

### Phase 1 — [Setup / Scaffolding]

- [ ] **Task 01** — [What to build or configure].
  Verify: [Command output, file exists, test passes].

- [ ] **Task 02** — [Next task].
  Verify: [Verification step].

- [ ] **Task 03** — Invoke the `code-review` skill to review this phase's changes. Focus: class ownership, layer separation, method size, coupling. Apply any high-confidence architectural fixes before continuing.

- [ ] **Task 04** — Run `make test` (and E2E suite if separate). If all pass, commit: `git add -A && git commit -m "Phase 1: [setup description]"`.

---

### Phase 2 — [Core Logic / Backend]

- [ ] **Task 04** — [Description].
  Verify: [Verification].

- [ ] **Task 05** *(independent)* — [Description with no dependency on Task 04].
  Verify: [Verification].

- [ ] **Task 06** *(requires Task 04)* — [Description that builds on Task 04].
  Verify: [Verification].

- [ ] **Task 07** — Invoke the `code-review` skill to review this phase's changes. Focus: class ownership, layer separation, method size, coupling between modules. Apply any high-confidence architectural fixes.

- [ ] **Task 08** — Write E2E tests for this phase's features in `tests/test_e2e.py` (golden path + key failure cases, grouped by `class TestFeatureName:`). Run `make test` (and E2E suite if separate). If all pass, commit: `git add -A && git commit -m "Phase 2: [description]"`.

---

### Phase 3 — [Frontend / Integration]

- [ ] **Task 08** — [Description].
  Verify: [Verification].

- [ ] **Task 09** — Invoke the `code-review` skill to review this phase's changes. Focus: class ownership, layer separation, method size. Apply any high-confidence architectural fixes.

- [ ] **Task 10** — Write E2E tests for this phase's features in `tests/test_e2e.py`. Run `make test` (and E2E suite if separate). If all pass, commit: `git add -A && git commit -m "Phase 3: [description]"`.

---

### Phase 4 — Tests, Tooling, Final Check

- [ ] **Task 10** — Run `pre-commit run --all-files`. Fix any remaining issues.

- [ ] **Task 11** — Run `make test`. Confirm coverage ≥ 80% and zero lint errors. Commit: `git add -A && git commit -m "Phase 4: tests, tooling"`.

---

When every task above is checked, output: `<promise>DONE</promise>`
