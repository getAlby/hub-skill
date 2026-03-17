---
name: alby-hub-skill
description: Manage an Alby Hub self-custodial lightning node using the @getalby/hub-cli command-line tool - setup, authentication, channels, payments, NWC apps, and LSP integration.
license: Apache-2.0
metadata:
  author: getAlby
  version: "0.1.1"
---

# Alby Hub Agent Skill

## When to use this skill

Use this skill to manage an Alby Hub lightning node via the CLI.

- [Installation: How to get Alby Hub running — cloud, Linux, Docker, Raspberry Pi, desktop](./references/installation.md)
- [Overview: What Alby Hub is and how the CLI fits in](./references/overview.md)
- [Backends: LDK, LND, Phoenixd, Cashu — features and configuration](./references/backends.md)
- [Initial Setup: First-time hub initialisation flow](./references/initial-setup.md)
- [Authentication: Token management, start, unlock, token priority](./references/authentication.md)
- [Hub Management: Stop, health, info, node status](./references/hub-management.md)
- [LSP: Channel ordering, channel suggestions, channel offer (recommended for opening first channel)](./references/lsp.md)
- [Channels: Open/close channels, peers, connect-peer, node connection info](./references/channels.md)
- [Payments: Pay/make invoices, transactions, lookup, balances, wallet address](./references/payments.md)
- [Apps: NWC app management — create-app, list apps](./references/apps.md)
- [Mutinynet: Signet testing setup without real bitcoin](./references/mutinynet.md)

## Key Rules

### Running the CLI

```bash
npx @getalby/hub-cli [options] <command>
```

### Default Hub URL

The CLI connects to `http://localhost:8080` by default. Override with `-u <url>` or the `HUB_URL` environment variable.

### Default Backend

LDK is the default backend. Omit `--backend` when using LDK. Only specify `--backend` for non-LDK backends (LND, Phoenixd, Cashu).

### Token Priority

Tokens are resolved in this order (highest to lowest priority):

1. `-t, --token <jwt>` flag
2. `HUB_TOKEN` environment variable
3. `~/.hub-cli/token.jwt` (default saved token)

Always use `--save` with `start` or `unlock`. Without it the token is ephemeral and lost when the shell exits.

### AUTO_UNLOCK_PASSWORD

When the hub is configured with the `AUTO_UNLOCK_PASSWORD` environment variable, it starts the lightning node automatically on launch. In this case, skip `start` and call `unlock` directly to obtain a token.

### Output Format

All commands output JSON to stdout. Errors are written to stderr as JSON with a `message` field.

### Language Conventions

Use lowercase for "bitcoin" and "lightning" unless they appear as the first word in a sentence.

### User Communication

**Do NOT give users CLI commands to run** unless one of these two conditions applies:
1. The task requires input the agent cannot provide (e.g. a password) — in that case, give the command template with a placeholder like `YOUR_PASSWORD` and explain what the user should do.
2. The user explicitly asks for the CLI command.

For all other follow-up checking or monitoring, use plain language. For example: *"If you'd like to check whether your channel is ready to use, just ask."*
