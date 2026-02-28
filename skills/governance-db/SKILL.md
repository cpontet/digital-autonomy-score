---
name: governance-db
user-invocable: false
description: |
  Reference database of open-source foundations, standards bodies, and
  corporate stewards with jurisdiction, governance model, and S3 score
  guidance. Used by the DAS assessor for Governance Independence scoring.
---

## How to Use This Database

- During scanning phase 6 (Documentation & Governance), match findings against this reference
- Check NOTICE files, LICENSE headers, README badges, and package metadata for foundation/org affiliations
- Use the S3 guidance to inform Governance Independence scoring
- When a dependency is governed by multiple entities (e.g., a Linux Foundation project with a single dominant corporate contributor), score based on the effective governance, not the nominal structure

## S3 Score by Governance Model

| Governance Model | S3 Range | Description |
|---|---|---|
| International standards body (IETF, W3C, ISO, OASIS) | 8–10 | Multilateral, consensus-based, no single-entity veto |
| EU/neutral foundation (Eclipse, CERN) | 7–8 | EU-domiciled or international; broad governance |
| US foundation, broad governance (Apache, Linux Foundation) | 5–6 | Open governance but US-domiciled; theoretical US jurisdiction risk |
| US foundation, single-company dominated | 3–4 | Foundation exists but one company controls direction |
| Single company, EU-based | 2–3 | EU jurisdiction but single point of control |
| Single company, US-based | 0–2 | US jurisdiction + single point of control |

## International Standards Bodies

| Organisation | HQ | Governance Model | S3 Guidance | Detection Signals |
|---|---|---|---|---|
| IETF | International (administered from US) | Rough consensus, open participation | S3 = 9 | RFC references (`RFC xxxx`), IETF standards mentions |
| W3C | International (US/FR/JP/CN hosts) | Member consortium, open process | S3 = 9 | W3C spec references, `www-` mailing lists |
| ISO / IEC | Geneva, CH | National body representatives | S3 = 10 | ISO standard references (`ISO xxxx`) |
| OASIS | US (non-profit) | Open, member-driven | S3 = 8 | OASIS standard references, TC mentions |
| ECMA International | Geneva, CH | Member-driven | S3 = 9 | ECMA-xxx references (e.g., ECMA-262 for JS) |
| IEEE | US (non-profit) | Member-driven | S3 = 8 | IEEE standard references |
| Unicode Consortium | US (non-profit) | Member-driven | S3 = 8 | Unicode/ICU references |

## EU/Neutral Foundations

| Foundation | HQ | Governance Model | S3 Guidance | Notable Projects | Detection Signals |
|---|---|---|---|---|---|
| Eclipse Foundation | Brussels, BE | Multi-stakeholder, EU-domiciled since 2021 | S3 = 7–8 | Jakarta EE, Eclipse IDE, Adoptium, Mosquitto | `eclipse.org`, Eclipse Public License, `org.eclipse` |
| CERN | Geneva, CH | International treaty org | S3 = 8 | ROOT, Indico, CERNBox, CERN Open Hardware Licence | CERN-OHL, `cern.ch` |
| NLnet Foundation | Amsterdam, NL | EU non-profit, funds FOSS | S3 = 7 | Funds various EU open-source projects | NLnet mentions in funding/acknowledgments |
| OW2 Consortium | Paris, FR | EU non-profit, open-source community | S3 = 7 | LemonLDAP, Lutece, Joram | `ow2.org`, OW2 mentions |
| Open Source Business Alliance (OSBA) | DE | German industry association | S3 = 7 | Sovereign Cloud Stack | OSBA mentions, `osb-alliance.de` |
| Gaia-X | Brussels, BE | EU initiative, multi-stakeholder | S3 = 7 | Gaia-X Federation Services | Gaia-X mentions, `gaia-x.eu` |

## US Foundations (Broad Governance)

| Foundation | HQ | Governance Model | S3 Guidance | Notable Projects | Detection Signals |
|---|---|---|---|---|---|
| Apache Software Foundation | US (DE) | Merit-based, diverse committers | S3 = 5–6 | Kafka, Hadoop, Spark, Tomcat, Cassandra, Airflow | `apache.org`, Apache-2.0 from ASF, `org.apache` |
| Linux Foundation | US (CA) | Corporate consortium + open governance | S3 = 5–6 | Linux kernel, Kubernetes (CNCF), Node.js (OpenJS) | `linuxfoundation.org`, LF project mentions |
| CNCF (under LF) | US (CA) | TOC + end-user community | S3 = 5–6 | Kubernetes, Prometheus, Envoy, containerd, Helm, Argo | `cncf.io`, CNCF badges, graduated/incubating status |
| OpenJS Foundation (under LF) | US | Cross-project council | S3 = 5 | Node.js, jQuery, webpack, Electron, ESLint | `openjsf.org`, OpenJS mentions |
| Python Software Foundation | US (DE) | PEP process, elected board | S3 = 5–6 | CPython, PyPI | `python.org`, PSF mentions |
| Rust Foundation | US (DE) | Multi-stakeholder board | S3 = 5 | Rust language, Cargo, crates.io | `foundation.rust-lang.org`, Rust Foundation mentions |
| Free Software Foundation | US (MA) | RMS-founded, GPL steward | S3 = 5 | GNU tools, GCC, Emacs, glibc | `fsf.org`, FSF mentions, GNU project |
| Mozilla Foundation | US (CA) | Non-profit + for-profit subsidiary | S3 = 4–5 | Firefox, Thunderbird, MDN | `mozilla.org`, MPL-2.0 from Mozilla |
| OpenSSL Software Foundation | US | Small team, corporate sponsors | S3 = 4 | OpenSSL | `openssl.org` |

## Corporate-Dominated Projects

These are projects where a single company controls governance despite being open-source:

| Company | HQ | Governance Reality | S3 Guidance | Projects | Detection Signals |
|---|---|---|---|---|---|
| Google | US | Single-company governance | S3 = 1–2 | Angular, Go, TensorFlow, Flutter, V8 | `google.golang.org`, `angular.io`, Google copyright headers |
| Meta | US | Single-company governance | S3 = 1–2 | React, PyTorch (now LF), Llama | `reactjs.org`, Meta copyright, but check if transferred to foundation |
| Microsoft | US | Single-company governance | S3 = 1–2 | VS Code, TypeScript, .NET, PowerShell | Microsoft copyright headers, `dotnet` |
| HashiCorp | US | Single-company, BSL-licensed | S3 = 1–2 | Terraform, Vault, Consul, Nomad (BSL since 2023) | `hashicorp.com`, BSL-1.1 license |
| Elastic | US (NL origin) | Single-company, SSPL/Elastic License | S3 = 2 | Elasticsearch, Kibana, Logstash | `elastic.co`, Elastic License |
| MongoDB | US | Single-company, SSPL | S3 = 2 | MongoDB | `mongodb.com`, SSPL |
| Redis Ltd | US | Single-company (Redis fork → Valkey under LF) | S3 = 2 | Redis (post-license change) | `redis.io`, Redis Source Available License |
| Vercel | US | Single-company | S3 = 1–2 | Next.js | `vercel.com`, Vercel copyright |
| Automattic | US | Single-company | S3 = 2 | WordPress (note: WordPress Foundation exists but Automattic dominates) | `automattic.com`, WordPress mentions |
| Grafana Labs | SE/US | Single-company, AGPL | S3 = 3 | Grafana, Loki, Tempo, Mimir | `grafana.com`, AGPL from Grafana Labs |
| GitLab | US | Single-company, open-core | S3 = 2–3 | GitLab CE/EE | `gitlab.com`, GitLab copyright |
| Canonical | UK | Single-company | S3 = 3 | Ubuntu, Snap | `canonical.com`, Canonical CLA |
| Red Hat (IBM) | US | Corporate steward, community projects | S3 = 3–4 | Fedora, CentOS Stream, Podman, Ansible | `redhat.com`, Red Hat copyright |
| SUSE | DE (EQT-owned) | EU-based, corporate steward | S3 = 3–4 | openSUSE, Rancher | `suse.com`, SUSE copyright |

## Community-Governed Projects (No Foundation)

Some significant projects are community-governed without a formal foundation:

| Project | Governance | S3 Guidance | Detection Signals |
|---|---|---|---|
| Debian | Debian Constitution, elected DPL | S3 = 7 | `debian.org`, DFSG, Debian Social Contract |
| FreeBSD | Core team, elected | S3 = 6 | `freebsd.org` |
| Arch Linux | Trusted User system | S3 = 6 | `archlinux.org` |
| PostgreSQL (PGDG) | PostgreSQL Global Development Group, meritocratic | S3 = 7 | `postgresql.org`, PGDG mentions |
| MariaDB | MariaDB Foundation (FI) | S3 = 7 | `mariadb.org`, MariaDB Foundation mentions |
| Nextcloud | Nextcloud GmbH (DE) | EU-based, AGPLv3 | S3 = 4–5 | `nextcloud.com`, Nextcloud CLA |
| Keycloak | Red Hat (IBM) → CNCF incubating | S3 = 5 | `keycloak.org`, CNCF status |

## CLA vs DCO

| Mechanism | S3 Impact | Rationale |
|---|---|---|
| No CLA, no DCO | Neutral | No explicit IP assignment |
| DCO (Developer Certificate of Origin) | Neutral to +1 | Lightweight, doesn't transfer rights |
| CLA with foundation (Apache ICLA, Eclipse CLA) | Neutral | Rights held by non-profit |
| CLA with corporate owner | S3 -1 to -2 | Company accumulates IP rights; can relicense |
| CLA with relicensing rights | S3 -2 to -3 | Company can switch to proprietary (as HashiCorp, Redis, Elastic did) |

Detection: search for `CLA`, `CONTRIBUTING.md` mentioning contributor agreements, `.github/CLA.md`, `DCO`, `Signed-off-by` in commit messages.

## Assessment Workflow

When evaluating S3 for a dependency or the project itself:

1. Check LICENSE/NOTICE for foundation affiliation
2. Check README for badges (CNCF graduated, Apache project, Eclipse project)
3. Check package metadata (`author`, `organization` fields)
4. Run `git log --format='%ae' | sort | uniq -c | sort -rn | head -20` to assess contributor diversity
5. If >80% commits from single email domain → S3 ≤ 3 regardless of nominal governance
6. Check for CLA in CONTRIBUTING.md
7. Look up the governing entity in the tables above
8. Apply the S3 score, adjusted for contributor diversity
