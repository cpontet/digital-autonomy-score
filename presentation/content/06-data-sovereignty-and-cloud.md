# Data Sovereignty and Cloud

## Data Sovereignty

> How likely is it that US Authorities emit a legal request to your cloud or SaaS vendor to give them access to your data?

This provocative opening question sets the stage for understanding the legal and geopolitical risks European organizations face when relying on US-based cloud and SaaS providers.

---

## The CLOUD Act

The **CLOUD Act** (**Clarifying Lawful Overseas Use of Data**) is a US law enacted in **2018** that allows US authorities to demand data from US-based tech companies, **even if the data is stored outside the United States**.

The implications for European organizations are significant:

- **Data Sovereignty Risk** -- Data stored by EU companies with US-based cloud providers (e.g., Microsoft, Google, Amazon) may be subject to US legal requests, including criminal investigations.
- **Potential GDPR Conflict** -- The CLOUD Act may clash with EU data protection laws (GDPR), especially regarding data transfers outside the EU.
- **Compliance Challenges** -- EU companies face uncertainty over whose laws to follow if US authorities request data in ways that violate EU privacy laws.
- **Need for Due Diligence** -- When choosing cloud providers, EU companies must assess risks and legal obligations related to cross-border data requests.

---

## Cloud Weaponization

> How likely is it that AWS, Azure or GCP stop providing cloud services your system depends on, if the US government request them to?

This question highlights the risk of **cloud weaponization** -- the possibility that US-based hyperscalers could be compelled by the US government to discontinue services to specific countries, organizations, or entities. Given that European infrastructure overwhelmingly depends on these providers, such an action would be devastating.

---

## Public Cloud IaaS Vendors in 2024

Up to **70% of worldwide workloads** run on the three major US hyperscalers:

- **AWS** -- 30-33% market share
- **Microsoft Azure** -- 20-24% market share
- **Google Cloud (GCP)** -- 10-12% market share

> **Figure:** On the right side of the slide, an IDC 2024 MarketScape quadrant chart maps cloud IaaS providers by Capabilities (y-axis) and Strategies (x-axis), divided into four tiers: Leaders, Major Players, Contenders, and Participants. **AWS** sits firmly in the Leaders quadrant at the top. **Google** and **Microsoft** are positioned at the boundary between Leaders and Major Players. **Oracle** appears in the Major Players zone. European providers are scattered across the lower tiers: **OVHcloud** and **IBM** appear as Major Players, **IONOS SE**, **T-Systems**, and **Orange** sit between Major Players and Contenders, while **Exoscale**, **Gcore**, **Aruba**, **OUTSCALE**, **Telefonica Tech**, **Anexia**, **plusserver**, **Cleura AB**, **Claranet**, and **TIM** occupy the Contenders and Participants zones.

> Sources: Statista -- "Amazon and Microsoft Stay Ahead in Global Cloud Market"; AWS vs Azure vs Google Cloud 2024 Comparison

---

## Worldwide SaaS and Cloud-Enabled Apps in 2024

The SaaS landscape is also built on top of the same US cloud infrastructure. Major SaaS and cloud-enabled applications are **built on AWS, Azure, and Google Cloud**.

> **Figure:** An IDC 2024 MarketScape quadrant chart maps worldwide SaaS and cloud-enabled applications by Capabilities (y-axis) and Strategies (x-axis). In the **Leaders** quadrant: **SAP (S/4HANA)**, **Microsoft (Dynamics 365)**, and **Oracle**. In the **Major Players** zone: **Infor**, **Workday**, **Epicor**, **Certinia**, **Acumatica**, **Oracle (NetSuite)**, **Sage Intacct**, **SAP (Business ByDesign)**, **Plex by Rockwell Automation**, **Deltek (Vantagepoint)**, **Deltek (Costpoint)**, **Ramco**, **Priority Software**. In the **Contenders** zone: **SAP (Business One)**, **Unit4**, **Rootstock**, **Deltek (Maconomy)**, **ECI Software**. The left side of the slide shows the logos of AWS, Azure, and Google Cloud, emphasizing that all these SaaS applications are built on US cloud platforms.

> Source: IDC, 2024

---

## "We're Doomed! ... Unless..."

> **Figure:** The slide displays the cover art of the board game "We're Doomed! The Game of Global Panic" by M. Horton (from Breaking Games), showing stylized silhouettes of world leaders against an orange background with a rocket in the center. The word "Unless..." is overlaid in white, signaling a transition from the alarming dependency analysis to potential response strategies.

This transitional slide acknowledges the severity of the situation while signaling that options and responses do exist.

---

## "I Should Start Migrating Away from US Public Cloud Now!"

This reactive impulse is presented as a natural first reaction to the dependency and sovereignty risks outlined in the previous slides. However, the presentation cautions against this knee-jerk response and instead advocates for a more nuanced, graduated approach.

---

## Gradual Response

The recommended approach is a **gradual response**, depending on your context and the **criticality of your digital assets**. Rather than an immediate, wholesale migration away from US cloud providers, organizations should assess their specific situation and adopt measures proportional to their risk exposure.

---

## Apply Public Cloud Best Practices

The first level of response is to **apply public cloud best practices** within existing US cloud environments:

- **Apply policies** -- enforce governance and compliance rules
- **Limit available regions** -- restrict deployments to EU regions only
- **Encrypt everything** -- ensure all data is encrypted at rest and in transit
- **Externalize your keys (HSM)** -- use Hardware Security Modules to manage encryption keys independently from the cloud provider
- **Plan for recovery (DRP)** -- establish Disaster Recovery Plans that account for provider disruption scenarios

---

## Sovereign Options Offered by Hyperscalers

**Hyperscalers are very aware of sovereignty issues** and already propose some options. The major US cloud providers have developed sovereign cloud offerings specifically designed to address European concerns about data residency, operational control, and legal jurisdiction.

---

## AWS European Sovereign Cloud

The **AWS European Sovereign Cloud** is a dedicated sovereign infrastructure offering with the following characteristics:

- **Fully Sovereign Infrastructure** -- Operated independently from existing AWS Regions
- **Located in Europe** -- All infrastructure and services run and reside within the European Union
- **Operated by EU Residents** -- Only EU residents will have control of operations and support
- **Independent Operations** -- Day-to-day operations managed only by EU-based personnel and entities
- **Data Residency and Access Controls** -- Designed to allow customers to keep all data and metadata within the EU
- **Familiar AWS Experience** -- Same APIs, services, and tools as standard AWS regions

> **Figure:** The right side of the slide shows a diagram titled "Sovereignty requirements of customers" with four pillars, each represented by an icon: (1) **Data residency** -- "I want to know where all my data is, and control where that data is stored and transferred to at all times." (2) **Operator Access Restriction** -- "I want to be sure that neither AWS nor a foreign government can access my data in the cloud." (3) **Resiliency and Survivability** -- "I want to be sure that I can sustain operations despite any kind of foreign disruption and influence." (4) **Operational Autonomy** -- "We want our digital industries and sectors to thrive and compete at the global level."

> Sources: AWS Digital Sovereignty; AWS Digital Sovereignty Pledge: Control without compromise; AWS re:Invent 2023 -- AWS European Sovereign Cloud: A closer look (SEC216)

---

## Microsoft Sovereign Cloud

Microsoft announced **comprehensive sovereign solutions empowering European organizations** (June 16, 2025, by Judson Althoff, Executive Vice President and Chief Commercial Officer).

The **Microsoft Sovereign Cloud** is described as the "most comprehensive set of sovereignty solutions, with integrated productivity, security and cloud platform." It is structured into three tiers:

### Sovereign Public Cloud
- Data stays in Europe, under European law
- **Data Guardian**: operations and access controlled by Europeans
- Sovereign controls for policy enforcement
- Applies to existing Europe cloud datacenter regions with no migration required

### Sovereign Private Cloud
- **Azure Local + Microsoft 365 Local**: integrated cloud and productivity
- Hybrid or disconnected deployment at your location
- Validated architecture and partner ecosystem
- Virtualization services

### National Partner Clouds
- For government and critical infrastructure criteria
- Government-approved local operator independent from Microsoft
- Clouds in **Germany (Delos Cloud)** and **France (Bleu)** with local ownership and isolated infrastructure

All three tiers share a **consistent management and development platform**.

> **Figure:** The slide shows a screenshot from the official Microsoft Blog, featuring a diagram of the three-tier Microsoft Sovereign Cloud architecture. The three columns -- Sovereign Public Cloud (green), Sovereign Private Cloud (teal), and National Partner Clouds (red) -- are arranged side by side with their respective features listed below each heading, connected at the bottom by a horizontal arrow labeled "Consistent management and development platform."

> Source: Announcing comprehensive sovereign solutions empowering European organizations -- The Official Microsoft Blog

---

## EU Already Protects Your Strategic Autonomy

The presentation concludes this section by noting that the **EU already protects your strategic autonomy**. Key aspects include:

- **Control over essential technologies** (e.g., cloud, AI, semiconductors)
- **Data sovereignty** (keeping data within EU jurisdiction)
- **Reduced dependence on non-EU tech giants**
- **Ability to set and enforce own digital standards and regulations**

These protections form part of Europe's broader strategy to maintain technological independence and ensure that European organizations have viable paths to sovereignty without abandoning the benefits of cloud computing altogether.
