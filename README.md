# Agent Memory Architecture Consult Pack

> Public, sanitized context pack for external review of a personal-agent memory architecture.

This repository is a **review packet**, not a production codebase. It summarizes the current memory architecture, the user's core pain, the historical influences behind the design, the current implementation state, known gaps, and the proposed next plan.

## Why this exists

The operator's main problem is the classic agent-memory trap:

1. If the agent carries a large context, every turn becomes bloated, expensive, and noisy.
2. If the agent does not carry enough context, important details disappear.
3. Missing details cause repeated mistakes, wrong project routing, and fragile multi-session work.
4. Corrections accumulate, but unless they become future behavior, the same bugs reappear.

The goal is **not** "more memory". The goal is:

> Capture broadly, preserve evidence, promote carefully, retrieve narrowly, and build a small source-backed Context Pack for the current task.

## Requested external review

Please review this repository as if you were advising on a production personal-agent memory system.

Focus questions:

1. Is the architecture still aligned with the Human 2.0-style memory direction described here?
2. Is the next plan correctly prioritizing Context Pack / retrieval policy before cleanup work?
3. What is missing to prevent context bloat while keeping high recall for important project details?
4. How should multi-session work be isolated so that Main / domain threads do not contaminate each other?
5. What is the smallest implementation path that gives strong evidence the memory loop works?

## Repository map

| Path | Purpose |
|---|---|
| `docs/00-publication-boundary.md` | What was sanitized and why raw private memory is not dumped here. |
| `docs/01-problem-statement.md` | The user's actual pain and success criteria. |
| `docs/02-current-architecture.md` | Current Hermes/readable_tree architecture and runtime behavior. |
| `docs/03-historical-influences.md` | Human 2.0 / Hy-Memory / GBrain influences and what was adopted or rejected. |
| `docs/04-current-state-and-evidence.md` | Tool-backed snapshot of current memory health. |
| `docs/05-known-gaps.md` | What is not solved yet. |
| `docs/06-plan-v2-human2-aligned.md` | Revised plan: Context-Pack-first, not cleanup-first. |
| `docs/07-original-plan-v1.md` | Original plan that was reviewed and found too cleanup-first. |
| `docs/08-review-prompts.md` | Prompts to give another model/reviewer. |
| `docs/09-glossary.md` | Terms used in the packet. |
| `docs/10-external-audit-and-implementation-start.md` | External audit verdict plus first implementation slice and test evidence. |

## Current verdict

The system is **not off-track**, but the plan needed correction.

- It is still aligned with the intended direction: raw sessions → events → source-backed notes → retrieval → Context Packs → behavior preflight → outcome review.
- The dangerous drift was prioritizing provenance cleanup before the actual bottleneck: **Context Pack policy and project-scoped retrieval precision**.
- The next phase should prove that the agent can retrieve a small, correct, project-specific context bundle across sessions without pulling unrelated domain memory.
- Implementation has now started: the first slice adds an executable Context Pack contract surface, deterministic routing decision metadata, inclusion/exclusion logs, and targeted tests in the Hermes readable_tree codebase.

## Public-safety note

This repository intentionally avoids raw transcripts, secrets, private contact data, credentials, full personal profile dumps, and sensitive operational logs. It includes enough architecture and evidence for review without publishing the operator's private life. Public memory packs that dump everything are not transparency; they are a data breach wearing a lab coat.
