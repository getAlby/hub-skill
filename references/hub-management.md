# Hub Management

Commands for monitoring hub health, status, stopping the lightning node, and managing credentials.

## Commands

```bash
# Hub status, version, and backend type
npx @getalby/hub-cli get-info

# Lightning node readiness check
npx @getalby/hub-cli get-node-status

# Health check with active alarms
npx @getalby/hub-cli get-health

# Stop the lightning node (hub HTTP server keeps running)
npx @getalby/hub-cli stop

# Trigger a wallet sync
npx @getalby/hub-cli sync

# Export wallet recovery phrase to a file
npx @getalby/hub-cli backup --password YOUR_PASSWORD

# Export to a custom path
npx @getalby/hub-cli backup --password YOUR_PASSWORD --output /path/to/backup.recovery

# Change the hub unlock password
npx @getalby/hub-cli change-password \
  --current-password YOUR_PASSWORD \
  --confirm-current-password YOUR_PASSWORD \
  --new-password NEW_PASSWORD
```

## Backup

`backup-mnemonic` writes the 12-word wallet recovery phrase to a `.recovery` file (default: `~/.hub-cli/albyhub.recovery`). The command outputs `{ "success": true, "file": "<path>" }`.

> **IMPORTANT:** The agent MUST NOT read the backup file at any point. Just tell the user the file location so they can store it securely offline. The recovery phrase is sensitive — reading it would expose it in conversation history.

## Change Password

`change-password` requires the `--current-password` and `--confirm-current-password` to match (client-side check) before the API call is made. After a successful password change, all existing tokens remain valid until they expire.

## Notes

- `stop` stops the lightning node but leaves the hub HTTP server running. To restart the node, use `start`.
- `get-health` returns active alarms that may indicate issues requiring attention (e.g. low balance, channel problems).
- `get-node-status` indicates whether the lightning node is ready to send and receive payments.
- `sync` queues a wallet sync — the operation may take up to a minute to complete.
