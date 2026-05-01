# psypowers — monorepo

Monorepo hosting a psychological consultation plugin for **Claude Code**. One marketplace (`psypowers`) hosts the `psy` plugin which provides subagents and skills for clinical psychology practice support.

| Plugin | Command prefix | Documentation |
|---|---|---|
| [`psy`](./plugins/psy) | `/psy:…` | [`psy/README.md`](./plugins/psy/README.md), [`psy/CLAUDE.md`](./plugins/psy/CLAUDE.md) |

User-facing install instructions live in the root [`README.md`](./README.md). This file is for contributors working on the repo itself.

## Repository layout

```
psypowers/
├── README.md                       # user-facing — install guide
├── CLAUDE.md                       # this file — contributor context
├── CHANGELOG.md                    # monorepo-level structural log
├── .version-bump.json              # maps versioned fields in plugin/marketplace manifests
├── LICENSE                         # MIT
├── .claude-plugin/
│   └── marketplace.json            # marketplace catalog ("psypowers"); lists psy plugin
├── plugins/
│   └── psy/                        # plugin "psy" — psychological consultations
│       ├── README.md               # user-facing
│       ├── CLAUDE.md               # contributor context
│       ├── CHANGELOG.md            # plugin-level change log
│       ├── .claude-plugin/plugin.json
│       ├── agents/
│       └── skills/
└── site/                           # public landing page (static Astro site, not a plugin)
```

## Contribution principles

- **Evidence-based content only.** All therapeutic techniques, assessment scales, and diagnostic criteria must reference published clinical evidence. No fabricated protocols or invented assessment tools.
- **Language.** All plugin content, agents, skills, and documentation are in English.
- **Command prefixes come from plugin names.** `name` in `plugin.json` becomes the namespace — `/psy:…`. Agent and skill file names inside the plugin don't need a prefix; Claude Code adds it automatically.
- **Shared license.** MIT, applied at the repo root.
- **Release tags.** Tags are namespaced: `psy/vX.Y.Z`. The tag version always matches the plugin's `version` field exactly.

## Client case file structure

Agents read/write structured markdown files per client in the user's working directory:

```
cases/
└── {client-id}/
    ├── intake.md              # Initial assessment
    ├── diagnosis.md           # Working diagnosis (ICD-11)
    ├── treatment-plan.md      # Goals, modalities, timeline
    ├── progress.md            # Running progress log
    └── sessions/
        └── YYYY-MM-DD.md      # Individual session notes
```

The `cases/` directory is created by agents on first use. It lives in the user's working directory, not inside the plugin.

## Shared editorial rules

- **Evidence-based only.** All techniques must have published clinical evidence; cite source studies, meta-analyses, or clinical guidelines where possible.
- **No fabricated protocols.** Reference real assessment tools (PHQ-9, GAD-7, C-SSRS, etc.), real therapeutic models (CBT, DBT, ACT, etc.), and real diagnostic criteria (ICD-11).
- **Disclaimer on every agent output.** "This is a clinical support tool for professional psychologists. It does not replace clinical judgment, supervision, or ethical obligations."
- **Placeholders for client data.** Templates must use placeholders (`[client name]`, `[date of birth]`, `[client-id]`). Never commit real client data.
- **Fetch-first for ICD-11.** Agents and skills that reference diagnostic codes must attempt `WebFetch` from `icd.who.int` before using hardcoded references. Hardcoded values are annotated with `_(fallback; as of [date])_`.
- **Modality-neutral by default.** Agents don't push a single therapeutic modality; `practice-recommender` selects based on diagnosis and treatment plan.
- **Crisis safety.** `crisis-assessor` always recommends professional escalation for high/imminent risk; never suggests managing acute crises via AI alone.
- **Drafts, not clinical advice.** Everything agents produce is a working draft for a qualified psychologist to review. Final clinical responsibility is always human.

## Key resources

| Resource | URL | Usage |
|---|---|---|
| ICD-11 (Mental health) | [icd.who.int](https://icd.who.int/browse/2024-01/mms/en) | Diagnostic criteria, Chapter 06 |
| APA Practice Guidelines | [apa.org](https://www.apa.org/practice/guidelines) | Evidence-based treatment guidelines |
| NICE Guidelines (Mental Health) | [nice.org.uk](https://www.nice.org.uk/guidance/conditions-and-diseases/mental-health-and-behavioural-conditions) | Clinical recommendations |
| Cochrane Library | [cochranelibrary.com](https://www.cochranelibrary.com/) | Systematic reviews of interventions |

## Release flow

1. Bump version in two files listed in `.version-bump.json`: `plugins/psy/.claude-plugin/plugin.json:version` and `.claude-plugin/marketplace.json:plugins[0].version`.
2. Add a new section in `plugins/psy/CHANGELOG.md`.
3. Open a PR, merge.
4. Tag the merge commit: `git tag -a psy/vX.Y.Z <sha> -m "..."` + `git push origin psy/vX.Y.Z`.
5. Publish a GitHub Release with the CHANGELOG excerpt.
6. Users update: `/plugin marketplace update psypowers` + `/reload-plugins`.
