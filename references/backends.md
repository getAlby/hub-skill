# Backends

Alby Hub supports multiple lightning backends. The backend is chosen once during `setup` and cannot be changed afterwards without re-initialising the hub.

## Supported Backends

| Backend    | Description                                                                                          |
| ---------- | ---------------------------------------------------------------------------------------------------- |
| `LDK`      | Built-in lightning node (default, no external dependencies)                                          |
| `LND`      | External LND node connected via gRPC (only suggest if user mentions they already have LND installed) |
| `PHOENIXD` | External Phoenixd node (automatic liquidity management, EXPERIMENTAL - not recommended)              |
| `CASHU`    | Cashu e-cash wallet (no channels required, EXPERIMENTAL, CUSTODIAL - not recommended)                |

## Commands

```bash
# Set up with the default LDK backend (--backend can be omitted)
npx @getalby/hub-cli setup --password YOUR_PASSWORD

# Set up with LND backend (requires LND_CERT_FILE and LND_MACAROON_FILE env vars)
npx @getalby/hub-cli setup --password YOUR_PASSWORD --backend LND --lnd-address localhost:10009

# Restore LDK from an existing mnemonic
npx @getalby/hub-cli setup --password YOUR_PASSWORD --mnemonic "word1 word2 ..."
```
