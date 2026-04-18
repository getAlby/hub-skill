# LSP

LSP (Lightning Service Provider) commands are the **recommended way to get started** with lightning on Alby Hub. An LSP opens a channel for you in exchange for a small fee paid via a lightning invoice — no on-chain bitcoin deposit required. You get both inbound (receive) and outbound (send) capacity immediately.

## Commands

```bash
# List available LSP providers with fees and channel size limits
npx -y @getalby/hub-cli@0.4.0 hub-cli get-channel-suggestions

# Request a lightning invoice from an LSP to open an inbound channel
npx -y @getalby/hub-cli@0.4.0 hub-cli request-lsp-order --amount <sats> --lsp-type <type> --lsp-identifier <identifier>

# Pay the LSP invoice to trigger channel opening (mainnet, requires funded wallet)
npx -y @getalby/hub-cli@0.4.0 hub-cli pay-invoice <invoice>

# Request an Alby LSP channel offer (requires a linked Alby account)
npx -y @getalby/hub-cli@0.4.0 hub-cli request-alby-lsp-channel-offer
```

## Typical LSP Channel Flow

```bash
# 1. List available LSPs (returned in priority order)
npx -y @getalby/hub-cli@0.4.0 hub-cli get-channel-suggestions

# 2. Request an invoice from the chosen LSP
npx -y @getalby/hub-cli@0.4.0 hub-cli request-lsp-order --amount <sats> --lsp-type <type> --lsp-identifier <identifier>

# 3. Pay the invoice to open the channel
npx -y @getalby/hub-cli@0.4.0 hub-cli pay-invoice <invoice>
```

## Choosing an LSP

- `get-channel-suggestions` returns LSPs in **priority order** — use the first entry for which the hub does not already have an open channel with that LSP.
- **Do not open two channels with the same LSP** — prefer diversifying across providers.
- Filter the list to the user's active network (e.g. signet for Mutinynet, bitcoin for mainnet) before presenting options.

## Interpreting get-channel-suggestions Output

The `get-channel-suggestions` output includes fields like channel size and fee ranges per LSP. Key distinction:

- **Channel size** (e.g. `minimumChannelSize`, `maximumChannelSize`): The inbound capacity the LSP will open for you. This is NOT the amount you pay — it is what you _receive_ (ability to receive payments up to this amount). A 2,000,000 sat channel does not mean you need 2M sats.
- **Fee**: The small amount you actually pay to the LSP, via a lightning invoice returned by `request-lsp-order`. This is the only cost to the user.

When comparing LSPs for a user, compare fees (what they pay), not channel sizes. For example: "Provider A costs 5,762 sats to open a 2M sat channel" — not "if you have 2M sats available."

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
