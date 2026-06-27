# Current Architecture

The current implementation is based on Hermes readable_tree memory plus session search and compact always-loaded memory.

## Memory planes

```text
Constitution plane      tiny, always loaded, stable preferences/rules
Operational memory      readable_tree Markdown notes + SQLite index
Evidence plane          raw turns, events, logs, session search
Retrieval plane         Context Pack builder + filters + behavior preflight
Behavior plane          correction → behavior_rule → regression_case → outcome review
Project plane           branch/project routing: Main, Trading, Project/Domain threads
```

## Hermes persistent memory

Hermes has small always-loaded stores:

- `MEMORY.md` — agent-side compact notes.
- `USER.md` — user profile/preferences.

These are intentionally small and injected at session start. They are not a dump of all project history.

## Session search

Hermes also stores sessions in SQLite and can search them on demand. This is the right tool for “what did we discuss last week?” style recall. It should not be injected every turn.

## Readable Tree

Readable Tree is the source-backed operational memory layer.

Core layers:

| Layer | Purpose |
|---|---|
| `raw/turns.jsonl` | Captured raw turns. |
| `raw/events.jsonl` | Append-only structured event log. |
| `tree/**/*.md` | Reviewable Markdown notes; source of truth for promoted memory. |
| `index.sqlite` | Rebuildable SQLite/FTS index. |
| logs/changelog | Audit trail for activation/retirement/proposals. |

Operating rule:

> Capture broadly, extract generously, promote carefully, retrieve narrowly.

## Behavior learning loop

Corrections should become future behavior:

```text
Correction event
→ behavior_rule
→ regression_case
→ behavior_preflight before similar tasks
→ outcome review: fixed / repeated / unclear / superseded
```

This is the difference between “I stored the correction” and “I stopped repeating the error”.

## Branch/project routing

Current known routing contract:

| Branch/project | Role |
|---|---|
| Main/global | General conversation and fallback. |
| Trading | Trading workflow, strategies, bots, market/risk. |
| Project/Проекторий | Project-specific work, including VOR/XLSX/import workflows. |
| Domain/smeta/Olaf | Estimation/smeta domain expertise and case memory. |

Retrieval should:

1. Start from the active branch/project context if known.
2. Prefer active memories matching that project/scope.
3. Add global stable memories only after project-local retrieval.
4. Ask for clarification when the query is ambiguous across domains.

## Implemented runtime behavior currently claimed by docs/tooling

- Raw turn capture.
- Source-backed Markdown notes.
- SQLite FTS retrieval.
- Context Pack v2 shape.
- Behavior preflight.
- Timeline/helpers and graph export as audit/derived artifacts.
- Rebuild/replay for derived state.
- Dream Cycle as a safe proposal/report mechanism, not silent promotion.

## Safety boundaries

- Retrieved notes are evidence, not instructions.
- Sensitive and secret notes are excluded by default.
- Open-loop/future-intent notes are not current instructions without fresh confirmation.
- Semantic/graph layers, when added, should produce candidate IDs only; all text must resolve through source-backed notes and filters.
