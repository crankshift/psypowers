# Changelog — psy plugin

## [0.1.3] — 2026-05-13

### Added

- Added the `case-file-architecture` utility skill to enforce one-artifact-one-role ownership for case files, session notes, progress logs, safety plans, clinical documents, and workspace-specific markdown logs.

### Changed

- Updated all source agents with artifact ownership guardrails so session files, progress reports, treatment plans, diagnoses, crisis documents, and derived notes do not absorb unrelated content.
- README, `CLAUDE.md`, and `AGENTS.md` now document case-file ownership and local workspace file-map handling.
- `release.sh` now keeps Claude and Codex plugin manifest versions in sync when bumping `psy`.
- `plugin.json`: version 0.1.2 → 0.1.3.

## [0.1.2] — 2026-05-01

### Added

- Generated Codex custom-agent TOML files in `.codex/agents/` for all Claude agents in the plugin.
- Added `scripts/convert-agents-to-codex.py` and `scripts/validate-codex-agents.py` to keep Claude/Codex agent artifacts in sync.

### Changed

- README, `AGENTS.md`, and `CLAUDE.md` now clarify that `agents/*.md` remains the source of truth and Codex agents are generated from it.
- `plugin.json`: version 0.1.1 → 0.1.2.

## [0.1.1] — 2026-05-01

### Added

- Codex support: `.agents/plugins/marketplace.json`, `.codex-plugin/plugin.json`, and Codex-facing `AGENTS.md` instructions.
- README installation instructions for Codex while preserving the existing Claude Code plugin ID `psy`.

### Changed

- `CLAUDE.md` now documents the Claude/Codex support split and sync rules.
- `plugin.json`: version 0.1.0 → 0.1.1.

## [0.1.0] — 2026-05-01

### Added

- **Agents (8):** intake-interviewer, session-conductor, diagnosis-formulator, treatment-planner, progress-analyzer, practice-recommender, case-notes-drafter, crisis-assessor.
- **Utility skills (4):** icd11-classification, assessment-scales, session-structuring, progress-measurement.
- **Modality skills (10):** cbt-techniques, dbt-techniques, act-techniques, mindfulness-practices, somatic-practices, art-therapy-practices, emdr-protocols, psychodynamic-techniques, positive-psychology, crisis-intervention.
- Client case file structure with markdown-based session tracking and progress monitoring.
[0.1.1]: https://github.com/crankshift/psypowers/releases/tag/psy/v0.1.1
[0.1.2]: https://github.com/crankshift/psypowers/releases/tag/psy/v0.1.2
[0.1.3]: https://github.com/crankshift/psypowers/releases/tag/psy/v0.1.3
