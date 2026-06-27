# Plan v2 — Human2-Aligned Memory Work

## Verdict

The old plan was useful but too cleanup-first. The revised plan is **Context-Pack-first**.

The goal is to prove that the agent can carry a small, correct, project-specific memory bundle instead of either dragging everything or forgetting important details.

## Phase 0 — Human 2.0 alignment matrix

Create a matrix:

| Layer | Intended idea | Current implementation | Gap | Priority |
|---|---|---|---|---|
| Raw sessions | Preserve source evidence | session DB + raw turns | verify coverage | high |
| Structured events | Link raw turns, notes, actions | events.jsonl | incomplete event_ids on older notes | medium |
| Atomic notes | Source-backed durable facts/rules | readable_tree Markdown | quality varies | high |
| Evolution | supersedes/conflicts/open loops | partly present | needs more use | medium |
| Context Pack | small task-specific memory bundle | partly present | contract missing | critical |
| Behavior loop | correction → rule → regression → outcome | present | outcomes incomplete | high |
| Project routing | isolate domains/branches | project_context notes | e2e tests missing | critical |
| Cleanup/Dream | consolidate safely | proposal tooling | contract unclear | medium |

Deliverable: `human2-alignment-matrix.md`.

## Phase 1 — Context Pack Contract

Define exactly what gets injected for a task.

Required sections:

1. Branch/project context.
2. Project-local active facts/decisions.
3. Matching behavior preflight rules.
4. Minimal global stable preferences.
5. Optional session snippets only when the user asks for historical recall.
6. Exclusions: sensitive/secret/open_loop/raw transcripts by default.

Acceptance criteria:

- A memory-heavy task produces a bounded Context Pack under a fixed character budget.
- The pack states why each item was included.
- The pack excludes unrelated project memory.
- Ambiguous project queries trigger clarification.

## Phase 2 — Multi-session routing tests

Test scenarios:

| Scenario | Expected retrieval |
|---|---|
| Main: memory architecture | memory architecture + global rules, no VOR/trading unless relevant |
| Smeta/VOR | VOR/smeta rules, no trading baseline |
| Project/Проекторий | project context + related file/import rules |
| Trading | trading context, but old archived bots not canonical baseline |
| Ambiguous “that project” | ask which project |

Acceptance criteria:

- Cross-domain contamination tests pass.
- Branch/project context is first retrieval step.
- The system asks rather than guesses when branch is unknown.

## Phase 3 — Retrieval precision tuning

Only after the Context Pack contract exists.

Work:

- Fix project/scope metadata on important notes.
- Deflate overused `importance: high`.
- Add query normalization / relaxed fallback tests.
- Validate ranking order: active + project match + source quality + behavior relevance.

Acceptance criteria:

- Representative queries show fewer irrelevant results.
- Retrieval logs explain which strategy succeeded.
- Context Pack stays small.

## Phase 4 — Behavior outcome review

Review regression cases after preflight routing is proven.

Work:

- For each active regression case, test a representative query.
- Mark outcome: fixed, repeated, unclear, superseded.
- Improve weak generic rules.

Acceptance criteria:

- Most active behavior rules have outcome evidence.
- Repeated/unclear rules become targeted fixes.
- No generic “I will do better” rules remain active without concrete triggers.

## Phase 5 — Dream Cycle / cleanup

Clarify Dream Cycle’s real role.

Work:

- Define what it scans: inbox? raw turns? active notes? archive?
- Define what it proposes vs refuses.
- Add safe apply workflow.
- Add review queue thresholds.

Acceptance criteria:

- Dream Cycle never silently promotes active memory.
- Sensitive/secret notes remain excluded by default.
- Inbox does not become permanent storage.

## Phase 6 — E2E proof

End-to-end scenario:

```text
Work in Main
→ switch to Smeta/VOR
→ switch to Project/Проекторий
→ switch to Trading
→ return to Main
→ retrieve correct details
→ exclude unrelated context
→ behavior preflight catches relevant past corrections
→ no repeated known mistake
```

Acceptance criteria:

- Tool-backed evidence for each step.
- Context Pack sizes measured.
- Cross-project contamination checked.
- Rebuild/restart/fresh-session behavior verified.

## Implementation priority

1. Context Pack Contract.
2. Multi-session routing tests.
3. Retrieval precision tuning.
4. Behavior outcome review.
5. Provenance cleanup for high-risk active notes.
6. Dream Cycle cleanup.
7. Full e2e proof.

This plan intentionally avoids new graph/vector magic until the source-backed retrieval contract is proven.
