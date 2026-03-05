# Apps

Commands for managing NWC (Nostr Wallet Connect) app connections. NWC apps allow external applications to interact with the hub's wallet.

## Commands

```bash
# List NWC app connections
npx @getalby/hub-cli apps

# Create a new NWC connection with default permissions
npx @getalby/hub-cli create-app --name "My App"

# Create with custom scopes and a spending budget
npx @getalby/hub-cli create-app --name "My App" \
  --scopes "pay_invoice,get_balance" \
  --max-amount 10000 \
  --budget-renewal monthly

# Create an isolated sub-wallet app (separate balance)
npx @getalby/hub-cli create-app --name "Isolated App" --isolated --unlock-password YOUR_PASSWORD
```

## Notes

- `create-app` returns a `nostrWalletConnectUrl` (NWC connection string) that the external app uses to connect.
- Isolated apps have their own sub-wallet balance separate from the main hub wallet.
- `--budget-renewal` accepts: `daily`, `weekly`, `monthly`, `yearly`, `never`.
- Available scopes include: `pay_invoice`, `get_balance`, `get_info`, `make_invoice`, `lookup_invoice`, `list_transactions`, `sign_message`.
