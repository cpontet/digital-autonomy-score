# Assessment Process — Step-by-Step Guide

This document provides a structured, phased process for assessing the sovereignty and portability of technology systems. Follow phases sequentially; each phase builds on the previous.

---

## Phase 1: Scope & Inventory

**Goal:** Define what you're assessing and decompose it into scoreable layers.

### Step 1.1: Define the System Boundary

Answer these scoping questions:

- **What is the system?** (Name, purpose, business criticality)
- **Who uses it?** (Internal users, external customers, other systems)
- **What data does it process?** (Classification: public, internal, confidential, regulated)
- **Who is the vendor/maintainer?** (For each component)

### Step 1.2: Layer Decomposition

Break the system into standard layers. Not all layers apply to every system.

| Layer | Description | Questions |
|-------|-------------|-----------|
| **Presentation** | User interface, client applications | Web app? Native? Which framework? |
| **Application** | Business logic, APIs, services | Language? Framework? License? |
| **Data** | Databases, file storage, caches | What DB? Where hosted? Export formats? |
| **Integration** | Connections to other systems | Protocols? APIs? Vendor SDKs? |
| **Infrastructure** | Compute, networking, cloud services | Which provider? Region? IaC? |
| **Operations** | Monitoring, deployment, maintenance | Who operates? What skills needed? Managed service? |

### Step 1.3: Component Inventory

For each layer, list every significant component:

```
System: [Name]
Date: [Assessment date]
Assessor: [Name]

Layer: Presentation
  - Component: React SPA
    Vendor: Meta (open-source, MIT)
    Hosting: CDN (Cloudflare)

Layer: Application
  - Component: Spring Boot API
    Vendor: VMware/Broadcom (open-source, Apache 2.0)
    Hosting: AWS ECS

Layer: Data
  - Component: AWS Aurora (MySQL-compatible)
    Vendor: Amazon (proprietary managed service)
    Hosting: AWS eu-west-1

Layer: Integration
  - Component: Stripe Payment API
    Vendor: Stripe (US, proprietary)
    Protocol: REST/JSON, webhook
  - Component: SendGrid Email
    Vendor: Twilio (US, proprietary)
    Protocol: SMTP + proprietary API

Layer: Infrastructure
  - Component: AWS ECS + ALB
    Vendor: Amazon (US)
    IaC: Terraform

Layer: Operations
  - Component: Datadog monitoring
    Vendor: Datadog (US, proprietary SaaS)
```

---

## Phase 2: Quick Assessment

**Goal:** Fast-path screening in 30 minutes using three ceiling questions. Useful for triaging a large portfolio before investing in detailed assessment.

### The Three Ceiling Questions

Answer each question for the system as a whole. Each "No" sets a ceiling on the Composite Portability Score (CPS).

#### Question 1: Data Export

> **"Can you export ALL data today — completely, in a standard format, without the vendor's cooperation?"**

| Answer | Effect |
|--------|--------|
| **Yes** | No ceiling from this question |
| **Partial** (some data exportable, some not) | CPS ≤ 5 |
| **No** | CPS ≤ 3 |

*Why it matters:* If you can't get your data out, nothing else matters. Data gravity is the primary lock-in vector.

#### Question 2: Provider Alternatives

> **"Are there ≥ 3 independent service providers in the EU that can deliver an equivalent service?"**

| Answer | Effect |
|--------|--------|
| **Yes** (3+ viable EU alternatives) | No ceiling from this question |
| **Partial** (1–2 alternatives exist) | CPS ≤ 6 |
| **No** (no EU alternatives) | CPS ≤ 5 |

*Why it matters:* Provider diversity is a prerequisite for real portability. Without alternatives, portability is theoretical.

#### Question 3: Migration Feasibility

> **"Could your team migrate this system in < 12 months with existing budget and staff?"**

| Answer | Effect |
|--------|--------|
| **Yes** (under 6 months) | No ceiling from this question |
| **Possible** (6–12 months) | CPS ≤ 7 |
| **No** (12+ months or unknown) | CPS ≤ 6 |

### Quick Sovereignty Estimate

For sovereignty, use a simpler quick check:

| Question | If Yes → | If No → |
|----------|----------|---------|
| Is any component from a US/CLOUD Act vendor? | S ≤ 4 (if critical data involved) | — |
| Is any core component proprietary (source unavailable)? | S ≤ 5 | — |
| Is all hosting within the EU? | — | S ≤ 6 |

### Quick Quadrant Placement

Apply the lowest ceiling from each set of questions to get a (S, CPS) pair, and place on the quadrant (see [quadrant-and-actions.md](quadrant-and-actions.md)).

---

## Phase 3: Detailed Scoring

**Goal:** Apply the full sovereignty and portability sub-dimensions to each layer.

### Step 3.1: Score Each Layer

For each component identified in Phase 1, score all sub-dimensions:

**Sovereignty sub-dimensions** (see [sovereignty-scale.md](sovereignty-scale.md)):
- S1: Legal & Jurisdictional Exposure
- S2: Technical Autonomy
- S3: Governance Independence

**Portability sub-dimensions** (see [portability-scale.md](portability-scale.md)):
- P1: Code/Runtime Portability
- P2: Data Portability
- P3: API/Integration Portability
- P4: Operational Portability
- P5: Migration Feasibility

### Step 3.2: Scoring Template

```
System: [Name]
Layer: [Layer name]
Component: [Component name]

SOVEREIGNTY
  S1 Legal/Jurisdictional: [0-10] — [Brief rationale]
  S2 Technical Autonomy:   [0-10] — [Brief rationale]
  S3 Governance:           [0-10] — [Brief rationale]
  S_composite: [weighted score]

PORTABILITY
  P1 Code/Runtime:   [0-10] — [Brief rationale]
  P2 Data:           [0-10] — [Brief rationale]
  P3 API/Integration:[0-10] — [Brief rationale]
  P4 Operational:    [0-10] — [Brief rationale]
  P5 Migration:      [0-10] — [Brief rationale]
  CPS: [weighted score]
```

### Step 3.3: System-Level Aggregation

1. **Within each layer**: Compute composite sovereignty (S) and portability (CPS) per the weighted formulas
2. **Across layers**: System-level score = **minimum** per dimension across layers (weakest-link)
3. **Apply caps**: If any sub-dimension ≤ 2, cap the composite at 4

### Step 3.4: Validate Against Reference Assessments

Compare your scores to the [reference assessments](reference-assessments.md) for calibration. If your PostgreSQL scores wildly differently from the reference, re-examine your rationale.

---

## Phase 4: Quadrant Placement

**Goal:** Position the system on the sovereignty × portability prioritization matrix.

### Step 4.1: Plot the System

Using the system-level S_composite and CPS from Phase 3:

- **X-axis**: Sovereignty score (0–10)
- **Y-axis**: Composite Portability Score (0–10)
- **Threshold**: Midpoint at 5 divides the quadrants

### Step 4.2: Determine Quadrant

| Quadrant | Condition | Interpretation |
|----------|-----------|----------------|
| Green (top-right) | S ≥ 5 AND CPS ≥ 5 | Sovereign and portable — maintain |
| Blue (top-left) | S < 5 AND CPS ≥ 5 | Portable but not sovereign — migrate to sovereign alternative |
| Red (bottom-left) | S < 5 AND CPS < 5 | Not sovereign, not portable — urgent action needed |
| Yellow (bottom-right) | S ≥ 5 AND CPS < 5 | Sovereign but not portable — modernize for portability |

See [quadrant-and-actions.md](quadrant-and-actions.md) for detailed action playbooks.

---

## Phase 5: Recommendations

**Goal:** Translate quadrant position into actionable next steps.

### Step 5.1: Priority Ordering

Within each quadrant, prioritize systems by:

1. **Business criticality** (use Core Domain Charts to classify as Core, Supporting, or Generic)
2. **Data sensitivity** (regulated data → higher priority)
3. **Contract timeline** (upcoming renewals → act before renewal)
4. **Effort/impact ratio** (quick wins before long transformations)

### Step 5.2: Action Plan Template

```
System: [Name]
Quadrant: [Color]
Priority: [High / Medium / Low]
Current scores: S=[X], CPS=[Y]
Target scores: S=[X'], CPS=[Y']

Immediate actions (0-3 months):
  - [Action 1]
  - [Action 2]

Short-term actions (3-12 months):
  - [Action 1]
  - [Action 2]

Long-term actions (12+ months):
  - [Action 1]
  - [Action 2]

Key risks:
  - [Risk 1 and mitigation]

Decision record:
  - Reference ADR: [Link to Architecture Decision Record]
```

### Step 5.3: Portfolio View

When assessing multiple systems, create a portfolio scatter plot:

- Plot all systems on the quadrant
- Size each dot by business criticality
- Color-code by domain (Core, Supporting, Generic)
- Identify clusters and systemic patterns

Common portfolio patterns:
- **Cluster in Red**: Systemic vendor lock-in — consider platform-level migration
- **Cluster in Blue**: Good technical foundation but hosting/vendor risk — provider migration may address many systems at once
- **Spread across all**: Normal — prioritize by business criticality
