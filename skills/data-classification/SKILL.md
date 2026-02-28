---
name: data-classification
user-invocable: false
description: |
  Detection patterns for data types (personal, financial, health, critical
  infrastructure) with mapping to applicable EU regulations and S1 scoring
  implications. Bridges the eu-regulatory skill to actual codebase signals.
---

## How to Use This Reference

- During scanning phases 2–5, look for data type indicators alongside vendor detection
- When data type is identified, cross-reference with the eu-regulatory skill to determine applicable regulations
- Use the sensitivity tier to adjust how aggressively to score S1 — higher sensitivity = stricter scoring
- Data classification findings should appear in the Flags section of the report
- If no data processing is detected (docs-only repo, static site), note "no data processing detected" and skip data classification

## Sensitivity Tiers

| Tier | Data Types | S1 Strictness | Regulatory Trigger |
|---|---|---|---|
| **Critical** | Health (ePHI), biometric, genetic, judicial, minors' data | S1 penalties doubled; US vendor = S1 ≤ 1 | GDPR Art. 9 (special categories), national health data laws |
| **High** | Financial transactions, payment data, credit scores, tax records | S1 penalties +50%; US vendor = S1 ≤ 2 | DORA, PSD2, PCI-DSS |
| **Standard** | Personal data (name, email, address, phone, IP, cookies) | Normal S1 scoring from vendor-db | GDPR |
| **Low** | Aggregated analytics, anonymised data, public data, code, docs | S1 penalties halved; focus on availability risk not data protection | Minimal regulatory trigger |

When multiple data types are present, score based on the **highest sensitivity tier** detected.

## Personal Data Detection (GDPR)

### Direct Identifiers

| Signal | Detection Patterns | Confidence | Notes |
|---|---|---|---|
| Email addresses | `email`, `e-mail`, `mail_address`, `user_email`, `EMAIL_FIELD` | High | Almost always personal data |
| Names | `first_name`, `last_name`, `full_name`, `display_name`, `username` in DB schemas/models | Medium | Could be usernames vs real names |
| Phone numbers | `phone`, `telephone`, `mobile`, `phone_number`, `tel` | High | Personal data |
| Physical addresses | `address`, `street`, `city`, `postal_code`, `zip_code`, `country` in user context | High | Personal data |
| National IDs | `ssn`, `social_security`, `nif`, `nin`, `bsn`, `national_id`, `passport`, `id_card` | Critical | Special category adjacent |
| IP addresses | `ip_address`, `client_ip`, `remote_addr`, `x-forwarded-for` | Medium | Personal data under GDPR |
| Date of birth | `date_of_birth`, `dob`, `birth_date`, `birthday` | High | Personal data; can indicate minors |

### Indirect / Behavioural

| Signal | Detection Patterns | Confidence | Notes |
|---|---|---|---|
| User tracking | `analytics`, `tracking`, `pixel`, `gtag`, `ga(`, `mixpanel`, `segment`, `amplitude`, `hotjar` | High | Behavioural profiling; cookie consent required |
| Cookies | `cookie`, `set-cookie`, `cookie-consent`, `gdpr-consent`, `cookie-banner` | Medium | Indicates personal data processing awareness |
| Session data | `session`, `session_id`, `jwt`, `access_token`, `refresh_token` | Medium | Contains or references personal data |
| Logging with PII | `logger.info.*user`, `console.log.*email`, `log.*request` with user context | Medium | PII in logs is a common oversight |
| Geolocation | `latitude`, `longitude`, `geolocation`, `geoip`, `location` in user context | High | Personal data under GDPR |
| Device fingerprinting | `user-agent`, `fingerprint`, `device_id`, `browser_fingerprint` | High | GDPR and ePrivacy |

### Data Subject Indicators

| Signal | Detection Patterns | Implications |
|---|---|---|
| User registration | `signup`, `register`, `create_account`, `onboarding` | System processes personal data at scale |
| User profiles | `profile`, `account_settings`, `preferences` | Stored personal data |
| Contact forms | `contact_form`, `inquiry`, `support_ticket` | Personal data collected |
| Newsletter/marketing | `subscribe`, `newsletter`, `mailing_list`, `unsubscribe` | Marketing consent (GDPR Art. 6/7) |
| Children/minors | `age_gate`, `parental_consent`, `age_verification`, `COPPA` | Critical tier; GDPR Art. 8 |

## Financial Data Detection (DORA / PSD2)

| Signal | Detection Patterns | Tier | Regulatory Link |
|---|---|---|---|
| Payment processing | `stripe`, `adyen`, `mollie`, `payment_intent`, `charge`, `refund` | High | PSD2, PCI-DSS |
| Card data | `card_number`, `cvv`, `cvc`, `expiry`, `pan`, `cardholder` | Critical | PCI-DSS (never store CVV) |
| Bank accounts | `iban`, `bic`, `swift`, `account_number`, `routing_number`, `sort_code` | High | DORA, PSD2 |
| Transactions | `transaction`, `transfer`, `balance`, `ledger`, `debit`, `credit` | High | DORA |
| Credit/scoring | `credit_score`, `credit_check`, `risk_score`, `underwriting` | High | GDPR Art. 22 (automated decisions) |
| Cryptocurrency | `wallet_address`, `blockchain`, `smart_contract`, `web3`, `ethers` | High | MiCA regulation |
| Insurance | `policy`, `claim`, `premium`, `actuarial`, `underwriting` | High | DORA (insurance entities) |

## Health Data Detection

| Signal | Detection Patterns | Tier | Regulatory Link |
|---|---|---|---|
| Patient records | `patient`, `patient_id`, `medical_record`, `ehr`, `emr` | Critical | GDPR Art. 9, national health laws |
| Health standards | `hl7`, `fhir`, `dicom`, `icd-10`, `snomed`, `loinc` | Critical | Health data interoperability standards |
| Diagnoses | `diagnosis`, `condition`, `symptom`, `prescription`, `medication` | Critical | GDPR Art. 9 |
| Biometric | `biometric`, `fingerprint`, `face_recognition`, `iris`, `voice_print` | Critical | GDPR Art. 9 |
| Genetic | `genetic`, `dna`, `genome`, `sequencing`, `variant` | Critical | GDPR Art. 9 |
| Mental health | `therapy`, `counseling`, `mental_health`, `psychiatric` | Critical | GDPR Art. 9, heightened sensitivity |
| Fitness/wellness | `heart_rate`, `steps`, `calories`, `sleep_data`, `health_kit` | High | Grey area; may be Art. 9 depending on context |

## Critical Infrastructure Detection (NIS2)

| Signal | Detection Patterns | Sector | NIS2 Category |
|---|---|---|---|
| Energy/grid | `scada`, `modbus`, `dnp3`, `iec-61850`, `smart_grid`, `meter_reading` | Energy | Essential entity |
| Transport | `flight_data`, `rail_control`, `vessel_tracking`, `ais`, `traffic_management` | Transport | Essential entity |
| Water | `water_treatment`, `scada`, `plc`, `water_quality` | Water | Essential entity |
| Healthcare IT | `ehr`, `pacs`, `ris`, `hospital_information_system` | Health | Essential entity |
| Banking IT | `core_banking`, `swift`, `sepa`, `payment_gateway`, `clearing` | Banking | Essential entity (also DORA) |
| DNS/registry | `dns_server`, `domain_registry`, `tld`, `whois` | Digital infra | Essential entity |
| Cloud/hosting | Provider-side infrastructure management code | Digital infra | Essential entity |
| ICT service management | `itsm`, `service_desk`, `incident_management` (B2B) | ICT management | Important entity |
| Postal/courier | `shipment`, `tracking`, `delivery_management`, `parcel` | Postal | Important entity |
| Food | `food_safety`, `haccp`, `traceability`, `batch_tracking` | Food | Important entity |

## Assessment Workflow

When scanning a codebase:

1. **Run detection patterns** against source code, database schemas/models, config files, and API definitions
2. **Classify detected data** into sensitivity tiers using the tables above
3. **Determine applicable regulations** by cross-referencing with the eu-regulatory skill
4. **Adjust S1 scoring** based on sensitivity tier:
   - Critical tier: tighten all S1 scores (US vendor hosting critical health data → S1 = 0–1)
   - High tier: apply S1 penalties more strictly
   - Standard tier: use normal vendor-db S1 guidance
   - Low tier: relax S1 scoring; focus reporting on availability and portability
5. **Generate flags** for data classification findings:
   - Critical tier detected → severity: critical
   - High tier detected → severity: warning
   - Standard tier detected → severity: info
6. **Note in report** what data types were detected and which regulations apply

## Flag Templates

| Tier | Trigger | Flag Text Template |
|---|---|---|
| Critical | Health/biometric data + non-EU hosting | "Critical: [data type] detected ([file:line]); hosted on [vendor] (S1 ≤ [score]); GDPR Art. 9 special category data requires heightened protection" |
| Critical | Minors' data + non-EU hosting | "Critical: minors' data indicators detected ([file:line]); GDPR Art. 8 applies; non-EU hosting significantly increases regulatory risk" |
| High | Financial data + non-EU hosting | "Warning: financial data processing detected ([file:line]); [regulation] applies; [vendor] hosting exposes to [jurisdiction] government access" |
| Standard | Personal data + non-EU hosting | "Info: personal data processing detected ([file:line]); GDPR applies; ensure transfer mechanism (SCCs/DPF) is in place for [vendor]" |
| NIS2 | Critical infra indicators | "Warning: NIS2-relevant sector indicators detected ([patterns]); supply chain sovereignty requirements apply under NIS2 Art. 21" |
