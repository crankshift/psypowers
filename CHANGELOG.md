# Changelog

Monorepo-level structural log. Plugin content changes go in the plugin's own CHANGELOG.

## 2026-05-01 — Codex agent compatibility

- `psy` bumped to `0.1.2`: generated Codex custom-agent TOML files from the existing Claude agents.
- Added `scripts/convert-agents-to-codex.py` and `scripts/validate-codex-agents.py` for keeping Claude and Codex agent artifacts in sync.
- Marketplace `metadata.version` bumped to `0.1.2`.

## 2026-05-01 — Codex support

- `psy` bumped to `0.1.1`: Codex marketplace/manifest support, `AGENTS.md`, and Codex install docs.
- Marketplace `metadata.version` bumped to `0.1.1`.

## 2026-05-01 — Initial repository setup

- Created monorepo with single plugin: `psy` (v0.1.0).
- Added 8 agents and 14 skills.
- Added Astro + Firebase landing site scaffold.
