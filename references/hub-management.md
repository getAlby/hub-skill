# Hub Management

Commands for monitoring hub health, status, and stopping the lightning node.

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
```

## Notes

- `stop` stops the lightning node but leaves the hub HTTP server running. To restart the node, use `start`.
- `get-health` returns active alarms that may indicate issues requiring attention (e.g. low balance, channel problems).
- `get-node-status` indicates whether the lightning node is ready to send and receive payments.
