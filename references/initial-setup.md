# Initial Setup

The first-time setup flow initialises the hub and starts the lightning node. `setup` can only be run once — it is a one-time operation.

> **Important:** When the user asks to "set up a new wallet" or "install Alby Hub", start by confirming the hub is installed and running. Only proceed to `setup`/`start` after the hub process is up.

## Commands

```bash
# Step 1: Initialise the hub (one-time only) — LDK backend is the default
npx @getalby/hub-cli setup --password YOUR_PASSWORD

# Step 2: Start the node and save the JWT token to disk
npx @getalby/hub-cli start --password YOUR_PASSWORD --save

# Verify the node is running
npx @getalby/hub-cli get-info
npx @getalby/hub-cli get-node-status
```

> **Password privacy:** Do not ask the user to share their password in the conversation. Instead, tell the user the command to run themselves (substituting `YOUR_PASSWORD`), or acknowledge that the password will be visible in the terminal/shell history. Only accept the password in-chat if the user explicitly volunteers it. The user can also change their password later.

## Next Steps: Get Lightning Capacity

After setup, the recommended first step is opening a channel via an LSP — no on-chain bitcoin deposit required:

```bash
# See available LSPs — returned in priority order, filter to your active network
npx @getalby/hub-cli get-channel-suggestions

# Ask the user for their preferred channel size (suggest 500,000 sats as default)
# Use the first LSP in the list that you don't already have a channel with
npx @getalby/hub-cli request-lsp-order --amount 500000 --lsp-type <type> --lsp-identifier <identifier>

# Pay the invoice to open the channel (or have a human pay it on testnet)
npx @getalby/hub-cli pay-invoice <invoice>
```

See [LSP](./lsp.md) for full details.

Alternatively, deposit on-chain funds first with `get-onchain-address` and open an outbound channel — but the LSP path above is simpler for most users.

## After Opening a Channel

Remind the user to review their backup options to protect their funds. See [Hub Management](./hub-management.md) for backup details.

## Notes

- If user is using Alby Cloud, setup is NOT needed. Human will complete setup manually.
- Run `setup` only once. Re-running it on an already-initialised hub will fail.
- The default backend is LDK. Pass `--backend` only for non-LDK backends (LND, Phoenixd, Cashu).
- After a machine restart, run `start` again to relaunch the node and get a fresh token.
- Use `--save` so the token is persisted to `~/.hub-cli/token.jwt` and subsequent commands can authenticate automatically.
- See [Authentication](./authentication.md) for token management details.
- See [Backends](./backends.md) for backend-specific setup options.
