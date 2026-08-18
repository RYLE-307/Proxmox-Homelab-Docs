# Security Notes

This is a public documentation repository. Its contents must remain useful without exposing credentials, private access material, or externally routable infrastructure details.

## Never commit

- Passwords, password hashes, recovery codes, or authentication exports
- SSH private keys or unredacted authorized-key inventories
- API keys, access tokens, session cookies, or environment files containing secrets
- VPN private keys, credential-bearing client/server configurations, or QR codes
- Database dumps, production-like data exports, VM/LXC backups, or raw backup archives
- Public VPS credentials, real external IP addresses, or provider account details
- Screenshots containing secrets, browser sessions, terminal history, or sensitive URLs

Local RFC1918 addresses such as `192.168.2.200` may be documented because they are not publicly routable. Their presence does not make secret material safe to publish.

## Recommended host baseline

- Prefer SSH keys and restrict password authentication where operationally practical.
- Keep Proxmox, Debian, guest operating systems, and applications updated.
- Use firewall rules that permit only required traffic between trusted sources and services.
- Use separate named users and groups; avoid shared administrative identities.
- Grant the minimum permissions required for each account and service.
- Keep backup storage logically and physically separated from the system disk.
- Test restores regularly and record both platform-level and service-level results.
- Rotate passwords, keys, and tokens after major access or infrastructure changes.
- Review failed logins, privilege changes, service failures, and backup errors.

These are baseline recommendations. They are not presented as fully implemented controls unless evidence is added to the repository.

## Safe screenshot checklist

Before adding an image under `screenshots/`:

- [ ] Crop unrelated windows, browser tabs, bookmarks, and terminal history.
- [ ] Redact passwords, tokens, cookies, QR codes, keys, and external addresses.
- [ ] Check filenames and visible task logs for sensitive content.
- [ ] Remove user-identifying data that is not needed for the documentation.
- [ ] Confirm that no backup archive or database content is shown.
- [ ] Review the final exported image at full resolution before committing it.

## Repository review before publishing

1. Search all text files for common secret markers such as `password`, `token`, `secret`, `private key`, and credential URLs.
2. Inspect every screenshot manually.
3. Review the staged Git diff, including filenames and binary additions.
4. If a secret was committed, rotate or revoke it; deleting it from the latest file is not sufficient protection.
