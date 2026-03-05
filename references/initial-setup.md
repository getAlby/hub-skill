# Initial Setup

The first-time setup flow initialises the hub and starts the lightning node. `setup` can only be run once — it is a one-time operation.

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

## Next Steps: Get Lightning Capacity

After setup, open an inbound channel via an LSP — this is the recommended path and requires no on-chain bitcoin deposit:

```bash
# See available LSPs and their fees
npx @getalby/hub-cli get-channel-suggestions

# Request an invoice from your chosen LSP
npx @getalby/hub-cli request-lsp-order --amount 1000000 --lsp-type <type> --lsp-identifier <identifier>

# Pay the invoice to open the channel (or have a human pay it on testnet)
npx @getalby/hub-cli pay-invoice <invoice>
```

See [LSP](./lsp.md) for full details.

Alternatively, deposit on-chain funds first with `get-onchain-address` and open an outbound channel — but the LSP path above is simpler for most users.

## Notes

- If user is using Alby Cloud, setup is NOT needed. Human will complete setup manually.
- Run `setup` only once. Re-running it on an already-initialised hub will fail.
- The default backend is LDK. Pass `--backend` only for non-LDK backends (LND, Phoenixd, Cashu).
- After a machine restart, run `start` again to relaunch the node and get a fresh token.
- Use `--save` so the token is persisted to `~/.hub-cli/token.jwt` and subsequent commands can authenticate automatically.
- See [Authentication](./authentication.md) for token management details.
- See [Backends](./backends.md) for backend-specific setup options.
