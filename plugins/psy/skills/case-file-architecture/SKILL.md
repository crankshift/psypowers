---
name: case-file-architecture
description: Use before creating, editing, renaming, or choosing locations for case files, session notes, progress logs, safety plans, clinical documents, or workspace-specific markdown logs. Enforces one-artifact-one-role ownership, prevents mixing metrics with narrative notes, and respects local AGENTS.md/README file maps.
---

# case-file-architecture

Psypowers agents maintain structured clinical case files. Each markdown artifact has one primary role. Do not mix roles in one file, and do not invent new file naming patterns when an existing artifact owner is defined.

Use this skill before any write that affects case files, session files, progress logs, safety plans, clinical documents, or workspace-specific markdown logs.

## Core Rule

One artifact has one source-of-truth role.

Before writing:

1. Identify the artifact type: intake, diagnosis, treatment plan, progress analysis, session note, safety plan, derived note, external document, worksheet/homework record, or local workspace log.
2. Read local project instructions first: `AGENTS.md`, `CLAUDE.md`, README file maps, or existing templates in the working directory.
3. If local instructions define file ownership, follow them.
4. Otherwise use the canonical Psypowers case-file ownership below.
5. If the content belongs to multiple artifact types, split it into the correct files instead of combining it.
6. If ownership remains ambiguous after reading local instructions and canonical ownership, ask the user or psychologist before writing.

## Canonical Psypowers Ownership

Use this structure when the workspace follows the standard Psypowers clinical case layout:

```text
cases/
└── {client-id}/
    ├── intake.md
    ├── diagnosis.md
    ├── treatment-plan.md
    ├── progress.md
    ├── safety-plan.md
    ├── sessions/
    │   └── YYYY-MM-DD.md
    ├── notes/
    │   └── YYYY-MM-DD-[type].md
    └── documents/
        └── YYYY-MM-DD-[type].md
```

| Artifact | Owns | Must not own |
|---|---|---|
| `intake.md` | Baseline intake data, presenting problem, history, risk screening, initial assessment recommendations | Session-by-session updates, longitudinal trend analysis, treatment plan revisions |
| `diagnosis.md` | Working diagnostic formulation, differential diagnosis, diagnostic confidence, review triggers | Session diary, treatment goals, progress score tables |
| `treatment-plan.md` | Goals, modalities, timeline, measurable targets, review schedule, goal revision history | Raw session narrative, assessment score trends, formal notes |
| `progress.md` | Aggregate progress analysis, score trends, goal progress, plateau/regression alerts, intervention response patterns | Full session narratives, raw diary entries, standalone session notes |
| `sessions/YYYY-MM-DD.md` | Date-specific session narrative, observations, interventions, homework, risk notes, assessment scores administered that session | Longitudinal trend analysis, full progress reports, external formal documents |
| `safety-plan.md` | Active safety plan and safety contacts/actions | General session narrative, progress analysis, unrelated treatment plan content |
| `notes/YYYY-MM-DD-[type].md` | Derived session-specific notes such as SOAP, DAP, or narrative note drafts | Source-of-truth session history, progress analysis |
| `documents/YYYY-MM-DD-[type].md` | External/formal documents such as referral letters, progress reports, discharge summaries | Raw case data, session source notes |

## Local Workspace Maps

Some workspaces adapt Psypowers for private self-work, supervision prep, journaling, or other non-standard layouts. If local instructions define a map such as `logs/`, `worksheets/`, `sessions/`, or custom templates, treat that map as the artifact contract for that workspace.

Examples:

- Daily metrics belong in the file designated for daily check-ins or progress metrics.
- Date-specific narrative belongs in the file designated for daily logs or session notes.
- CBT thought records belong in the worksheet or thought-record artifact, not in the daily metrics file.
- Weekly summaries belong in the weekly review or progress review artifact.

Do not force such workspaces into `cases/{client-id}/` unless the user asks to migrate to the canonical clinical case layout.

## Split Mixed Content

When a request combines multiple kinds of content, split by ownership:

| Mixed request includes | Write to |
|---|---|
| A session narrative plus assessment scores from that session | `sessions/YYYY-MM-DD.md` |
| Assessment scores across multiple dates plus trend interpretation | `progress.md` |
| A formal SOAP/DAP note based on a session | `notes/YYYY-MM-DD-soap.md` or `notes/YYYY-MM-DD-dap.md` |
| A crisis assessment plus safety plan | Crisis section in current session file, plus `safety-plan.md` if a safety plan is created |
| Daily numeric ratings plus daily narrative in a local self-work workspace | Local daily metrics artifact plus local dated narrative log |

Reference rather than duplicate. For example, a progress report may summarize session themes and cite session dates, but it should not copy full session narratives.

## Before-Writing Checklist

- Have I read the local instructions or existing file map?
- Can I name the artifact type in one phrase?
- Does the target file already own this type of content?
- Am I duplicating a full narrative where a reference would be enough?
- Am I mixing raw source data with aggregate analysis?
- If I am creating a new file pattern, is there no existing owner and is the pattern consistent with the workspace?

If any answer is uncertain, stop and clarify before writing.
