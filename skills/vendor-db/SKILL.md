---
name: vendor-db
user-invocable: false
description: |
  Reference database of technology vendors, cloud providers, and services
  with jurisdiction, CLOUD Act exposure, detection patterns, sovereignty
  score guidance, and sovereign alternatives. Used by the DAS assessor
  during scanning and scoring.
---

# Vendor Sovereignty Database

This skill provides a structured reference of technology vendors, cloud providers,
and services for use during DAS assessments.

---

## How to Use This Database

- During scanning (steps 1–5), match grep/glob findings against the **detection patterns** below
- Use the **S1 guidance** to inform Legal & Jurisdictional scoring
- Use the **sovereign alternatives** when writing Recommended Actions
- Entries are grouped by category; when a match is found, also check the vendor's **parent company** — a subsidiary inherits its parent's jurisdictional exposure
- Detection patterns are case-insensitive; match against package names, imports, API domains, and config values
- When multiple vendors are detected, score based on the **weakest** (lowest S1) vendor present

---

## Cloud Providers

### US-Based (CLOUD Act Exposed)

| Provider | Parent / HQ | CLOUD Act | Detection Patterns | S1 Guidance | Sovereign Alternatives |
|----------|-------------|-----------|-------------------|-------------|----------------------|
| AWS | Amazon / US | Yes | `aws-sdk`, `@aws-sdk`, `boto3`, `amazonaws.com`, `aws_access_key` | S1 ≤ 2 | OVHcloud, Scaleway, IONOS, Outscale |
| Azure | Microsoft / US | Yes | `@azure`, `azure-sdk`, `azure.com`, `windowsazure.com`, `AZURE_` | S1 ≤ 2 | OVHcloud, T-Systems, IONOS |
| GCP | Google / US | Yes | `google-cloud`, `@google-cloud`, `googleapis.com`, `firebase`, `GOOGLE_CLOUD_` | S1 ≤ 2 | Scaleway, OVHcloud, Exoscale |
| Oracle Cloud | Oracle / US | Yes | `oracledb`, `cx_Oracle`, `oracle.jdbc`, `oraclecloud.com`, `oci-sdk` | S1 ≤ 2 | PostgreSQL + EU hosting |
| IBM Cloud | IBM / US | Yes | `ibm-cloud-sdk`, `cloud.ibm.com`, `ibm_cloud_sdk` | S1 ≤ 2 | OVHcloud, IONOS |

### Non-EU (Varies)

| Provider | Parent / HQ | CLOUD Act | Detection Patterns | S1 Guidance | Notes |
|----------|-------------|-----------|-------------------|-------------|-------|
| Alibaba Cloud | Alibaba / CN | No (China jurisdiction) | `alibabacloud`, `aliyun-sdk`, `aliyuncs.com` | S1 ≤ 1 | Authoritarian jurisdiction; data subject to Chinese gov access |
| Tencent Cloud | Tencent / CN | No (China jurisdiction) | `tencentcloud-sdk`, `tencentcloudapi.com` | S1 ≤ 1 | Authoritarian jurisdiction |

### EU-Based (Sovereign)

| Provider | HQ | Detection Patterns | S1 Guidance | Notes |
|----------|-----|-------------------|-------------|-------|
| OVHcloud | FR | `ovh-sdk`, `ovh.com`, `ovh.net`, `ovh.cloud` | S1 ≥ 7 | EU-headquartered, own data centres |
| IONOS / 1&1 | DE | `ionos.com`, `ionos-cloud-sdk` | S1 ≥ 7 | United Internet subsidiary |
| Scaleway | FR | `scaleway-sdk`, `scaleway.com`, `@scaleway` | S1 ≥ 7 | Iliad Group subsidiary |
| Hetzner | DE | `hetzner.com`, `hetzner-cloud` | S1 ≥ 7 | Family-owned, EU-only |
| Exoscale | CH | `exoscale.com`, `exoscale-sdk` | S1 ≥ 6 | CH has EU adequacy decision |
| T-Systems | DE | `t-systems.com`, `open-telekom-cloud` | S1 ≥ 7 | Deutsche Telekom subsidiary |
| Outscale | FR | `outscale.com`, `osc-sdk` | S1 ≥ 7 | Dassault Systèmes subsidiary |

### Sovereign Cloud Programs (Partial Mitigation)

These are US cloud providers operating under special EU-residency or joint-venture arrangements. They reduce but do not eliminate jurisdictional risk because the US parent remains subject to CLOUD Act.

| Program | Parent / Partner | Detection Patterns | S1 Guidance | Notes |
|---------|-----------------|-------------------|-------------|-------|
| AWS EU Sovereign Cloud | AWS + EU operations | `aws-sovereign`, EU-dedicated regions | S1 = 3–4 | EU-operated, data stays in EU, but US parent company |
| Microsoft Cloud for Sovereignty / Bleu | Microsoft + Orange + Capgemini | `bleu.cloud`, sovereign Azure regions | S1 = 3–5 | French JV; degree of isolation from US parent varies |
| Google S3NS | Google + Thales | `s3ns.io`, sovereign GCP regions | S1 = 3–5 | French JV with Thales; still maturing |

---

## SaaS Vendors

### Productivity / Collaboration

| Service | Parent / HQ | Detection Patterns | S1 Guidance | Sovereign Alternatives |
|---------|-------------|-------------------|-------------|----------------------|
| Microsoft 365 | Microsoft / US | `graph.microsoft.com`, `office365`, `sharepoint`, `outlook.office.com` | S1 ≤ 2 | Nextcloud, OnlyOffice, Collabora Online |
| Google Workspace | Google / US | `workspace.google.com`, `googleapis.com/calendar`, `googleapis.com/drive` | S1 ≤ 2 | Nextcloud, OnlyOffice, Collabora Online |
| Salesforce | Salesforce / US | `salesforce.com`, `force.com`, `apex`, `soql`, `lightning` | S1 ≤ 2 | SuiteCRM, Odoo (BE), EspoCRM |

### DevOps / Source Control

| Service | Parent / HQ | Detection Patterns | S1 Guidance | Sovereign Alternatives |
|---------|-------------|-------------------|-------------|----------------------|
| GitHub | Microsoft / US | `github.com`, `actions/`, `GITHUB_TOKEN`, `.github/` | S1 ≤ 2 | GitLab CE (self-hosted), Gitea, Codeberg (DE) |
| GitLab SaaS | GitLab Inc / US | `gitlab.com`, `GITLAB_TOKEN`, `.gitlab-ci.yml` | S1 = 3 | GitLab CE self-hosted in EU |

### Monitoring / Observability

| Service | Parent / HQ | Detection Patterns | S1 Guidance | Sovereign Alternatives |
|---------|-------------|-------------------|-------------|----------------------|
| Datadog | Datadog / US | `datadog`, `datadoghq.com`, `dd-agent`, `DD_API_KEY` | S1 ≤ 2 | Prometheus + Grafana, OpenTelemetry |
| New Relic | New Relic / US | `newrelic`, `NEW_RELIC_LICENSE_KEY` | S1 ≤ 2 | Prometheus + Grafana, OpenTelemetry |
| Splunk | Cisco / US | `splunk`, `splunkcloud.com` | S1 ≤ 2 | OpenSearch, Elastic (self-hosted) |

### Payments / Integration

| Service | Parent / HQ | Detection Patterns | S1 Guidance | Sovereign Alternatives |
|---------|-------------|-------------------|-------------|----------------------|
| Stripe | Stripe / US | `stripe`, `stripe.com`, `STRIPE_SECRET_KEY` | S1 ≤ 2 | Adyen (NL), Mollie (NL) |
| Twilio / SendGrid | Twilio / US | `twilio`, `sendgrid`, `TWILIO_`, `SENDGRID_API_KEY` | S1 ≤ 2 | Self-hosted SMTP, Brevo (FR) |

### Authentication

| Service | Parent / HQ | Detection Patterns | S1 Guidance | Sovereign Alternatives |
|---------|-------------|-------------------|-------------|----------------------|
| Auth0 / Okta | Okta / US | `auth0`, `okta`, `AUTH0_`, `OKTA_` | S1 ≤ 2 | Keycloak (self-hosted), Zitadel (CH) |

---

## Databases & Data Services

### Managed Cloud Databases

| Service | Parent / HQ | Detection Patterns | P2 Guidance | S1 Guidance | Sovereign Alternatives |
|---------|-------------|-------------------|-------------|-------------|----------------------|
| DynamoDB | AWS / US | `dynamodb`, `@aws-sdk/client-dynamodb` | P2 ≤ 3 | S1 ≤ 2 | ScyllaDB, Cassandra |
| CosmosDB | Microsoft / US | `@azure/cosmos`, `cosmosdb` | P2 ≤ 3 | S1 ≤ 2 | MongoDB (self-hosted), CouchDB |
| Cloud Spanner | Google / US | `@google-cloud/spanner`, `spanner` | P2 ≤ 3 | S1 ≤ 2 | CockroachDB, YugabyteDB |
| Firebase / Firestore | Google / US | `firebase`, `@firebase`, `firestore`, `FIREBASE_` | P2 ≤ 3 | S1 ≤ 2 | Supabase (self-hosted), PocketBase |
| MongoDB Atlas | MongoDB / US | `mongodb+srv://`, `mongodb.net` | P2 = 4 | S1 ≤ 2 | MongoDB self-hosted in EU |
| Aurora | AWS / US | `aurora`, `rds.amazonaws.com` | P2 = 5 (MySQL-compatible) | S1 ≤ 2 | MySQL/MariaDB, PostgreSQL |
| ElastiCache / MemoryDB | AWS / US | `elasticache`, `memorydb` | P2 ≤ 3 | S1 ≤ 2 | Redis (self-hosted), Valkey |
| Elasticsearch (Elastic NV) | Elastic / US (SSPL) | `elasticsearch`, `@elastic`, `elastic.co` | P2 = 5 | S1 = 3 | OpenSearch, Meilisearch, Typesense |

### Sovereign Data Services

| Service | HQ / Governance | Detection Patterns | P2 Guidance | S1 Guidance | Notes |
|---------|----------------|-------------------|-------------|-------------|-------|
| PostgreSQL | PGDG (international) | `postgresql`, `pg`, `psycopg`, `postgres` | P2 ≥ 6 | S1 neutral (hosting-dependent) | Self-host in EU for S1 ≥ 7 |
| MariaDB | MariaDB Foundation (FI) | `mariadb`, `mariadb-connector` | P2 ≥ 6 | S1 ≥ 7 if self-hosted in EU | EU foundation |
| SQLite | Public domain | `sqlite`, `better-sqlite3`, `sqlite3` | P2 = 9 | S1 = 10 (local) | Embedded, no network exposure |
| Redis / Valkey | Linux Foundation | `redis`, `valkey`, `ioredis`, `redis-py` | P2 ≥ 6 | S1 depends on hosting | Valkey is the LF fork of Redis |
| MinIO | MinIO Inc / US (Apache-2.0) | `minio`, `MINIO_` | P2 ≥ 7 | S1 depends on hosting | S3-compatible object storage |

---

## Message Queues & Integration

| Service | Parent / HQ | Detection Patterns | P3 Guidance | S1 Guidance | Sovereign Alternatives |
|---------|-------------|-------------------|-------------|-------------|----------------------|
| SQS / SNS | AWS / US | `sqs`, `sns`, `@aws-sdk/client-sqs`, `@aws-sdk/client-sns` | P3 ≤ 4 | S1 ≤ 2 | RabbitMQ, NATS |
| Azure Service Bus | Microsoft / US | `@azure/service-bus`, `servicebus.windows.net` | P3 ≤ 4 | S1 ≤ 2 | RabbitMQ, NATS |
| Google Pub/Sub | Google / US | `@google-cloud/pubsub`, `pubsub.googleapis.com` | P3 ≤ 4 | S1 ≤ 2 | RabbitMQ, NATS, Kafka |
| RabbitMQ | VMware → Broadcom / US (MPL) | `amqplib`, `amqp`, `rabbitmq` | P3 ≥ 7 | S1 depends on hosting | — |
| Kafka | Apache / Confluent (US) | `kafkajs`, `kafka-python`, `kafka` | P3 ≥ 7 | S1 depends on hosting | Redpanda |
| NATS | Synadia / US (Apache-2.0) | `nats`, `nats.go`, `nats.ws` | P3 ≥ 7 | S1 depends on hosting | — |
| MQTT | OASIS standard | `mqtt`, `mosquitto`, `paho-mqtt` | P3 ≥ 8 | S1 depends on hosting | — |

---

## Licensing Quick Reference

Use this table to inform S2 (Technical Autonomy) scoring based on the license of detected dependencies. Every OSI license gives the same S2 floor: the right to run, modify and fork. Copyleft is credited in S3 (+1) only when no single company holds the copyright; check for a CLA with the **governance-db** skill.

| License | SPDX ID | S2 Guidance | Notes |
|---------|---------|-------------|-------|
| AGPL-3.0 | `AGPL-3.0-only` | S2 ≥ 5 | Strong copyleft, covers network use; S3 +1 if no corporate CLA |
| GPL-3.0 | `GPL-3.0-only` | S2 ≥ 5 | Strong copyleft; S3 +1 if no corporate CLA |
| EUPL-1.2 | `EUPL-1.2` | S2 ≥ 5 | EU-authored copyleft, compatible with GPL; S3 +1 if no corporate CLA |
| MPL-2.0 | `MPL-2.0` | S2 ≥ 5 | Weak copyleft, file-level; S3 +1 if no corporate CLA |
| Apache-2.0 | `Apache-2.0` | S2 ≥ 5 | Permissive + patent grant |
| MIT | `MIT` | S2 ≥ 5 | Permissive |
| BSD-3-Clause | `BSD-3-Clause` | S2 ≥ 5 | Permissive |
| BSL-1.1 | `BUSL-1.1` | S2 = 3–4 | Source-available, converts to open after delay |
| SSPL | `SSPL-1.0` | S2 = 3 | Source-available, not OSI-approved |
| Elastic License | `Elastic-2.0` | S2 = 3 | Source-available, restricts SaaS |
| Proprietary | — | S2 ≤ 2 | No source access |
