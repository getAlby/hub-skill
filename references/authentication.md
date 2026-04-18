# Authentication

Most commands require a JWT token. Tokens are obtained via `start` or `unlock` and can be stored in multiple ways.

## Commands

```bash
# Start the node and save the JWT token (use after setup or machine restart)
npx -y @getalby/hub-cli@0.4.0 hub-cli start --password YOUR_PASSWORD --save

# Get a fresh token for an already-running hub (no node restart)
npx -y @getalby/hub-cli@0.4.0 hub-cli unlock --password YOUR_PASSWORD --save

# Get a readonly token
npx -y @getalby/hub-cli@0.4.0 hub-cli unlock --password YOUR_PASSWORD --permission readonly --save

# Pass token inline (highest priority)
npx -y @getalby/hub-cli@0.4.0 hub-cli balances -t eyJ...

# Use environment variable
export HUB_TOKEN="eyJ..."
npx -y @getalby/hub-cli@0.4.0 hub-cli balances
```

## Token Priority

| Priority | Location                 | How to use                    |
| -------- | ------------------------ | ----------------------------- |
| 1 (high) | `-t, --token <jwt>` flag | Pass inline with each command |
| 2        | `HUB_TOKEN` env var      | `export HUB_TOKEN=eyJ...`     |
| 3        | `~/.hub-cli/token.jwt`   | Written by `--save`           |

## Alby Cloud

See [Alby Cloud](./alby-cloud.md).

## AUTO_UNLOCK_PASSWORD

When the hub process is started with the `AUTO_UNLOCK_PASSWORD` environment variable set, it automatically starts the lightning node on launch. In this case:

- Skip `start` — the node is already running.
- Call `unlock` directly to obtain a JWT token.

This is recommended for agent-managed or unattended deployments, with the assumption that the local filesystem is trusted and no-one else has access to it.
