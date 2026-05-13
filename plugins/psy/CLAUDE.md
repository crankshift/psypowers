# psypowers / psy — contributor rules

Execution context for the `psy` plugin. For the agent/skill catalog and project structure see [`README.md`](./README.md) and root [`CLAUDE.md`](../../CLAUDE.md).

## Language — dual-layer model

The plugin separates **internal knowledge** (skills, research, reference material) from **user-facing output** (case files, session notes, clinical documents, agent responses).

- **Skills and reference material** are always in **English**. They are not shown to clients — they are internal knowledge bases.
- **Agent output language** (case files, session notes, progress reports, clinical documents, conversational responses) is determined by the **user's language preference**, stored in `cases/.config.md`.
- **Terminology:** Clinical terms (ICD-11 codes, scale names like PHQ-9, technique names like "cognitive restructuring") should be kept in their original English form even in non-English output, with a local-language explanation on first use. Example in Ukrainian: "когнітивне реструктурування (cognitive restructuring) — техніка CBT для виявлення та зміни дисфункціональних думок."

### Language preference detection

On first interaction with any agent, if `cases/.config.md` does not exist:

1. **Ask the user:** "What language should I use for clinical documents and session notes? (e.g., English, Ukrainian, Polish, German, etc.)"
2. **Create `cases/.config.md`** with the preference:
   ```markdown
   # Plugin Configuration
   
   ## Language
   - **Output language:** [user's choice, e.g., "Ukrainian"]
   - **Internal/research language:** English (fixed)
   ```
3. All subsequent agents read this file and generate output in the specified language.

If `cases/.config.md` already exists, read it silently and follow the preference. The user can change the language at any time by editing the config or asking any agent to update it.

### How this works in practice

- Agent reads skills (English) → processes internally (English) → generates output in user's preferred language
- Research via `WebFetch`/`WebSearch` can be done in English or the output language — whichever yields better results
- ICD-11 codes and scale names stay in English regardless of output language (they are international standards)
- Section headings in case files should be in the output language

## Evidence and verification

- **Evidence-based only.** Every technique, scale, and protocol must reference published clinical evidence — peer-reviewed studies, meta-analyses, or clinical practice guidelines (APA, NICE, WHO).
- **No fabricated tools.** Assessment instruments (PHQ-9, GAD-7, BDI-II, C-SSRS, etc.) are real, validated tools. Never invent a scale or modify scoring criteria.
- **ICD-11 is the primary diagnostic system.** Fetch current criteria from `icd.who.int` before using hardcoded references.
- **Cite sources.** When referencing a technique or protocol, include the original author/study and year where practical (e.g., "Beck's cognitive triad (Beck, 1967)", "Stanley-Brown safety plan (Stanley & Brown, 2012)").

## Client data

Templates use placeholders: `[client name]`, `[date of birth]`, `[client-id]`, `[session number]`. Never store real client data in plugin files.

## Case file ownership

Use the `case-file-architecture` skill before creating, editing, renaming, or choosing locations for case files, session notes, progress logs, safety plans, clinical documents, or workspace-specific markdown logs.

Each artifact has one primary role:

- `intake.md` owns baseline intake and initial assessment data.
- `diagnosis.md` owns working diagnostic formulation and differential reasoning.
- `treatment-plan.md` owns goals, modalities, measurable targets, timelines, and review schedule.
- `progress.md` owns aggregate progress analysis: score trends, goal progress, plateau/regression alerts, and recommendations.
- `sessions/YYYY-MM-DD.md` owns date-specific session narrative, observations, interventions, homework, risk notes, and scores administered that session.
- `safety-plan.md` owns the active safety plan.
- `notes/YYYY-MM-DD-[type].md` owns derived session-specific notes such as SOAP/DAP/narrative drafts.
- `documents/YYYY-MM-DD-[type].md` owns formal external documents such as referrals, progress reports, and discharge summaries.

If a user workspace has local `AGENTS.md` or README file maps, honor those local ownership rules before inventing new file paths. Split mixed content into the correct artifacts; reference rather than duplicate full source narratives.

## Fetch-first for diagnostic codes

Skills and agents that embed ICD-11 codes must include a **fetch-first block**: attempt `WebFetch` from `icd.who.int` before falling back to hardcoded values. Hardcoded values are annotated with `_(fallback; as of [date])_`.

## Output character

All plugin outputs are **working drafts for a qualified psychologist** to review, not final clinical documents or therapeutic advice to clients. The human clinician bears all professional responsibility.

## Crisis safety

The `crisis-assessor` agent and `crisis-intervention` skill always recommend professional escalation for high or imminent risk. The plugin never suggests managing acute crises via AI alone. Every crisis-related output includes a disclaimer that professional judgment and local emergency protocols take precedence.

## Codex support

This plugin also has Codex support. Keep `AGENTS.md` and `.codex-plugin/plugin.json` in sync with this Claude-facing file and `.claude-plugin/plugin.json` when user-visible behavior changes. Claude Code continues to use the existing Claude plugin ID; Codex may use a collision-safe ID documented in `AGENTS.md`.

Codex custom-agent files are generated into `.codex/agents/*.toml` from the Claude `agents/*.md` files. Keep `agents/*.md` authoritative, run `python3 scripts/convert-agents-to-codex.py` after agent edits, and verify with `python3 scripts/validate-codex-agents.py`. Do not hand-maintain generated TOML unless the converter is updated too. Current Codex plugin manifests do not declare agents directly; `.codex/agents/` is the compatibility/import layer.
