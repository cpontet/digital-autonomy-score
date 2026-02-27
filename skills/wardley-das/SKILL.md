---
name: wardley-das
user-invocable: false
description: |
  Background knowledge for generating Wardley Maps in OWM (Online Wardley Maps)
  syntax from Digital Autonomy Score (DAS) results. Trigger when the DAS assessor
  needs to produce a Wardley Map showing component evolution and sovereignty risks.
---

# Wardley Map — DAS Visualization (OWM Syntax)

Generate a Wardley Map in OWM syntax so users can paste it into
[onlinewardleymaps.com](https://onlinewardleymaps.com) to render.

---

## OWM Syntax Reference

```
title Wardley Map — [System Name]

anchor User [0.97, 0.63]
component Component Name [visibility, maturity]
component Another Component [visibility, maturity]

Component Name->Another Component
Another Component->User

evolve Component Name 0.65
note Risk: low sovereignty [visibility, maturity]
```

Key syntax rules:
- `anchor` = visible user need (top of map)
- `component Name [visibility, maturity]` — both values 0–1
- `Name->Dependency` for links (no spaces around `->`)
- `evolve Name target_maturity` to show movement direction
- `note Text [visibility, maturity]` for annotations
- Blank lines separate logical groups

---

## DAS Layer → OWM Visibility Mapping

Place components vertically based on their architectural layer:

| Layer | Visibility Range |
|-------|:----------------:|
| Presentation | 0.85–0.95 |
| Application | 0.65–0.80 |
| Data | 0.45–0.60 |
| Integration | 0.35–0.50 |
| Infrastructure | 0.15–0.30 |
| Operations | 0.05–0.20 |

Pick a specific value within the range. Stagger components in the same layer to avoid overlap.

---

## Component → Evolution Stage (Maturity) Mapping

Use S2 (Technical Autonomy) and S3 (Governance Independence) scores as indicators:

| Condition | Evolution Stage | Maturity Range |
|-----------|----------------|:--------------:|
| Proprietary SaaS, no alternatives | Genesis/Custom | 0.10–0.30 |
| Emerging OSS, few alternatives | Custom | 0.20–0.40 |
| Mature OSS, multiple vendors | Product | 0.50–0.70 |
| Industry standard, ubiquitous | Commodity | 0.75–0.95 |

---

## Sovereignty Overlay

- Components with S1 ≤ 3 positioned at Genesis/Custom → add `evolve` arrow to show desired migration + `note` with risk
- Components with S ≥ 7 → no action needed (mark as sovereign in notes if helpful)

---

## Generation Steps

1. List all significant components detected during the scan.
2. Assign each component a layer (→ visibility) and evolution stage (→ maturity).
3. Draw dependency links between components.
4. Add `evolve` arrows for components that need sovereignty improvement.
5. Add risk notes for components with S1 ≤ 3.

---

## Common Mistakes to Avoid

1. **Visibility/maturity out of range.** Both values must be 0–1.
2. **Spaces around arrows.** Use `A->B`, not `A -> B`.
3. **Missing anchor.** Every map needs at least one `anchor` at the top.
4. **Overlapping components.** Stagger visibility values within a layer range to keep the map readable.
5. **Forgetting evolve arrows.** Components with low sovereignty scores (S1 ≤ 3) should have `evolve` to show the target state.
