---
date: "2026-05-21"
title: "Automation Modules Overview"
weight: 10
teaser: "The structural manifest of security-hardened, composable automation primitives and platform collections."
layout: "single"
noAside: true
---

Modules within the Dettonville ecosystem serve as the standardized building blocks of the entire infrastructure lifecycle. In alignment with our strict **DRY (Don't Repeat Yourself)** baseline, these modules are written as highly parameterized, decoupled primitives designed to execute deterministically in air-gapped or restricted execution zones.

Rather than writing custom scripting loops for every application deploy, operations teams consume these version-controlled primitives by passing distinct data matrices into structured execution tracks.

---

## Core Module Classifications

The automation library is stratified into distinct operational tiers to separate structural system governance from application-level runtimes:

### 1. System Primitives (`dettonville.core`)
Foundational system utilities responsible for stabilizing bare-metal instances, virtual private clouds, or enterprise hardware foundations.
* **Storage Systems:** Automated provisioning of multi-tiered storage arrays, local volume maps, and hardware-bonded NIC configurations.
* **Identity Bounds:** Local Pluggable Authentication Modules (PAM) architecture configurations, local system account management, and hard tracking of `umask` permission baselines.

### 2. Guardrail Security (`dettonville.crypto`)
High-integrity modules dedicated to maintaining absolute defensive posture without internet access.
* **PKI Operations:** Automated local minting, distribution, and lifecycle rotation of internal transport layer security (TLS) assets and root authorities.
* **Compliance Hardening:** Injection and verification of Center for Internet Security (CIS) structural server policies and kernel hardening attributes.

### 3. Engine Engines (`dettonville.engine`)
Orchestration primitives that provision local developer platforms, artifact staging targets, and local inference infrastructures.
* **Local Supply Chain:** Automated stands of community-edition container registries, binary caches, and package index overrides.
* **Inference Foundations:** Configuration pipelines for dedicated GPU clusters, local AI inference servers, and accompanying orchestration controllers.

---

## Module Design Constraints

To remain compatible with the ecosystem's execution requirements, every module added to the collection must pass three structural gates:

1. **Zero External Trailing:** The module must contain no hidden commands pulling assets from public Git mirrors or public package managers at runtime. Everything must ingest from predefined local repository parameters.
2. **Strict Idempotency Proof:** Modules must test successfully against the Molecule framework. Re-running a module against an already modified system must yield an exact `changed=0` status flag.
3. **Flat-File Output Compatibility:** Module status or state modifications must capture cleanly into structured flat text schemas (YAML or JSON) to ensure audit durability.

---

## Next Steps

Explore the individual module integration blueprints to understand parameters and input expectations:

* **[Core System Modules](/modules/core/)** — Storage bounds, network bonding, and core compute profiles.
* **[Crypto & Hardening Modules](/modules/crypto/)** — Local PKI provisioning and CIS structural loops.
* **[Platform Engine Modules](/modules/engine/)** — Local container stacks, local AI clusters, and supply chain proxies.
