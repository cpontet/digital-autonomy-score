---
name: seal
description: |
  Assess a system against the EU Cloud Sovereignty Framework (SEAL).
  Scores a Sovereignty Effectiveness Assurance Level (SEAL-0 to SEAL-4) for each
  of the eight Sovereignty Objectives, computes the weighted Sovereignty Score and
  the minimum SEAL, and recommends actions to raise the SEAL level.
  Complements — does not replace — the Digital Autonomy Score (/das).
argument-hint: "[path-or-repo-url]"
---

# Cloud Sovereignty Framework (SEAL) Assessment

Run a SEAL assessment using the **das-seal-assessor** agent. This evaluates the system
against the European Commission Cloud Sovereignty Framework v1.2.1 (Oct. 2025) and is a
**complement** to the Digital Autonomy Score (`/das`).

## Target

$ARGUMENTS

If no argument was provided, assess the **current working directory**.

If a path was provided, assess the codebase at that path.

If a GitHub URL was provided, clone it first then assess.

## Instructions

Use the Task tool to launch the **das-seal-assessor** agent with this prompt:

> Run a full SEAL assessment on the codebase. Follow your orchestration steps:
> conduct the SEAL context interview, launch the scanner, score all eight Sovereignty
> Objectives (SOV-1 to SOV-8) into SEAL levels with evidence, conduct the gap-fill
> interview if needed, compute the weighted Sovereignty Score and the minimum SEAL,
> generate recommendations to raise each objective's SEAL level, and present the full
> structured report to the user.

After the agent completes, present the full report to the user.
