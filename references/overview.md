# Overview

Alby Hub is a self-custodial lightning node you run yourself. The `@getalby/hub-cli` is a command-line tool built for agents to manage it — setup, authentication, channels, payments, and NWC app connections.

## Commands

```bash
# Show help
npx @getalby/hub-cli --help

# Hub status, version, backend type
npx @getalby/hub-cli get-info

# Lightning node readiness
npx @getalby/hub-cli get-node-status

# Health check with active alarms
npx @getalby/hub-cli get-health
```

## Global Options

```
-u, --url <url>     Hub URL (default: http://localhost:8080 or HUB_URL env)
-t, --token <jwt>   JWT token (or set HUB_TOKEN env)
```

## Output

All commands output JSON to stdout. Errors are written to stderr as JSON with a `message` field.
