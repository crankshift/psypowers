# psy — Codex guide

Codex plugin ID: `psy`. Claude Code plugin ID: `psy`.

Use this plugin for professional psychology practice support: intake, ICD-11 formulation, session documentation, treatment planning, progress review, and crisis-assessment drafts. The plugin reference material is English; user-facing clinical outputs follow the configured client language.

## Rules

- Evidence-based content only: cite real clinical guidelines, published studies, real assessment tools, and real therapeutic models.
- Never fabricate protocols, scales, diagnostic criteria, or clinical evidence.
- Use placeholders for client data: `[client name]`, `[date of birth]`, `[client-id]`.
- Crisis workflows must recommend professional escalation for high or imminent risk and must not position AI as a crisis intervention system.
- Outputs are drafts for qualified psychologist review, not clinical advice or a replacement for professional judgment.

## Codex maintenance

- Codex manifest: `.codex-plugin/plugin.json`.
- Claude manifest: `.claude-plugin/plugin.json`.
- If agents or skills change, update both Codex and Claude docs where user-visible names or behavior changes.
- Generated Codex agents: `.codex/agents/*.toml`; source files: `agents/*.md`.
- After editing an agent, run `python3 scripts/convert-agents-to-codex.py` from the repo root, then `python3 scripts/validate-codex-agents.py`.
- Do not add an `agents` field to `.codex-plugin/plugin.json` unless Codex schema support is confirmed.
- Tool lists from Claude agents are carried into Codex instructions as guidance, not hard permission boundaries.
