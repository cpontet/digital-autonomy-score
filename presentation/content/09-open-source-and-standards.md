# Open Source and Open Standards

There are many open-source tools and standards that are already at your disposal and serve as powerful enablers of digital sovereignty.

## Open Source for Sovereignty

**Open-source software (OSS)** is computer software that is released under a license in which the copyright holder grants users the rights to use, study, change, and distribute the software and its source code to anyone and for any purpose.

The **Open Source Initiative's (OSI)** definition is recognized by several governments internationally as the standard or de facto definition.

> **Figure:** The Open Source Initiative (OSI) logo -- a green keyhole-shaped symbol -- alongside the text "open source initiative" with a registered trademark symbol.

Source: [Open-source software - Wikipedia](https://en.wikipedia.org/wiki/Open-source_software)

---

## The Story of OpenTofu

The **OpenTofu** story illustrates how open-source communities can respond when a vendor changes licensing terms, and why open-source governance matters for sovereignty.

> **Figure:** Two logos displayed side by side -- the HashiCorp Terraform logo (purple background, white geometric symbol) on the left, and the OpenTofu logo (black background, white text with a yellow cube icon) on the right.

### The License Change

In August 2023, **HashiCorp** announced that **Terraform** would move from the open-source **MPL (Mozilla Public License)**, a weak copyleft license, to the more restrictive **BSL (Business Source License)**. This change worried many users, cloud vendors, and tech companies because BSL restricts use in some commercial scenarios and ends further contributions to truly open infrastructure tooling.

### The Community Response

In response, prominent members of the Terraform community and major tech companies (like Google, GitLab, AWS, Red Hat, and others) formed **OpenTF**, which aimed to fork Terraform from its last open-source release and continue development in a fully open manner. Soon, OpenTF announced its name change to **OpenTofu**, after negotiation with HashiCorp over naming and trademarks.

Source: [OpenTofu](https://opentofu.org)

---

## Open Standards

Open standards form the foundation of interoperable, vendor-neutral technology. The presentation catalogs a comprehensive list of open standards across multiple domains.

### Internet and Web

- **HTML (HyperText Markup Language):** The standard markup for webpages.
- **CSS (Cascading Style Sheets):** Style sheets for web design.
- **HTTP (HyperText Transfer Protocol):** Enables communications between clients and servers.
- **SMTP (Simple Mail Transfer Protocol):** Standard for email transmission.
- **IMAP/POP3:** Standards for retrieving email.
- **WebRTC:** Standard for real-time communications in browsers.
- **XML (eXtensible Markup Language):** A flexible text format for structured data.
- **JSON (JavaScript Object Notation):** Open data interchange format.

### Networking

- **TCP/IP (Transmission Control Protocol/Internet Protocol):** Core of internet networking.
- **DNS (Domain Name System):** Internet's phonebook.
- **SSH (Secure Shell):** Secure network protocol.

### Data and File Formats

- **PDF (Portable Document Format):** Open document standard (since 2008, ISO 32000).
- **ODF (OpenDocument Format):** Open standard for office documents (used in LibreOffice).
- **SVG (Scalable Vector Graphics):** Vector image format for web.
- **MP3, OGG, FLAC:** Open standards for audio files.

### APIs and Interoperability

- **OAuth 2.0:** Standard for authentication (authorization delegation).
- **OpenID Connect:** Identity layer on top of OAuth 2.0.
- **OpenAPI (Swagger):** Describes RESTful APIs in a standard way.
- **SAML (Security Assertion Markup Language):** For exchanging authentication and authorization data.
- **ActivityPub:** Decentralized social networking communication protocol.

### Telecommunications and Messaging

- **SMS (Short Message Service):** Standardized texting.
- **XMPP (Extensible Messaging and Presence Protocol):** Instant messaging protocol used by Jabber.

---

## Matrix Protocol

**Matrix** defines a set of open APIs for decentralized communication, suitable for securely publishing, persisting, and subscribing to data over a global open federation of servers with no single point of control.

> **Figure:** ASCII architecture diagram of the Matrix protocol showing two Matrix clients (A and B) each connected to their respective homeservers via a Client-Server API (events flow up and down). The two homeservers communicate with each other over HTTPS via the Server-Server API for History Synchronization (Federation).

Uses include:

- **Instant Messaging (IM)**
- **Voice over IP (VoIP)** signalling
- **Internet of Things (IoT)** communication
- Bridging together existing communication silos -- providing the basis of a new open real-time communication ecosystem

Source: [https://spec.matrix.org](https://spec.matrix.org)

---

## The CDMI Counter Example

Standards do not always win on merit alone. The case of **CDMI vs. Amazon S3** illustrates how market dominance can override formal standardization.

### CDMI (Cloud Data Management Interface)

**CDMI (Cloud Data Management Interface)** is a standard for managing objects in cloud storage, formalized as **ISO/IEC 17826** (Information technology).

Cloud Data Management Interface (CDMI) Version 2.0.0 is an international standard that specifies a protocol for self-provisioning, administering, and managing access to data stored in cloud storage, object storage, storage area network, and network attached storage systems. The CDMI standard is developed and maintained by the **Storage Networking Industry Association (SNIA)**, who makes a publicly accessible version of the specification available.

**Supported by:** Hitachi, NetApp, DataCore, Fujitsu, Huawei, OpenStack

### Amazon S3 API

The **Amazon S3 API** is the most widely adopted object storage API, used by AWS and many third-party and on-premises systems.

**Supported by:** AWS S3, MinIO, Ceph, Dell ECS, NetApp StorageGRID, Wasabi, Backblaze B2

**Strengths:** Ubiquity, extensive documentation, language SDKs, robust third-party tool support.

Despite CDMI being a formal international standard, the S3 API has become the de facto standard through market adoption -- a cautionary tale about the relationship between open standards and market power.

