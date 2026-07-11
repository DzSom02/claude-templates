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

### 1. TRD first — no code before the design is agreed

Before writing any code, write `TRD.md` (use the template). Cover:
product overview, architecture, data model, API, UX flows, tech stack, open questions, out of scope.

Resolve all open questions before moving on. The TRD is the contract — the PROMPT.md is derived from it.

### 2. PROMPT.md — the ralph-loop task list

Once TRD is agreed, translate it into `PROMPT.md`: an ordered checklist of concrete, verifiable tasks
grouped into phases. Rules embedded in the prompt:
- Tasks run top-to-bottom (dependencies flow sequentially).
- Each task is checked off (`[x]`) before the next begins.
- Each task has a **Verify** step (command output, file existence, test pass).
- Final task always runs `make test` and `pre-commit run --all-files`.
- Prompt ends with: `When every task is checked, output: <promise>DONE</promise>`

### 3. Run the ralph-loop

```
/ralph-loop "Read PROMPT.md and follow all tasks in order" --completion-promise "DONE"
```

Claude reads PROMPT.md, works on the next unchecked task, checks it off (`[x]`) in the file, then stops.
The next iteration sees the updated file and picks up from where it left off.
Continues until `<promise>DONE</promise>` is emitted.

### 4. Subsequent sprints

Never overwrite PROMPT.md. Create `PROMPT_v2.md`, `PROMPT_v3.md`, etc. for new sprints.
Each sprint gets its own TRD revision if the architecture changes (TRD_v2.md, etc.).
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
