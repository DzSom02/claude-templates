# CLAUDE.md

This file provides guidance to Claude Code when working in this repository.

## Commands

```bash
# Run the app
make dev

# Run all tests (with coverage)
make test

# Run a single test file
python3 -m pytest tests/test_foo.py -v

# Lint and format
make lint

# Run pre-commit hooks manually
pre-commit run --all-files

# Install pre-commit hooks (once, after cloning)
pre-commit install
```

## Architecture

<!-- Describe the project here:
- What does this project do?
- What are the main layers/modules?
- What must be preserved? (e.g. "no framework imports in the engine layer")
- What is the entry point?
-->

---

## Working Methodology

### 1. Write the TRD — no code before the design is agreed

Fill in `TRD.md` (use the template). The document has two parts:

**Design sections (top):** product overview, architecture, data model, API, UX flows, tech stack.
Resolve all open questions before moving to the tasks.

**Implementation tasks (bottom):** an ordered checklist of concrete, verifiable tasks grouped into phases.
Tasks reference the design sections above directly — no separate prompt file needed.
- **Phases complete in order** — phase 2 can't start until phase 1 is fully checked.
- **Within a phase, respect dependencies** — default top-to-bottom; mark tasks `(independent)` or `(requires Task N)` when relevant.
- **Commit at the end of each phase** — last task in every phase runs `make test` and commits if green.

### 2. Run the ralph-loop

```
/ralph-loop:ralph-loop "Read TRD.md and follow all tasks in the Implementation Tasks section" --completion-promise "DONE"
```

Claude reads the full TRD for context, works on the next unchecked task, marks it `[x]` in the file,
then stops. The next iteration sees the updated file and continues until `<promise>DONE</promise>`.

### 3. Subsequent sprints

Never overwrite `TRD.md`. Create `TRD_v2.md`, `TRD_v3.md`, etc. for new sprints — each with its own
updated design sections and a fresh task list at the bottom.
This preserves the full decision history alongside the code.

---

## Programming Guidelines

### Classes

- Each class has one clearly stated responsibility. The class docstring names what it **owns**, not just what it does:
  `"""Owns scenario traversal: current node, advance, and shard cost checks."""`
- State lives in `__init__`. No attributes added later in other methods.
- Use `@property` / setter pairs only when a state change has a side effect (event emission, clamping). Plain assignment otherwise.
- Subclass only to **extend behaviour**. Never subclass just to share a utility — use composition or a free function instead.
- Keep the public interface minimal. Implementation details get a `_` prefix.

### Methods

- Each method does one thing. If you need "and" to describe it, split it.
- Aim for ≤15 lines. A private helper that names an idea is always worth extracting, even if called once.
- Private helpers (`_log`, `_check_outcome`) are preferred over inline logic inside public methods.
- Return early on guard conditions to keep the happy path unindented.

### Docstrings

- Every public class and every public method gets a docstring.
- **Class docstring:** one line — what it owns or is responsible for. Note observable side effects (events emitted, etc.) in a second paragraph if needed.
- **Method docstring:** one-line summary. Add `Args` / `Returns` (Google style) only when the signature alone isn't clear.
- **Private methods:** no docstring.
- Never describe HOW — only WHAT. No multi-paragraph explanations of the implementation.

### Testing

- One assertion per test as a default. Related attribute checks on the same object are fine together.
- Test names follow `test_<action>_<expected_outcome>`: `test_player_attack_deals_damage`.
- Use `conftest.py` for shared fixtures. Never repeat construction in individual tests.
- Test **behaviour**, not implementation. Don't assert on private state or internal method calls.
- Unit tests for logic; integration tests for boundaries (API endpoints, DB, file I/O).
- Do not mock the database or filesystem — use real fixtures and a test DB.
- E2E tests go in `tests/test_e2e.py`. Run them after every code change before marking work done.
- Coverage threshold: 80%, enforced by `make test`.

### Comments

- Default: no comments.
- Add one only when WHY is non-obvious: a workaround, a hidden constraint, a subtle invariant, or behaviour that would surprise a reader.
- Never explain what the code does — names do that.

### Error handling

- Validate only at system boundaries: user input, external APIs, file I/O.
- Don't add fallbacks for paths that cannot be reached.
- Prefer raising a clear exception over silently returning a default.

### General

- Separate pure logic from framework / UI code. Logic must be importable and testable without starting the app.
- No premature abstractions. Three similar things before extracting a pattern.
- No feature flags or backwards-compat shims — just change the code.
- No command injection, SQL injection, XSS, or other OWASP top 10 vulnerabilities. Never commit secrets.
