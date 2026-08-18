# Storage Layout

The host uses a dedicated SSD for Proxmox and local VM storage, an 8 TB HDD for main storage, and a separate 2 TB HDD for backups. No mdraid or ZFS pool was present in the supplied system output.

## Physical disks

| Device | Model | Serial | Reported size | Filesystem / role |
|---|---|---|---:|---|
| `/dev/sdb` | Samsung SSD 860 EVO 250GB | Not recorded | 232.9G | Proxmox system disk and LVM |
| `/dev/sda` | HGST HUS728T8TALE6L4 | `VDKY29DM` | 7.3T | ext4 at `/mnt/storage`; `hdd-storage` |
| `/dev/sdc` | WDC WD20NMVW-11AV3S2 | `WD-WX51A55N9ZRD` | 1.8T | ext4 at `/mnt/backup`; `usb-backup` |

Disk serial numbers identify hardware but are not authentication secrets. They are included here for maintenance and replacement tracking.

## System SSD allocation

```text
/dev/sdb  Samsung SSD 860 EVO 250GB (232.9G)
├── EFI system partition       1G   vfat   /boot/efi
└── /dev/sdb3                  LVM physical volume for VG pve
    ├── pve-root              ~68G  ext4   /
    ├── pve-swap                8G  swap
    ├── local-lvm thin pool  ~137.1G
    └── unallocated VG space   16G
```

The LVM volume group is `pve`, its physical volume is `/dev/sdb3`, and the thin-pool data capacity is approximately 137.11G.

## Proxmox storage status

The following values preserve the original `pvesm status` units.

| Storage ID | Type | Active | Total (KiB) | Used (KiB) | Available (KiB) | Used |
|---|---|---:|---:|---:|---:|---:|
| `hdd-storage` | dir | Yes | 7,751,271,852 | 259,092,624 | 7,101,461,584 | 3.34% |
| `local` | dir | Yes | 69,573,880 | 6,973,972 | 59,020,004 | 10.02% |
| `local-lvm` | lvmthin | Yes | 143,773,696 | 36,173,461 | 107,600,234 | 25.16% |
| `usb-backup` | dir | Yes | 1,921,694,920 | 524,055,404 | 1,299,949,048 | 27.27% |

## Storage roles

- **`local`:** directory storage on the Proxmox root filesystem.
- **`local-lvm`:** LVM thin storage on the system SSD for virtual disks.
- **`hdd-storage`:** main-capacity directory storage mounted at `/mnt/storage`.
- **`usb-backup`:** separate backup directory storage mounted at `/mnt/backup`.

The separate backup disk reduces dependence on the system SSD, but it is still part of the same physical site. An offsite copy remains a recommended TODO; see [Backup Strategy](backup-strategy.md).
