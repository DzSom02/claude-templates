# [Project / Sprint Name] — Build Prompt

Read `TRD.md` before starting. Complete every task below in order.
Mark each `[x]` when done. When all tasks are checked, output `<promise>DONE</promise>`.

## Rules

- Work top-to-bottom. Do not skip or reorder tasks — dependencies flow sequentially.
- After completing a task, edit this file to replace `- [ ]` with `- [x]`, then stop for the iteration.
- If a task fails (missing dependency, test error, etc.), add a comment line below the task describing
  the error, fix the blocker, then complete the task before moving on.
- Run `make test` after the final task. Only emit the promise if tests pass.

---

## Phase 1 — [Setup / Scaffolding]

- [ ] **Task 01** — [What to build or configure].
  Verify: [How to confirm it's done — command output, file exists, test passes].

- [ ] **Task 02** — [Next task].
  Verify: [Verification step].

---

## Phase 2 — [Core Logic / Backend]

- [ ] **Task 03** — [Description].
  Verify: [Verification].

---

## Phase 3 — [Frontend / Integration]

- [ ] **Task 04** — [Description].
  Verify: [Verification].

---

## Phase 4 — [Tests, Tooling, Final Check]

- [ ] **Task 05** — Run `make test`. Confirm coverage ≥ 80% and zero lint errors.

- [ ] **Task 06** — Run `pre-commit run --all-files`. Fix any remaining issues.

---

When every task above is checked, output: `<promise>DONE</promise>`
