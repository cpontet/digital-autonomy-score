# DAS Portability Scale

## Critique of the Original Scale

The original portability scale (0–10) in the presentation focuses exclusively on code/runtime portability and has several issues:

### 1. Docker is Not Portability

Docker (score 7) is a packaging format — a shipping box. It says nothing about what's *inside*. A containerized vendor-locked application (e.g., an app hardwired to AWS DynamoDB, packaged in Docker) is NOT portable. The container moves; the application doesn't.

### 2. Web Apps Should Rank Above Containers

Web applications (score 8) provide inherently higher end-user portability than containers (score 7). A web app runs on any device with a browser — no container runtime needed. The original ordering is correct directionally but the gap should be wider, and the rationale needs clarification.

### 3. Single-Dimension Assessment

The scale measures only code/runtime portability. In practice, the hardest portability challenges are:
- **Data portability**: Can you export and import your data? (Data gravity is the primary lock-in vector)
- **API portability**: Do integrations use standard protocols?
- **Operational portability**: Can you actually run this elsewhere?
- **Migration feasibility**: What's the practical effort to move?

A system with perfectly portable code but completely locked-in data (e.g., Salesforce with extensive custom objects) scores misleadingly high on the original scale.

### 4. Composite Systems Ignored

Real projects are stacks, not single components. A "Docker + Spring Boot + AWS Aurora" system has different portability at each layer. The original scale provides no guidance for scoring composite systems.

---

## P1: Code/Runtime Portability (Refined)

The original code/runtime scale is largely correct. Refined version with clearer ordering:

| Score | Category | Description | Examples |
|:-----:|----------|-------------|----------|
| 0 | Hardware/Platform Locked | Only runs on specific hardware or tightly integrated environments. | Embedded firmware, BIOS, proprietary hardware drivers |
| 1 | Vendor-Locked APIs | Deeply tied to one vendor's stack with no abstraction layer. | Windows kernel drivers, CoreML-only apps, Xbox-exclusive |
| 2 | Single-OS Native | Runs on one OS using standard OS APIs. Rewrite needed to port. | Windows .exe apps, native iOS-only apps |
| 3 | Multi-Platform via Rebuild | Can run on different platforms if recompiled. No binary portability. | C/C++ with POSIX, Go binaries, JNI apps |
| 4 | Portable Source, OS Dependencies | Source is mostly portable but requires platform-specific runtimes or dependencies. | .NET Framework (not Core), Qt with native builds |
| 5 | Runtime-Portable | Runs identically on any platform with the right runtime installed. | Java/JVM, Python, Node.js, .NET Core |
| 6 | Cross-Platform Frameworks | Write-once with per-platform adaptation. Framework provides abstraction. | Electron, React Native, Flutter |
| 7 | Sandboxed Environments | Code executes identically in highly standardized or virtualized environments. | WebAssembly (Wasm), portable sandboxed runtimes |
| 8 | Web Applications | Accessible on any device/browser with standard web technologies. No installation. | HTML/CSS/JS web apps, PWAs |
| 9 | Containerized + Standard | Packaged with all dependencies AND uses only standard, non-vendor-specific APIs internally. | Docker/OCI container running standards-compliant code |
| 10 | Universal Standards | Relies solely on universally adopted standards. Extreme portability and longevity. | ANSI C (portable subset), ANSI SQL, OpenAPI services, POSIX shell |

### Key Change: Containers Moved to Score 9 (Conditional)

Containers score 9 only when the *contents* are also portable (standard APIs, no vendor lock-in). A Docker container wrapping vendor-locked code scores based on what's inside, not the container itself. This resolves the "Docker fallacy."

---

## P2: Data Portability

*Can you get your data out, completely, in a format others can use?*

| Score | Criteria | Examples |
|:-----:|----------|----------|
| 0 | No export capability. Data is inaccessible outside the platform. | Proprietary SaaS with no API, no export |
| 1 | Manual, partial export only (copy-paste, screenshots). | Some legacy enterprise systems |
| 2 | Vendor-specific export format. Requires vendor tools to read. | Proprietary database dump formats |
| 3 | Export available but incomplete (metadata lost, relationships broken, history missing). | CRM exports missing workflow rules and automation |
| 4 | Full export in vendor-specific format. Third-party converters exist. | Salesforce data export (CSV + metadata), Exchange PST files |
| 5 | Export in semi-standard format. Major fields preserved, some manual cleanup needed. | JSON/CSV exports that lose schema relationships |
| 6 | Export in standard format with most metadata preserved. Tested import path exists for at least one alternative. | PostgreSQL pg_dump, standard SQL export |
| 7 | Full export in open standard format. Relationships, metadata, and history preserved. | Git repositories, standard SQL with schema, CalDAV/CardDAV |
| 8 | Real-time data access via standard APIs. Continuous sync possible. | Systems with full REST/GraphQL API, database replication |
| 9 | Data stored natively in open, standard formats. No export step needed — data is inherently portable. | Files on filesystem (PDF, ODF), SQLite databases, Git repos |
| 10 | Data uses ratified international standard formats with multiple independent implementations for reading and writing. | HTML content, iCalendar (RFC 5545), vCard (RFC 6350), CSV (RFC 4180) |

---

## P3: API/Integration Portability

*Do integrations use standard protocols? Can you swap connected services without rewriting?*

| Score | Criteria | Examples |
|:-----:|----------|----------|
| 0 | No documented API. Integration is ad-hoc or impossible. | Legacy systems with no integration points |
| 1 | Proprietary SDK required. Vendor-specific protocol. | Vendor-specific binary protocols |
| 2 | REST API but undocumented or unstable. Breaking changes frequent. | Undocumented internal APIs |
| 3 | Documented proprietary API. Stable but vendor-unique. | AWS SDK, Azure SDK, Salesforce SOQL |
| 4 | Documented API following common patterns (REST/JSON) but with vendor-specific authentication and data models. | Most cloud vendor APIs |
| 5 | Standard protocol with vendor extensions. Core portable, extensions not. | SQL with vendor extensions, LDAP with proprietary schema |
| 6 | OpenAPI/AsyncAPI-documented interface. Standard auth (OAuth2/OIDC). Vendor-specific data models. | Well-documented SaaS APIs with OAuth2 |
| 7 | Standard protocols throughout (SMTP, CalDAV, IMAP, SQL). Vendor-neutral data models. | Email servers (SMTP/IMAP), calendar servers (CalDAV) |
| 8 | Fully standards-compliant interfaces with abstraction layers. Multiple providers available as drop-in replacements. | S3-compatible storage API (MinIO, Ceph, Cloudflare R2) |
| 9 | Open protocol with multiple independent implementations. Federated by design. | ActivityPub, Matrix, XMPP, WebFinger |
| 10 | Ratified international standard interfaces with formal conformance testing. | HTTP (IETF), SQL (ISO 9075), OIDC (OpenID Foundation) |

---

## P4: Operational Portability

*Can you actually run this somewhere else? Are the skills, tooling, and providers available?*

| Score | Criteria | Examples |
|:-----:|----------|----------|
| 0 | Vendor-managed SaaS only. No self-hosting option exists. | Salesforce, Workday, ServiceNow |
| 1 | Self-hosting theoretically possible but undocumented and unsupported. | Some "open core" products where self-hosting is discouraged |
| 2 | Self-hosting documented but requires vendor-specific infrastructure or specialized skills. | Oracle Database (requires DBA expertise, specific hardware recommendations) |
| 3 | Self-hosting possible on limited platforms. Single-cloud IaC only. | AWS-only Terraform modules, Azure-only ARM templates |
| 4 | Self-hosting on major clouds. Some cloud-agnostic config exists. Operational docs limited. | Applications with deployment guides for 2-3 clouds |
| 5 | Well-documented self-hosting. Works on any major cloud. Requires specialized but available skills. | GitLab self-hosted, Keycloak |
| 6 | Standard deployment patterns (Kubernetes, Ansible). Operational runbooks available. Multiple EU providers offer managed versions. | PostgreSQL managed by multiple EU providers |
| 7 | Infrastructure-as-Code available. Cloud-agnostic configuration. Monitoring via standard tools (Prometheus, OpenTelemetry). | Well-architected cloud-native applications |
| 8 | Fully documented operations. Multiple independent service providers globally and within the EU. Active community support. | Linux, nginx, PostgreSQL, Redis |
| 9 | Commodity operational knowledge. Any competent team can deploy and manage. Abundant documentation, training, and tooling. | Apache HTTP Server, MySQL, basic web hosting |
| 10 | Zero operational overhead. Runs anywhere with standard infrastructure. No specialized skills needed. | Static HTML sites, SQLite, standard CLI tools |

---

## P5: Migration Feasibility

*What's the practical effort, timeline, and risk to actually move?*

| Score | Criteria |
|:-----:|----------|
| 0 | Migration considered impossible or prohibitively expensive. Multi-year timeline with extreme risk. |
| 1 | Migration theoretically possible but no known successful case. Would require fundamental re-architecture. |
| 2 | Migration possible but requires 18+ months, dedicated team, and significant budget. High risk of failure. |
| 3 | Migration achievable in 12–18 months with dedicated resources. Proven in some cases but complex. |
| 4 | Migration achievable in 6–12 months. Known migration paths exist. Moderate risk. |
| 5 | Migration achievable in 3–6 months with existing team. Documented migration guides available. |
| 6 | Migration achievable in 1–3 months. Standard tooling available. Low-to-moderate risk. |
| 7 | Migration achievable in weeks. Automated migration tools exist. Low risk. |
| 8 | Migration achievable in days. Drop-in replacement available. Minimal risk. |
| 9 | Migration is a configuration change. No data transformation or code changes needed. |
| 10 | No migration needed — system is inherently environment-independent. |

---

## Composite Portability Score (CPS)

### Weighted Formula

```
CPS = 0.15 × P1 + 0.30 × P2 + 0.20 × P3 + 0.20 × P4 + 0.15 × P5
```

### Weight Rationale

| Dimension | Weight | Rationale |
|-----------|:------:|-----------|
| P1: Code/Runtime | 0.15 | Least important alone — code portability is easily abstracted via containers or rewriting |
| P2: Data | **0.30** | Highest weight — data gravity is the primary lock-in vector. Losing data is catastrophic. |
| P3: API/Integration | 0.20 | Integration portability affects the entire ecosystem around a component |
| P4: Operational | 0.20 | Practical ability to run elsewhere determines real-world portability |
| P5: Migration | 0.15 | Practical effort matters but is a one-time cost, not structural |

### Weakest-Link Principle

For composite systems (stacks with multiple layers), apply scores at each layer, then:

> **System score per dimension = minimum across all layers for that dimension**

Example: A system with a portable web frontend (P2=8) but a vendor-locked database (P2=2) has a system-level P2 of **2**, because you can't migrate the system without migrating the data.

### Scoring Override

If any sub-dimension scores ≤ 2, the composite CPS is capped at 4. A single critical portability weakness limits overall portability regardless of other strengths.

---

## Worked Example: Docker + Spring Boot + AWS Aurora

| Layer | P1 Code | P2 Data | P3 API | P4 Ops | P5 Migration |
|-------|:-------:|:-------:|:------:|:------:|:------------:|
| Frontend (React SPA) | 8 | 9 | 7 | 8 | 8 |
| Application (Spring Boot in Docker) | 9 | N/A | 6 | 7 | 7 |
| Database (AWS Aurora MySQL) | 5 | 4 | 5 | 2 | 4 |
| **System minimum** | **5** | **4** | **5** | **2** | **4** |

```
CPS = 0.15×5 + 0.30×4 + 0.20×5 + 0.20×2 + 0.15×4
    = 0.75 + 1.20 + 1.00 + 0.40 + 0.60
    = 3.95 → 4
```

**But** P4 (Operational) ≤ 2, so the cap applies: **CPS = min(4, 4) = 4**.

Despite having a containerized Spring Boot app (often assumed to be "portable"), the AWS Aurora dependency drags the entire system to a CPS of 4. This is the weakest-link principle in action — the Docker container is irrelevant if you can't move the database.
