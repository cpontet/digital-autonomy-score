---
name: das
description: |
  Run a Digital Autonomy Score (DAS) assessment on a codebase.
  Analyses sovereignty and portability across all architectural layers
  and produces a structured report with scores, quadrant placement,
  Mermaid chart, Wardley Map, and remediation recommendations.
argument-hint: "[path-or-repo-url]"
---

# Digital Autonomy Score Assessment

Run a full DAS assessment using the **das-assessor** agent.

## Target

$ARGUMENTS

If no argument was provided, assess the **current working directory**.

If a path was provided, assess the codebase at that path.

If a GitHub URL was provided, clone it first then assess.

## Instructions

Use the Task tool to launch the **das-assessor** agent with this prompt:

> Run a full DAS assessment on the codebase. Follow your orchestration steps:
> conduct the context interview, launch the scanner, launch the scorer,
> conduct the gap-fill interview if needed, launch the reporter, and
> present the full structured report to the user.

After the agent completes, present the full report to the user.

When the agent finishes, it will offer a complementary **SEAL assessment** (EU Cloud
Sovereignty Framework). You can also run that separately at any time with `/seal`.
