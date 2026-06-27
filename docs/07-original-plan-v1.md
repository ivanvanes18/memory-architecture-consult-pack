# Original Plan v1 — Cleanup-First Draft

This is a summarized version of the first implementation plan. It was useful but reviewed as too cleanup-first.

## Original order

1. Targeted Memory Health Audit.
2. Clean Critical Provenance Gaps.
3. Close Regression Case Outcome Review Loop.
4. Tune Retrieval Ranking and Project Routing.
5. E2E Memory Stability Verification.
6. Final Integration and Documentation.

## Why it was insufficient

It correctly identified real work, but the priority was wrong.

The operator's primary pain is not missing `event_ids`. The primary pain is:

```text
large context causes noise
small context loses details
wrong retrieval causes repeated mistakes
```

Therefore the first artifact must be a Context Pack Contract, not a cleanup report.

## What survives from v1

The following work remains valid and should be reused:

- memory health audit;
- provenance cleanup;
- regression outcome review;
- retrieval tuning;
- e2e stability verification;
- operator troubleshooting docs.

But these should be subordinated to the v2 plan:

```text
Context Pack contract first → routing tests → retrieval tuning → cleanup/outcomes
```

## Original file location

The local original plan was saved at:

```text
docs/superpowers/plans/2026-06-27-readable-memory-full-power.md
```

It is not reproduced verbatim here because it contains local operational assumptions and pseudo-code that should be revised before implementation.
