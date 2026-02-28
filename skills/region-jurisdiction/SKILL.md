---
name: region-jurisdiction
user-invocable: false
description: |
  Maps cloud provider region codes to countries, jurisdictions, and S1 score
  impact. Includes EU adequacy decision countries and special partitions.
  Used by the DAS assessor when interpreting region strings found during scanning.
---

# Region-to-Jurisdiction Mapping

When the scanner detects region strings in IaC files, config, environment variables,
or connection strings, use this reference to determine jurisdictional impact on S1.

## How to Use

1. Match detected region strings against the tables below
2. Determine the **country** and whether it is **EU/EEA**, **EU-adequate**, or **other**
3. Apply the S1 adjustment — but remember: region alone does not determine sovereignty. The vendor's HQ jurisdiction matters too (see vendor-db skill)
4. A US vendor in an EU region → S1 baseline 3–5 (EU data residency, but CLOUD Act applies to parent)
5. An EU vendor in an EU region → S1 ≥ 7

## S1 Impact by Jurisdiction Category

| Category | Examples | S1 Impact |
|----------|----------|-----------|
| EU/EEA member state | France, Germany, Netherlands | EU vendor: S1 ≥ 7; US vendor: S1 = 3–5 |
| EU adequacy decision | Switzerland, UK, Japan, South Korea, Canada, Israel, New Zealand | S1 = 3–4 (data transfer legal, but not EU jurisdiction) |
| US / CLOUD Act | US states, US GovCloud | S1 ≤ 2 |
| China | Mainland China regions | S1 ≤ 1 |
| Other (no adequacy) | Brazil, India, Singapore, Australia | S1 ≤ 2 |

---

## AWS Regions

### EU/EEA

| Region Code | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `eu-west-1` | Ireland | IE | EU |
| `eu-west-2` | London | GB | EU-adequate (post-Brexit) |
| `eu-west-3` | Paris | FR | EU |
| `eu-central-1` | Frankfurt | DE | EU |
| `eu-central-2` | Zurich | CH | EU-adequate |
| `eu-south-1` | Milan | IT | EU |
| `eu-south-2` | Spain | ES | EU |
| `eu-north-1` | Stockholm | SE | EU |
| `il-central-1` | Tel Aviv | IL | EU-adequate |

### US

| Region Code | Location | S1 Note |
|-------------|----------|---------|
| `us-east-1` | N. Virginia | US — CLOUD Act |
| `us-east-2` | Ohio | US — CLOUD Act |
| `us-west-1` | N. California | US — CLOUD Act |
| `us-west-2` | Oregon | US — CLOUD Act |
| `us-gov-east-1` | GovCloud East | US — FedRAMP; S1 ≤ 1 for EU purposes |
| `us-gov-west-1` | GovCloud West | US — FedRAMP; S1 ≤ 1 for EU purposes |

### Asia-Pacific

| Region Code | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `ap-northeast-1` | Tokyo | JP | EU-adequate |
| `ap-northeast-2` | Seoul | KR | EU-adequate |
| `ap-northeast-3` | Osaka | JP | EU-adequate |
| `ap-southeast-1` | Singapore | SG | No adequacy; S1 ≤ 2 |
| `ap-southeast-2` | Sydney | AU | No adequacy; S1 ≤ 2 |
| `ap-southeast-3` | Jakarta | ID | No adequacy; S1 ≤ 2 |
| `ap-southeast-4` | Melbourne | AU | No adequacy; S1 ≤ 2 |
| `ap-southeast-5` | Malaysia | MY | No adequacy; S1 ≤ 2 |
| `ap-south-1` | Mumbai | IN | No adequacy; S1 ≤ 2 |
| `ap-south-2` | Hyderabad | IN | No adequacy; S1 ≤ 2 |
| `ap-east-1` | Hong Kong | HK | No adequacy; S1 ≤ 2 |

### Other

| Region Code | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `ca-central-1` | Montreal | CA | EU-adequate |
| `ca-west-1` | Calgary | CA | EU-adequate |
| `sa-east-1` | São Paulo | BR | No adequacy; S1 ≤ 2 |
| `af-south-1` | Cape Town | ZA | No adequacy; S1 ≤ 2 |
| `me-south-1` | Bahrain | BH | No adequacy; S1 ≤ 2 |
| `me-central-1` | UAE | AE | No adequacy; S1 ≤ 2 |
| `cn-north-1` | Beijing | CN | China partition; S1 ≤ 1 |
| `cn-northwest-1` | Ningxia | CN | China partition; S1 ≤ 1 |

---

## Azure Regions

### EU/EEA

| Region Name | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `westeurope` | Netherlands | NL | EU |
| `northeurope` | Ireland | IE | EU |
| `francecentral` | Paris | FR | EU |
| `francesouth` | Marseille | FR | EU |
| `germanywestcentral` | Frankfurt | DE | EU |
| `germanynorth` | Berlin | DE | EU |
| `swedencentral` | Gävle | SE | EU |
| `swedensouth` | Malmö | SE | EU |
| `norwayeast` | Oslo | NO | EEA |
| `norwaywest` | Stavanger | NO | EEA |
| `italynorth` | Milan | IT | EU |
| `polandcentral` | Warsaw | PL | EU |
| `spaincentral` | Madrid | ES | EU |
| `switzerlandnorth` | Zurich | CH | EU-adequate |
| `switzerlandwest` | Geneva | CH | EU-adequate |

### US

| Region Name | Location | S1 Note |
|-------------|----------|---------|
| `eastus` | Virginia | US — CLOUD Act |
| `eastus2` | Virginia | US — CLOUD Act |
| `centralus` | Iowa | US — CLOUD Act |
| `westus` | California | US — CLOUD Act |
| `westus2` | Washington | US — CLOUD Act |
| `westus3` | Arizona | US — CLOUD Act |
| `southcentralus` | Texas | US — CLOUD Act |
| `northcentralus` | Illinois | US — CLOUD Act |
| `westcentralus` | Wyoming | US — CLOUD Act |
| `usgovvirginia` | Virginia (Gov) | US — FedRAMP; S1 ≤ 1 |
| `usgovarizona` | Arizona (Gov) | US — FedRAMP; S1 ≤ 1 |

### Asia-Pacific

| Region Name | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `japaneast` | Tokyo | JP | EU-adequate |
| `japanwest` | Osaka | JP | EU-adequate |
| `koreacentral` | Seoul | KR | EU-adequate |
| `koreasouth` | Busan | KR | EU-adequate |
| `southeastasia` | Singapore | SG | No adequacy; S1 ≤ 2 |
| `eastasia` | Hong Kong | HK | No adequacy; S1 ≤ 2 |
| `australiaeast` | Sydney | AU | No adequacy; S1 ≤ 2 |
| `australiasoutheast` | Melbourne | AU | No adequacy; S1 ≤ 2 |
| `centralindia` | Pune | IN | No adequacy; S1 ≤ 2 |
| `southindia` | Chennai | IN | No adequacy; S1 ≤ 2 |

### Other

| Region Name | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `canadacentral` | Toronto | CA | EU-adequate |
| `canadaeast` | Quebec | CA | EU-adequate |
| `uksouth` | London | GB | EU-adequate |
| `ukwest` | Cardiff | GB | EU-adequate |
| `brazilsouth` | São Paulo | BR | No adequacy; S1 ≤ 2 |
| `southafricanorth` | Johannesburg | ZA | No adequacy; S1 ≤ 2 |
| `uaenorth` | Dubai | AE | No adequacy; S1 ≤ 2 |
| `chinanorth` | Beijing | CN | China; S1 ≤ 1 |
| `chinaeast` | Shanghai | CN | China; S1 ≤ 1 |

---

## GCP Regions

### EU/EEA

| Region Code | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `europe-west1` | Belgium | BE | EU |
| `europe-west2` | London | GB | EU-adequate |
| `europe-west3` | Frankfurt | DE | EU |
| `europe-west4` | Netherlands | NL | EU |
| `europe-west6` | Zurich | CH | EU-adequate |
| `europe-west8` | Milan | IT | EU |
| `europe-west9` | Paris | FR | EU |
| `europe-west10` | Berlin | DE | EU |
| `europe-west12` | Turin | IT | EU |
| `europe-southwest1` | Madrid | ES | EU |
| `europe-north1` | Finland | FI | EU |
| `europe-central2` | Warsaw | PL | EU |

### US

| Region Code | Location | S1 Note |
|-------------|----------|---------|
| `us-central1` | Iowa | US — CLOUD Act |
| `us-east1` | South Carolina | US — CLOUD Act |
| `us-east4` | Virginia | US — CLOUD Act |
| `us-east5` | Columbus | US — CLOUD Act |
| `us-west1` | Oregon | US — CLOUD Act |
| `us-west2` | Los Angeles | US — CLOUD Act |
| `us-west3` | Salt Lake City | US — CLOUD Act |
| `us-west4` | Las Vegas | US — CLOUD Act |
| `us-south1` | Dallas | US — CLOUD Act |

### Asia-Pacific

| Region Code | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `asia-northeast1` | Tokyo | JP | EU-adequate |
| `asia-northeast2` | Osaka | JP | EU-adequate |
| `asia-northeast3` | Seoul | KR | EU-adequate |
| `asia-southeast1` | Singapore | SG | No adequacy; S1 ≤ 2 |
| `asia-southeast2` | Jakarta | ID | No adequacy; S1 ≤ 2 |
| `asia-south1` | Mumbai | IN | No adequacy; S1 ≤ 2 |
| `asia-south2` | Delhi | IN | No adequacy; S1 ≤ 2 |
| `asia-east1` | Taiwan | TW | No adequacy; S1 ≤ 2 |
| `asia-east2` | Hong Kong | HK | No adequacy; S1 ≤ 2 |
| `australia-southeast1` | Sydney | AU | No adequacy; S1 ≤ 2 |
| `australia-southeast2` | Melbourne | AU | No adequacy; S1 ≤ 2 |

### Other

| Region Code | Location | Country | S1 Note |
|-------------|----------|---------|---------|
| `northamerica-northeast1` | Montreal | CA | EU-adequate |
| `northamerica-northeast2` | Toronto | CA | EU-adequate |
| `southamerica-east1` | São Paulo | BR | No adequacy; S1 ≤ 2 |
| `southamerica-west1` | Santiago | CL | No adequacy; S1 ≤ 2 |
| `me-west1` | Tel Aviv | IL | EU-adequate |
| `me-central1` | Doha | QA | No adequacy; S1 ≤ 2 |
| `africa-south1` | Johannesburg | ZA | No adequacy; S1 ≤ 2 |

---

## EU Adequacy Decisions

Countries with a valid EU adequacy decision (data transfers permitted without additional safeguards):

| Country | Status | Notes |
|---------|--------|-------|
| Andorra | Adequate | — |
| Argentina | Adequate | — |
| Canada | Adequate | Commercial organisations under PIPEDA only |
| Faroe Islands | Adequate | — |
| Guernsey | Adequate | — |
| Isle of Man | Adequate | — |
| Israel | Adequate | — |
| Japan | Adequate | Mutual recognition with EU |
| Jersey | Adequate | — |
| New Zealand | Adequate | — |
| South Korea | Adequate | — |
| Switzerland | Adequate | — |
| United Kingdom | Adequate | Post-Brexit decision; review due periodically |
| Uruguay | Adequate | — |
| United States | EU-US Data Privacy Framework | Requires certified organisations; does not override CLOUD Act for government access |

**Important:** EU-US Data Privacy Framework (DPF) provides a legal basis for transfers to *certified* US companies, but it does **not** prevent government access under CLOUD Act, FISA 702, or EO 12333. For sovereignty purposes, DPF-certified US vendors still score S1 ≤ 2–3.

---

## Detection Patterns

Common patterns in config files that indicate region selection:

```
# AWS
AWS_REGION=eu-west-1
AWS_DEFAULT_REGION=us-east-1
region = "eu-central-1"           # Terraform
provider "aws" { region = "..." }

# Azure
AZURE_REGION=westeurope
location = "francecentral"        # Terraform
azure_rm_resource_group { location = "..." }

# GCP
GOOGLE_CLOUD_REGION=europe-west1
region = "europe-west9"           # Terraform
gcloud config set compute/region ...
```

When multiple regions are detected (e.g., multi-region deployment), score based on the **least sovereign** region — data in any non-EU region exposes the system to that jurisdiction.
