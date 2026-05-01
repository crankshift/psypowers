# psypowers — monorepo

Monorepo hosting a psychological consultation plugin for **Claude Code and Codex**. One marketplace (`psypowers`) hosts the `psy` plugin which provides subagents and skills for clinical psychology practice support.

| Plugin | Command prefix | Documentation |
|---|---|---|
| [`psy`](./plugins/psy) | `/psy:…` | [`psy/README.md`](./plugins/psy/README.md), [`psy/CLAUDE.md`](./plugins/psy/CLAUDE.md) |

User-facing install instructions live in the root [`README.md`](./README.md). This file is for contributors working on the repo itself.

## Repository layout

```
psypowers/
├── README.md                       # user-facing — install guide
├── CLAUDE.md                       # this file — Claude Code contributor context
├── AGENTS.md                       # Codex contributor context (mirrors CLAUDE.md for Codex)
├── CHANGELOG.md                    # monorepo-level structural log
├── .version-bump.json              # maps versioned fields in plugin/marketplace manifests
├── LICENSE                         # MIT
├── .claude-plugin/
│   └── marketplace.json            # Claude Code marketplace catalog ("psypowers")
├── .agents/
│   └── plugins/
│       └── marketplace.json        # Codex marketplace catalog (psy)
├── scripts/
│   ├── release.sh                  # release helper (bump, prepare, publish)
│   ├── convert-agents-to-codex.py  # generates .codex/agents/*.toml from Claude agents/*.md
│   └── validate-codex-agents.py    # validates generated Codex agent TOML files
├── plugins/
│   └── psy/                        # plugin "psy" — psychological consultations
│       ├── README.md               # user-facing
│       ├── CLAUDE.md               # Claude Code contributor context
│       ├── AGENTS.md               # Codex contributor context
│       ├── CHANGELOG.md            # plugin-level change log
│       ├── .claude-plugin/plugin.json  # Claude Code manifest; name: "psy"
│       ├── .codex-plugin/plugin.json   # Codex manifest; name: "psy"
│       ├── .codex/agents/*.toml    # generated Codex custom-agent shims (from agents/*.md)
│       ├── agents/                 # source agent definitions (Claude + Codex source of truth)
│       └── skills/                 # skill definitions (shared by Claude Code and Codex)
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

All release steps are automated by `scripts/release.sh`. Requirements: `bash`, `git`, `gh` (authenticated), `jq`, `awk`, `claude` CLI.

### Quick reference

```bash
# 1. Prepare a release (bumps versions, creates branch, opens PR)
./scripts/release.sh prepare psy 0.2.0

# 2. After PR merges — tag and publish GitHub Release
./scripts/release.sh publish psy 0.2.0
```

### Step-by-step

1. **`./scripts/release.sh prepare psy <version>`** — from a clean `main`, creates branch `release-psy-v<version>`, bumps version in `plugins/psy/.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`, validates with `claude plugin validate`, prompts you to edit `plugins/psy/CHANGELOG.md`, commits, pushes, opens a PR.
2. **Review and merge the PR** on GitHub.
3. **`./scripts/release.sh publish psy <version>`** — pulls `main`, tags the merge commit as `psy/v<version>`, pushes the tag, creates a GitHub Release with the CHANGELOG excerpt.
4. **Users update:** `/plugin marketplace update psypowers` + `/reload-plugins`.

### Individual commands

| Command | What it does |
|---|---|
| `bump psy <version>` | Update version in plugin.json + marketplace.json, validate |
| `bump-marketplace <version>` | Update marketplace metadata.version only (catalog-shape changes) |
| `prepare psy <version>` | Full PR flow: branch → bump → changelog → commit → push → PR |
| `publish psy <version>` | Post-merge: tag → push tag → GitHub Release |

## Codex support

This repository also ships Codex plugin metadata. Keep Claude and Codex surfaces in sync when changing plugin structure.

- Claude marketplace: `.claude-plugin/marketplace.json`; Codex marketplace: `.agents/plugins/marketplace.json`.
- Claude plugin manifest stays in `plugins/psy/.claude-plugin/plugin.json`; Codex plugin manifest stays in `plugins/psy/.codex-plugin/plugin.json`.
- Claude contributor instructions live in `CLAUDE.md`; Codex contributor instructions live in `AGENTS.md`.
- Claude and Codex both use the plugin ID `psy`.
- When adding an agent, skill, or public install instruction, update README, CLAUDE.md, AGENTS.md, and both manifest families as applicable.
- Codex custom-agent files live in `plugins/*/.codex/agents/*.toml` and are generated from Claude `agents/*.md` files.
- After changing any agent frontmatter/body, run `python3 scripts/convert-agents-to-codex.py` and `python3 scripts/validate-codex-agents.py`.
- Do not hand-edit generated Codex agent TOML unless you also update the converter; Claude agent files remain the source of truth.
- Current Codex plugin manifests do not declare agents directly, so `.codex/agents/` is the compatibility/import layer.
