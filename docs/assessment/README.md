# Digital Autonomy Score (DAS)

## Purpose

The **Digital Autonomy Score (DAS)** is a structured, repeatable methodology for assessing the **digital sovereignty** and **portability** of technology components and systems. It refines and extends the original assessment scales from the [presentation material](../content/12-assessment-tools.md) into a comprehensive toolkit suitable for both manual expert assessment and future automated analysis.

## Why DAS?

The original 0–10 sovereignty and portability scales in the presentation are useful for building intuition, but contain logical inconsistencies that prevent reliable, repeatable scoring. DAS resolves those issues while preserving the core two-axis model and prioritization quadrant.

Key improvements:

- **Sovereignty scale**: corrected license ordering (copyleft scores higher than permissive, as it prevents proprietary capture), added governance dimension, removed duplicate entries
- **Portability scale**: expanded from code/runtime-only to five sub-dimensions covering data, APIs, operations, and migration feasibility
- **Composite scoring**: weakest-link principle ensures a system is only as portable as its least portable layer
- **Structured process**: phased assessment from quick screening to detailed analysis

## How to Use DAS

### Quick Assessment (30 minutes)

1. Read [assessment-process.md](assessment-process.md), Phase 2
2. Answer the three ceiling questions for your system
3. Place on the quadrant using [quadrant-and-actions.md](quadrant-and-actions.md)
4. Determine immediate action

### Thorough Assessment (half-day per system)

1. Follow all five phases in [assessment-process.md](assessment-process.md)
2. Use the detailed rubrics in [sovereignty-scale.md](sovereignty-scale.md) and [portability-scale.md](portability-scale.md)
3. Score each layer and sub-dimension
4. Place on the quadrant and develop action plans per [quadrant-and-actions.md](quadrant-and-actions.md)
5. Calibrate your scores against [reference-assessments.md](reference-assessments.md)

### Building Automated Tooling

See [automated-signals.md](automated-signals.md) for machine-detectable signals mapped to each sub-dimension, serving as the specification for a future DAS sub-agent.

## Document Index

| Document | Description |
|----------|-------------|
| [sovereignty-scale.md](sovereignty-scale.md) | Refined sovereignty scale with critique, corrected 0–10 scale, and three sub-dimensions (S1–S3) |
| [portability-scale.md](portability-scale.md) | Refined portability scale with five sub-dimensions (P1–P5), composite scoring formula, and weakest-link principle |
| [assessment-process.md](assessment-process.md) | Step-by-step guide: scope & inventory, quick screening, detailed scoring, quadrant placement, recommendations |
| [quadrant-and-actions.md](quadrant-and-actions.md) | Prioritization matrix with detailed action playbooks per quadrant |
| [reference-assessments.md](reference-assessments.md) | Worked examples of well-known technology stacks scored under the refined framework |
| [automated-signals.md](automated-signals.md) | Machine-detectable signals for each sub-dimension, specification for future DAS sub-agent |

## Relationship to Original Material

DAS builds on and replaces the assessment scales in [`docs/content/12-assessment-tools.md`](../content/12-assessment-tools.md). The original scales remain useful as teaching aids for building sovereignty intuition. DAS is the operational version for actual decision-making.

The strategic analysis tools (Wardley Mapping, Core Domain Charts, ADRs) described in the original material remain unchanged and complement DAS — they help identify *which* components to assess and *how* to act on results.
