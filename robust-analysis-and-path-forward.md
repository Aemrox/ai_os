# Personal OS: Robust Analysis and Path Forward

This document summarizes the current codebase's functional pieces and outlines a more robust architecture and implementation path for building a production-grade system.

## Functional Summary (Current Codebase)

### 1) Workspace Contract and Docs
- `README.md`, `AGENTS.md`, `Knowledge/README.md`, `Tasks/README.md`, and `examples/` define the end-user workflow: backlog capture → triage → task creation → goal-driven focus.
- The system is intentionally lightweight: plain markdown files and a single MCP server.

### 2) Bootstrapping
- `setup.sh` scaffolds `Tasks/`, `Knowledge/`, `BACKLOG.md`, and generates `GOALS.md` via prompts.
- Template files live in `core/templates/`.

### 3) MCP Server (Core Runtime)
- `core/mcp/server.py` exposes tools for:
  - Task CRUD and listing
  - Backlog parsing and clearing
  - Deduplication and ambiguity detection
  - Status summaries and priority limit checks
  - Eval tooling (partially stubbed)

### 4) Task Model
- Each task is a markdown file in `Tasks/` with YAML frontmatter for metadata.

### 5) Dedup + Triage Heuristics
- Duplicate detection uses fuzzy title match + keyword overlap.
- Ambiguity detection uses regex heuristics with generated clarifying questions.
- Category guess via keyword rules.

### 6) Auto Task Content Generation
- Category-based templates for Overview/Next Actions/Notes and optional extra sections.

### 7) Evals (Incomplete)
- Tools exist for evaluation files, but referenced trace scripts are not in this repo.

---

## Gaps vs. a Robust System

### Data Model and Storage
- Tasks are file-named by title; renames and collisions are likely.
- No stable task IDs or relationship model.
- No transactional storage or indexing for querying.

### Concurrency and Integrity
- File writes are unguarded; concurrent tool calls can overwrite or lose updates.
- No locking or optimistic concurrency control.

### Validation and Schema
- YAML frontmatter is loosely parsed with no schema enforcement or migrations.
- No validation of categories/priorities/status values.

### Deduplication Quality
- String similarity is brittle; no semantic or project-aware dedup.
- High false positives/negatives for similarly named tasks.

### Ambiguity Detection
- Regex rules are naive; little context awareness.
- Clarification questions are generic and not grounded in user goals or history.

### Configurability
- Template config exists but isn’t loaded into the runtime.
- Hardcoded category guessing and priority thresholds.

### Security and Safety
- Filename sanitization is minimal; risk of path issues.
- No input validation guardrails on tool calls.

### Observability
- Minimal logging; no structured logs or tracing.

### Evaluation Pipeline
- Tooling references missing dependencies.
- No reliable metrics for assistant quality or task outcomes.

---

## Path Forward (Robust Version)

### Phase 1: Architecture and Data Model
1. **Introduce persistent storage**
   - SQLite for local-first; Postgres for shared/remote.
   - Define stable task IDs (UUIDs) and normalized entities.
2. **Task schema**
   - Required fields: id, title, status, priority, category, created_at, updated_at, due_date.
   - Optional: estimates, tags, related goals, dependencies, recurrence.
3. **Goal linkage**
   - Explicit table or join on goals to tasks.
   - Enforce “goal alignment” metadata at creation.

### Phase 2: Core Services
1. **Task service**
   - CRUD with validation and strict schemas.
   - Optimistic concurrency (updated_at + version).
2. **Backlog service**
   - Parsing, triage, and enrichment pipeline.
   - Status: pending / clarified / rejected / converted.
3. **Dedup service**
   - Hybrid approach: lexical + embeddings + metadata signals.
   - Task similarity index with thresholds by category.

### Phase 3: Intelligence and Workflow
1. **Ambiguity detection**
   - Train or prompt-driven classification: “actionable vs. unclear”.
   - Clarification grounded in goals and recent tasks.
2. **Prioritization**
   - Use goal alignment score + due dates + energy/time slots.
3. **Templates**
   - Task templates per category and project.
   - Configurable in `config.yaml` or DB.

### Phase 4: MCP and API Layer
1. **MCP server refactor**
   - Thin tool layer; move logic to services.
   - Strong input validation and error handling.
2. **Rate limits + auth (if networked)**
   - If shared or hosted, use token auth and audit logs.

### Phase 5: Quality and Observability
1. **Structured logs and metrics**
   - Request tracing, task creation outcomes, dedup decisions.
2. **Eval pipeline**
   - Include session logs, tool call logs, success criteria.

---

## Suggested Technical Stack (Local-First)
- **Storage**: SQLite + SQLAlchemy (or equivalent)
- **API/MCP**: FastAPI + MCP adapter
- **Embeddings**: Local model or API-based embedding provider
- **Schema**: Pydantic models for strict validation
- **Client**: CLI + optional lightweight UI

---

## Minimal Milestone Plan

1. **M1: Stable Tasks**
   - Define schema
   - Add UUIDs
   - Move storage to SQLite

2. **M2: Backlog Pipeline**
   - Parse backlog into a “staging” table
   - Add clarification status + prompts

3. **M3: Dedup Quality**
   - Hybrid dedup (string + embeddings)
   - Tuning thresholds per category

4. **M4: Goal Alignment**
   - Explicit goal-task linking
   - Prioritization rules with scoring

5. **M5: Observability + Eval**
   - Add logs/metrics
   - Validate the eval pipeline end-to-end

---

## Open Questions
- Should tasks remain markdown-first for portability, or is a DB-only model acceptable?
- Is this system single-user local, or multi-user/shared?
- Do you want a UI, or is CLI/MCP enough?
- What are the top three workflows that must be bulletproof?

---

## Suggested Next Step
If you want, I can draft a concrete spec (schema + API) and a migration strategy that preserves existing markdown tasks.
