# Assessment Tools

Where do we start? We need tools to help us make decisions about digital sovereignty. This chapter presents a practical toolkit for evaluating technology choices through the lenses of sovereignty and portability, along with strategic analysis frameworks for managing complex information systems.

## Software Over Hardware

When addressing digital sovereignty, **software** should be prioritized over **hardware**.

**Software (priority focus):**
- Most immediate and meaningful impact
- Many options available
- Constant evolution and investment
- Lots of decision factors to take into account

**Hardware (secondary focus):**
- Long-term strategic planning
- Not that many options
- Upfront investment
- Hardware supply chain heavily globalized

> **Figure:** Side-by-side comparison showing software code on the left and a hardware circuit board on the right, illustrating the two domains of sovereignty concern.

---

## Critical Systems Over Commodities

**Critical systems** (left) deserve sovereignty focus over **commodity systems** (right).

**Critical systems:**
- Directly contribute to your mission and objectives
- Specific to and depending on the business context
- Most vital components focusing on the core domain
- Derive a competitive advantage

**Commodity systems:**
- Secondary to the mission-critical systems
- Standardized solutions widely available on the global market
- Require significant investment but offer limited strategic value in the short term

> **Figure:** Left side shows a person working at multiple monitors with dashboards and analytics (representing critical business systems). Right side shows the Microsoft Word icon (representing a commodity tool).

---

## Objective Assessment Factors

Two complementary dimensions are used to objectively assess any technology component:

### Sovereignty

- Data control and privacy
- Security and trust
- Regulatory compliance
- Strategic autonomy

> **Figure:** A European shield icon with EU map silhouette, symbolizing data protection under European jurisdiction.

### Portability

- Compatibility and installability
- Avoid vendor lock-in
- Adaptability and replaceability
- Cost

> **Figure:** A European cloud icon with shipping containers, symbolizing the ability to move workloads between providers.

---

## Sovereignty Scale

A **sovereignty scale** from 0 to 10 rates technologies based on jurisdiction, ownership, governance, and licensing. Within open source, who can change the license matters more than the license itself.

| Score | Description | Examples |
|:-----:|-------------|----------|
| **0** | Proprietary technology owned by a private company with headquarters in the US subject to the CLOUD Act or in an autocratic country (e.g. Russia, China) | AWS (US), Oracle (US), Microsoft Azure (US), GCP (US), Alibaba (CN), Tencent (CN), Baidu (CN), Kaspersky (RU) |
| **1** | Proprietary technology owned by a private company with headquarters outside the EU | Samsung (KR), Rakuten (JP), Atlassian (AU) |
| **2** | Proprietary technology owned by a private company with headquarters in Europe but outside the EU | Exoscale (CH), Deliveroo (UK), Revolut (UK), Visma (NO) |
| **3** | Proprietary technology owned by a private company with headquarters within the EU | OVHcloud (FR), SAP (DE), Dassault Systemes (FR) |
| **4** | Proprietary technology maintained by a private company with source-available licenses | Elasticsearch (NL), MongoDB |
| **5** | Open-source technology owned by a single company that holds all the copyright (CLA) and can relicense, whatever the license | MySQL (GPL), Qt (LGPL), Grafana (AGPL), TensorFlow (Apache) |
| **6** | Open-source technology no one can relicense, but governed by one company or a US-domiciled foundation | Kubernetes, OpenSearch, OpenTofu, Valkey, Firefox, Nextcloud |
| **7** | Open-source technology no one can relicense, governed by an EU/neutral body or an independent multi-vendor community (permissive license) | Eclipse projects, PostgreSQL |
| **8** | Same as 7, under a copyleft license: it can be neither relicensed nor enclosed | Linux, LibreOffice |
| **9** | Federated open protocols with multiple independent implementations | Matrix protocol, ActivityPub, XMPP |
| **10** | Ratified international standards with multilateral governance | HTML, HTTP, TCP/IP, SMTP, PDF |

---

## Portability Scale

A **portability scale** from 0 to 10 rates technologies based on how easily they can be moved across platforms and environments.

| Score | Description | Details | Examples |
|:-----:|-------------|---------|----------|
| **0** | **Hardware/Platform Locked** | Only runs on specific hardware, systems, or tightly integrated environments. Requires substantial rewriting to move. | Embedded firmware for a single chipset, BIOS, device drivers for proprietary hardware |
| **1** | **Vendor-Locked APIs/Frameworks** | Deeply tied to one vendor's technology stack or OS, with no abstraction. | Windows kernel drivers, macOS-specific frameworks (like CoreML), Xbox-only games |
| **2** | **Native Applications with some abstraction** | App can only run on one OS, but uses standard OS APIs. | Windows .exe desktop apps, native Android or iOS apps written without cross-platform frameworks |
| **3** | **Language-specific but multi-platform via rebuild** | Can run on different platforms if recompiled/rebuilt, but no source/performance guarantees. | C/C++ apps using POSIX, Java Native Interface apps (JNI), Go binaries |
| **4** | **Portable with OS-level dependency** | Requires platform-specific dependencies or runtimes, but source code is mostly portable. | .NET Framework apps (not .NET Core), Qt apps with native builds, shell scripts with Unix/Linux specifics |
| **5** | **VM/Runtime dependent and supported across platforms** | Runs the same on any platform with the right runtime installed. | Java (JVM), Python, Node.js scripts, .NET Core/C# |
| **6** | **Abstraction layers for major platforms** | Uses cross-platform frameworks requiring adaptation for each target, some "write-once, tweak-everywhere." | Electron apps, React Native apps, Xamarin, Flutter |
| **7** | **Containerized applications** | Packaged with all dependencies for consistent deployment on any system running the container engine. | Docker containers, OCI containers |
| **8** | **Web applications with standard web stack** | Accessible on any device/browser with no platform dependencies, but relies on browser features. | HTML/CSS/JS web apps, PWAs (Progressive Web Apps) |
| **9** | **Interpreted/sandboxed environments** | Code executes identically in highly standardized or virtualized environments. | WebAssembly (Wasm), portable Python scripts |
| **10** | **Universal standards-compliant code** | Runs anywhere with virtually no modification, relying solely on universally adopted standards, designed for extreme portability and longevity. | ANSI C (portable code only), POSIX shell scripts, OpenAPI/RESTful services, SQL scripts (ANSI SQL only) |

---

## Prioritization Quadrant

The sovereignty and portability scores combine into a **prioritization quadrant** that guides action for each technology component.

> **Figure:** A 2x2 matrix with Sovereignty on the x-axis (Low to High) and Portability on the y-axis (Low to High), forming four colored quadrants.

### Top-Right: Portable and Sovereign (Green)
- **Best case** -- "Don't do anything"
- Action: **Maintain and leverage**
- Example: Open standards on EU cloud

### Top-Left: Portable but Not Sovereign (Blue)
- **Good case** -- "Low-hanging fruit"
- Action: **Move ASAP**
- Example: Docker on US cloud

### Bottom-Left: Not Portable and Not Sovereign (Red)
- **Worst case** -- "Locked-in and at risk"
- Action: **Migrate or replace ASAP**
- Example: SaaS on non-EU provider

### Bottom-Right: Not Portable but Sovereign (Yellow)
- **Questionable case** -- "Sovereign but hard to move"
- Action: **Modernize for portability**
- Example: On-prem closed system

---

## Sovereignty/Portability Quiz

Estimate each scenario in terms of sovereignty and portability.

### Scenario 1

**A company deploys its critical database using Managed MongoDB Atlas hosted entirely on AWS infrastructure (US region), with MongoDB using the Server Side Public License (SSPL).**

**Sovereignty Score: 4**
MongoDB is a private company offering source-available licenses, but the entire setup is hosted on US infrastructure, subject to CLOUD Act risks.

**Portability Score: 7**
Managed MongoDB can be containerized or the database "dumped" and restored elsewhere, but the managed implementation is tied to cloud services. Still, MongoDB itself is typically portable (especially the open source version).

---

### Scenario 2

**A public sector agency builds an online citizen portal using an open-source web application stack:**
- Back end: Python/Flask
- Front end: React
- Deployed as Docker containers on a European sovereign cloud provider (OVHcloud, France)
- The team follows the ActivityPub protocol for some services

**Sovereignty Score: 8-9**
Uses open-source technologies, follows federated and open standards (ActivityPub), and is hosted on an EU-compliant cloud. Slight ambiguity depending on the licensing of all stack components.

**Portability Score: 7-8**
Docker containers provide high portability across platforms (score 7); since it is a web app using standard web technologies, it nears score 8.

---

### Scenario 3

**A fintech startup develops its new desktop trading application as a Windows-only executable in C++ using proprietary Microsoft libraries and distributes it via the Microsoft Store.**

**Sovereignty Score: 0**
Fully reliant on proprietary US technology, distributed and managed via Microsoft; subject to US law and CLOUD Act.

**Portability Score: 2**
Native application for a single OS, uses standard OS APIs -- could only run on Windows, requiring substantial rewrite for any other platform.

---

## Tools for Analysing Complex Systems

> "There are too many components in our Information System"

When information systems grow large, specialized strategic tools are needed to analyse and decompose them for sovereignty assessment.

## Wardley Mapping

Use **Wardley Maps** to analyse and decompose your information systems.

> "A map is visual and context-specific, but instead of magnetic North, the anchor is the User being served and their corresponding needs."

> **Figure:** A complete Wardley Map with two axes -- the vertical axis represents the **Value Chain** (from "Invisible" at the bottom to "Visible" at the top), and the horizontal axis represents **Evolution** (from "Genesis" through "Custom Built" and "Product (+rental)" to "Commodity (+utility)"). Components plotted include Customer, Online Image Manipulation, Print, Online Photo Storage, Web Site, CRM, Platform, Compute, Data Centre, and Power, connected by dependency lines. Courtesy of Simon Wardley, CC BY-SA 4.0.

### Step 1: Users and Needs

Start by identifying the **users** and their **needs**. In the example, the Customer needs Online Image Manipulation, Online Photo Storage, Print, and Web Site.

> **Figure:** A simple tree diagram showing "Customer" at the top connected to four needs: Online Image Manipulation, Online Photo Storage, Print, and Web Site.

### Step 2: Capabilities

Identify all the **capabilities** required to fulfill those needs, and position them along the Value Chain axis (visible to invisible).

> **Figure:** A scatter plot on the Value Chain axis showing all components: Customer-facing services at the top (Online Image Manipulation, Print, Online Photo Storage, Web Site) and infrastructure components lower down (CRM, Data Centre, Platform, Power, Compute).

### Step 3: Value Chain

Map the **dependency relationships** between components using "Needs" connections, forming the full value chain.

> **Figure:** The same components now connected by labeled "Needs" arrows forming a dependency chain: Customer needs services, which need Web Site, which needs CRM and Platform, which need Compute, which needs Data Centre, which needs Power.

### Step 4: Climate (Evolution)

Position each component along the **Evolution** axis to understand its maturity stage:

| Genesis | Custom | Product (+rental) | Commodity (+utility) |
|---------|--------|--------------------|----------------------|
| Focus on exploring | Focus on learning and developing the craft | Focus on refining and improving | Focus on ruthlessly removing deviation, industrialising, and increasing operational efficiency |

> **Figure:** An evolution arrow from left (Genesis) to right (Commodity), with four stages described by their focus areas.

### Step 5: The Complete Map

The final **Wardley Map** combines all four elements: users, capabilities, value chain dependencies, and evolutionary positioning.

> **Figure:** The complete Wardley Map with all components positioned on both axes and connected by dependency lines. Genesis-stage items (Online Image Manipulation, Online Photo Storage) appear on the left; Product-stage items (Print, Web Site, CRM, Platform) in the middle; and Commodity-stage items (Compute, Data Centre, Power) on the right. Courtesy of Simon Wardley, CC BY-SA 4.0.

---

## Core Domain Charts

**Core Domain Charts** (from Domain-Driven Design) help identify which sub-domains are strategic versus commodity, guiding where to invest sovereignty efforts.

> **Figure:** A 2x2 chart with **Business Differentiation** on the x-axis (Low to High) and **Model Complexity** on the y-axis (Low to High). Three zones are marked:
>
> - **GENERIC** (left/top area, gray) -- low differentiation
> - **SUPPORTING** (bottom area, purple) -- low complexity, varying differentiation
> - **CORE** (right/top area, green) -- high differentiation, high complexity
>
> Several sub-domains are plotted as colored circles:
> - Red circles: current position of sub-domains (e.g. "matchmaking" with team size 8)
> - Gray circles: future position (showing planned movement over time with dashed arrows)
> - Blue circles: big-bet sub-domains (e.g. "fault prediction")
> - Yellow circles: platform sub-domains (e.g. "notifications" with team size 5)
> - Green circles: outsourced/purchased sub-domains (e.g. "identity" with team size 2)
>
> Team Topologies notation includes: team size (number), X-as-a-service (marked X), and collaboration zones.

Key questions to ask:
- Is my monitoring stack core?
- Is my operating system core?
- Is my notification system core?
- Is my secret algorithm that makes me a lot of money core?

*Reference: [ddd-crew/core-domain-charts](https://github.com/ddd-crew/core-domain-charts)*

---

## Architecture Decision Records

An **Architecture Decision Record (ADR)** is a document that captures significant architectural decisions made during a project, including the context, options considered, and the rationale for the chosen solution. It helps maintain clarity and understanding among team members, especially in larger or distributed projects.

How to use ADRs for sovereignty decisions:
- Consider sovereignty and portability scoring for your decision making
- Use the quadrant to compare the different options
- Pick the most suitable options based on features, but also based on the quadrant

> **Figure:** A screenshot of an ADR management interface (Notion Marketplace template) showing:
> - Quick Actions panel with "New Architectural Decision Record," "Guidelines," and "All Decisions"
> - Hints panel advising to read guidelines, check existing decisions, and start new ADRs with a template
> - "Accepted Decision Records" section for reviewed and approved decisions, arranged in ascending order by creation date
> - "Proposed Decision Records" section for decisions still being drafted or under review
>
> *Reference: [Architecture Decision Records (ADR) Template | Notion Marketplace](https://www.notion.so/templates/architecture-decision-records)*
