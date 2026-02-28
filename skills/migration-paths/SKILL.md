---
name: migration-paths
user-invocable: false
description: |
  Known migration paths between vendor services and sovereign alternatives
  with estimated effort, tooling, and risk factors. Used by the DAS assessor
  for evidence-based P5 (Migration Feasibility) scoring.
---

## How to Use This Database

- After identifying vendor dependencies (via vendor-db) and scoring P1–P4, use this reference to score P5
- Look up the source vendor service and the target sovereign alternative
- Use the effort estimate and P5 guidance to score migration feasibility
- If multiple migration paths exist, score based on the easiest viable path
- If no path is listed, estimate P5 based on the closest analogy and note "no known documented path"

## Effort Scale

| P5 Score | Effort | Timeline | Description |
|---|---|---|---|
| 10 | None | N/A | Environment-independent, no migration needed |
| 9 | Trivial | Hours | Configuration change only |
| 8 | Low | Days | Drop-in replacement, minimal code changes |
| 7 | Moderate-low | 1–2 weeks | Automated migration tools exist, minor adaptation |
| 6 | Moderate | 1–3 months | Standard tooling, some manual work |
| 5 | Significant | 3–6 months | Dedicated effort, existing team |
| 4 | High | 6–12 months | Known paths but substantial rework |
| 3 | Very high | 12–18 months | Major re-architecture |
| 2 | Extreme | 18+ months | Fundamental redesign, dedicated team + budget |
| 1 | Near-impossible | Unknown | No known successful migration at scale |
| 0 | Impossible | N/A | Vendor lock-in is absolute |

## Cloud Infrastructure Migration

### Compute

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| EC2 | Any EU provider VMs | 7–8 | Days–weeks | Re-deploy containers/VMs; OCI images portable | Terraform/OpenTofu, Ansible | Network config, IAM policies don't transfer |
| AWS Lambda | Self-hosted (OpenFaaS, Knative) | 4–5 | 3–6 months | Rewrite handler wrappers; event sources change | OpenFaaS, Knative | Event source bindings are vendor-specific |
| Azure Functions | Self-hosted (OpenFaaS, Knative) | 4–5 | 3–6 months | Similar to Lambda migration | OpenFaaS, Knative | Azure-specific triggers need replacement |
| GCP Cloud Run | Self-hosted containers | 7–8 | Days–weeks | Already containerised; redeploy | Docker, K8s | IAM, Cloud SQL proxy, service mesh differences |
| AWS ECS/EKS | Self-hosted K8s | 6–7 | 1–3 months | K8s manifests largely portable; IAM/networking differ | K8s, Helm | AWS ALB/NLB ingress, EBS volumes, IAM roles for service accounts |
| Azure AKS | Self-hosted K8s | 6–7 | 1–3 months | Similar to EKS migration | K8s, Helm | Azure AD integration, Azure Disk volumes |
| GKE | Self-hosted K8s | 7 | 2–4 weeks | GKE closely follows upstream K8s | K8s, Helm | GKE Autopilot features, Workload Identity |

### Storage

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| S3 | MinIO (self-hosted) | 8–9 | Days | S3 API-compatible; change endpoint URL | MinIO, rclone, s3cmd | Lifecycle policies, S3 Select, event notifications differ |
| S3 | OVHcloud Object Storage | 8 | Days | S3-compatible API | rclone | Some S3 features not supported |
| Azure Blob Storage | MinIO or S3-compatible | 5–6 | 1–3 months | Different API; need to rewrite storage layer | AzCopy (export), rclone | No API compatibility; code changes required |
| GCS | MinIO or S3-compatible | 7 | 1–2 weeks | GCS has S3 interop mode; or use rclone | rclone, gsutil (export) | GCS-specific features (signed URLs differ) |

## Database Migration

### Relational

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| Aurora MySQL | MySQL/MariaDB (self-hosted) | 7–8 | Days–weeks | Aurora is MySQL-compatible; dump and restore | mysqldump, mydumper, DMS | Aurora-specific features (parallel query, fast cloning) won't work |
| Aurora PostgreSQL | PostgreSQL (self-hosted) | 7–8 | Days–weeks | Aurora is PG-compatible; dump and restore | pg_dump, pg_restore | Aurora extensions, Babelfish won't transfer |
| Azure SQL | PostgreSQL (self-hosted) | 4–5 | 3–6 months | SQL dialect differences (T-SQL → PL/pgSQL) | pgLoader, ora2pg (adapted) | Stored procedures, triggers need rewrite |
| Cloud SQL (MySQL) | MySQL/MariaDB (self-hosted) | 8 | Days | Standard MySQL; export and import | mysqldump | Managed features (auto-backup, HA) need replacement |
| Cloud SQL (PostgreSQL) | PostgreSQL (self-hosted) | 8 | Days | Standard PostgreSQL; export and import | pg_dump, pg_restore | Same as above |
| Oracle DB | PostgreSQL | 3–4 | 6–18 months | Significant SQL dialect differences (PL/SQL → PL/pgSQL) | Ora2Pg, AWS SCT (ironic) | PL/SQL procedures, Oracle-specific types, performance tuning |

### NoSQL

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| DynamoDB | ScyllaDB | 3–4 | 6–12 months | Different data model; DynamoDB Streams → ScyllaDB CDC | Custom ETL | Query patterns change; DynamoDB-specific features (DAX, Streams) |
| DynamoDB | PostgreSQL (JSONB) | 3 | 6–12 months | Fundamental model change (document → relational) | Custom migration scripts | Application query rewrite, consistency model changes |
| CosmosDB | MongoDB (self-hosted) | 5–6 | 1–3 months | CosmosDB has MongoDB API mode; data export possible | mongodump/mongorestore | CosmosDB-specific consistency levels, stored procedures |
| MongoDB Atlas | MongoDB (self-hosted) | 8 | Days | Same technology; change connection string | mongodump, mongorestore | Ops burden shifts to you (backups, monitoring, scaling) |
| Firebase/Firestore | Supabase (self-hosted) | 4 | 3–6 months | Different data model; real-time sync differs | Custom migration | Firebase Auth, Cloud Functions, real-time listeners need rework |
| Firebase/Firestore | PocketBase | 4 | 3–6 months | Simpler target but less feature-rich | Custom migration | Same as above |
| Elasticsearch (managed) | OpenSearch (self-hosted) | 7–8 | 1–2 weeks | OpenSearch is an ES fork; largely compatible up to 7.10 | Snapshot/restore, reindex | Post-7.10 Elasticsearch features don't exist in OpenSearch |
| Elasticsearch (managed) | Meilisearch | 3–4 | 3–6 months | Different API and query language | Custom reindexing | Feature gap for complex queries; different relevance tuning |

### Cache / In-Memory

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| ElastiCache (Redis) | Redis (self-hosted) | 8–9 | Days | Same technology; change endpoint | redis-cli, RDB export | Ops: need to manage HA, persistence, monitoring |
| ElastiCache (Redis) | Valkey (self-hosted) | 8–9 | Days | Valkey is a Redis fork; drop-in compatible | Same as Redis | Valkey feature parity may lag on newest Redis features |
| MemoryDB | Redis/Valkey (self-hosted) | 7–8 | Days–weeks | Redis-compatible; export and import | RDB snapshot | Durability guarantees differ (MemoryDB is durable by default) |

## SaaS Migration

### DevOps / Source Control

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| GitHub (repos) | GitLab CE (self-hosted) | 7 | 1–2 weeks | Git repos transfer natively; issues/PRs need migration | GitLab importer, gh2gl | GitHub Actions → GitLab CI requires rewrite |
| GitHub Actions | GitLab CI | 5 | 1–3 months | Different YAML syntax; different runner model | Manual rewrite | Marketplace actions have no GitLab equivalent; rewrite each |
| GitHub Actions | Self-hosted (Gitea + Woodpecker/Drone) | 4–5 | 2–4 months | More migration effort; smaller ecosystem | Manual rewrite | Fewer integrations, smaller community |

### Monitoring / Observability

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| Datadog | Prometheus + Grafana | 5–6 | 1–3 months | Replace agents; rewrite dashboards; recreate alerts | OTel Collector, Prometheus | Datadog APM → Jaeger/Tempo; log management → Loki |
| New Relic | Prometheus + Grafana | 5–6 | 1–3 months | Similar to Datadog migration | OTel Collector | Same trade-offs |
| CloudWatch | Prometheus + Grafana | 6 | 1–2 months | Standard metrics via OTel; replace CloudWatch-specific alarms | OTel Collector, Prometheus | CloudWatch Logs → Loki; CloudWatch Alarms → Alertmanager |
| Splunk | OpenSearch | 5 | 2–4 months | Different query language (SPL → OpenSearch DSL) | Logstash/Fluentd | SPL queries need complete rewrite |

### Authentication

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| Auth0 | Keycloak (self-hosted) | 5–6 | 1–3 months | Export users; reconfigure OIDC clients; rewrite Auth0 Rules → Keycloak SPI | Auth0 Management API (export), Keycloak import | Auth0 Rules/Actions have no direct equivalent; custom SPI needed |
| Auth0 | Zitadel | 5 | 1–3 months | Similar to Keycloak migration | Zitadel API | Newer product, smaller ecosystem |
| Okta | Keycloak | 5 | 1–3 months | Export users/groups; reconfigure OIDC/SAML | Okta API (export) | Okta-specific policies need recreation |
| AWS Cognito | Keycloak | 4–5 | 2–4 months | Export users (passwords cannot be exported); reconfigure clients | AWS CLI, Keycloak API | User password reset required (Cognito doesn't export password hashes) |

### Payments

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| Stripe | Adyen (NL) | 4–5 | 3–6 months | Different API; rewrite payment integration | Stripe migration guides, Adyen docs | Subscription management, webhooks, payment methods differ |
| Stripe | Mollie (NL) | 4–5 | 3–6 months | Simpler API but fewer features | Mollie SDK | Feature gap for complex billing; fewer payment methods |

### Collaboration / Productivity

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| Microsoft 365 | Nextcloud + OnlyOffice/Collabora | 3–4 | 6–12 months | Major user re-training; data export via Graph API | Microsoft Graph API, Nextcloud migration tools | User adoption is the biggest risk; feature gap in collaboration |
| Google Workspace | Nextcloud + OnlyOffice/Collabora | 3–4 | 6–12 months | Google Takeout for data; reconfigure email (self-host or EU provider) | Google Takeout, Nextcloud | Same adoption challenges; Gmail → self-hosted mail is complex |
| Salesforce | Odoo (BE, self-hosted) | 2–3 | 12–18 months | Fundamental platform change; custom objects need recreation | Custom ETL, Odoo import | Apex code cannot be migrated; business process re-engineering |

## Message Queues

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| SQS | RabbitMQ | 5–6 | 1–2 months | Replace AWS SDK calls with AMQP client; change queue semantics | amqplib, pika | SQS FIFO, dead-letter queues need recreation; visibility timeout → NACK model |
| SNS | RabbitMQ (fanout exchange) | 5–6 | 1–2 months | Replace topic subscriptions with exchange bindings | amqplib, pika | SNS filtering → RabbitMQ headers exchange |
| Google Pub/Sub | Kafka or RabbitMQ | 5 | 1–3 months | Different semantics (Pub/Sub ack model vs Kafka offsets) | kafkajs, Confluent tools | Ordering guarantees, exactly-once semantics differ |
| Azure Service Bus | RabbitMQ | 5–6 | 1–2 months | Replace SDK; adapt session/partition model | amqplib | Service Bus sessions → RabbitMQ equivalent needs custom routing |

## IaC Migration

| From | To | P5 | Timeline | Approach | Tooling | Key Risks |
|---|---|---|---|---|---|---|
| CloudFormation | Terraform/OpenTofu | 5–6 | 1–3 months | Rewrite templates as HCL; no automated converter for full fidelity | cf-to-tf (partial), manual | CloudFormation custom resources need Terraform providers |
| ARM Templates | Terraform/OpenTofu | 5–6 | 1–3 months | Rewrite as HCL | aztfexport (partial), manual | Azure-specific resource types remain |
| Terraform (single-cloud) | Terraform multi-cloud | 6–7 | 1–2 months | Abstract provider-specific resources; add new provider config | Terraform modules | State migration, provider-specific features |

## Common Migration Blockers

List common issues that reduce P5 regardless of the specific migration:

| Blocker | Impact on P5 | Mitigation |
|---|---|---|
| No data export API | P5 -2 | Screen scraping, API reverse engineering (fragile) |
| Vendor-specific encryption (KMS) | P5 -1 | Re-encrypt with portable key management before migration |
| Proprietary stored procedures | P5 -2 | Rewrite in target dialect; no automated conversion |
| SSO/auth deeply integrated | P5 -1 | Plan auth migration first or run parallel auth during transition |
| User password hashes non-exportable | P5 -1 | Force password reset for all users post-migration |
| Vendor lock-in through pricing/credits | P5 -0 (soft lock-in) | Not a technical blocker but affects business case |
| Large dataset (>10 TB) | P5 -1 | Physical transfer (snowball-equivalent), incremental sync |
| Real-time sync requirements | P5 -1 | Need dual-write or CDC during migration window |
