---
name: eu-regulatory
user-invocable: false
description: |
  EU regulatory context for DAS assessments. Covers GDPR, NIS2, DORA,
  Cyber Resilience Act, EUCS, and Schrems II implications for sovereignty
  scoring and recommended actions.
---

# EU Regulatory Context for DAS Assessments

This skill provides a structured reference of EU regulations and legal frameworks
relevant to digital sovereignty assessments. It is intended for use by the DAS
assessor agent during scoring and recommendation generation.

---

## How to Use This Reference

- **Flags**: reference this skill when writing Flags to cite specific regulations, articles, and legal obligations that apply to the assessed codebase
- **Recommended Actions**: ground recommendations in concrete legal requirements rather than abstract sovereignty concerns
- **S1 scoring**: when regulatory obligations apply (e.g., the codebase processes personal data, serves a regulated sector, or targets the EU market), use the guidance below to inform and justify Legal & Jurisdictional (S1) scores
- Cross-reference with the **vendor-db** skill to combine vendor jurisdiction data with regulatory exposure

---

## GDPR (General Data Protection Regulation)

**Regulation (EU) 2016/679** — in force since 25 May 2018.

### Key Requirements Relevant to DAS

- **Data residency**: personal data transfers outside the EU/EEA require a valid legal mechanism (Art. 44-49)
- **Transfer mechanisms**: Standard Contractual Clauses (SCCs, Art. 46(2)(c)), Binding Corporate Rules (BCRs, Art. 47), adequacy decisions (Art. 45). These are legal safeguards but do not prevent government access under foreign surveillance laws
- **Processor obligations**: data processors must provide sufficient guarantees of compliance (Art. 28); sub-processor chains must be transparent
- **Data Protection Impact Assessments**: required for high-risk processing (Art. 35); hosting jurisdiction is a factor

### Impact on Scoring

- Systems processing personal data on infrastructure in non-adequate jurisdictions receive an S1 penalty
- US-hosted personal data processing: S1 capped at 2 (even with SCCs, due to Schrems II — see below)
- EU-hosted but US-headquartered provider: S1 capped at 3-5 (CLOUD Act exposure remains)

### Detection Signals

- User databases, authentication stores, session management
- Analytics and tracking (user behaviour data)
- Logging with PII (IP addresses, user agents, usernames)
- Contact forms, newsletter subscriptions, CRM integrations
- Health data, financial records, employment data (special categories under Art. 9)

---

## NIS2 (Network and Information Security Directive)

**Directive (EU) 2022/2555** — transposition deadline: 17 October 2024.

### Scope

Applies to **essential entities** and **important entities** across sectors including:

- Energy, transport, banking, financial market infrastructure, health
- Drinking water, waste water, digital infrastructure
- ICT service management (B2B), public administration
- Postal services, waste management, chemicals, food, manufacturing
- Digital providers (online marketplaces, search engines, social networks)

### Key Requirements

- **Supply chain security** (Art. 21(2)(d)): entities must address security risks in their supply chain and relationships with direct suppliers
- **Incident reporting** (Art. 23): significant incidents must be reported within 24 hours (early warning) and 72 hours (full notification)
- **Risk management** (Art. 21): appropriate technical, operational, and organisational measures

### Impact on Scoring

- If the codebase serves a NIS2-covered sector, dependency on non-sovereign infrastructure represents higher risk
- Supply chain provisions mean that third-party vendor jurisdiction matters even for internal tools
- Non-EU cloud dependency for a NIS2-covered entity should trigger a flag

### Status

- Member states were required to transpose by October 2024; implementation varies across the EU
- Enforcement and penalties: up to 10M EUR or 2% of global turnover for essential entities

---

## DORA (Digital Operational Resilience Act)

**Regulation (EU) 2022/2554** — applies from 17 January 2025.

### Scope

Applies to **financial entities**:

- Credit institutions, payment institutions, investment firms
- Insurance and reinsurance undertakings
- Crypto-asset service providers
- ICT third-party service providers to financial entities

### Key Requirements

- **ICT risk management** (Art. 6-16): comprehensive framework for identifying, protecting, detecting, responding to, and recovering from ICT-related incidents
- **Third-party risk / concentration risk** (Art. 28-30): financial entities must assess and manage ICT third-party concentration risk; contractual requirements for ICT providers
- **Operational resilience testing** (Art. 24-27): regular testing including threat-led penetration testing for significant entities
- **Incident reporting** (Art. 17-23): major ICT-related incidents must be reported to competent authorities

### Impact on Scoring

- Financial sector codebases with heavy reliance on a single US cloud provider should be flagged for ICT concentration risk
- Multi-provider and multi-cloud strategies are effectively mandated for significant financial entities
- Contractual requirements under Art. 28-30 require explicit provisions on data location, processing, and audit rights

---

## EU Cyber Resilience Act (CRA)

**Regulation (EU) 2024/2847** — phased application from 2025-2027.

### Scope

Applies to **products with digital elements** placed on the EU market — hardware and software with a network connection or data processing capability.

### Key Requirements

- **Secure by design**: cybersecurity requirements must be met throughout the product lifecycle
- **Vulnerability handling**: manufacturers must have coordinated vulnerability disclosure processes
- **SBOM requirements**: technical documentation must include a Software Bill of Materials
- **Security updates**: free security patches for the expected product lifetime (minimum 5 years)
- **Conformity assessment**: self-assessment for most products; third-party assessment for critical products

### Impact on Scoring

- Affects S2 (Technical Autonomy): projects need clear maintenance and vulnerability handling processes
- SBOM requirements strengthen the case for open-source and transparent dependency management
- Products without documented vulnerability processes or SBOM should be flagged

### Timeline

- September 2026: reporting obligations for manufacturers
- September 2027: full application of all requirements

### Note on Open Source

- **Non-commercial open-source stewards** (e.g., foundations) have lighter obligations: vulnerability handling and cooperation with authorities, but not full conformity assessment
- **Commercial use** of open-source components triggers full compliance obligations for the integrator
- Open-source developers contributing voluntarily are explicitly excluded from the scope

---

## EUCS (EU Cloud Certification Scheme)

**Status**: under development by ENISA (European Union Agency for Cybersecurity).

### Assurance Levels

| Level | Requirements | Intended Use |
|-------|-------------|--------------|
| **Basic** | Baseline security controls | Low-risk workloads |
| **Substantial** | Enhanced controls, third-party audit | Standard business use |
| **High** | Strictest controls; initially proposed to require EU-headquartered providers (sovereignty requirement) | Sensitive and public sector workloads |

### Sovereignty Requirement Controversy

- The original draft required "High" level cloud providers to be EU-headquartered and EU-controlled, with no foreign jurisdiction exposure
- This was controversial: some member states pushed back under pressure from US cloud providers
- The requirement may be watered down to a voluntary "sovereignty" label within the High level

### Impact on Scoring

- If EUCS High ultimately requires EU HQ, it validates the S1 scoring approach of penalising non-EU vendors for sensitive workloads
- Currently voluntary, but some member states (notably France) may mandate it for public sector procurement
- Watch for finalisation: the scheme's outcome directly affects the legitimacy of sovereignty-based scoring

---

## Schrems II and CLOUD Act Interaction

### Schrems II (CJEU C-311/18, 16 July 2020)

- **Invalidated** the EU-US Privacy Shield framework
- **Held** that US surveillance laws — specifically FISA Section 702 and Executive Order 12333 — are incompatible with EU fundamental rights (Art. 7, 8, 47 EU Charter)
- **Ruled** that SCCs remain valid but data exporters must conduct transfer impact assessments and implement supplementary measures where necessary
- **Established** that data protection authorities must suspend transfers if adequate protection cannot be ensured

### CLOUD Act (Clarifying Lawful Overseas Use of Data Act, 2018)

- US federal law requiring US-headquartered companies to produce data stored anywhere in the world in response to lawful US government requests
- Applies to the **corporate entity**, not the data storage location
- A US company storing data in Frankfurt is still subject to CLOUD Act demands

### Interaction

- Even with the **EU-US Data Privacy Framework (DPF)** adopted in July 2023, the CLOUD Act continues to apply to US corporate entities
- The DPF addresses government access under FISA 702 through an executive order (EO 14086) and a redress mechanism, but:
  - Executive orders can be revoked by future administrations
  - The redress mechanism has not been tested at scale
  - CLOUD Act access is separate from the intelligence surveillance addressed by DPF
- **This is why US-headquartered vendors score S1 <= 2** regardless of data centre location: the corporate chain of control remains under US jurisdiction

### Sovereign Cloud Programs

- Programs like **Bleu** (Microsoft + Orange/Capgemini), **S3NS** (Google + Thales), and **AWS EU Sovereign Cloud** attempt to break the corporate chain through joint ventures or operationally independent EU entities
- These are **partially effective**: S1 = 3-5, depending on the degree of legal and operational separation from the US parent
- Full sovereignty requires the operating entity to be outside US jurisdictional reach — difficult to guarantee when the technology stack is licensed from a US parent

---

## Regulatory Flag Templates

Ready-to-use flag text the agent can adapt when regulatory triggers are detected:

| Regulation | Trigger Condition | Flag Text Template |
|---|---|---|
| GDPR | Personal data + non-EU hosting | "GDPR Art. 44: personal data processed on [vendor] infrastructure subject to [jurisdiction] law; transfer mechanism review required" |
| NIS2 | Critical sector + US cloud dependency | "NIS2 supply chain risk: critical infrastructure component depends on [vendor] (US jurisdiction); concentration risk assessment recommended" |
| DORA | Financial sector indicators + single cloud | "DORA ICT concentration risk: [X]% of infrastructure on single provider [vendor]; multi-provider strategy required under DORA Art. 28-30" |
| CRA | Software product + missing SBOM | "CRA: product with digital elements lacks SBOM; vulnerability handling process undocumented" |
| Schrems II | Any US vendor with EU data | "Schrems II: [vendor] is US-headquartered; CLOUD Act applies regardless of EU data centre location; S1 capped at [score]" |
