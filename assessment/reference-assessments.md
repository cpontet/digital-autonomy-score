# DAS Reference Assessments

These worked assessments provide calibration anchors for consistent scoring. When assessing a new system, compare your scores to similar reference cases. If your results diverge significantly, re-examine your rationale.

---

## 1. PostgreSQL on Linux VM (EU-hosted)

**System:** PostgreSQL 16 running on a Linux VM at an EU cloud provider (e.g., OVHcloud).

### Sovereignty Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 9 | Self-managed in EU data center; no third-party data access; EU jurisdiction |
| S2: Technical Autonomy | 9 | Open-source (PostgreSQL License ≈ MIT); trivially self-hosted; massive ecosystem; can maintain independently |
| S3: Governance | 6 | PostgreSQL Global Development Group (PGDG) is community-governed but informal and US-centric; no formal foundation in EU |
| **S_composite** | **8.1** | 0.40×9 + 0.30×9 + 0.30×6 = 8.1 → **8** |

### Portability Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| P1: Code/Runtime | 8 | Runs on virtually any OS; standard SQL interface |
| P2: Data | 8 | pg_dump provides full SQL export; logical replication; standard formats |
| P3: API/Integration | 9 | SQL (ISO 9075); standard wire protocol; hundreds of compatible tools |
| P4: Operational | 8 | Managed by every major EU cloud provider; abundant skills available |
| P5: Migration | 7 | Migration tools mature (pgloader, DMS); weeks for moderate databases |
| **CPS** | **8.1** | 0.15×8 + 0.30×8 + 0.20×9 + 0.20×8 + 0.15×7 = 8.05 → **8** |

**Quadrant: Green** (S=8, CPS=8) — Maintain and leverage.

---

## 2. Microsoft 365

**System:** Microsoft 365 (Exchange Online, SharePoint, Teams, OneDrive) as primary collaboration platform.

### Sovereignty Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 1 | US company, CLOUD Act applies; data residency options exist but Microsoft retains access capabilities; Schrems II concerns |
| S2: Technical Autonomy | 0 | Fully proprietary SaaS; no source access; no self-hosting; limited and incomplete data export |
| S3: Governance | 0 | Single company controls entire stack, roadmap, pricing, and terms |
| **S_composite** | **0.4** | 0.40×1 + 0.30×0 + 0.30×0 = 0.4 → **0** |

### Portability Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| P1: Code/Runtime | 0 | N/A — proprietary SaaS, not deployable |
| P2: Data | 3 | Partial export possible (PST for mail, OneDrive download); metadata/permissions/workflows lost; Teams data very hard to export |
| P3: API/Integration | 4 | Microsoft Graph API is well-documented but proprietary; SMTP/IMAP available for mail but Teams has no standard equivalent |
| P4: Operational | 0 | No self-hosting option; no EU-equivalent managed service |
| P5: Migration | 3 | 12–18 months for large organizations; extensive user retraining; workflow recreation |
| **CPS** | **2.15** | 0.15×0 + 0.30×3 + 0.20×4 + 0.20×0 + 0.15×3 = 2.15 → **2** |

**Quadrant: Red** (S=0, CPS=2) — Urgent: migrate or replace.

---

## 3. Self-Hosted GitLab CE

**System:** GitLab Community Edition, self-hosted on EU infrastructure, used for source code management, CI/CD, and issue tracking.

### Sovereignty Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 8 | Self-hosted in EU; data stays on your infrastructure; no external access |
| S2: Technical Autonomy | 7 | Open-source (MIT license); can self-host and maintain; active community; but GitLab Inc. (US) drives development |
| S3: Governance | 4 | GitLab Inc. is a US company controlling the roadmap; CE is MIT-licensed but feature disparity with EE grows; community influence is limited |
| **S_composite** | **6.5** | 0.40×8 + 0.30×7 + 0.30×4 = 6.5 → **6** |

### Portability Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| P1: Code/Runtime | 7 | Ruby/Rails app with good containerization; runs on standard Linux |
| P2: Data | 7 | Git repos are inherently portable; issues/MRs exportable via API; CI config in-repo (.gitlab-ci.yml needs adaptation) |
| P3: API/Integration | 6 | Comprehensive REST/GraphQL API; Git protocol standard; CI syntax proprietary |
| P4: Operational | 6 | Well-documented self-hosting; Omnibus package; but complex to operate at scale; fewer EU managed options |
| P5: Migration | 5 | Migration to alternatives (Gitea, Forgejo) possible in 3–6 months; Git repos trivial, CI pipelines and issues require rework |
| **CPS** | **6.3** | 0.15×7 + 0.30×7 + 0.20×6 + 0.20×6 + 0.15×5 = 6.3 → **6** |

**Quadrant: Green** (S=6, CPS=6) — Maintain; monitor GitLab Inc. governance.

---

## 4. Salesforce CRM

**System:** Salesforce Sales Cloud with extensive custom objects, Apex triggers, Process Builder workflows, and AppExchange integrations.

### Sovereignty Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 1 | US company, CLOUD Act applies; EU data residency available (Hyperforce) but Salesforce retains access |
| S2: Technical Autonomy | 0 | Proprietary SaaS; Apex is proprietary language; no source access; completely vendor-dependent |
| S3: Governance | 0 | Single company controls everything; no community governance |
| **S_composite** | **0.4** | 0.40×1 + 0.30×0 + 0.30×0 = 0.4 → **0** |

### Portability Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| P1: Code/Runtime | 1 | Apex/Visualforce/Lightning are proprietary; code cannot run outside Salesforce |
| P2: Data | 4 | Data Export service provides CSV; but custom objects, relationships, metadata, and automation rules are difficult to extract meaningfully |
| P3: API/Integration | 4 | REST/SOAP APIs available; but SOQL is proprietary; object model vendor-specific |
| P4: Operational | 0 | SaaS only; no self-hosting; no EU-equivalent platform |
| P5: Migration | 2 | 18+ months for complex implementations; requires complete re-implementation of business logic |
| **CPS** | **2.45** | 0.15×1 + 0.30×4 + 0.20×4 + 0.20×0 + 0.15×2 = 2.45 → **2** |

Cap applies: P4 = 0 (≤ 2), so CPS capped at 4. Actual formula gives 2.45, which is below cap anyway.

**Quadrant: Red** (S=0, CPS=2) — Urgent: migrate or replace.

---

## 5. Docker + Spring Boot + AWS Aurora (Composite Stack)

**System:** A Java Spring Boot application in Docker containers, deployed on AWS ECS, using AWS Aurora (MySQL-compatible) for data, with a React frontend served via CloudFront.

This example demonstrates the **weakest-link principle** for composite systems.

### Per-Layer Scoring

#### Presentation Layer: React SPA on CloudFront

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1 | 1 | CloudFront is AWS (US, CLOUD Act) |
| S2 | 8 | React is MIT open-source; SPA can be served from anywhere |
| S3 | 4 | React governed by Meta (US); but easy to replace with other frameworks |
| P2 | 9 | Static files; no data lock-in |
| P4 | 8 | Any CDN or static hosting works |

#### Application Layer: Spring Boot in Docker on ECS

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1 | 1 | Hosted on AWS (US, CLOUD Act) |
| S2 | 8 | Spring Boot is Apache 2.0; Docker is standard OCI |
| S3 | 5 | VMware/Broadcom governs Spring; mixed governance |
| P1 | 9 | Containerized with standard APIs |
| P4 | 6 | Runs on any Kubernetes/container platform, but ECS config is AWS-specific |

#### Data Layer: AWS Aurora MySQL-compatible

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1 | 0 | AWS proprietary service; CLOUD Act; data accessible by Amazon |
| S2 | 3 | Aurora-specific features (fast cloning, Aurora Serverless) have no equivalent; MySQL-compatible but not identical |
| S3 | 0 | AWS controls entirely |
| P2 | 4 | MySQL dump possible; but Aurora-specific features, performance characteristics, and configurations don't transfer |
| P4 | 2 | Aurora is AWS-only; migration to standard MySQL requires testing and performance profiling |
| P5 | 4 | 6–12 months to migrate to standard MySQL and re-validate performance |

### System-Level Scores (Weakest-Link)

| Dimension | Presentation | Application | Data | **System (min)** |
|-----------|:---:|:---:|:---:|:---:|
| S1 Legal | 1 | 1 | 0 | **0** |
| S2 Technical | 8 | 8 | 3 | **3** |
| S3 Governance | 4 | 5 | 0 | **0** |
| S_composite | — | — | — | 0.40×0 + 0.30×3 + 0.30×0 = **0.9 → 1** |

| Dimension | Presentation | Application | Data | **System (min)** |
|-----------|:---:|:---:|:---:|:---:|
| P1 Code | 8 | 9 | 5 | **5** |
| P2 Data | 9 | N/A | 4 | **4** |
| P3 API | 7 | 6 | 5 | **5** |
| P4 Ops | 8 | 6 | 2 | **2** |
| P5 Migration | 9 | 7 | 4 | **4** |
| CPS | — | — | — | 0.15×5 + 0.30×4 + 0.20×5 + 0.20×2 + 0.15×4 = **3.95 → 4** |

Cap applies: P4_system = 2 (≤ 2), CPS capped at 4 regardless.

**Quadrant: Red** (S=1, CPS=4) — Despite Docker containers and Spring Boot, the AWS Aurora dependency dominates.

**Key insight:** Containerization creates an *illusion* of portability. The real lock-in is in the data layer and infrastructure, not the application runtime.

---

## 6. Python/Flask on OVHcloud with ActivityPub

**System:** Public sector citizen portal with Python/Flask backend, React frontend, Docker containers on OVHcloud, using ActivityPub for some services.

### Sovereignty Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 9 | OVHcloud is French, EU jurisdiction; data in EU |
| S2: Technical Autonomy | 8 | Flask (BSD), React (MIT), Docker (Apache 2.0), ActivityPub (W3C); all open-source; can self-host entirely |
| S3: Governance | 7 | ActivityPub is W3C standard; Flask has Pallets Project governance (small but independent); OVHcloud is EU |
| **S_composite** | **8.1** | 0.40×9 + 0.30×8 + 0.30×7 = 8.1 → **8** |

### Portability Assessment

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| P1: Code/Runtime | 9 | Docker containers with standard web stack; runs anywhere |
| P2: Data | 7 | Assuming PostgreSQL with standard SQL; ActivityPub data is federated/standard |
| P3: API/Integration | 8 | ActivityPub is W3C standard; REST APIs; standard auth |
| P4: Operational | 7 | Docker on any cloud; OVHcloud has alternatives (Scaleway, IONOS); standard skills |
| P5: Migration | 7 | Weeks to move containers to another provider; data migration standard |
| **CPS** | **7.5** | 0.15×9 + 0.30×7 + 0.20×8 + 0.20×7 + 0.15×7 = 7.5 → **7** |

**Quadrant: Green** (S=8, CPS=7) — Sovereign and portable. Maintain and leverage.

---

## 7. Managed MongoDB Atlas on AWS (US Region)

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 0 | AWS US region; CLOUD Act; MongoDB Inc. is US-based |
| S2: Technical Autonomy | 4 | MongoDB was SSPL (source-available); community edition exists; can self-host |
| S3: Governance | 1 | MongoDB Inc. controls development and licensing decisions |
| **S_composite** | **1.5 → 2** | 0.40×0 + 0.30×4 + 0.30×1 = 1.5; cap doesn't further reduce |

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| P1: Code/Runtime | 6 | MongoDB runs on many platforms but requires its own runtime and management tooling |
| P2: Data | 5 | mongodump works but BSON format; schema-less means application-level dependencies; migration requires careful testing |
| P3: API/Integration | 3 | MongoDB query language is proprietary (not SQL); Atlas-specific features (Atlas Search, Triggers) are vendor-locked |
| P4: Operational | 4 | Self-hosted MongoDB well-documented but complex at scale; some EU providers offer managed MongoDB |
| P5: Migration | 4 | 6–12 months to migrate to PostgreSQL or another DB; query language rewrite needed |
| **CPS** | **4.4 → 4** | 0.15×6 + 0.30×5 + 0.20×3 + 0.20×4 + 0.15×4 = 4.4 |

**Result: S=2, CPS=4** — Red quadrant.

**Key insight:** Jurisdictional exposure (US company, CLOUD Act, US-hosted) dominates the sovereignty score. Portability is constrained by the proprietary query language (not SQL) and vendor-specific features (Atlas Search, Triggers) that have no standard equivalent.

---

## 8. Windows-Only C++ Trading App via Microsoft Store

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| S1: Legal/Jurisdictional | 0 | Entirely Microsoft ecosystem; CLOUD Act; US distribution |
| S2: Technical Autonomy | 1 | Proprietary Microsoft libraries; source is proprietary; completely dependent on Microsoft platform |
| S3: Governance | 0 | Microsoft controls the entire platform (Windows, Store, libraries) |
| **S_composite** | **0.3 → 0** | Cap: S2 ≤ 2, but formula gives 0.3 which rounds to 0 anyway |

| Dimension | Score | Rationale |
|-----------|:-----:|-----------|
| P1: Code/Runtime | 2 | Windows-only native executable; Microsoft-specific libraries |
| P2: Data | 3 | Depends on data storage approach; local files may be recoverable |
| P3: API/Integration | 2 | Proprietary Microsoft APIs; no standard integration protocols |
| P4: Operational | 1 | Windows-only; Microsoft Store distribution; no alternative deployment |
| P5: Migration | 1 | Fundamental rewrite required; 18+ months |
| **CPS** | **2.0** | 0.15×2 + 0.30×3 + 0.20×2 + 0.20×1 + 0.15×1 = 1.95 → 2 |

Cap applies: P4 = 1 (≤ 2), CPS capped at 4. Formula gives 2, which is below cap.

**Result: S=0, CPS=2** — Red quadrant. Complete vendor lock-in across all dimensions.

---

## Summary Table

| System | S | CPS | Quadrant |
|--------|:---:|:---:|:--------:|
| PostgreSQL on EU VM | 8 | 8 | Green |
| Microsoft 365 | 0 | 2 | Red |
| Self-hosted GitLab CE | 6 | 6 | Green |
| Salesforce CRM | 0 | 2 | Red |
| Docker + Spring Boot + AWS Aurora | 1 | 4 | Red |
| Python/Flask + ActivityPub on OVHcloud | 8 | 7 | Green |
| MongoDB Atlas on AWS | 2 | 4 | Red |
| Windows C++ Trading App | 0 | 2 | Red |
