# Sovereignty Scale — Refined Assessment

## Critique of the Original Scale

The original sovereignty scale (0–10) in the presentation has several logical issues that prevent consistent, repeatable scoring:

### 1. License Ordering is Inverted

The original scale places GPL/AGPL (score 5) *below* MIT/BSD/Apache (score 7). This is backwards from a sovereignty perspective: **copyleft licenses prevent proprietary capture**. A GPL-licensed project cannot be taken proprietary by a vendor — it structurally preserves sovereignty. Permissive licenses (MIT, Apache) allow any party to create closed forks, reducing long-term sovereignty guarantees.

### 2. Duplicate and Conflated Entries

Mastodon appears at both score 5 ("GPL open-source") and score 9 ("EU-compliant open-source"). This reveals the scale conflates three independent dimensions — **jurisdiction**, **licensing**, and **standardization** — into a single axis, creating contradictions.

### 3. Non-Linear Comparison

Proprietary EU software (score 3) vs. open-source US-governed software (score 5–7) represents fundamentally different *kinds* of sovereignty risk. An EU proprietary vendor may be preferable to a US-governed open-source foundation depending on the threat model.

### 4. Missing Governance Dimension

The original scale ignores *who controls the project's evolution*. The Linux Foundation is a US entity; the Eclipse Foundation is based in Belgium. This distinction matters enormously for long-term sovereignty but is invisible in the original scale.

### 5. Infrastructure Standards at Score 10

Score 10 includes HTTP, TCP/IP, and SMTP — foundational infrastructure standards that organizations don't "choose" in the way they choose application software. This conflates infrastructure with decision-relevant technology choices.

---

## Refined Sovereignty Scale (0–10)

The refined scale corrects the ordering and provides clearer criteria. The key principle: **sovereignty increases as the risk of external parties controlling, restricting, or compelling access to your technology decreases**.

| Score | Category | Description | Examples |
|:-----:|----------|-------------|----------|
| **0** | Proprietary, CLOUD Act / Authoritarian | Proprietary software from a US (CLOUD Act) or authoritarian-state vendor. Data and operations subject to foreign government compulsion. | AWS, Azure, GCP, Oracle Cloud, Alibaba Cloud, Tencent Cloud, Kaspersky |
| **1** | Proprietary, Non-EU | Proprietary software from a vendor outside both the EU and CLOUD Act jurisdictions, but not subject to EU regulatory alignment. | Samsung, Rakuten, Atlassian (AU) |
| **2** | Proprietary, EU-Adjacent | Proprietary software from European but non-EU countries (UK, Switzerland, Norway). Partial regulatory alignment but outside EU jurisdiction. | Exoscale (CH), Deliveroo (UK), Visma (NO) |
| **3** | Proprietary, EU | Proprietary software from an EU-headquartered vendor. Subject to EU law, but source unavailable — dependency on vendor continuity. | OVHcloud (FR), SAP (DE), Dassault Systèmes (FR) |
| **4** | Source-Available | Source code is viewable but usage is restricted by non-open-source licenses (BSL, SSPL, Elastic License). Vendor can change terms; forks may be legally constrained. | Elasticsearch (SSPL→proprietary→AGPL journey), MongoDB (SSPL), HashiCorp (BSL) |
| **5** | Open-Source Permissive, US-Governed | Open-source with permissive license (MIT, BSD, Apache 2.0) but governance controlled by a US entity. Permissive license allows proprietary forks. | Kubernetes (CNCF/Linux Foundation), TensorFlow (Google/Apache 2.0), PostgreSQL (PGDG, US-based) |
| **6** | Open-Source Permissive, EU/Neutral Governance | Open-source with permissive license, governed by an EU or jurisdiction-neutral entity. Same license risk as score 5, but governance is outside US reach. | Eclipse IDE (Eclipse Foundation, Belgium), OpenSearch (Linux Foundation but Apache 2.0) |
| **7** | Open-Source Copyleft, Weak | Open-source with weak copyleft (LGPL, MPL). Modifications must stay open, but linking/embedding with proprietary code is permitted. Moderate enclosure resistance. | Firefox (MPL), GNU C Library (LGPL), Qt Framework (LGPL) |
| **8** | Open-Source Copyleft, Strong | Open-source with strong copyleft (GPL, AGPL). Derivative works must remain open-source. Strong structural protection against proprietary capture. | Linux (GPL), MySQL (GPL), Nextcloud (AGPL), Mastodon (AGPL) |
| **9** | Federated Open Protocols | Open-source with strong licenses AND based on federated, open protocols with multiple independent implementations. No single entity can control the ecosystem. | Matrix protocol (multiple clients/servers), ActivityPub ecosystem (Mastodon, PeerTube, Pixelfed), XMPP |
| **10** | Ratified International Standards | Ratified by international standards bodies (IETF, W3C, ISO, OASIS). Governance is multilateral. Multiple independent implementations exist. | HTTP/2 (IETF RFC 7540), HTML5 (W3C), PDF (ISO 32000), SQL (ISO 9075), SMTP (IETF RFC 5321) |

### Key Changes from Original

1. **GPL/AGPL moved from 5 → 8**: copyleft provides structural sovereignty protection
2. **MIT/Apache moved from 7 → 5–6**: permissive licenses allow proprietary capture
3. **Governance split introduced**: scores 5 vs. 6 distinguish US-governed from EU/neutral-governed projects
4. **Mastodon consolidated**: scores once at 8 (AGPL copyleft) — not duplicated
5. **Score 9 refined**: requires both open protocol AND multiple independent implementations
6. **Score 10 clarified**: specifically ratified *international* standards with multilateral governance

---

## Sub-Dimensions for Detailed Assessment

For thorough assessments, sovereignty breaks into three sub-dimensions. Each scored 0–10 independently, then combined.

### S1: Legal & Jurisdictional Exposure

*Where can data be compelled? What law governs the vendor relationship?*

| Score | Criteria |
|:-----:|----------|
| 0 | Data stored/processed in CLOUD Act or authoritarian jurisdiction; vendor subject to foreign government data demands |
| 1–2 | Data in non-EU jurisdiction without adequacy decision; limited legal protections |
| 3–4 | Data in jurisdiction with EU adequacy decision (e.g., Switzerland, Japan, South Korea); contractual protections in place |
| 5–6 | Data in EU jurisdiction; standard GDPR protections; vendor is EU-based but has US subsidiaries or dependencies |
| 7–8 | Data in EU jurisdiction; vendor has no dependencies on non-EU entities; no extraterritorial exposure |
| 9–10 | Data never leaves your infrastructure; no third-party access; fully self-hosted with EU-only supply chain |

### S2: Technical Autonomy

*Can you run, modify, and maintain the technology independently of any single vendor?*

| Score | Criteria |
|:-----:|----------|
| 0 | Fully vendor-managed SaaS; no access to source, configuration, or data export |
| 1–2 | Vendor-managed with limited configuration; data export possible but incomplete |
| 3–4 | Source-available or partial API access; could theoretically self-host but not practically supported |
| 5–6 | Open-source with permissive license; can fork and self-host; but limited community beyond original vendor |
| 7–8 | Open-source with copyleft; active community; multiple maintainers; documented self-hosting |
| 9–10 | Multiple independent implementations; reference implementations available; can fully self-maintain with in-house skills |

### S3: Governance Independence

*Who controls the technology's evolution? Can the roadmap be influenced or blocked by a foreign entity?*

| Score | Criteria |
|:-----:|----------|
| 0 | Single private company controls roadmap; no external governance; US/authoritarian jurisdiction |
| 1–2 | Single company control but EU-based; or US company with open governance but veto power |
| 3–4 | Multi-stakeholder governance but dominated by one entity (e.g., Google in Kubernetes) |
| 5–6 | Foundation-governed (Apache, Linux Foundation) with broad contributor base but US-domiciled foundation |
| 7–8 | EU/neutral foundation governance (Eclipse Foundation, CERN); multiple major contributors; no single-entity veto |
| 9–10 | International standards body (IETF, W3C, ISO); multilateral governance; changes require broad consensus |

### Combining Sub-Dimensions

**Default composite sovereignty score:**

```
S_composite = 0.40 × S1 + 0.30 × S2 + 0.30 × S3
```

S1 (Legal/Jurisdictional) is weighted highest because legal compulsion is the most acute sovereignty risk — it can override all technical safeguards.

**Override rule:** If any sub-dimension scores ≤ 2, the composite score is capped at 4 regardless of the formula result. A system cannot be sovereign if it has a critical weakness in any dimension.

---

## Worked Examples

### PostgreSQL (self-hosted on EU infrastructure)

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 9 | Self-hosted in EU; no third-party data access |
| S2: Technical Autonomy | 9 | Open-source (PostgreSQL License ≈ MIT); extremely mature; trivially self-hosted; large ecosystem |
| S3: Governance | 6 | PGDG is informal, US-based core team; no foundation veto risk but governance is US-centric |
| **Composite** | **8.1** | 0.40×9 + 0.30×9 + 0.30×6 = 8.1 |
| **Headline score** | **8** | |

### Microsoft 365

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 0 | US company, CLOUD Act applies, data stored globally |
| S2: Technical Autonomy | 0 | Proprietary SaaS, no source access, limited export |
| S3: Governance | 0 | Single company controls everything |
| **Composite** | **0** | All dimensions at 0 |
| **Headline score** | **0** | |

### Mastodon (self-hosted)

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 9 | Self-hosted in EU; federated — no central data store |
| S2: Technical Autonomy | 9 | AGPL; multiple active forks (Glitch, Hometown); well-documented self-hosting |
| S3: Governance | 8 | German non-profit (Mastodon gGmbH); ActivityPub is W3C standard; multiple independent implementations |
| **Composite** | **8.7** | 0.40×9 + 0.30×9 + 0.30×8 = 8.7 |
| **Headline score** | **9** | Rounded; federated protocol pushes toward top of scale |
