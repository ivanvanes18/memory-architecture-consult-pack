# Known Gaps

## Critical gap: Context Pack contract

Status: **implementation started**.

The system needs an explicit contract for what enters prompt context for a task. The first implementation slice now exposes contract metadata, routing decisions, included items, excluded items, and exclusion reasons. This is not the full solution yet, but the gap is no longer purely conceptual.

Without it, the system oscillates between:

- too much context → noise and cost;
- too little context → missing details and repeated mistakes.

Needed contract:

| Input type | Default behavior |
|---|---|
| Active project context | Always include first if branch/project known. |
| Active project facts | Include only if matching current task/project. |
| Behavior rules | Include only through behavior preflight when triggered. |
| Global stable user preferences | Include minimal subset. |
| Raw transcripts | Never include by default; use session_search only on demand. |
| Open loops/future intent | Exclude unless user freshly confirms. |
| Sensitive/secret notes | Exclude by default. |
| Ambiguous project references | Ask rather than guess. |

## Multi-session contamination

Risk scenario:

```text
Main: memory architecture discussion
Trading: strategy/risk discussion
Smeta/Project: VOR/XLSX work
```

Failure modes:

- Trading history appears in Main memory architecture analysis.
- Smeta rules trigger on unrelated project work.
- Old archived trading bot context becomes treated as canonical for new trading workflow.
- Project-specific corrections are promoted as global rules.

Mitigation needed:

- Branch/project context note first.
- Project-scoped retrieval before global retrieval.
- Cross-project negative tests.
- Clarifying question when project is ambiguous.

## Provenance gaps

Many active notes still lack `event_ids`. This weakens auditability but should not dominate the plan.

Priority rule:

1. Fix provenance for high-risk active rules/decisions.
2. Mark useful legacy notes as legacy/manual.
3. Archive stale/duplicate notes.
4. Do not fabricate provenance.

## Outcome review gap

Only a small subset of regression cases has outcome review. The system needs evidence that behavior rules are actually used and successful.

But outcome review should come after Context Pack/preflight routing works; otherwise rules may be good but never retrieved.

## Retrieval quality gap

Known issue: strict FTS AND semantics can return zero for natural-language queries where relaxed OR finds relevant notes.

Needed:

- Query normalization.
- Deterministic fallback attempts.
- Ranking based on active status, project match, source quality, importance, recency, and behavior-rule relevance.
- Retrieval logs that explain failures.

## Dream Cycle gap

Dream Cycle is intended as safe review/proposal, but it is not yet proven as a full backlog consolidation loop.

Needed:

- Define exactly what Dream Cycle scans.
- Define what it refuses to scan/promote.
- Add e2e tests from raw turns → candidates → review → activation/retirement.

## Architecture packet boundary

This packet is now kept as an internal/sanitized architecture map for implementation. It should not introduce a separate external-audit process layer unless Ivan explicitly asks for that again.
