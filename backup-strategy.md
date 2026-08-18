# Backup Strategy

## Goals

- Protect VM and LXC configuration and data.
- Recover from administrative mistakes, failed changes, and data corruption.
- Keep backup copies on storage separate from the Proxmox system disk.
- Prove recoverability with repeatable restore tests.

## Backup targets

| Target | Location | Role |
|---|---|---|
| `hdd-storage` | `/mnt/storage` | Main-capacity storage and an available backup target |
| `usb-backup` | `/mnt/backup` | Separate 2 TB backup storage |

Exact job schedules and per-guest inclusion rules are not claimed here because they were not present in the supplied configuration.

## Suggested retention policy

This is a proposed baseline to be applied and adjusted according to available space and workload importance.

| Retention class | Suggested value |
|---|---:|
| Most recent backups | `keep-last 3` |
| Daily | 7 |
| Weekly | 4 |
| Monthly | 3 |

## Backup workflow

1. Select the VM and LXC workloads that require protection.
2. Run scheduled Proxmox backup jobs to a designated backup target.
3. Review the job result and investigate warnings or failures.
4. Monitor target capacity, filesystem health, and disk SMART status.
5. Restore a selected backup to a new, isolated guest ID.
6. Prevent network or IP conflicts before starting the restored workload.
7. Validate the guest and its application or service.
8. Record the result and remove or retain the test guest according to the test plan.

> A backup is not considered working until a restore has been tested.

## Restore-testing policy

- Restore into a new VM or CT ID rather than overwriting the source workload.
- Keep the restored guest stopped until network identity and IP-conflict risks are reviewed.
- Validate both the Proxmox restore task and the application or service inside the guest.
- Record the source backup, target guest ID, task outcome, service check, tester, and date.
- Run restore tests after important platform changes and on a regular schedule.

The first documented LXC restore is recorded in [Restore Test](restore-test.md).

## Remaining resilience gap

An encrypted offsite backup is recommended but is currently a TODO. This repository does **not** claim that an offsite copy exists. An offsite design should define encryption, key custody, retention, bandwidth, restore procedure, and periodic verification before it is treated as operational.
