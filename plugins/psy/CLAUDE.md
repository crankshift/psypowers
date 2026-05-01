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

## Fetch-first for diagnostic codes

Skills and agents that embed ICD-11 codes must include a **fetch-first block**: attempt `WebFetch` from `icd.who.int` before falling back to hardcoded values. Hardcoded values are annotated with `_(fallback; as of [date])_`.

## Output character

All plugin outputs are **working drafts for a qualified psychologist** to review, not final clinical documents or therapeutic advice to clients. The human clinician bears all professional responsibility.

## Crisis safety

The `crisis-assessor` agent and `crisis-intervention` skill always recommend professional escalation for high or imminent risk. The plugin never suggests managing acute crises via AI alone. Every crisis-related output includes a disclaimer that professional judgment and local emergency protocols take precedence.

## Codex support

This plugin also has Codex support. Keep `AGENTS.md` and `.codex-plugin/plugin.json` in sync with this Claude-facing file and `.claude-plugin/plugin.json` when user-visible behavior changes. Claude Code continues to use the existing Claude plugin ID; Codex may use a collision-safe ID documented in `AGENTS.md`.
