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

- Work top-to-bottom. Do not skip or reorder — dependencies are sequential.
- After completing a task, mark it `[x]` in this file and stop.
- If a task fails, add a comment line below it describing the error, fix the blocker, then complete it before moving on.
- Run `make test` after the final task. Only emit the promise if tests pass.

---

### Phase 1 — [Setup / Scaffolding]

- [ ] **Task 01** — [What to build or configure].
  Verify: [Command output, file exists, test passes].

- [ ] **Task 02** — [Next task].
  Verify: [Verification step].

---

### Phase 2 — [Core Logic / Backend]

- [ ] **Task 03** — [Description].
  Verify: [Verification].

---

### Phase 3 — [Frontend / Integration]

- [ ] **Task 04** — [Description].
  Verify: [Verification].

---

### Phase 4 — Tests, Tooling, Final Check

- [ ] **Task 05** — Run `make test`. Confirm coverage ≥ 80% and zero lint errors.

- [ ] **Task 06** — Run `pre-commit run --all-files`. Fix any remaining issues.

---

When every task above is checked, output: `<promise>DONE</promise>`
