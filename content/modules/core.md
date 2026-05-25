---
date: "2026-05-21"
title: "Core System Modules"
weight: 20
teaser: "Automated provisioning patterns for storage topologies, bonded networks, and local filesystem controls."
layout: "single"
noAside: true
---

The `dettonville.core` module collection provides the primary lifecycle primitives required to bootstrap and stabilize raw compute instances before platform runtimes or container clusters are deployed. These assets operate natively on bare-metal systems, hypervisor instances, or private enterprise network matrices.

---

## Module Inventory & Parameter Specifications

### 1. Network Interface Bonding (`core_network_bond`)
Configures kernel-level network interface aggregation to guarantee path redundancy and maximum throughput for data-plane traffic without relying on external upstream dhcp daemons.

* **Primary Variables:**
    * `core_network_bond_interface`: The master virtual interface name (e.g., `bond0`).
    * `core_network_bond_slaves`: A structured list of physical network interface cards (NICs) to bind.
    * `core_network_bond_mode`: Aggregation protocol definition (standardized on `active-backup` or `803.ad` LACP).
* **Flat-File Artifact Immutability:** Network topologies are written directly to standard interface configuration matrices. The module drops persistent local configuration records into `/etc/sysconfig/network-scripts/` or `NetworkManager` system tracking layers.

### 2. Multi-Tier Storage Arrays (`core_storage_array`)
Handles target system volume mapping, automated partition mapping, and disk alignment for persistent system storage fixtures (e.g., local storage groups or high-capacity arrays).

* **Primary Variables:**
    * `core_storage_disks`: A list of hardware disk targets (e.g., `/dev/sdb`, `/dev/nvme0n1`).
    * `core_storage_filesystem`: The target layout format (standardized on upstream open-source `xfs` or `ext4`).
    * `core_storage_mount_options`: Explicit mount flags enforced at boot (e.g., `noatime,nodiratime,pquota`).
* **DRY Parameterization:** Rather than writing custom mounting scripts for every distinct physical node type, a centralized variable matrix in inventory tracking dynamically informs this primitive, mapping specific disks based on host fact discoveries.

### 3. File Execution & Permissions Boundary (`core_system_boundary`)
Enforces global system environment boundaries and security masking at the storage tier to protect configuration files from arbitrary local runtime mutation.

* **Primary Variables:**
    * `core_system_global_umask`: The global file creation mask (strictly enforced at `027` across all systemic profiles).
    * `core_system_secure_paths`: Array of directory targets requiring absolute ownership and explicit mode protection (e.g., `/etc/cron.d`, `/var/log/audit`).
* **Idempotency Mechanic:** The module continuously scans file attribute states. If a local system tool modifies permissions outside of the declared configuration manifest, the execution loop rolls it back to the baseline profile without cycling target service daemons.

---

## Sample Integration Manifest

To consume these primitives within a standard execution track, properties are declared in a plain text configuration play:

```yaml
- name: Stabilize Bare-Metal Compute Nodes
  hosts: compute_infrastructure
  gather_facts: true
  vars:
    core_network_bond_interface: "bond0"
    core_network_bond_mode: "802.3ad"
    core_network_bond_slaves:
      - "ens1f0"
      - "ens1f1"
    core_storage_disks:
      - "/dev/sdb"
    core_system_global_umask: "027"

  roles:
    - role: dettonville.core.network_bond
    - role: dettonville.core.storage_array
    - role: dettonville.core.system_boundary
```

---

## Validation Execution Gates

Every execution of a `core` primitive undergoes a structured post-flight attestation sweep:
1. **Fact Assert Check:** Verifies that physical storage array paths and network interfaces are present and unmapped by rogue processes.
2. **Atomic Ingest Validation:** Validates written files using integrated validation hooks before updating live system layouts.
3. **Flat State Drop:** Writes execution state logs into a structured `/var/log/dettonville/core_state.json` file for integration with local compliance monitoring systems.
