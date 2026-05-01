# psy — Psychological Consultation Plugin

A Claude Code and Codex plugin for professional psychologists — structured intake interviews, ICD-11 diagnosis formulation, session documentation, progress tracking, and evidence-based therapeutic practices.

## Language support

The plugin uses a **dual-layer language model**:

- **Skills and research** — always in English (internal reference material)
- **Output** (case files, session notes, clinical documents, agent responses) — in **your preferred language**

On first use, any agent will ask: *"What language should I use for clinical documents and session notes?"* Your choice is saved to `cases/.config.md` and used by all agents automatically. You can change it at any time.

Clinical terms (ICD-11 codes, scale names like PHQ-9, technique names like "cognitive restructuring") stay in English with a local-language explanation on first use — so you can reference standard literature regardless of output language.

## Install in Codex

Codex plugin ID: `psy`. Claude Code plugin ID: `psy`.

From the GitHub marketplace:

```bash
codex plugin marketplace add crankshift/psypowers
```

From a local checkout:

```bash
cd /path/to/psypowers
codex plugin marketplace add .
```

After adding the marketplace, enable `psy` in the Codex plugin UI / marketplace flow. Codex reads instructions from `AGENTS.md`; Claude Code reads `CLAUDE.md`.

Codex custom-agent files are included in `.codex/agents/`. They are generated from `agents/*.md`, so update the Markdown source first and run the repo-level converter/validator before release.


## Agents

Subagents handle complex clinical workflows. Use them by name with the `psy:` prefix.

| Agent | Description | Use when… |
|---|---|---|
| `intake-interviewer` | Structures initial client assessment — demographics, presenting complaints, history, risk screening | Starting work with a new client |
| `session-conductor` | Structures therapy sessions — agenda, interventions, observations, homework | Conducting or documenting a session |
| `diagnosis-formulator` | Formulates working diagnosis using ICD-11 — differential, comorbidities, clinical reasoning | Formulating or reviewing a diagnosis |
| `treatment-planner` | Creates treatment plans — SMART goals, modality selection, timeline, outcome criteria | Planning a course of treatment |
| `progress-analyzer` | Analyzes progress/regression — score trends, goal attainment, plateau detection | Reviewing client progress across sessions |
| `practice-recommender` | Recommends therapeutic techniques matched to diagnosis, goals, and current progress | Selecting interventions or homework exercises |
| `case-notes-drafter` | Drafts clinical documentation — SOAP/DAP notes, referral letters, discharge summaries | Preparing professional documentation |
| `crisis-assessor` | Assesses acute risk — suicidality, self-harm, safety planning, escalation | Evaluating a client in crisis |

## Skills

Skills provide reference material and are triggered automatically by context.

### Utility skills

| Skill | Description |
|---|---|
| `icd11-classification` | ICD-11 Chapter 06 mental health codes, diagnostic criteria, differential diagnosis aids |
| `assessment-scales` | Standardized psychometric instruments — PHQ-9, GAD-7, PCL-5, BDI-II, WHO-5, C-SSRS, and more |
| `session-structuring` | Frameworks for organizing therapy sessions by modality and session type |
| `progress-measurement` | Methods for tracking therapeutic outcomes — RCI, GAS, plateau detection |

### Modality skills

| Skill | Description |
|---|---|
| `cbt-techniques` | Cognitive Behavioral Therapy — cognitive restructuring, behavioral activation, exposure |
| `dbt-techniques` | Dialectical Behavior Therapy — mindfulness, distress tolerance, emotion regulation, interpersonal effectiveness |
| `act-techniques` | Acceptance and Commitment Therapy — six core processes, metaphors, values work |
| `mindfulness-practices` | Mindfulness and meditation — breath work, body scan, grounding, compassion, RAIN |
| `somatic-practices` | Body-based techniques — somatic experiencing, window of tolerance, vagal toning, TRE |
| `art-therapy-practices` | Creative/expressive therapy — visual art, collage, writing, music, clay |
| `emdr-protocols` | EMDR 8-phase protocol — bilateral stimulation, SUD/VOC, cognitive interweave |
| `psychodynamic-techniques` | Psychodynamic interventions — transference, defense mechanisms, object relations |
| `positive-psychology` | Positive psychology — VIA strengths, gratitude, flow, PERMA model |
| `crisis-intervention` | Crisis protocols — C-SSRS, Stanley-Brown safety plan, de-escalation, mandated reporting |

## Client case files

Agents create and maintain structured markdown files per client in your working directory:

```
cases/
└── {client-id}/
    ├── intake.md              # Initial assessment
    ├── diagnosis.md           # Working diagnosis (ICD-11)
    ├── treatment-plan.md      # Goals, modalities, timeline
    ├── progress.md            # Running progress log with metrics
    └── sessions/
        └── YYYY-MM-DD.md      # Individual session notes
```

## Disclaimer

This plugin is a **clinical support tool for professional psychologists**. It does not replace clinical judgment, supervision, or ethical obligations. All outputs are working drafts that must be reviewed by a qualified mental health professional. In crisis situations, always follow your professional training and local emergency protocols.
