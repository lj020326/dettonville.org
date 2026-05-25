---
date: "2026-05-21"
title: "Ansible Automation Reference"
weight: 60
teaser: "The technical execution blueprints and configuration parameters for the core system, runtime fabric, and service roles driving site.yml."
layout: "single"
noAside: true
---

The execution loops managed by `site.yml` rely entirely on a library of specialized, reusable automation roles. To eliminate manual intervention and enforce strict **DRY (Don't Repeat Yourself)** baseline compliance, these roles function as generic state engines that ingest flat variable matrices and translate them into deterministic target node layouts.

---

## Technical Stand-Up Dependency Sequence

Before high-level application or control-plane services are deployed, every host node must progress through a rigid, sequential stand-up pipeline to stabilize credentials, operating system baselines, and execution fabrics:

```mermaid
graph TD
    P1[1. Initial Access<br/><code>bootstrap_ansible_user</code>] --> P2[2. OS Optimization<br/><code>bootstrap_linux</code>]
    P2 --> P3{Machine Profile?}
    
    P3 -- GPU Equipped --> P4[3. Core Compute Layer<br/><code>bootstrap_gpu_drivers</code>]
    P4 --> P5[4. Container Engine<br/><code>bootstrap_docker</code>]
    
    P3 -- Standard Compute --> P5
    
    P5 --> P6[5. Service Fabric<br/><code>bootstrap_docker_stack</code>]
    P6 --> P7{Service Purpose?}
    
    P7 -- AI/Inference Host --> P8[6. Local AI Runtimes<br/><code>bootstrap_llm_host</code>]
    P7 -- Other Grid Targets --> P9[6. Platform / Infrastructure<br/><code>Identity, Tower, Registry, etc.</code>]

    style P1 fill:#f1f5f9,stroke:#cbd5e1,stroke-width:2px;
    style P2 fill:#f1f5f9,stroke:#cbd5e1,stroke-width:2px;
    style P3 fill:#fff,stroke:#cbd5e1,stroke-width:2px;
    style P4 fill:#f8fafc,stroke:#94a3b8,stroke-width:1px,stroke-dasharray: 5 5;
    style P5 fill:#f1f5f9,stroke:#cbd5e1,stroke-width:2px;
    style P6 fill:#f1f5f9,stroke:#cbd5e1,stroke-width:2px;
    style P7 fill:#fff,stroke:#cbd5e1,stroke-width:2px;
    style P8 fill:#f8fafc,stroke:#94a3b8,stroke-width:1px,stroke-dasharray: 5 5;
    style P9 fill:#f1f5f9,stroke:#cbd5e1,stroke-width:2px;
```

---

## Step-by-Step Execution Role Blueprint

### 1. Initial Access Authentication (`bootstrap_ansible_user`)
* **Core Purpose:** Injects initial execution profiles, administrative service groups, and SSH public keys.
* **Operational Position:** This is the absolute prerequisite step for new nodes. It establishes secure, key-based authentication paths so downstream automated runs can connect without manual password entries.

### 2. Base Operating System Stabilization (`bootstrap_linux`)
* **Core Purpose:** Shapes raw compute instances into optimized, hardened platforms.
* **Operational Position:** Applies kernel optimizations, configures persistent network interface channel-bonding rules, locks down file permissions, and enforces critical CIS benchmark kernel security profiles.

### 3. Acceleration Layer Integration (`bootstrap_gpu_drivers`)
* **Core Purpose:** Automates the discovery, injection, and stabilization of hardware accelerator software layers.
* **Operational Position:** Executed conditionally *only* on machines equipped with dedicated physical graphics processing units. It installs required kernel modules and toolkit architectures to prepare the bare iron for high-density computing blocks.

### 4. Container Engine Activation (`bootstrap_docker`)
* **Core Purpose:** Establishes the primary containment layer required across the enterprise.
* **Operational Position:** Deploys a stable container runtime engine on the node, locking down system sockets and mapping storage backends (`overlay2`) without introducing floating package dependencies to the host OS.

### 5. Unified Service Stack Architecture (`bootstrap_docker_stack`)
* **Core Purpose:** Evaluates flat variable structures to hydrate platform workloads uniformly.
* **Operational Position:** Handles configuration rendering, runtime port exposures, and mounts **Docker Secrets** safely to container spaces in a reusable, generic implementation across standalone engines or Swarm grids.

### 6. Local AI Inference Infrastructure (`bootstrap_llm_host`)
* **Core Purpose:** Sets up localized, air-gapped machine learning engines and model servers.
* **Operational Position:** Executed conditionally *only* on designated AI infrastructure nodes. It binds containerized model caches and local orchestration endpoints to feed downstream development spaces securely.

---

## Ansible Roles Navigation Tracks

Explore the explicit technical layouts, variable schemas, and verification testing tasks for each underlying playbook tier:

* **[Core System Hardening Roles](/ansible/system-hardening/)** — Deep dives into foundational access mechanics and base OS optimization code (`bootstrap_ansible_user` and `bootstrap_linux`).
* **[Runtime Fabric & Containment Roles](/ansible/runtime-fabric/)** — Technical boundaries governing `bootstrap_docker`, hardware-accelerated `bootstrap_gpu_drivers`, and the generic `bootstrap_docker_stack` engine.
* **[Control-Plane Service Roles](/ansible/control-plane-services/)** — Technical documentation for `bootstrap_llm_host` configurations and inventory-driven domain architecture mapping.
---
