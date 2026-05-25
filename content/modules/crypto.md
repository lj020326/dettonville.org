---
date: "2026-05-21"
title: "Crypto & Hardening Modules"
weight: 30
teaser: "Automated local PKI orchestration, mutual TLS enforcement, and CIS compliance baseline injection."
layout: "single"
noAside: true
---

The `dettonville.crypto` collection provides high-integrity primitives engineered to establish absolute defensive boundaries on target nodes. Operating under a zero-trust model inside isolated networks, these modules eliminate manual key generation and configuration drift for security fixtures.

---

## Module Inventory & Parameter Specifications

### 1. Local Root & Intermediate PKI (`crypto_pki_mint`)
Orchestrates the lifecycle of a self-contained, high-availability cryptographic trust anchor. It automates local root CA distribution, intermediate certificate signing, and automated endpoint minting.

* **Primary Variables:**
    * `crypto_pki_root_common_name`: The authoritative internal domain string for the root certificate authority.
    * `crypto_pki_cert_lifespan_days`: The strict expiration limit for minted node leaf certificates (defaulting to a short window to enforce continuous rotation).
    * `crypto_pki_m_tls_required`: Enforces strict mutual verification across system endpoints when set to `true`.
* **DRY Execution Strategy:** A singular, abstract certificate engine processes distinct data arrays representing target nodes. Instead of rewriting unique generation hooks per application, this generic role dynamically mints and injects keys based on simple inventory host properties.

### 2. CIS Operating System Hardening (`crypto_cis_baseline`)
Translates complex Center for Internet Security (CIS) server benchmarks directly into executable system state configurations.

* **Primary Variables:**
    * `crypto_cis_profile_level`: The target string identifying the strictness tier (standardized on `level_2_server`).
    * `crypto_cis_disable_subsystems`: A list of legacy or unprivileged kernel modules to blacklist (e.g., `dccp`, `sctp`, `rds`).
    * `crypto_cis_ssh_hardening`: Explicit configuration map forcing key-only authentication and removing legacy cryptographic ciphers.
* **Idempotent Attestation Loop:** The module evaluates active kernel flags and config permissions during runtime execution. If any parameters deviate from the declarative source model, the engine replaces them instantly with zero noise, tracking compliance via a standard state log.

### 3. Supply Chain Integrity Validation (`crypto_supply_chain`)
Enforces strict cryptographic confirmation on all software packages, binaries, and container archives moving into local storage layers.

* **Primary Variables:**
    * `crypto_supply_chain_allowed_hashes`: A flat manifest mapping archive targets to absolute SHA-256 integrity strings.
    * `crypto_supply_chain_fail_on_mismatch`: Boolean flag forcing execution pipelines to immediately drop if an ingested artifact lacks a verifiable hash match.

---

## Sample Integration Manifest

To tie these cryptographic guardrails into your unified execution track, pass the variable matrices through plain text automation tasks:

```yaml
- name: Apply Domain Cryptographic Guardrails
  hosts: control_plane, compute_infrastructure
  gather_facts: true
  vars:
    crypto_pki_root_common_name: "Dettonville Local Authority"
    crypto_pki_cert_lifespan_days: 90
    crypto_pki_m_tls_required: true
    crypto_cis_profile_level: "level_2_server"
    crypto_cis_disable_subsystems:
      - "usb-storage"
      - "cramfs"
      - "freevxfs"

  roles:
    - role: dettonville.crypto.pki_mint
    - role: dettonville.crypto.cis_baseline
```

---

## Technical Flow and Audit Output

Every execution pass within the `crypto` library records state changes natively into structured flat text schemas to preserve long-term audit trail visibility without external data backends:

1. **Pre-Flight Validation:** Verifies the presence of the localized parent signing key and evaluates current kernel parameter mappings.
2. **Atomic State Realization:** Replaces target configurations, updates systemic service configurations, and reloads active daemons only when state mutations are observed.
3. **Flat Audit Storage:** Outputs structured json tracking straight into `/var/log/dettonville/compliance_audit.json` to facilitate immediate auditing using standard local text parsers.
