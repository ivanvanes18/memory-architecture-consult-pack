# Publication Boundary

This repository is a **sanitized public review packet**.

## Included

- Architecture description.
- Current state metrics from memory tools.
- Selected non-secret design decisions and summarized memory notes.
- Known gaps and implementation plan.
- Public-facing reviewer prompts.

## Excluded

- Raw Telegram/DM transcripts.
- API keys, tokens, passwords, `.env` files, session files, OAuth credentials.
- Full personal memory tree dump.
- Sensitive personal-life details.
- Private file paths where not needed for architecture analysis.
- Any `secret_ref` or `sensitive` notes.

## Why not dump everything?

The user explicitly wants enough context for another model to reason well. That does **not** require publishing the entire personal memory corpus. The useful review unit is the architecture, state, representative evidence, and decision history.

Raw private logs would create three problems:

1. **Privacy risk** — personal working context can contain names, secrets, financial details, health details, and third-party information.
2. **Prompt-injection risk** — raw historical text can contain instructions that should be treated only as evidence.
3. **Review noise** — a reviewer needs a structured Context Pack, not a landfill.

This packet follows the same philosophy as the target system:

> broad capture privately, careful promotion publicly, narrow retrieval for review.
