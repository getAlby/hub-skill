# Mutinynet

Mutinynet is a bitcoin signet used for testing. Use it to test the hub without spending real bitcoin.

## Hub Setup for Mutinynet

Start the Alby Hub binary with Mutinynet environment variables:

```bash
NETWORK=signet \
MEMPOOL_API=https://mutinynet.com/api \
LDK_ESPLORA_SERVER=https://mutinynet.com/api \
./bin/albyhub
```

## Commands

```bash
# Initialise and start the hub (LDK is the default backend)
npx @getalby/hub-cli setup --password YOUR_PASSWORD
npx @getalby/hub-cli start --password YOUR_PASSWORD --save

# Verify the node is running
npx @getalby/hub-cli get-info

# Get an on-chain deposit address for test funds
npx @getalby/hub-cli get-onchain-address
```

## Getting Test Funds

Visit https://faucet.mutinynet.com to get test sats sent to your on-chain address. This step requires a human with a GitHub login — it cannot be automated.

## Notes

- LSP channel invoices on Mutinynet must also be paid manually via the faucet — the agent cannot pay them.
- Mutinynet transactions use signet coins with no real value.
- Use Mutinynet to test the full setup, channel opening, and payment flows before going to mainnet.
