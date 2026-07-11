# Technical Requirements Document
## [Project Name]

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

### Modes / Features

| Feature | Status | Purpose |
|---------|--------|---------|
| **Feature A** | v1 | … |
| **Feature B** | deferred | … |

---

## 2. Architecture

<!-- High-level diagram or prose description.
     Include the key constraint that drove this choice (e.g. "local files → can't use cloud storage").
     Name what is explicitly NOT used and why. -->

```
Layer A
    ↕
Layer B
    ├── Component 1
    └── Component 2
```

### Key design decisions

<!-- One paragraph per non-obvious decision. Format:
     Decision: what was chosen.
     Why: the constraint or tradeoff that made this the right call.
     Not: what was rejected and why. -->

---

## 3. Data Model

<!-- Full schema. Every table, every column, types, constraints, foreign keys.
     This is the contract — the API and pipeline are derived from it. -->

```sql
table_name (
  id          INTEGER PRIMARY KEY,
  field       TEXT NOT NULL,
  ...
)
```

---

## 4. API Endpoints

<!-- Skip this section for CLI tools or libraries — only needed for webapps/services.
     For each endpoint: method, path, request body (if any), response shape.
     Keep it concise — implementation details go in PROMPT.md. -->

```
GET  /api/resource            → list
GET  /api/resource/:id        → single item
POST /api/resource/:id/action → {field: value}
```

---

## 5. UX / User Flows

<!-- Skip this section for CLI tools or libraries — only needed for webapps.
     Key screens and the state transitions between them.
     ASCII wireframes are fine. Describe what the user sees and does, not how it's implemented. -->

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

<!-- Unresolved decisions. Resolve all of these before writing PROMPT.md.
     Format: Question → Decision (or "TBD") -->

| # | Question | Decision |
|---|----------|----------|
| 1 | … | … |

---

## 9. Out of Scope (v1)

<!-- Explicit list of things NOT being built. Prevents scope creep during ralph-loop. -->

- …
- …
