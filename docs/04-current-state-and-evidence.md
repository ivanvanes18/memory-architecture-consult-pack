# Current State and Evidence Snapshot

Snapshot date: 2026-06-27.

## Tool-backed metrics

```json
{
  "notes": 207,
  "active_notes": 122,
  "archived_notes": 85,
  "raw_turns": 863,
  "events": 238,
  "retrieval_logs": 2230
}
```

## Backfill / provenance state

Recent backfill dry-run:

- scanned active notes: 110
- legacy corrections: 0
- weak provenance: 0
- missing `event_ids`: many active legacy/manual notes still need linking, legacy marking, or archive decisions

Interpretation:

- The previously noisy legacy-correction false positives were fixed.
- The remaining issue is not broken behavior chains; it is weaker provenance on older notes.
- Provenance cleanup matters, but it is not the first-order solution to context bloat.

## Regression / behavioral memory state

Regression report:

- scanned regression cases: 18
- reviewed case IDs: 2
- unreviewed cases: 16

Representative mistake classes:

- `preserve_vor_section_structure`
- `normalize_legacy_xls_symbols`
- `avoid_artificial_vor_fields`
- `preserve_excel_template_formatting`
- `humanize_normative_work_names`
- `minimal_ooxml_patch_for_import_xlsx`
- `deliver_legacy_xls_for_smeta_import`
- `expensive_model_overuse`
- `wrong_agent_routing`
- `overinclude_agent_context`
- `noisy_self_audit`
- `missing_case_memory`
- `utility_for_utility`

Interpretation:

- The behavior loop exists.
- Some regression cases are high quality and domain-specific.
- Outcome review is still underdeveloped, so not all rules are proven to change future behavior.

## Flush / extraction state

Recent flush dry-run over 50 raw turns:

- candidates: 15
- written: 0 because dry-run
- includes a mix of requirements, artifacts, facts, and open loops

Notable extraction observations:

- Some candidates are useful memory architecture requirements.
- Some are stale or operationally noisy.
- Open loops are correctly marked as future intent / not-current-instruction.

Interpretation:

- Capture/extraction works.
- Review/promotion policy must prevent inbox from becoming permanent clutter.

## Implementation start evidence

The first Context Pack Contract slice has started in the Hermes readable_tree implementation:

- `context_pack_contract_v1` appears in Context Pack output.
- Context Packs now expose `routing_decision`, `included_items`, and `excluded_items`.
- Excluded candidates carry machine-readable reasons such as `archived`, `superseded`, `open_loop`, `sensitive`, `secret_ref`, or `over_budget`.
- A deterministic BranchResolver covers Main / Trading / Projectoriy / Hermes memory contexts and can mark unknown or multi-branch queries as clarification-required.
- Targeted verification: `120 passed` for Context Pack contract, retrieval, behavioral-memory, lifecycle, memory, and metrics tests.

## Current strongest parts

- Raw/session evidence exists.
- Readable Markdown memory exists.
- Behavior preflight exists.
- Regression cases exist.
- Project context notes exist for Main / Trading / Project domains.
- Backfill detector for behavior links no longer reports the fixed chains as legacy.

## Current weakest parts

- Context Pack policy is not yet explicit enough.
- Project-scoped retrieval needs tests and tuning.
- Importance is likely inflated across too many notes.
- Many older active notes lack `event_ids` provenance links.
- Dream Cycle behavior is not proven as a full consolidation loop.
- Multi-session routing needs e2e tests, not just notes saying it should work.
