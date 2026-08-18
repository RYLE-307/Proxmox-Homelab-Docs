# Restore Test

## Test record

| Field | Result |
|---|---|
| Backup type | Proxmox LXC backup archive |
| Source backup | `vzdump-lxc-203-2026_08_16-01_09_03.tar.zst` |
| Original container | CT 203 — `database` |
| Restore target | CT 801 — `exam` |
| Restore task result | `TASK OK` |
| Inventory result | Restored CT appeared in the Proxmox inventory |
| Final state | Stopped after the test |

The backup filename dates this restore artifact to 2026-08-16. The verified evidence covers the Proxmox restore operation and the restored container's appearance in inventory.

## Verification checklist

- [x] Backup selected.
- [x] Restored to a new CT ID.
- [x] Restore task completed successfully.
- [x] Restored CT appeared in the Proxmox inventory.
- [ ] Confirm IP-conflict prevention before starting the restored CT.
- [ ] Start the restored CT in an isolated or otherwise safe network state.
- [ ] Verify container boot and system health.
- [ ] Complete a database service-level test.
- [ ] Record application-level recovery results and cleanup action.

## What this test proves

- Proxmox could read the selected LXC backup archive.
- The archive could be restored under a different container ID.
- The restore task completed without a Proxmox task error.
- The new container was registered in the inventory.

## What remains unproven

There is no supplied evidence that CT 801 was started, that the restored database accepted connections, or that its network identity was isolated from CT 203. These items remain explicitly open rather than being presented as successful checks.

## Next test procedure

1. Review CT 801 network settings while it is stopped.
2. Change or isolate its address if it could conflict with CT 203.
3. Start CT 801 and confirm normal boot.
4. Check the database service, logs, listening socket, and a test query.
5. Record the results and return the test container to the intended final state.
