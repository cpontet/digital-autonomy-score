# EU Cloud Sovereignty Framework (SEAL) — Methodology

This document is the **source of truth** for the SEAL assessment methodology. It mirrors the
`seal-framework` skill (which the `das-seal-assessor` agent consults at runtime) and must stay
in sync with it. It adapts the **European Commission — Cloud Sovereignty Framework, Version
1.2.1 (Oct. 2025)** (DG Digital Services, Luxembourg) for assessing a *system / codebase*.

## Relationship to the DAS Sovereignty Scale

The SEAL assessment is a **complement** to the DAS Sovereignty (S) scale — it does **not**
replace it.

| | DAS Sovereignty (S) | SEAL (this document) |
|---|---|---|
| Question | "Can a foreign entity control, restrict, or compel access?" | "What assurance level does each EU sovereignty objective reach?" |
| Scale | 0–10, three sub-dimensions (S1–S3) | SEAL-0 to SEAL-4, eight objectives (SOV-1–SOV-8) |
| Origin | DAS methodology | EC procurement framework, adapted |
| New coverage | — | Adds Supply Chain (SOV-5), Security & Compliance (SOV-7), Environmental (SOV-8) |

Run `/das` for the portability-aware quadrant view; run `/seal` for the objective-by-objective
EU-framework view. The two share the same code scan (`das-scanner`) and interview context.

## The Two-Fold Assessment

The original framework is two-fold, and we preserve both parts:

1. **SEAL (Minimum Assurance Level)** — a SEAL level per objective. A tender sets a minimum
   SEAL per objective; failing it on any objective is disqualifying. We report the **minimum
   SEAL across objectives** as the equivalent signal.
2. **Sovereignty Score (Award Criterion)** — a weighted aggregate used to rank services. We
   compute an **adapted** version (see below).

## The 8 Sovereignty Objectives

| # | Objective | Focus |
|---|-----------|-------|
| SOV-1 | Strategic Sovereignty | Anchoring in the EU legal/financial/industrial ecosystem; ownership stability, governance influence. |
| SOV-2 | Legal & Jurisdictional Sovereignty | Legal environment, exposure to foreign authority, enforceability of rights. |
| SOV-3 | Data & AI Sovereignty | Control and independence of data assets and AI services within the EU. |
| SOV-4 | Operational Sovereignty | EU actors' ability to run, support, and evolve the technology independently. |
| SOV-5 | Supply Chain Sovereignty | Origin, transparency, and resilience of the technology supply chain. |
| SOV-6 | Technology Sovereignty | Openness, transparency, and independence of the technological stack. |
| SOV-7 | Security & Compliance Sovereignty | EU control over security operations, compliance, and resilience. |
| SOV-8 | Environmental Sustainability | Energy, dependency, and raw-material resilience over the long term. |

Each objective has explicit **contributing factors** — see the `seal-framework` skill,
Section 1, for the full list. The objective's SEAL level is set by its **weakest material
contributing factor** (weakest-link, mirroring the DAS cap rules).

## The 5 SEAL Levels

| Level | Name | Definition |
|:-----:|------|------------|
| SEAL-0 | No Sovereignty | Under exclusive control of non-EU third parties, governed entirely in non-EU jurisdictions. |
| SEAL-1 | Jurisdictional Sovereignty | EU law formally applies with limited practical enforceability; exclusive non-EU control. |
| SEAL-2 | Data Sovereignty | EU law applicable and enforceable, with material non-EU dependencies; indirect non-EU control. |
| SEAL-3 | Digital Resilience | EU actors exercise meaningful but not full influence; marginal non-EU control. |
| SEAL-4 | Full Digital Sovereignty | Complete EU control, subject only to EU law, no critical non-EU dependencies. |

## Weights and the Adapted Sovereignty Score

| Objective | Weight |
|-----------|:------:|
| SOV-1 Strategic | 15% |
| SOV-2 Legal & Jurisdictional | 10% |
| SOV-3 Data & AI | 10% |
| SOV-4 Operational | 15% |
| SOV-5 Supply Chain | 20% |
| SOV-6 Technology | 15% |
| SOV-7 Security & Compliance | 10% |
| SOV-8 Environmental Sustainability | 5% |
| **Total** | **100%** |

The original formula is:

```
Sovereignty Score = Σ (n=1..8)  [ Score(SOVn) / Max.Score(SOVn) ] × Weight(SOVn) %
```

`Score(SOVn)` is the points a tenderer earns on the SOV-tagged questionnaire — evidence we do
not have when assessing a codebase. We therefore **substitute the assessed SEAL level** as the
normalised objective score, with `Max = 4`:

```
Sovereignty Score % = Σ (n=1..8)  ( SEALₙ / 4 ) × Weightₙ
```

This adaptation must be stated explicitly wherever the score is reported. A SEAL-4 on every
objective yields 100%. The score is complementary to — and never overrides — the per-objective
SEAL levels and the minimum SEAL.

## Scoring Process

The `das-seal-assessor` agent:

1. Runs a quick pre-scan, then conducts a **SEAL context interview** for the factors code
   cannot reveal (ownership/financing, hardware/firmware origin, certifications, SOC location,
   energy mix, key control, AI hosting).
2. Delegates code scanning to **das-scanner** (reused from the DAS team).
3. Maps signals + interview answers to the 8 objectives via the **DAS→SOV crosswalk** and
   assigns each a SEAL level (0–4) using the **per-objective rubric**, with evidence and
   confidence. (Both live in the `seal-framework` skill.)
4. Conducts a **gap-fill interview** for low-confidence objectives.
5. Computes the adapted Sovereignty Score and the minimum SEAL.
6. Emits per-objective **recommendations to raise the SEAL level by one step**, grounded in the
   capping contributing factor and the `eu-regulatory` / `migration-paths` references.

## Conservative & Evidence-Based

As with DAS: when uncertain, score the lower SEAL level and mark confidence Low; every level
must cite a specific signal or interview answer. SOV-5, SOV-7, and SOV-8 will typically be Low
confidence without an interview, because code analysis cannot evaluate supply-chain origin,
security operations location, or energy usage.

## References

- European Commission, *Cloud Sovereignty Framework v1.2.1* (Oct. 2025) — `docs/Cloud-Sovereignty-Framework.pdf`.
- Draws on CIGREF Trusted Cloud Referential v2, Gaia-X policy rules, and the European
  Cybersecurity Certification Framework (ENISA, NIS2, DORA).
- See also: `sovereignty-scale.md` (DAS S-scale), `eu-regulatory` skill (GDPR/NIS2/DORA/CRA/EUCS).
