# Mutinynet

Mutinynet is a bitcoin signet used for testing. Use it to test the hub without spending real bitcoin.

> **Only use Mutinynet when the user explicitly asks for it** (e.g. mentions "mutinynet", "testnet", "test setup", or "no real funds"). Mainnet is always the default — do not suggest Mutinynet proactively.

## Hub Setup for Mutinynet

Create a `.env` file in the folder where you run the hub. Hub reads it automatically — do not pass env vars inline and do not `source` it manually:

```
NETWORK=signet
MEMPOOL_API=https://mutinynet.com/api
LDK_ESPLORA_SERVER=https://mutinynet.com/api
WORK_DIR=.
```

Then run the hub in the background:

```bash
./bin/albyhub &
```

Do **not** redirect stdout. Logs are written to `{WORK_DIR}/log/nwc.log`.

## Commands

```bash
# Initialise and start the hub (LDK is the default backend)
npx @getalby/hub-cli setup --password YOUR_PASSWORD
npx @getalby/hub-cli start --password YOUR_PASSWORD --save

# Verify the node is running
npx @getalby/hub-cli get-info
```

## Getting Inbound Capacity (Recommended Path)

Opening a channel via an LSP is the recommended first step — no on-chain deposit required.

```bash
# List available LSPs — filter results to signet/Mutinynet entries only
npx @getalby/hub-cli get-channel-suggestions

# Request an invoice from the chosen LSP
npx @getalby/hub-cli request-lsp-order --amount 500000 --lsp-type <type> --lsp-identifier <identifier>
```

Print the invoice as a **single unbroken line** so the user can copy-paste it easily. If the terminal may wrap it, offer to write it to a file.

The LSP invoice must be paid manually via https://faucet.mutinynet.com — the agent cannot pay it. This step requires a human with a GitHub login.

## Getting Test Funds (Alternative / On-Chain)

If an on-chain deposit is needed instead:

```bash
npx @getalby/hub-cli get-onchain-address
```

Visit https://faucet.mutinynet.com to send test sats to the address.

## Notes

- Hub reads `.env` automatically — do not source it or pass vars inline.
- Logs go to `{WORK_DIR}/log/nwc.log` — do not redirect stdout.
- `get-channel-suggestions` returns all networks; filter to signet/Mutinynet entries only.
- LSP channel invoices on Mutinynet must be paid manually via the faucet — the agent cannot pay them.
- Mutinynet transactions use signet coins with no real value.
- Use Mutinynet to test the full setup, channel opening, and payment flows before going to mainnet.
