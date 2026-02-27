# Digital Commons and Portability

## Digital Commons

**Digital commons** are shared online resources -- like content, tools, infrastructure, or knowledge -- that are managed collectively by a community according to agreed-upon rules.

### Key Features

- Open access or shared use
- Collaborative management or governance
- Non-exclusive (many users can benefit simultaneously)
- Community-driven oversight

### Examples

- **Wikipedia** (free encyclopedia collectively edited and owned)
- **Open-source software** (e.g., Linux, collaboratively developed code)
- **Creative Commons-licensed content** (images, music, texts)

---

## Data Commons

A **data commons** is a type of digital commons focused specifically on datasets and related tools/technologies. It is an organized ecosystem where datasets, analysis tools, and computing resources are pooled and shared, mainly for research, discovery, or innovation.

### Key Features

- Shared pool of datasets (often scientific or research-oriented)
- Tools/services for data management, analysis, or sharing
- Collective governance and access policies
- Enabling efficient data reuse, interoperability, and collaboration

### Examples

- **NIH Data Commons** (biological/health data for research)
- **Genomic Data Commons** (public genomics datasets)
- **Open data portals** (government, science, etc.)

---

## FAIR Principles

The **FAIR principles** provide a framework for ensuring that data and metadata are managed in a way that maximizes their value and usability.

### Findable

The first step in (re)using data is to find them. Metadata and data should be easy to find for both humans and computers. Machine-readable metadata are essential for automatic discovery of datasets and services.

### Accessible

Once the user finds the required data, she/he/they need to know how they can be accessed, possibly including authentication and authorization.

### Interoperable

The data usually need to be integrated with other data. In addition, the data need to interoperate with applications or workflows for analysis, storage, and processing.

### Reusable

The ultimate goal of FAIR is to optimize the reuse of data. To achieve this, metadata and data should be well-described so that they can be replicated and/or combined in different settings.

> **Source:** FAIR Principles - GO FAIR

---

## GAIA-X

**GAIA-X** is a Franco-German-led pan-European initiative to build a federated data infrastructure where data sovereignty, interoperability, and common standards are central.

Its goal is to enable **secure, transparent, and sovereign information sharing and cloud services** across sectors (e.g., health, manufacturing, mobility).

---

## Containers for Portability

### OCI (Open Container Initiative)

**OCI (Open Container Initiative)** defines standards for container formats and runtimes. The Open Container Initiative is an open governance structure for the express purpose of creating open industry standards around container formats and runtimes.

> **Figure:** The OCI logo and member logos are displayed, showing the breadth of industry support. Members include: Alibaba Cloud, Amazon Web Services, Chainguard, Cisco, Docker, EasyStack, Goldman Sachs, Google, Huawei, IBM, Microsoft, OpenStack, Red Hat, Replicated, Sysdig, and Weaveworks.

> **Source:** Open Container Initiative - Open Container Initiative

---

## containerd

**containerd** is an industry-standard container runtime with an emphasis on simplicity, robustness, and portability.

As of February 28, 2019, containerd is officially a graduated project within the **Cloud Native Computing Foundation**, following Kubernetes, Prometheus, Envoy, and CoreDNS.

containerd is available as a daemon for Linux and Windows. It manages the complete container lifecycle of its host system, from image transfer and storage to container execution and supervision to low-level storage to network attachments and beyond.

> **Figure:** A detailed architecture diagram of the containerd ecosystem, organized into layers:
>
> - **Platform layer (ecosystem):** Google Cloud Platform, Docker, IBM Cloud, Microsoft Azure, Alibaba Cloud, AWS, Rancher
> - **Client layer:** kubelet (CRI Runtime), Container Engine Pouch (containerd client), BuildKit (containerd client), ctr (containerd client)
> - **API layer:** gRPC CRI (containerd client), gRPC containerd Service Handlers, Prometheus Metrics
> - **Core Services layer:** Containers Service, Content Service, Diff Service, Images Service, Leases Service, Namespaces Service, Snapshots Service, Tasks Service
> - **Metadata layer (namespaced):** Containers, Content, Images, Leases, Namespaces, Snapshots, GC
> - **Backend layer:** Content Store (plugin: local), Snapshotter (overlay, btrfs, devmapper, native, windows, plugin), Runtime (v2 shim client via ttrpc)
> - **containerd-shim layer:** runc, runhcs, kata, Firecracker, gVisor, shim
> - **System layer:** ARM, Intel, Windows, Linux

> **Source:** https://containerd.io

---

## Cloud Native Computing Foundation (CNCF)

> **Figure:** The full CNCF (Cloud Native Computing Foundation) landscape map, an extensive visualization of the cloud-native ecosystem organized into major categories:
>
> - **Application Definition & Image Build:** dapr, Helm, Buildpacks.io, KubeVela, KubeVirt, Operator Framework, and many more
> - **Databases:** TiKV, Vitess, and others
> - **Continuous Integration & Delivery:** Argo, Flux, Keptn, OpenSource, and more
> - **Streaming & Messaging:** CloudEvents, STRIMZI, and others
> - **Scheduling & Orchestration:** Kubernetes, Crossplane, KARMADA, Katas, KubeEdge, Volcano, WasmCloud, and many more
> - **Service Proxy:** Envoy, Contour, and others
> - **API Gateway:** various projects
> - **Service Mesh:** Istio, Linkerd, and others
> - **Remote Procedure Call:** gRPC
> - **Coordination & Service Discovery:** etcd, CoreDNS, and more
> - **Cloud Native Storage:** CubeFS, Longhorn, and many others
> - **Cloud Native Network:** Cilium, CNI, and more
> - **Container Runtime:** containerd, CRI-O, Lima, and others
> - **Security & Compliance:** Falco, in-toto, Keycloak, Kubescape, Kyverno, and many more
> - **Automation & Configuration:** KubeEdge, Cloud Custodian, OpenYurt, Chef, and others
> - **Container Registry:** various projects
> - **Key Management:** Spiffe, SPIRE, and others
> - **Observability:** Fluentd, Cortex, Thanos, and many more
> - **Continuous Optimization:** OpenCost and others
> - **Chaos Engineering:** Chaos Mesh, Litmus, and more
> - **Feature Flagging:** OpenFeature and others
>
> The landscape contains hundreds of projects across all categories, illustrating the vast and diverse cloud-native ecosystem.

> **Source:** Cloud Native Computing Foundation
