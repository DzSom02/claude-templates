# Claude Templates

Project templates for working with Claude Code. Each template includes programming guidelines,
tooling configuration, and a working methodology built around TRD-first design and the Ralph Loop.

## Templates

| Template | Stack | Description |
|----------|-------|-------------|
| [`python/`](python/) | Python 3.10+ | FastAPI / CLI projects with ruff, mypy, pytest, pre-commit |

---

## How to start a new project

### 1. Copy the template

```bash
cp -r path/to/claude-templates/python ~/projects/my-new-project
cd ~/projects/my-new-project
git init
git add -A
git commit -m "chore: scaffold from claude-templates/python"
```

### 2. Customise the scaffold

| File | What to change |
|------|---------------|
| `pyproject.toml` | Replace `known-first-party = ["app"]` with your package name |
| `Makefile` | Update `dev` entry point and `migrate` command for your stack |
| `CLAUDE.md` | Fill in the **Architecture** section |
| `.pre-commit-config.yaml` | Add stubs packages to the mypy hook if needed |

### 3. Write the TRD

Fill in `TRD.md` before writing any code. The document has two parts:

**Design sections (top):**
- Product overview and v1 scope
- Architecture and key design decisions (with rationale)
- Data model / schema
- API endpoints *(skip for CLI/library projects)*
- UX flows *(skip for CLI/library projects)*
- Tech stack with rationale
- Open questions — **resolve all before writing any tasks**
- Out of scope for v1

**Implementation tasks (bottom):** an ordered checklist of concrete, verifiable tasks grouped into phases.
Tasks reference the design sections above directly. Key rules baked in:
- Top-to-bottom, no skipping — dependencies are sequential.
- After each task, Claude marks `[x]` in the file and stops the iteration.
- Each task has a **Verify** step.
- A task failure is noted as a comment in-place, then fixed before moving on.
- Final task runs `make test` and `pre-commit run --all-files`.
- Last line: `When every task is checked, output: <promise>DONE</promise>`

Revisions go in new files: `TRD_v2.md`, `TRD_v3.md`. Never overwrite history.

### 4. Run the Ralph Loop

```
/ralph-loop:ralph-loop "Read TRD.md and follow all tasks in the Implementation Tasks section" --completion-promise "DONE"
```

Claude reads the full TRD for context, works on the next unchecked task, marks it `[x]`, then stops.
The next iteration continues until the completion promise is emitted.

---

## What's in the Python template

```
python/
├── CLAUDE.md                  # Commands, architecture placeholder, methodology, programming guidelines
├── TRD.md                     # Design + implementation task list (single source of truth)
├── Makefile                   # dev, test, lint, build, migrate
├── pyproject.toml             # ruff + mypy config
├── .pre-commit-config.yaml    # ruff, mypy, pytest hooks
├── .gitignore
└── .claude/
    └── settings.local.json    # Auto-allowed Claude Code permissions
```

### Programming guidelines summary

The full guidelines are in [`python/CLAUDE.md`](python/CLAUDE.md). Key points:

**Classes** — one responsibility per class, stated in the docstring as what it *owns*.
State lives in `__init__`. Public interface is minimal; internals use `_` prefix.

**Methods** — one thing per method, ≤15 lines. Return early on guard conditions.
Extract private helpers to name ideas, even if called once.

**Docstrings** — every public class and method gets one. Class: one line stating ownership.
Method: one-line summary + Args/Returns (Google style) only when the signature isn't self-explanatory.
Private methods: no docstring.

**Testing** — one assertion per test. Name: `test_<action>_<expected_outcome>`.
Shared setup in `conftest.py`. Test behaviour, not implementation. No mocking the DB.
E2E tests in `tests/test_e2e.py`. Coverage threshold: 80%.

**Comments** — default none. Add only when WHY is non-obvious.

**Error handling** — validate only at system boundaries. No fallbacks for unreachable paths.

**General** — pure logic must be importable without starting the app.
No premature abstractions. No feature flags. No OWASP top 10 vulnerabilities.
