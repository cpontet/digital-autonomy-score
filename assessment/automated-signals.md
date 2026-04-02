# Automated Signals — DAS Sub-Agent Specification

This document maps machine-detectable signals to each sovereignty and portability sub-dimension. It serves as the specification for a future automated DAS sub-agent that can analyze a codebase and produce preliminary Digital Autonomy Scores.

## Design Principles

1. **Signals suggest, humans decide**: Automated signals produce *preliminary* scores and flag areas for human review. They cannot capture context, intent, or organizational factors.
2. **Conservative scoring**: When uncertain, score lower. It's better to flag a false positive for human review than to miss a real risk.
3. **Evidence-based**: Every score must cite the specific signal(s) that produced it. No score without evidence.
4. **Layer-aware**: Signals should be analyzed per architectural layer, not globally.

---

## Sovereignty Signals

### S1: Legal & Jurisdictional Exposure

**Goal:** Determine where data can be compelled and what legal regime governs the system.

| Signal | Detection Method | Scoring Impact |
|--------|-----------------|----------------|
| Cloud provider identification | Scan IaC files (Terraform, CloudFormation, Pulumi) for provider blocks; check CI/CD configs for deployment targets | AWS/Azure/GCP → S1 ≤ 2; EU providers → S1 ≥ 7 |
| Region/zone configuration | Parse provider config for region strings (e.g., `eu-west-1`, `europe-west1`) | Non-EU region → S1 ≤ 3; EU region → S1 baseline 5+ |
| Dependency registry analysis | Analyze `package.json`, `requirements.txt`, `pom.xml`, `go.mod` — map packages to vendor HQ jurisdiction via registry metadata | >50% dependencies from CLOUD Act vendors → flag for review |
| SaaS/API endpoint detection | Scan code for API base URLs; map domains to service providers | `.amazonaws.com`, `.azure.com`, `.googleapis.com` → S1 ≤ 2 |
| Data storage configuration | Identify database connection strings, storage bucket references | Managed cloud DB → S1 depends on provider jurisdiction |

**Files to scan:**
- `terraform/*.tf`, `*.tfvars`
- `cloudformation/*.yaml`, `*.json`
- `docker-compose*.yml`
- `kubernetes/*.yaml`, `helm/*`
- `.github/workflows/*.yml`, `.gitlab-ci.yml`, `Jenkinsfile`
- Application config files (`application.yml`, `.env`, `config/*.json`)

### S2: Technical Autonomy

**Goal:** Determine whether the technology can be run, modified, and maintained independently.

| Signal | Detection Method | Scoring Impact |
|--------|-----------------|----------------|
| License detection (SPDX) | Scan `LICENSE`, `COPYING` files; parse SPDX identifiers in package manifests; use license detection tools | AGPL/GPL → S2 ≥ 7; MIT/Apache → S2 ≥ 5; Proprietary → S2 ≤ 2 |
| Source availability | Check if source code is present (not just binaries); check for `.git` directory | Source present → S2 ≥ 4; binary-only dependencies → flag |
| Dependency license audit | Run `license-checker` (npm), `pip-licenses` (Python), `license_finder` (Ruby/multi) | Aggregate license profile; flag proprietary transitive dependencies |
| Self-hosting documentation | Check for `INSTALL.md`, `DEPLOYMENT.md`, `docker-compose.yml`, Helm charts | Presence → S2 +1; absence → S2 -1 |
| Vendor SDK usage | Detect vendor-specific SDKs (e.g., `aws-sdk`, `@azure/*`, `google-cloud-*`) | Heavy vendor SDK usage → S2 ≤ 4 (depends on abstraction layers) |

**Files to scan:**
- `LICENSE`, `COPYING`, `NOTICE`
- `package.json` (license field + dependencies)
- `requirements.txt`, `Pipfile`, `pyproject.toml`
- `pom.xml`, `build.gradle`
- `go.mod`, `Cargo.toml`

### S3: Governance Independence

**Goal:** Determine who controls the technology's evolution.

| Signal | Detection Method | Scoring Impact |
|--------|-----------------|----------------|
| Governance metadata | Check for `GOVERNANCE.md`, `MAINTAINERS`, `CODEOWNERS`; look for foundation affiliation | EU foundation → S3 ≥ 7; US foundation → S3 = 5–6; single company → S3 ≤ 3 |
| Contributor diversity | Analyze Git log for email domains; assess commit concentration (bus factor) | Single-domain dominance (>80%) → S3 ≤ 3; diverse → S3 ≥ 6 |
| Foundation affiliation | Check README, NOTICE, website links for foundation mentions (Apache, Linux Foundation, Eclipse, CNCF) | Map foundation to jurisdiction and governance model |
| CLA/DCO requirements | Check for `CLA.md`, `.github/cla.yml`, DCO sign-off in commits | CLA with corporate owner → S3 ≤ 4; DCO → neutral |
| Standards compliance | Check for references to IETF RFC, W3C spec, ISO standard numbers in docs or code comments | Standards references → S3 ≥ 8 |

**Files to scan:**
- `GOVERNANCE.md`, `MAINTAINERS`, `CODEOWNERS`
- `README.md` (governance section, badges, foundation logos)
- `CONTRIBUTING.md`, `CLA.md`
- `NOTICE` (copyright holders)
- Git log (contributor analysis)

---

## Portability Signals

### P1: Code/Runtime Portability

**Goal:** Determine how platform-dependent the code is.

| Signal | Detection Method | Scoring Impact |
|--------|-----------------|----------------|
| Dockerfile/OCI presence | Check for `Dockerfile`, `Containerfile`, `.dockerignore` | Present → P1 ≥ 7 (conditional on contents) |
| Platform-specific imports | Scan for platform-specific modules (`win32`, `darwin`, `System.Windows`, `CoreFoundation`) | Platform imports detected → P1 ≤ 4 |
| Cross-platform CI matrix | Parse CI config for OS matrix (`matrix.os: [ubuntu, macos, windows]`) | Matrix testing → P1 ≥ 6 |
| Language/runtime | Identify primary language from file extensions, build files | JVM/Python/Node → P1 ≥ 5; C/C++ → P1 = 3; Assembly → P1 = 0 |
| WebAssembly targets | Check for `wasm32` target, `.wasm` files, `wasm-pack` in build | WASM target → P1 ≥ 7 |
| Web app indicators | Check for `index.html`, web framework dependencies (React, Vue, Angular, Next.js) | Web app → P1 ≥ 8 |
| Static HTML | Check for `.html` files with no build process | Static site → P1 = 10 |

**Files to scan:**
- `Dockerfile`, `Containerfile`, `docker-compose.yml`
- `.github/workflows/*.yml`, `.gitlab-ci.yml`
- `package.json`, `pom.xml`, `build.gradle`, `Cargo.toml`, `go.mod`
- Source files (language-specific platform imports)

### P2: Data Portability

**Goal:** Determine how locked-in the data is.

| Signal | Detection Method | Scoring Impact |
|--------|-----------------|----------------|
| Database type | Identify from connection strings, ORM config, migration files | PostgreSQL/MySQL → P2 ≥ 6; DynamoDB/CosmosDB → P2 ≤ 3; SQLite → P2 = 9 |
| Migration files | Check for migration directories (`migrations/`, `db/migrate/`, Flyway/Liquibase) | Standard migration tool → P2 +1 |
| Proprietary SQL extensions | Scan SQL files and queries for vendor-specific syntax | `CONNECT BY` (Oracle), `TOP` (SQL Server), Aurora-specific → P2 -2 |
| Export endpoints | Check API routes for export/download functionality (`/export`, `/download`, `/dump`) | Export API present → P2 +1 |
| File storage format | Check for proprietary file formats vs. standard formats (JSON, CSV, XML, Parquet) | Standard formats → P2 ≥ 7; proprietary binary formats → P2 ≤ 3 |
| ORM abstraction | Detect ORM usage (SQLAlchemy, Hibernate, Prisma, TypeORM) | ORM present → P2 +1 (abstraction from vendor SQL) |
| Vendor-specific database features | Detect usage of `aws-sdk` DynamoDB, Cloud Spanner client, Cosmos client | Vendor DB client → P2 ≤ 3 |

**Files to scan:**
- Database config files (`database.yml`, `knexfile.js`, `alembic.ini`)
- Migration directories
- SQL files (`*.sql`)
- ORM model definitions
- Application code (database query patterns)

### P3: API/Integration Portability

**Goal:** Determine how vendor-independent the integrations are.

| Signal | Detection Method | Scoring Impact |
|--------|-----------------|----------------|
| OpenAPI/AsyncAPI specs | Check for `openapi.yaml`, `swagger.json`, `asyncapi.yaml` | Present → P3 ≥ 6 |
| Auth standards | Detect OAuth2/OIDC configuration (`/.well-known/openid-configuration`, OIDC libraries) | Standard auth → P3 +2; proprietary auth → P3 -2 |
| Vendor SDK usage | Count and classify vendor SDK imports | >3 vendor-specific SDKs → P3 ≤ 4 |
| Standard protocol usage | Detect SMTP, IMAP, CalDAV, CardDAV, LDAP, S3-compatible API usage | Standard protocols → P3 ≥ 7 |
| GraphQL schema | Check for `schema.graphql`, GraphQL dependencies | Neutral — GraphQL is standard but schema is custom |
| Webhook configuration | Detect webhook patterns (standard HTTP callbacks vs. vendor-specific event systems) | Standard webhooks → P3 +1; vendor event bus → P3 -1 |
| Message queue type | Identify message broker (RabbitMQ/AMQP → standard; SQS/EventBridge → vendor) | AMQP/MQTT → P3 ≥ 7; SQS/SNS/PubSub → P3 ≤ 4 |

**Files to scan:**
- `openapi.yaml`, `swagger.json`, `asyncapi.yaml`
- Auth configuration files
- Application code (import statements for SDKs)
- Configuration files for message brokers, event systems
- `.env`, `config/*.json` (API endpoint URLs)

### P4: Operational Portability

**Goal:** Determine whether the system can be deployed and operated elsewhere.

| Signal | Detection Method | Scoring Impact |
|--------|-----------------|----------------|
| IaC presence | Check for Terraform, Pulumi, Ansible, CloudFormation, Helm | IaC present → P4 ≥ 5 |
| Cloud-agnostic config | Analyze IaC for cloud-specific vs. cloud-agnostic patterns | Single-cloud modules only → P4 ≤ 4; multi-cloud → P4 ≥ 7 |
| Operational docs | Check for `OPERATIONS.md`, `RUNBOOK.md`, `docs/operations/` | Present → P4 +1 |
| Monitoring standards | Detect Prometheus metrics endpoint (`/metrics`), OpenTelemetry config, Grafana dashboards | Standard monitoring → P4 +1; vendor-specific (CloudWatch, Datadog) → neutral |
| Kubernetes manifests | Check for `k8s/`, Helm charts, Kustomize overlays | K8s manifests → P4 ≥ 6 (portable orchestration) |
| CI/CD portability | Analyze CI config for cloud-specific deployment steps | Generic Docker push → P4 +1; AWS-specific deployment → P4 -1 |
| Secret management | Detect secret management approach (Vault, SOPS vs. AWS Secrets Manager, Azure Key Vault) | Standard tools (Vault, SOPS) → P4 +1; cloud-specific → P4 -1 |

**Files to scan:**
- `terraform/`, `pulumi/`, `ansible/`, `helm/`
- `k8s/`, `kubernetes/`, `manifests/`
- `OPERATIONS.md`, `RUNBOOK.md`, `docs/operations/`
- `.github/workflows/*.yml`, `.gitlab-ci.yml`
- Monitoring config (`prometheus.yml`, `otel-collector.yml`)
- `docker-compose*.yml`

---

## Assessment Output Format

The sub-agent should produce a structured assessment in the following format:

```yaml
system:
  name: "Example Application"
  assessed_at: "2025-01-15T10:30:00Z"
  confidence: "preliminary"  # preliminary | reviewed | confirmed

layers:
  - name: "Application"
    components:
      - name: "Spring Boot API"
        sovereignty:
          s1_legal:
            score: 1
            signals:
              - type: "cloud_provider"
                evidence: "terraform/main.tf: provider 'aws' with region 'us-east-1'"
                impact: "AWS US region → CLOUD Act jurisdiction"
          s2_technical:
            score: 8
            signals:
              - type: "license"
                evidence: "pom.xml: spring-boot-starter (Apache-2.0)"
                impact: "Open-source, self-hostable"
          s3_governance:
            score: 5
            signals:
              - type: "foundation"
                evidence: "Spring Framework governed by VMware/Broadcom (US)"
                impact: "US corporate governance, but Apache license allows forking"
        portability:
          p1_code:
            score: 9
            signals:
              - type: "dockerfile"
                evidence: "Dockerfile present, multi-stage build"
              - type: "language"
                evidence: "Java/JVM — cross-platform runtime"
          p2_data: null  # N/A for this layer
          p3_api:
            score: 6
            signals:
              - type: "openapi"
                evidence: "openapi.yaml present"
              - type: "vendor_sdk"
                evidence: "aws-sdk-java used for S3 access"
                impact: "S3 SDK creates AWS dependency; consider S3-compatible abstraction"
          p4_operational:
            score: 6
            signals:
              - type: "iac"
                evidence: "terraform/ directory with AWS-specific modules"
              - type: "kubernetes"
                evidence: "helm/ chart available"
          p5_migration:
            score: 7
            signals:
              - type: "estimated"
                evidence: "Container-based, standard Java — weeks to migrate runtime"

composite:
  sovereignty: 1
  portability: 4
  quadrant: "red"

flags:
  - severity: "critical"
    dimension: "s1"
    message: "All data in US jurisdiction (CLOUD Act exposure)"
  - severity: "warning"
    dimension: "p3"
    message: "AWS SDK usage in application layer — consider abstraction"
  - severity: "info"
    dimension: "p2"
    message: "Database layer not analyzed — requires database config access"
```

---

## Implementation Notes

### Scanning Priority

When building the sub-agent, scan in this order (highest signal density first):

1. **IaC files** (Terraform, Helm, K8s manifests) — reveals infrastructure, provider, and region
2. **Package manifests** (`package.json`, `pom.xml`, `requirements.txt`) — reveals dependencies, licenses, vendor SDKs
3. **CI/CD configuration** — reveals deployment targets, test matrix, build process
4. **Application configuration** — reveals database connections, API endpoints, auth providers
5. **Source code** — reveals platform-specific imports, vendor SDK usage patterns
6. **Documentation** — reveals governance, operational procedures, self-hosting guides

### Known Limitations

- **Cannot assess organizational factors**: team skills, budget, vendor relationships, contract terms
- **Cannot assess data volume**: data gravity depends on volume, not just format
- **Cannot assess custom configurations**: managed service configurations (e.g., Aurora-specific tuning) require runtime analysis
- **False positives on SDK usage**: presence of an SDK import doesn't mean deep dependency; it might be behind an abstraction layer
- **Missing runtime analysis**: cannot detect runtime behavior, actual data flows, or network calls without execution

### Confidence Levels

| Level | Meaning | When to Use |
|-------|---------|-------------|
| **High** | Signal is definitive (e.g., `LICENSE` file says GPL-3.0) | Clear, unambiguous signals |
| **Medium** | Signal is strong but context-dependent (e.g., AWS SDK detected, but might be behind abstraction) | Most automated detections |
| **Low** | Signal is suggestive but needs human verification (e.g., no export endpoint found, but export might exist via another mechanism) | Absence-of-evidence signals |

The sub-agent should report confidence per signal and per dimension, enabling human reviewers to focus on low-confidence areas.
