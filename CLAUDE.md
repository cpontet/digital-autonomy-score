# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code plugin** that implements the **Digital Autonomy Score (DAS)** — a methodology for assessing the digital sovereignty and portability of technology systems. The plugin provides agents, skills, and commands that analyse codebases and produce structured assessment reports.

The project also contains research materials and presentation content on digital sovereignty and geopolitics, written primarily in French.

## Repository Structure

```
.
├── agents/              # Agent definitions (Claude Code subagents)
│   ├── das-assessor.md  # Orchestrator — interviews user, coordinates sub-agents
│   ├── das-scanner.md   # Scans codebase for raw signals (IaC, deps, CI, config, source, docs)
│   ├── das-scorer.md    # Scores dimensions from signals + interview context
│   ├── das-reporter.md  # Generates final report with Mermaid chart, Wardley Map, actions
│   └── das-seal-assessor.md  # SEAL orchestrator — scores 8 EU Sovereignty Objectives (complement)
├── skills/              # Reference databases and output templates used by agents
│   ├── vendor-db/       # Vendor sovereignty lookup (detection patterns, S1/P2 guidance, alternatives)
│   ├── seal-framework/  # EU Cloud Sovereignty Framework (SOV-1..8 objectives, SEAL-0..4, scoring)
│   ├── governance-db/   # Open-source governance models (foundations, standards bodies → S3 scoring)
│   ├── migration-paths/ # Known migration paths with effort estimates (→ P5 scoring)
│   ├── region-jurisdiction/  # Cloud region → jurisdiction mapping (→ S1 scoring)
│   ├── eu-regulatory/   # EU regulatory context (GDPR, NIS2, DORA, EUCS, Schrems II)
│   ├── data-classification/  # Data type detection and regulatory mapping
│   ├── abstraction-patterns/ # Vendor abstraction layer detection heuristics
│   ├── remediation-playbook/ # Per-quadrant remediation guidance
│   ├── mermaid-das/     # Mermaid quadrantChart output template
│   └── wardley-das/     # Wardley Map (OWM syntax) output template
├── commands/            # Slash commands
│   ├── das.md           # /das command — entry point for running DAS assessments
│   └── seal.md          # /seal command — entry point for SEAL (EU framework) assessments
├── assessment/          # Methodology documentation (scales, process, reference assessments, SEAL)
│   └── seal-framework.md     # SEAL methodology (source of truth, synced with seal-framework skill)
├── presentation/        # Research content on digital sovereignty (French)
├── plugin.json          # Plugin manifest
└── CLAUDE.md            # This file
```

## How the Plugin Works

The plugin uses a multi-agent team coordinated by the **das-assessor** orchestrator:

1. The user runs `/das [path-or-url]` to trigger an assessment.
2. The **das-assessor** (orchestrator) runs a quick pre-scan, then **interviews the user** about business criticality, data sensitivity, and organisational factors that code analysis cannot reveal.
3. The **das-scanner** scans the target codebase for signals across 6 phases (IaC, dependencies, CI/CD, config, source, docs) and returns structured signal data.
4. The **das-scorer** takes the scan signals + interview context and scores each sub-dimension (S1–S3, P1–P5) with evidence and confidence levels.
5. The orchestrator reviews low-confidence scores and conducts a **gap-fill interview** — asking the user targeted questions about ambiguous findings.
6. If gap-fill answers are obtained, the **das-scorer** re-scores affected dimensions.
7. The **das-reporter** generates the final report: quadrant placement, Mermaid chart, Wardley Map, flags, and recommended actions.

Skills are reference databases that agents consult during their work — they are not invoked directly by users.

### SEAL Assessment (complement)

A second, complementary flow evaluates the system against the **EU Cloud Sovereignty Framework**:

1. The user runs `/seal [path-or-url]` (or accepts the offer at the end of a `/das` run).
2. The **das-seal-assessor** (orchestrator) runs a SEAL-specific context interview, then reuses the **das-scanner** for code signals.
3. It scores each of the **8 Sovereignty Objectives** (SOV-1…SOV-8) into a **SEAL level (0–4)** with evidence, computes an adapted weighted **Sovereignty Score (%)** and the **minimum SEAL**, and emits **recommendations to raise each objective's SEAL level**.
4. When invoked as a `/das` add-on, it reuses the DAS interview context and scan signals instead of re-collecting them.

This complements — and never replaces — the DAS Sovereignty (S) score.

## Key Methodology Concepts

- **Sovereignty (S)**: Legal exposure (S1, 40%), technical autonomy (S2, 30%), governance independence (S3, 30%). Cap: any sub-dimension <= 2 caps composite at 4.
- **Portability (CPS)**: Code (P1, 15%), data (P2, 30%), API (P3, 20%), operational (P4, 20%), migration (P5, 15%). Cap: any sub-dimension <= 2 caps composite at 4.
- **Weakest-link principle**: For multi-layer systems, system score = minimum across layers per dimension.
- **Conservative scoring**: When uncertain, score lower. Every score must cite evidence.
- **SEAL (EU Cloud Sovereignty Framework — complement)**: 8 Sovereignty Objectives (SOV-1 Strategic 15%, SOV-2 Legal 10%, SOV-3 Data & AI 10%, SOV-4 Operational 15%, SOV-5 Supply Chain 20%, SOV-6 Technology 15%, SOV-7 Security & Compliance 10%, SOV-8 Environmental 5%), each scored on a 5-level assurance scale (SEAL-0…SEAL-4). An objective's level is capped by its weakest material contributing factor. Adapted Sovereignty Score = Σ (SEALₙ/4) × Weightₙ. SOV-5, SOV-7, SOV-8 are dimensions DAS does not score. See `assessment/seal-framework.md`.

## Development Guidelines

- Assessment methodology docs live in `assessment/` — these are the source of truth for scoring rules and should stay in sync with agent instructions.
- Skills are standalone reference files — each `SKILL.md` should be self-contained with detection patterns, scoring guidance, and examples.
- The **das-scorer** agent embeds the full scoring rubric so it can operate without reading assessment docs at runtime.
- The **das-assessor** is the orchestrator — it handles user interaction and delegates scanning, scoring, and reporting to sub-agents via Task.
- Sub-agents (scanner, scorer, reporter) are stateless workers with strict input/output contracts. Only the orchestrator has `AskUserQuestion`.
- The `/das` command is a thin entry point — it spawns the orchestrator which coordinates everything.
- All assessment output uses structured markdown with Mermaid charts and OWM Wardley Map syntax.
- The **das-seal-assessor** is a second orchestrator (spawned by `/seal` or offered at the end of `/das`). It reuses the **das-scanner** and consults the **seal-framework** skill for the rubric, crosswalk, and report template. Keep `assessment/seal-framework.md` and the `seal-framework` skill in sync (objectives, SEAL levels, weights, adapted formula).
