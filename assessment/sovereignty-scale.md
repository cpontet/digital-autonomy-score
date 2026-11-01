# DAS Sovereignty Scale

## Design Rationale

The DAS sovereignty scale addresses several challenges that arise when attempting to score sovereignty on a single 0–10 axis:

### Who Can Change the License Matters More Than the License

**A copyleft license does not stop its copyright holder.** MongoDB was AGPL before it moved to SSPL in 2018; Terraform was MPL before it moved to BSL in 2023. In both cases a single company held all the copyright, through a Contributor License Agreement (CLA), and could relicense future versions at will. Linux, by contrast, can never be relicensed: its copyright is spread across thousands of contributors who never assigned it.

The open-source band of the scale is therefore ordered by three questions, in this order:

1. **Can a single party relicense?** If one company holds all the copyright, the project sits at 5 whatever its license.
2. **Who governs the roadmap?** One company or a US-domiciled foundation (6), or an EU/neutral body or a multi-vendor community no one controls (7).
3. **Is the license copyleft?** Only among projects no one can relicense does the license type make the difference (8): copyleft then prevents anyone from enclosing the commons with closed derivatives, which permissive licenses (MIT, BSD, Apache) allow.

Every OSI license, copyleft or permissive, gives you the right to fork the last open version — which is how OpenSearch, OpenTofu and Valkey came about. That is why all of open source sits above source-available (4).

### Three Independent Dimensions

Sovereignty risk comes from three distinct sources — **jurisdiction**, **licensing**, and **governance** — that do not always move together. A technology can be open-source yet governed by a US entity, or proprietary yet EU-headquartered. The headline scale below provides a combined view; the sub-dimensions (S1–S3) allow precise analysis when these dimensions diverge.

### Governance Matters

*Who controls the project's evolution* has a direct impact on sovereignty. The Linux Foundation is a US entity; the Eclipse Foundation is based in Belgium. This distinction matters enormously for long-term sovereignty and is explicitly captured in sub-dimension S3.

### Infrastructure vs. Application Choices

Foundational infrastructure standards (HTTP, TCP/IP, SMTP) score 10 for sovereignty because they are governed multilaterally and cannot be captured. However, organizations don't "choose" these the way they choose application software — DAS assessments typically focus on decision-relevant technology choices.

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
| **5** | Open-Source, Single Owner | OSI license, but one company holds all the copyright (CLA or copyright assignment) and can relicense future versions. The license type does not change this. | MySQL (GPL, Oracle), Qt (LGPL, The Qt Company), Grafana (AGPL, Grafana Labs), TensorFlow (Apache 2.0, Google), MongoDB before 2018 (AGPL), Terraform before 2023 (MPL) |
| **6** | Open-Source, Controlled Governance | No single party can relicense (copyright spread across contributors or held by a foundation), but the roadmap is controlled by one company or by a US-domiciled foundation. | Kubernetes (CNCF), OpenSearch, OpenTofu and Valkey (Linux Foundation), Firefox (MPL, Mozilla), Nextcloud (AGPL, DCO, roadmap set by Nextcloud GmbH) |
| **7** | Open-Source, Independent Governance | No single party can relicense, and governance sits with an EU or jurisdiction-neutral body, or with a multi-vendor community no single company controls. Permissive license. | Eclipse projects (Eclipse Foundation, Belgium), PostgreSQL (PGDG) |
| **8** | Open-Source, Independent Governance, Copyleft | As 7, under a copyleft license (GPL, AGPL, EUPL; MPL and LGPL at file or library level). Improvements must stay open: the project can be neither relicensed nor enclosed. | Linux (GPL-2.0), LibreOffice (MPL-2.0, The Document Foundation, Germany) |
| **9** | Federated Open Protocols | Open-source with strong licenses AND based on federated, open protocols with multiple independent implementations. No single entity can control the ecosystem. | Matrix protocol (multiple clients/servers), ActivityPub ecosystem (Mastodon, PeerTube, Pixelfed), XMPP |
| **10** | Ratified International Standards | Ratified by international standards bodies (IETF, W3C, ISO, OASIS). Governance is multilateral. Multiple independent implementations exist. | HTTP/2 (IETF RFC 7540), HTML5 (W3C), PDF (ISO 32000), SQL (ISO 9075), SMTP (IETF RFC 5321) |

### Scale Design Highlights

1. **Relicensing power first**: a project one company can relicense sits at 5, even under AGPL
2. **Governance next**: scores 6 vs. 7 distinguish company or US-foundation control from EU/neutral or community governance
3. **License last**: copyleft lifts a project from 7 to 8 only when no one can relicense it
4. **Score 9 requires federation**: both open protocol AND multiple independent implementations — no single entity can control the ecosystem
5. **Score 10 is multilateral**: specifically ratified *international* standards with multilateral governance (IETF, W3C, ISO)

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
| 5–6 | Open-source (any OSI license); can fork and self-host; but maintenance depends on the original vendor or a few maintainers |
| 7–8 | Open-source (any OSI license); active community; multiple maintainers; documented self-hosting; a fork would be viable |
| 9–10 | Multiple independent implementations; reference implementations available; can fully self-maintain with in-house skills |

The license type does not raise S2: every OSI license grants the right to run, modify and fork. Copyleft is credited in S3, where it protects against enclosure.

### S3: Governance Independence

*Who controls the technology's evolution, and who can change its license? Can the roadmap be influenced or blocked by a foreign entity?*

| Score | Criteria |
|:-----:|----------|
| 0 | Single private company controls roadmap; no external governance; US/authoritarian jurisdiction |
| 1–2 | Single company control but EU-based; or US company with open governance but veto power |
| 3–4 | Multi-stakeholder governance but dominated by one entity (e.g., Google in Kubernetes) |
| 5–6 | Foundation-governed (Apache, Linux Foundation) with broad contributor base but US-domiciled foundation |
| 7–8 | EU/neutral foundation governance (Eclipse Foundation, CERN); multiple major contributors; no single-entity veto |
| 9–10 | International standards body (IETF, W3C, ISO); multilateral governance; changes require broad consensus |

**Modifiers:**

- **Relicensing power**: one company holds all the copyright through a CLA or copyright assignment → S3 ≤ 4, whatever the license. It can relicense future versions, as MongoDB, HashiCorp, Elastic and Redis did.
- **Enclosure resistance**: copyleft license (GPL, AGPL, EUPL, MPL, LGPL) *and* copyright spread across contributors (no CLA, or DCO only) → S3 +1, up to 10. Improvements must stay open, and no one can take the project closed.

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
