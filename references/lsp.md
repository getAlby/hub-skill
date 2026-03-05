# LSP

LSP (Lightning Service Provider) commands are the **recommended way to get started** with lightning on Alby Hub. An LSP opens a channel for you in exchange for a small fee paid via a lightning invoice — no on-chain bitcoin deposit required. You get both inbound (receive) and outbound (send) capacity immediately.

## Commands

```bash
# List available LSP providers with fees and channel size limits
npx @getalby/hub-cli get-channel-suggestions

# Request a lightning invoice from an LSP to open an inbound channel
npx @getalby/hub-cli request-lsp-order --amount 1000000 --lsp-type <type> --lsp-identifier <identifier>

# Pay the LSP invoice to trigger channel opening (mainnet, requires funded wallet)
npx @getalby/hub-cli pay-invoice <invoice>

# Request an Alby LSP channel offer (requires a linked Alby account)
npx @getalby/hub-cli request-alby-lsp-channel-offer
```

## Typical LSP Channel Flow

```bash
# 1. List available LSPs and choose one
npx @getalby/hub-cli get-channel-suggestions

# 2. Request an invoice from the chosen LSP
npx @getalby/hub-cli request-lsp-order --amount 1000000 --lsp-type <type> --lsp-identifier <identifier>

# 3. Pay the invoice to open the channel
npx @getalby/hub-cli pay-invoice <invoice>
```

## Notes

- On Mutinynet (signet), a human must pay the LSP invoice via https://faucet.mutinynet.com — the agent cannot pay it automatically.
- `--amount` is the desired inbound capacity in satoshis.
- `--lsp-type` and `--lsp-identifier` come from the `get-channel-suggestions` output.
- See [Mutinynet](./mutinynet.md) for testing LSP flows without real bitcoin.
