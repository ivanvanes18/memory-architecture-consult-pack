# Problem Statement

## Operator pain

The operator works with multiple agent sessions and multiple project domains. The recurring failure mode is:

```text
large memory/context → bloated prompts and noise
small memory/context → missing details
missing details → wrong assumptions and repeated mistakes
wrong assumptions → corrections accumulate
corrections not operationalized → same bug repeats later
```

The operator wants the agent to remember projects, decisions, details, and repeated corrections without dragging an entire historical transcript into every turn.

## Practical success criteria

The memory system should be:

| Criterion | Meaning |
|---|---|
| Compact | Does not inject raw history or large summaries by default. |
| Precise | Retrieves the right project/task facts when needed. |
| Complete enough | Can recover past decisions and project details on demand. |
| Behavior-changing | Corrections become preflight rules and regression cases, not diary entries. |
| Multi-session safe | Separate work streams do not contaminate each other. |
| Auditable | Important memories have source/provenance and can be retired or superseded. |
| Public/review safe | Sensitive and secret notes are excluded by default. |

## Non-goals

- Do not turn always-loaded prompt memory into a chronological second brain.
- Do not publish or inject raw private transcripts by default.
- Do not add vector/graph/semantic layers before the source-backed retrieval contract is proven.
- Do not silently promote future-intent/open-loop notes into active instructions.
- Do not treat searchable Markdown as a real expert brain unless it changes future behavior.

## The central design target

The agent should build a bounded **Context Pack** for each task:

```text
current branch/project context
+ relevant active project facts
+ behavior preflight rules only when triggered
+ minimal stable user preferences
+ recent session snippets only when explicitly needed
= small source-backed task context
```

The target is not maximal recall every turn. It is **high precision first, recoverable recall on demand**.
