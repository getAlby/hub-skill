# Hub Management

Commands for monitoring hub health, status, stopping the lightning node, and managing credentials.

## Commands

```bash
# Hub status, version, and backend type
npx -y @getalby/hub-cli@0.4.0 hub-cli get-info

# Lightning node readiness check
npx -y @getalby/hub-cli@0.4.0 hub-cli get-node-status

# Health check with active alarms
npx -y @getalby/hub-cli@0.4.0 hub-cli get-health

# Stop the lightning node (hub HTTP server keeps running)
npx -y @getalby/hub-cli@0.4.0 hub-cli stop

# Trigger a wallet sync
npx -y @getalby/hub-cli@0.4.0 hub-cli sync

# Export wallet recovery phrase to a file
npx -y @getalby/hub-cli@0.4.0 hub-cli backup --password YOUR_PASSWORD

# Export to a custom path
npx -y @getalby/hub-cli@0.4.0 hub-cli backup --password YOUR_PASSWORD --output /path/to/backup.recovery

# Change the hub unlock password
npx -y @getalby/hub-cli@0.4.0 hub-cli change-password \
  --current-password YOUR_PASSWORD \
  --confirm-current-password YOUR_PASSWORD \
  --new-password NEW_PASSWORD
```

## Backup

See [Backups](./backups.md) for backup information.

## Change Password

`change-password` requires the `--current-password` and `--confirm-current-password` to match (client-side check) before the API call is made. After a successful password change, all existing tokens remain valid until they expire.

## Notes

- `stop` stops the lightning node but leaves the hub HTTP server running. To restart the node, use `start`.
- `get-health` returns active alarms that may indicate issues requiring attention (e.g. low balance, channel problems).
- `get-node-status` indicates whether the lightning node is ready to send and receive payments.
- `sync` queues a wallet sync — the operation may take up to a minute to complete.
