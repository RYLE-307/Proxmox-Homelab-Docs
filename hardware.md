# Hardware

This page records the physical platform used by the current Proxmox host.

## Server platform

| Component | Details |
|---|---|
| Vendor | INTEL |
| Model / motherboard | X79_VG6 |
| Board version | V1.3 |
| BIOS vendor | American Megatrends Inc. |
| BIOS version | 4.6.5 |
| BIOS release date | 2026-01-15 |
| Hostname | `pve` |

## Processor

| Property | Value |
|---|---|
| Model | Intel Xeon E5-2670 v2 @ 2.50 GHz |
| Sockets | 1 |
| Physical cores | 10 |
| Threads | 20 |
| Maximum frequency | 3.30 GHz |
| L3 cache | 25 MB |
| Virtualization | Intel VT-x |

The 10-core, 20-thread CPU provides capacity for the mixed Windows, Linux, infrastructure, and test workloads described in the [guest inventory](vm-lxc-inventory.md).

## Memory

| Property | Value |
|---|---|
| Installed capacity | 64 GB |
| Type | DDR3 ECC |
| Effective speed | 1333 MT/s |
| Configuration | 4 × 16 GB modules |
| Module vendors | Mixed SK Hynix and Samsung |
| Error correction | ECC Multi-bit |

## Expansion and networking

| Component | Details |
|---|---|
| GPU | NVIDIA GeForce GT 640 |
| Ethernet controller | Realtek RTL8111/8168/8211 PCIe Gigabit Ethernet |
| Physical interface | `enp7s0` |
| Proxmox bridge | `vmbr0` |
| Link class | 1 GbE |

## Platform software

| Component | Version |
|---|---|
| Operating system | Debian GNU/Linux 13 (trixie) |
| Proxmox VE | 9.2.0 |
| `pve-manager` | 9.2.10 |
| Kernel | Linux 7.0.14-4-pve |

Disk hardware and volume allocation are documented separately in [Storage Layout](storage-layout.md).
