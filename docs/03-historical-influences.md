# Historical Influences and Design Lineage

## Human 2.0-style direction

The desired direction came from a Human 2.0-style memory architecture: persistent work across many sessions, with connections between sessions and compact retrieval rather than massive context carryover.

The durable split that emerged:

1. **Strong skills methodology** — how repeatable work is executed via SSoT, workflow, tools, guardrails, verification, artifacts, and memory hooks.
2. **Agent memory methodology** — how the agent preserves experience through raw sessions, structured events, atomic source-backed memories, indexes, Context Packs, and safe review/apply loops.

## Hy-Memory ideas considered

Hy-Memory was considered as a reference, but not blindly adopted.

Useful ideas:

- Multi-level memory / different authority levels.
- Fast capture vs slow consolidation.
- Evolution chains / supersedes.
- Dense fewer memories instead of a vector-only pile.
- Future-intent memories should not automatically become instructions.

Rejected or deferred:

- Blind install of a third-party plugin.
- Treating marketing claims as verified benchmark proof.
- Defaulting to opaque vector storage when the current design wants readable Markdown as source of truth.
- Injecting unsourced semantic text directly into prompts.

## GBrain / domain expert memory lesson

For the estimation/smeta domain, the operator explicitly rejected “searchable archive as brain”. The desired agent should develop expert judgment:

```text
case evidence
→ lessons
→ rules / registries / heuristics
→ applied in future tasks
→ regression/outcome review
```

This is a stronger bar than storage/search. A memory system is useful only if it changes future behavior.

## Current conclusion

The project has not fundamentally departed from the original Human 2.0-style direction. The main risk is implementation priority drift:

- Too much focus on cleanup/provenance first.
- Not enough focus on the Context Pack contract and project-scoped retrieval precision.

The revised plan restores the intended priority:

```text
alignment check
→ Context Pack contract
→ multi-session routing tests
→ retrieval tuning
→ behavior outcome loop
→ Dream Cycle cleanup
→ e2e proof
```
