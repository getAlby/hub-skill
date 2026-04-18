# Channels

Commands for managing lightning channels and peers, including opening, closing, and querying channel state.

## Commands

```bash
# List lightning channels
npx -y @getalby/hub-cli@0.4.0 hub-cli list-channels

# Get your node's connection info (pubkey, address, port)
npx -y @getalby/hub-cli@0.4.0 hub-cli get-node-connection-info

# List connected peers
npx -y @getalby/hub-cli@0.4.0 hub-cli list-peers

# Connect to a lightning peer
npx -y @getalby/hub-cli@0.4.0 hub-cli connect-peer --pubkey <pubkey> --address <host> --port <port>

# Open a private outbound channel to a peer (requires on-chain funds)
npx -y @getalby/hub-cli@0.4.0 hub-cli open-channel --pubkey <pubkey> --amount-sats 500000

# Open a public outbound channel
npx -y @getalby/hub-cli@0.4.0 hub-cli open-channel --pubkey <pubkey> --amount-sats 500000 --public

# Close a channel cooperatively
npx -y @getalby/hub-cli@0.4.0 hub-cli close-channel --peer-id <pubkey> --channel-id <id>

# Force-close a channel
npx -y @getalby/hub-cli@0.4.0 hub-cli close-channel --peer-id <pubkey> --channel-id <id> --force
```

## After Opening a Channel

After opening a channel (either outbound or via LSP), immediately run `list-channels` and report the confirmation status to the user:

```bash
npx -y @getalby/hub-cli@0.4.0 hub-cli list-channels
```

Look at the `confirmations` and `confirmationsRequired` fields on the new channel and tell the user: how many confirmations are required, and how many have been received so far. This sets expectations — the channel won't be usable until fully confirmed.

See [Backups](./backups.md) for information on static channel backups.

## Notes

- Opening an outbound channel requires on-chain funds. Use `get-onchain-address` to deposit first.
- For most users, opening a channel via an LSP is the preferred and simpler path — no on-chain deposit needed. See [LSP](./lsp.md).
- Force-closing a channel has a time-lock delay before funds are available on-chain. Prefer cooperative close when possible.
