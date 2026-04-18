# Payments

Commands for sending and receiving lightning payments, checking balances, and querying transaction history.

## Commands

```bash
# Lightning + on-chain balances
npx -y @getalby/hub-cli@0.4.0 hub-cli get-balances

# Get an on-chain deposit address
npx -y @getalby/hub-cli@0.4.0 hub-cli get-onchain-address

# Pay a BOLT11 invoice
npx -y @getalby/hub-cli@0.4.0 hub-cli pay-invoice lnbc...

# Pay a zero-amount invoice, specifying the amount in millisatoshis
npx -y @getalby/hub-cli@0.4.0 hub-cli pay-invoice lnbc... --amount 1000

# Pay a lightning address (user@domain)
npx -y @getalby/hub-cli@0.4.0 hub-cli pay-lightning-address user@domain.com --amount 1000

# Create a BOLT11 invoice
npx -y @getalby/hub-cli@0.4.0 hub-cli make-invoice --amount 1000 --description "test"

# List recent payments
npx -y @getalby/hub-cli@0.4.0 hub-cli list-transactions

# List with pagination
npx -y @getalby/hub-cli@0.4.0 hub-cli list-transactions --limit 50 --offset 0

# Look up a specific payment by payment hash
npx -y @getalby/hub-cli@0.4.0 hub-cli lookup-transaction <paymentHash>
```

## On-Chain Reserve Warning

After running `get-balances`, check the on-chain balance. If `lightning.totalSpendable > 0` and `onchain.spendable < 20000`, warn the user in a friendly, non-scary way:

> Your on-chain balance is low. While your funds are safe in your channel, having at least ~20,000 sats on-chain provides a safety reserve in case a channel ever needs to close on-chain unexpectedly. You can top up via `get-onchain-address`.

## Notes

- `--amount` for `pay-invoice` is in millisatoshis (msat). Use for zero-amount invoices only.
- `--amount` for `make-invoice` is in millisatoshis.
- `--amount` for `pay-lightning-address` is in satoshis.
- `get-balances` returns both lightning (channel) and on-chain balances.
