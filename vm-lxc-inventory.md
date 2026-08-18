# VM and LXC Inventory

This inventory reflects the documented `qm list` and `pct list` output. Resource values are recorded as reported by Proxmox; a configured boot-disk size is not the same as current disk usage.

## KVM virtual machines

| VM ID | Name | State | RAM | Boot disk | Purpose |
|---:|---|---|---:|---:|---|
| 204 | Ubuntu | Running | 10,000 MB | 50.00 GB | Linux lab / DevOps practice |
| 301 | dc01 | Running | 8,000 MB | 200.00 GB | Windows Server / AD domain controller |
| 302 | dc02 | Running | 8,192 MB | 200.00 GB | Additional domain controller |
| 304 | win10 | Running | 4,000 MB | 200.00 GB | Windows client lab |
| 305 | win11 | Running | 6,000 MB | 200.00 GB | Windows client lab |
| 306 | UbuntAD | Running | 4,000 MB | 200.00 GB | Ubuntu joined to AD / Linux AD integration |
| 307 | dc04 | Running | 8,124 MB | 200.00 GB | Additional Windows Server lab |
| 400 | vpn | Running | 2,048 MB | 32.00 GB | VPN services |
| 500 | 3X-UI-MAIN | Running | 2,048 MB | 20.00 GB | 3x-ui / Xray |
| 800 | VM 800 | Stopped | 128 MB | 0.00 GB | Test VM |

**VM summary:** 10 documented; 9 running and 1 stopped.

## LXC containers

CPU, memory, and root-disk allocations were not present in the supplied `pct list` data, so they are intentionally not inferred.

| CT ID | Name | State | Purpose |
|---:|---|---|---|
| 201 | zabbix | Running | Monitoring |
| 202 | web-proxy | Running | Nginx web proxy / local sites |
| 203 | database | Running | Database server |
| 205 | nocoDB | Running | NocoDB service |
| 206 | Dashboard | Running | Internal dashboard |
| 801 | exam | Stopped | Restore-test container |

**LXC summary:** 6 documented; 5 running and 1 stopped.

## Workload groups

- **Identity:** `dc01`, `dc02`, and `dc04` form the Windows Server / Active Directory lab.
- **Client and integration:** `win10`, `win11`, Ubuntu, and `UbuntAD` support client, Linux, and directory-integration practice.
- **Platform services:** `web-proxy`, `database`, `nocoDB`, and `Dashboard` support local applications.
- **Operations:** `zabbix` provides the monitoring platform; `vpn` and `3X-UI-MAIN` provide network-access services.
- **Recovery and experiments:** VM 800 and CT 801 are stopped test workloads. CT 801 is the documented restore target for CT 203.

Guest IP addresses are omitted because they were not confirmed in the source inventory. Known service names are listed in [Network Map](network-map.md).
