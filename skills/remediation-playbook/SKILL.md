---
name: remediation-playbook
user-invocable: false
description: |
  Structured remediation playbooks for each DAS quadrant. Provides the
  DAS assessor with concrete, prioritised action templates for the
  Recommended Actions section of every report.
---

# DAS Remediation Playbooks

After computing quadrant placement, use the matching playbook below to write
the **Recommended Actions** section of the report. Adapt actions to the
specific findings — do not copy verbatim; instead, reference the actual
vendors, components, and layers detected during the scan.

Rules:
- Every recommended action must link back to a specific flag or score from the assessment
- Recommend sovereign alternatives from the vendor-db skill when available
- Be concrete: name the technology to replace *and* the replacement
- Acknowledge trade-offs honestly — sovereignty improvements can have cost, performance, or feature implications
- If the codebase is documentation-only or has minimal technical signals, state that no remediation is needed and recommend monitoring for when code is added

---

## RED Quadrant — Not Sovereign, Not Portable (S < 5, CPS < 5)

**Posture: Urgent — high vendor dependency with high switching cost.**

This is the highest-risk position. The system is locked into non-sovereign vendors
*and* difficult to move. Remediation requires a phased approach to avoid disruption.

### Immediate (0–3 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Inventory and classify data flows** | Identify what data is exposed to CLOUD Act jurisdiction; prioritise by sensitivity |
| 2 | **Contractual review** | Review vendor contracts for data residency clauses, exit provisions, SLA guarantees |
| 3 | **Introduce abstraction interfaces** | Add adapter/port layers around the most tightly coupled vendor SDKs; do not migrate yet — just decouple |
| 4 | **Encrypt data at rest and in transit** | Use client-side encryption with keys you control; reduces exposure even on non-sovereign infra |
| 5 | **Establish exit criteria** | Define measurable thresholds (cost, timeline, risk) that trigger migration |

### Short-term (3–12 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Migrate data layer first** | Data has the highest sovereignty impact (S1) and is hardest to move later; target EU-hosted open-source databases |
| 2 | **Containerise workloads** | Package applications as OCI containers to decouple from cloud compute services |
| 3 | **Replace vendor-specific IaC** | Move from CloudFormation/ARM to Terraform or OpenTofu with cloud-agnostic modules |
| 4 | **Adopt standard protocols** | Replace proprietary messaging (SQS, SNS) with AMQP/MQTT; replace proprietary auth with OIDC/OAuth2 |
| 5 | **Set up parallel sovereign environment** | Deploy a staging/test environment on an EU provider to validate migration path |

### Long-term (12+ months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Complete infrastructure migration** | Move production workloads to sovereign infrastructure |
| 2 | **Replace remaining SaaS dependencies** | Migrate collaboration, monitoring, and DevOps tools to self-hosted or EU alternatives |
| 3 | **Establish governance** | Create internal policies for technology selection requiring sovereignty assessment before adoption |
| 4 | **Re-assess** | Run DAS again to verify improvement; target Green quadrant |

### Common Pitfalls

- **Big-bang migration** — resist the urge to move everything at once; phased migration reduces risk
- **Sovereign-washing** — sovereign cloud programs (e.g., Bleu, S3NS) reduce but do not eliminate CLOUD Act exposure; score them S1 = 3–5, not S1 = 7+
- **Ignoring data gravity** — large datasets are expensive to move; start migration early
- **Neglecting operations** — migrating code without migrating monitoring, CI/CD, and runbooks creates operational risk

---

## BLUE Quadrant — Portable but Not Sovereign (S < 5, CPS ≥ 5)

**Posture: Strategic opportunity — the system is portable enough to migrate.**

Good news: the system's portability means migration is feasible. The focus is on
choosing the right sovereign target and executing the move.

### Immediate (0–3 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Map vendor exposure** | List every component with S1 ≤ 2; these are migration candidates |
| 2 | **Evaluate sovereign alternatives** | For each vendor-locked component, evaluate EU alternatives from the vendor-db; run PoC on top 2 options |
| 3 | **Encrypt sensitive data** | Client-side encryption as interim protection during migration planning |
| 4 | **Review data residency** | Verify current data hosting regions; reconfigure to EU regions where possible as a quick win |

### Short-term (3–12 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Migrate infrastructure** | Move cloud hosting to an EU provider; portability is already there so focus on DNS, networking, and storage migration |
| 2 | **Replace SaaS dependencies** | Swap non-sovereign SaaS (monitoring, auth, payments) for sovereign alternatives |
| 3 | **Update CI/CD pipeline** | Point deployments at sovereign infrastructure; migrate from GitHub Actions to self-hosted GitLab CI if needed |
| 4 | **Validate portability** | Run the system on the new infrastructure; confirm no hidden vendor dependencies surfaced |

### Long-term (12+ months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Decommission non-sovereign accounts** | Remove old cloud provider accounts once migration is verified |
| 2 | **Establish selection policy** | Require sovereignty assessment for all new technology choices |
| 3 | **Re-assess** | Target Green quadrant |

### Common Pitfalls

- **Underestimating hidden dependencies** — a portable codebase may still depend on vendor-specific CI/CD, DNS, CDN, or secret management
- **Region ≠ sovereignty** — running on `eu-west-1` does not make AWS sovereign; the vendor is still US-headquartered and subject to CLOUD Act
- **Ignoring SaaS layer** — migrating infra while keeping GitHub, Datadog, and Auth0 leaves significant exposure

---

## YELLOW Quadrant — Sovereign but Not Portable (S ≥ 5, CPS < 5)

**Posture: Modernise — sovereignty is sound but the system is hard to move.**

The system is hosted and governed appropriately, but vendor lock-in or technical
debt makes future migration difficult. Focus on increasing portability without
sacrificing sovereignty.

### Immediate (0–3 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Identify portability bottlenecks** | List components with P1–P5 ≤ 3; these are the main lock-in points |
| 2 | **Add abstraction layers** | Introduce interfaces/adapters around tightly coupled components (especially data and integration layers) |
| 3 | **Document deployment** | Write DEPLOYMENT.md, docker-compose, or Helm charts if missing; undocumented deployment is a portability blocker |

### Short-term (3–12 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Containerise** | Package all services as OCI containers; this immediately improves P1 and P4 |
| 2 | **Standardise data access** | Replace proprietary database features with standard SQL; add migration tooling (Flyway, Liquibase, Alembic) |
| 3 | **Adopt standard APIs** | Document APIs with OpenAPI/AsyncAPI; replace proprietary protocols with standard ones (AMQP, OIDC, S3-compatible) |
| 4 | **Introduce cloud-agnostic IaC** | Replace provider-specific IaC with Terraform/OpenTofu modules that can target multiple providers |

### Long-term (12+ months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Validate multi-target deployment** | Prove the system can deploy to at least two independent providers |
| 2 | **Eliminate proprietary data formats** | Migrate any remaining vendor-specific storage to open formats |
| 3 | **Re-assess** | Target Green quadrant |

### Common Pitfalls

- **Over-abstraction** — don't add abstraction layers where there's no realistic alternative (e.g., abstracting SQLite is pointless)
- **Breaking sovereignty while modernising** — don't introduce non-sovereign tools (GitHub Actions, Datadog) just because they're portable
- **Gold-plating** — some lock-in is acceptable if the component is low-risk and unlikely to need migration

---

## GREEN Quadrant — Sovereign and Portable (S ≥ 5, CPS ≥ 5)

**Posture: Maintain — the system is well-positioned. Focus on preservation and contribution.**

The system scores well on both axes. The goal is to maintain this position and
prevent regression as the system evolves.

### Immediate (0–3 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Review any warning-level flags** | Even in Green, individual dimensions may have room for improvement |
| 2 | **Document sovereignty decisions** | Record why specific technology choices were made; this prevents future contributors from regressing |
| 3 | **Automate DAS checks** | Consider running DAS assessment in CI to catch sovereignty regressions when new dependencies are added |

### Short-term (3–12 months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Contribute upstream** | If using open-source sovereign tools, contribute back to strengthen the ecosystem |
| 2 | **Share patterns** | Document the architecture patterns that achieved Green status for other teams |
| 3 | **Monitor regulatory changes** | EU regulations (NIS2, DORA, EUCS) may raise the bar; stay ahead |

### Long-term (12+ months)

| Priority | Action | Rationale |
|----------|--------|-----------|
| 1 | **Periodic re-assessment** | Re-run DAS annually or when major dependencies change |
| 2 | **Mentor other teams** | Help other projects in Red/Blue quadrants learn from this system's approach |

### Common Pitfalls

- **Complacency** — a Green score today doesn't mean Green tomorrow; new dependencies, acquisitions (e.g., a sovereign vendor acquired by a US company), or regulatory changes can shift the score
- **Assuming Green = perfect** — a composite of 5.1 / 5.1 is technically Green but barely; review sub-dimension scores for weakness

---

## Cross-Quadrant Guidance

### Prioritisation Heuristic

When multiple components need remediation, prioritise by:

1. **Data layer** — highest sovereignty impact, hardest to move later
2. **Infrastructure layer** — determines jurisdiction for everything above
3. **Integration layer** — vendor SDKs create transitive dependencies
4. **Operations layer** — CI/CD and monitoring are often overlooked
5. **Application layer** — usually most portable already
6. **Presentation layer** — typically least coupled

### Quick Wins (Any Quadrant)

These improve scores with minimal effort:

| Action | Dimensions Improved |
|--------|-------------------|
| Switch to EU cloud regions | S1 +2–3 (but doesn't change CLOUD Act exposure) |
| Add client-side encryption | S1 +1 (risk mitigation, not elimination) |
| Containerise workloads | P1 +2, P4 +2 |
| Add OpenAPI spec | P3 +2 |
| Write DEPLOYMENT.md | P4 +1 |
| Add database migration tooling | P2 +1 |
| Replace proprietary auth with OIDC | P3 +2, S1 +1 |

### When NOT to Migrate

Sovereignty migration is not always the right answer:

- **Low-sensitivity systems** — a public marketing site on Netlify/Vercel may not warrant migration cost
- **Contractual protections in place** — some vendor agreements provide adequate legal protection
- **Transitional state** — if the system is being decommissioned within 12 months, invest in encryption rather than migration
- **No sovereign alternative exists** — for some niche services, no EU equivalent is available; document the risk and monitor

Always state these trade-offs in the report rather than blanket-recommending migration.
