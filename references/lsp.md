# LSP

LSP (Lightning Service Provider) commands are the **recommended way to get started** with lightning on Alby Hub. An LSP opens a channel for you in exchange for a small fee paid via a lightning invoice — no on-chain bitcoin deposit required. You get both inbound (receive) and outbound (send) capacity immediately.

## Commands

```bash
# List available LSP providers with fees and channel size limits
npx @getalby/hub-cli get-channel-suggestions

# Request a lightning invoice from an LSP to open an inbound channel
npx @getalby/hub-cli request-lsp-order --amount <sats> --lsp-type <type> --lsp-identifier <identifier>

# Pay the LSP invoice to trigger channel opening (mainnet, requires funded wallet)
npx @getalby/hub-cli pay-invoice <invoice>

# Request an Alby LSP channel offer (requires a linked Alby account)
npx @getalby/hub-cli request-alby-lsp-channel-offer
```

## Typical LSP Channel Flow

```bash
# 1. List available LSPs (returned in priority order)
npx @getalby/hub-cli get-channel-suggestions

# 2. Request an invoice from the chosen LSP
npx @getalby/hub-cli request-lsp-order --amount <sats> --lsp-type <type> --lsp-identifier <identifier>

# 3. Pay the invoice to open the channel
npx @getalby/hub-cli pay-invoice <invoice>
```

## Choosing an LSP

- `get-channel-suggestions` returns LSPs in **priority order** — use the first entry for which the hub does not already have an open channel with that LSP.
- **Do not open two channels with the same LSP** — prefer diversifying across providers.
- Filter the list to the user's active network (e.g. signet for Mutinynet, bitcoin for mainnet) before presenting options.

## Channel Size

Before requesting an invoice, **ask the user** how large a channel they want. Suggest **500,000 sats** as a reasonable default if they have no preference.

## Channel Privacy

- All channels should be either **all private** (default) or **all public** — do not mix.
- A mix of private and public channels will make private channels unusable for receiving payments.
- Default to private channels unless the user explicitly requests public.

## Invoice Display

Present the LSP invoice as a **single unbroken string** so the user can copy-paste it. If the terminal may wrap long lines, warn the user that they may need to manually remove any spaces introduced by wrapping. Alternatively, offer to display the invoice as a QR code.

## Notes

- On Mutinynet (signet), a human must pay the LSP invoice via https://faucet.mutinynet.com — the agent cannot pay it automatically.
- `--amount` is the desired inbound capacity in satoshis.
- `--lsp-type` and `--lsp-identifier` come from the `get-channel-suggestions` output.
- See [Mutinynet](./mutinynet.md) for testing LSP flows without real bitcoin.
