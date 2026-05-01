# psypowers — Codex contributor guide

This repository supports both Claude Code and Codex. Claude Code remains supported through `.claude-plugin/` manifests and `CLAUDE.md`; Codex support lives in `.agents/plugins/marketplace.json`, plugin-level `.codex-plugin/plugin.json`, and this `AGENTS.md` instruction file.

## Plugin map

| Plugin | Claude plugin ID | Codex plugin ID | Folder | Language |
|---|---|---|---|---|
| Psychological consultation toolkit | `psy` | `psy` | `plugins/psy` | English |

## Repository rules

- Evidence-based content only: use real assessment tools, real therapeutic models, and published clinical sources.
- `agents/` and `skills/` remain the source of truth for plugin behavior.
- When adding or renaming agents or skills, update the plugin README, `CLAUDE.md`, `AGENTS.md`, Claude manifest, and Codex manifest/marketplace when the public surface changes.
- Do not commit real client data. Use placeholders such as `[client name]`, `[date of birth]`, and `[client-id]`.
- Crisis workflows must always defer to professional judgment, supervision, institutional protocols, and emergency services for imminent danger.

## Codex layout

- `.agents/plugins/marketplace.json` is the Codex marketplace catalog.
- `plugins/psy/.codex-plugin/plugin.json` is the Codex plugin manifest.
- `AGENTS.md` files are Codex-facing contributor instructions.
- `CLAUDE.md` files remain Claude-facing contributor instructions.

## Verification

After changing Codex support, validate JSON manifests and verify the marketplace `source.path` points to `plugins/psy` with `.codex-plugin/plugin.json` and `skills/`.
