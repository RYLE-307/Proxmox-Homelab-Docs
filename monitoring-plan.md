# Monitoring Plan

The monitoring goal is to detect resource exhaustion, storage degradation, failed services, network problems, and backup failures early enough to act before they become outages or data-loss events.

The Zabbix container exists and is running, but this document does not claim that every check below is already configured.

## Monitoring coverage

| Area | Signals to monitor | Example tools |
|---|---|---|
| CPU | Load average, usage, steal time, sustained saturation | Proxmox dashboard, Zabbix, `top`, `htop` |
| Memory | Used/available RAM, swap use, memory pressure | Proxmox dashboard, Zabbix, `free` |
| Filesystems | Space, inodes, mount availability, growth rate | Zabbix, `df`, `du` |
| Disk I/O | Latency, throughput, queueing, I/O errors | Proxmox dashboard, Zabbix, `iostat`, journal |
| Disk health | SMART health, temperature, reallocated/pending sectors, errors | SMART tools / `smartctl` |
| Network | Interface/link state, traffic, packet loss, reachability | Zabbix, Proxmox dashboard, system journal |
| Services | Nginx, Zabbix, database, Samba/file services, VPN | Zabbix service and port checks, `systemctl` |
| Backups | Last job status, age of last success, failed jobs, target space | Proxmox tasks, Zabbix, logs |
| Recovery | Date and outcome of the latest restore test | Restore-test record and manual review |

## Priority checks

1. Alert on a failed backup job or an unexpectedly old last-successful backup.
2. Alert before `local`, `local-lvm`, `hdd-storage`, or `usb-backup` reaches critical capacity.
3. Alert on disk SMART failures, rising error counters, or unsafe temperature.
4. Alert when the Proxmox host, gateway, or critical infrastructure guests are unreachable.
5. Alert when Nginx, database, file, VPN, or monitoring services stop responding.
6. Review swap growth, persistent CPU saturation, and high I/O latency.

## Tool roles

- **Proxmox dashboard:** host and guest state, resource trends, storage usage, and task history.
- **Zabbix:** centralized metrics, availability checks, triggers, history, and notifications.
- **SMART tools / `smartctl`:** physical disk health, temperature, self-tests, and error attributes.
- **systemd and `journalctl`:** service status, boot problems, kernel messages, and unit logs.
- **`df`, `du`, `iostat`, `free`, `top`, and `htop`:** direct investigation and incident triage.

## Suggested review rhythm

This cadence is a proposal, not a claim about the current configuration.

| Frequency | Review |
|---|---|
| Continuous | Host/guest availability, critical services, capacity thresholds, backup failures |
| Daily | Failed Proxmox tasks, last backup result, active alerts |
| Weekly | Storage growth, performance trends, repeated warnings |
| Monthly | SMART extended tests, retention behavior, alert quality, restore-test status |
| After major changes | Service health, backup completion, and a targeted recovery check |

## Documentation rule

Monitoring should answer three questions for every critical service: **Is it reachable? Is it healthy? Can it be recovered?** Any check not yet implemented should remain documented as planned rather than silently assumed.
