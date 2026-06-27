# Review Prompts

Use one of these prompts with an external model or reviewer.

## Short prompt

You are reviewing a personal-agent memory architecture. Read this repository and answer:

1. Is the architecture aligned with the goal of compact but accurate cross-session memory?
2. Is the v2 plan prioritizing the right work?
3. What would you change before implementation?
4. What tests would prove the system avoids context bloat and cross-project contamination?

## Full prompt

You are an expert reviewer for long-running AI agent memory systems.

Context:

- The operator works across multiple projects/sessions.
- The main failure is a tradeoff between bloated context and missing details.
- The system uses Hermes readable_tree: raw turns, event log, Markdown notes, SQLite index, Context Packs, behavior preflight, regression cases, Dream Cycle proposal workflow.
- The desired architecture was inspired by Human 2.0-style session memory: store broad evidence, create structured memories, link sessions, retrieve compact context under task-specific policy.
- Current risk: plan drift toward cleanup/provenance work before proving Context Pack retrieval.

Tasks:

1. Review whether the architecture is coherent.
2. Identify missing layers or wrong assumptions.
3. Stress-test multi-session project routing.
4. Propose a minimal implementation sequence.
5. Define acceptance tests and metrics.
6. Warn about privacy/safety issues in public memory sharing.

Please be direct. Prefer concrete architectural changes, tests, and failure modes over generic commentary.

## Devil's advocate prompt

Assume this memory system will fail in production. Based on the repository, identify the top 10 ways it fails and the smallest changes that would prevent each failure.

## Implementation review prompt

Turn `docs/06-plan-v2-human2-aligned.md` into an implementation spec with acceptance criteria, real test cases, and a sequence of small commits. Avoid speculative infrastructure. Do not add vector/graph layers until source-backed Context Pack retrieval is proven.
