# Glossary

| Term | Meaning |
|---|---|
| Context Pack | Small, source-backed bundle of relevant memory injected for the current task. |
| Readable Tree | Hermes local Markdown memory provider with raw turns, events, notes, and rebuildable SQLite index. |
| Raw turn | Captured conversation turn, not directly trusted as active instruction. |
| Event | Structured append-only record linking raw sources, notes, activation, retirement, conflict resolution, etc. |
| Active note | Memory note eligible for retrieval by default, subject to filters. |
| Open loop | Future intent / unfinished thread; not a current instruction without fresh confirmation. |
| Behavior preflight | Retrieval of active behavior rules before similar tasks to avoid repeated mistakes. |
| Regression case | A structured test-like memory describing what behavior should change after a correction. |
| Outcome review | Marking a behavior rule/case as fixed, repeated, unclear, or superseded based on later evidence. |
| Dream Cycle | Safe review/proposal workflow for memory cleanup and consolidation. It should not silently promote memory. |
| Provenance | Source/event links explaining where a memory note came from. |
| Project routing | Choosing the right project/branch memory before global memory. |
| Cross-project contamination | Pulling facts/rules from the wrong project into the current task. |
