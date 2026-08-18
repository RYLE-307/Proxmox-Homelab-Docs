# Proxmox Homelab Documentation

Documentation for my Proxmox homelab: VM/LXC layout, network scheme, storage, backup strategy, restore testing and monitoring plan.

This repository describes a practical environment used for system administration, virtualization, Linux, networking, Active Directory integration, monitoring, backup, and recovery exercises.

## Project overview

| Item | Current state |
|---|---|
| Owner | Max Kozlov / RYLE-307 |
| Hypervisor | Proxmox VE 9.2.0 (`pve-manager` 9.2.10) |
| Host OS | Debian GNU/Linux 13 (trixie) |
| Host | `pve` — `192.168.2.200/24` |
| Compute | Intel Xeon E5-2670 v2 — 10 cores / 20 threads |
| Memory | 64 GB DDR3 ECC |
| Workloads | 10 KVM virtual machines and 6 LXC containers documented |
| Storage | 250 GB system SSD, 8 TB main HDD, 2 TB backup HDD |
| Network | `vmbr0` bridge on a 1 GbE Realtek interface |

At the time of the documented inventory, 9 VMs and 5 containers were running. One test VM and the restore-test container were stopped.

## Main services and lab areas

- Windows Server and Active Directory lab
- Windows client lab
- Ubuntu and Linux–AD integration practice
- Nginx reverse proxy and local websites
- Zabbix monitoring
- Database and NocoDB services
- Internal dashboard and file services
- VPN services and 3x-ui / Xray
- Backup and isolated restore testing

## High-level layout

```text
Remote access (VPN) / local administrator
                    |
          Home gateway 192.168.2.1
                    |
              LAN 192.168.2.0/24
                    |
         Proxmox bridge vmbr0
                    |
       Proxmox host 192.168.2.200
              /             \
         KVM VMs          LXC containers
              \             /
        Local, main, and backup storage
```

The detailed diagrams are in [Infrastructure Scheme](infrastructure-scheme.md), [Network Map](network-map.md), and [the plain-text homelab scheme](diagrams/homelab-scheme.txt).

## Documentation

| Document | Description |
|---|---|
| [Hardware](hardware.md) | Server platform, CPU, memory, GPU, NIC, and firmware |
| [Infrastructure Scheme](infrastructure-scheme.md) | Logical view of the host, workloads, storage, and access |
| [VM and LXC Inventory](vm-lxc-inventory.md) | Current guests and their documented roles |
| [Network Map](network-map.md) | LAN, bridge, gateway, DNS names, and access boundaries |
| [Storage Layout](storage-layout.md) | Physical disks, LVM, mount points, and Proxmox storage |
| [Backup Strategy](backup-strategy.md) | Backup goals, targets, retention proposal, and recovery rules |
| [Restore Test](restore-test.md) | Verified LXC restore result and remaining checks |
| [Monitoring Plan](monitoring-plan.md) | Metrics, services, tools, and alerting priorities |
| [Security Notes](security-notes.md) | Public-repository rules and homelab security baseline |

## Verified and planned work

Verified:

- The Proxmox host, hardware, storage, VM, and LXC inventory are documented.
- An LXC backup of CT 203 was restored as CT 801.
- The Proxmox restore task completed with `TASK OK` and the restored container appeared in inventory.

Planned:

- Complete a service-level validation of the restored database container.
- Document how IP conflicts are prevented during isolated restore tests.
- Add sanitized screenshots without host secrets or external addresses.
- Add an encrypted offsite backup; no offsite copy is claimed today.

## Public repository safety

This repository intentionally excludes passwords, tokens, private keys, credential-bearing VPN configurations, QR codes, database dumps, raw backup archives, and real external IP addresses. Local RFC1918 addresses are included only where they make the lab documentation useful.

## Suggested GitHub topics

`proxmox` `homelab` `virtualization` `linux` `lxc` `kvm` `backup` `zabbix` `nginx` `samba` `active-directory` `sysadmin` `devops-lab`
