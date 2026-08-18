# Infrastructure Scheme

The homelab is built around one Proxmox VE host. KVM virtual machines provide Windows, Linux, VPN, and application workloads; LXC containers provide monitoring, proxy, database, and internal services.

## Logical architecture

```mermaid
flowchart TB
    Admin["Local administrator"]
    Remote["Remote administrator via VPN"]
    Gateway["Home gateway<br/>192.168.2.1"]
    LAN["LAN<br/>192.168.2.0/24"]
    NIC["Realtek 1 GbE<br/>enp7s0"]
    Bridge["Proxmox bridge<br/>vmbr0"]
    Host["Proxmox VE host: pve<br/>192.168.2.200/24"]

    Admin --> LAN
    Remote --> Gateway
    Gateway --> LAN
    LAN --> NIC --> Bridge --> Host

    subgraph VMGroup["KVM virtual machines"]
        AD["AD lab<br/>301 dc01 · 302 dc02 · 307 dc04"]
        Clients["Client and Linux lab<br/>204 Ubuntu · 304 win10 · 305 win11 · 306 UbuntAD"]
        NetworkServices["Network services<br/>400 vpn · 500 3X-UI-MAIN"]
        TestVM["800 VM 800<br/>stopped test VM"]
    end

    subgraph LXCGroup["LXC containers"]
        Monitor["201 zabbix"]
        Proxy["202 web-proxy"]
        Data["203 database · 205 nocoDB"]
        Dashboard["206 Dashboard"]
        Restore["801 exam<br/>stopped restore test"]
    end

    Host --> VMGroup
    Host --> LXCGroup

    subgraph Storage["Host storage"]
        System["Samsung 250 GB SSD<br/>system, local, local-lvm"]
        Main["HGST 8 TB HDD<br/>hdd-storage"]
        Backup["WDC 2 TB HDD<br/>usb-backup"]
    end

    Host --> Storage
```

## Layers

1. **Physical layer:** the X79 server, Realtek NIC, system SSD, main HDD, and separate backup HDD.
2. **Virtualization layer:** Debian 13 and Proxmox VE 9.2.0 using KVM for VMs and LXC for containers.
3. **Network layer:** `enp7s0` is attached to `vmbr0`, which connects the host and guests to `192.168.2.0/24`.
4. **Service layer:** Active Directory, Linux labs, local web services, monitoring, databases, dashboard, VPN, and Xray management.
5. **Recovery layer:** backups are stored separately from the system disk and are validated through restore testing.

## Access model

Home services are intended to be reached from the local network or through VPN access. The documentation does not publish an external address, expose services directly, or include credential-bearing VPN configuration.

See [Network Map](network-map.md) for local DNS names and [VM and LXC Inventory](vm-lxc-inventory.md) for the workload list.
