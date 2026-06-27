# External Audit Follow-up and Implementation Start

Date: 2026-06-27

## External audit verdict

An external review of this packet agreed with the main architectural direction:

> Do not rethink the architecture. Revise the implementation contract.

The reviewer confirmed that the right next priority is not more memory, not cleanup-first, and not vector/graph-first. The strongest next step is to make Context Pack, routing, retrieval, behavior preflight, and Dream Cycle enforceable interfaces with tests and logs.

## Key audit findings accepted

| Finding | Accepted action |
|---|---|
| Context Pack is the central risk surface. | Make it an executable contract with schema, budgets, inclusion/exclusion logs, and source IDs. |
| Project routing must be a hard gate. | Add deterministic BranchResolver with confidence, aliases, allowed/denied scopes, and clarification mode. |
| Negative retrieval is under-specified. | Log excluded items with reasons such as archived, superseded, open_loop, sensitive, secret_ref, over_budget. |
| Behavior loop is right but under-proven. | Instrument rule firing/use/outcome and test positive/negative triggers. |
| Dream Cycle must remain proposal-only. | Keep cleanup and promotion behind explicit review/apply steps. |

## Implementation has started

The first production slice was started in the Hermes readable_tree codebase.

Implemented initial contracts:

1. `context_pack_contract_v1` metadata in Context Pack output.
2. Hard character-budget field and section-budget policy.
3. `routing_decision` included in the pack.
4. `included_items` with authority, scope, project, source IDs, event IDs, and why-included.
5. `excluded_items` with note ID and exclusion reason.
6. Deterministic `BranchResolver` for Main / Trading / Projectoriy / Hermes memory contexts.
7. Unknown or multi-branch query can require clarification instead of falling back to Main.
8. Regression tests for contract shape, archived exclusion, ambiguous routing, and Hermes-memory routing without trading contamination.

## Fresh verification evidence

Targeted tests run in the Hermes repo:

```text
python -m pytest tests/plugins/test_readable_tree_context_pack_contract.py \
  tests/plugins/test_readable_tree_retrieval.py \
  tests/plugins/test_readable_tree_behavioral.py \
  -q -o 'addopts='

16 passed in 0.65s
```

## What this proves

This does not prove the full memory architecture yet. It proves the first important slice:

- Context Pack output is no longer only a prose idea; it has an explicit contract surface.
- Exclusions are visible rather than silent.
- Routing is represented as machine-readable state.
- Ambiguity can become a clarification requirement rather than silent Main fallback.
- A Hermes-memory query can retrieve Hermes memory context without pulling a lexically tempting trading note in the targeted fixture.

## What remains unproven

- Full fresh-session dogfood through the live gateway.
- Behavior rule `rule_fired` / `rule_used_in_answer` outcome logging.
- Full cross-project suite: Main → Smeta/VOR → Projectoriy → Trading → Main.
- Dream Cycle safe proposal/apply e2e.
- Recall@K / Precision@K / contamination-rate reporting across a larger fixture set.
- Runtime rollout evidence after gateway restart or fresh Hermes session.

## Next implementation slice

Recommended next slice:

1. Add explicit Context Pack JSON schema fixture.
2. Add branch/project registry fixture with aliases and denied scopes.
3. Add cross-project contamination test matrix.
4. Add behavior preflight logging for `rule_fired` and `rule_used_in_answer`.
5. Add a small evaluator report that prints pack size, included IDs, excluded IDs, and contamination failures.

The direction is now implementation-first: each new architectural claim should come with code, a fixture, and test output.
