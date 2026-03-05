# Payments

Commands for sending and receiving lightning payments, checking balances, and querying transaction history.

## Commands

```bash
# Lightning + on-chain balances
npx @getalby/hub-cli balances

# Get an on-chain deposit address
npx @getalby/hub-cli get-onchain-address

# Pay a BOLT11 invoice
npx @getalby/hub-cli pay-invoice lnbc...

# Pay a zero-amount invoice, specifying the amount in millisatoshis
npx @getalby/hub-cli pay-invoice lnbc... --amount 1000

# Create a BOLT11 invoice
npx @getalby/hub-cli make-invoice --amount 1000 --description "test"

# List recent payments
npx @getalby/hub-cli list-transactions

# List with pagination
npx @getalby/hub-cli list-transactions --limit 50 --offset 0

# Look up a specific payment by payment hash
npx @getalby/hub-cli lookup-transaction <paymentHash>
```

## Notes

- `--amount` for `pay-invoice` is in millisatoshis (msat). Use for zero-amount invoices only.
- `--amount` for `make-invoice` is in millisatoshis.
- `balances` returns both lightning (channel) and on-chain balances.
