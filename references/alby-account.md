# Alby Account

Connecting an Alby account to your hub unlocks several benefits:

- **Lightning Address** — Personalized lightning address to receive payments
- **Email Notifications** — Instant notifications about incoming transactions and more
- **Encrypted Backups** — Automatic encrypted static channel backups saved to your Alby account, so you can always recover your funds
- **Support** — Human support via live chat when you need a helping hand
- **Fiat Top-ups** — Top up with fiat and get bitcoin delivered to your Alby Hub

## Connecting Your Alby Account

Connecting requires two steps:

**Step 1** — Get the authorization URL:

```bash
npx @getalby/hub-cli connect-alby-account
```

This returns a JSON object with an `albyAuthUrl`. Tell the user to open that URL in their browser, sign in to their Alby account, and copy the authorization code they receive.

**Step 2** — Submit the authorization code:

```bash
npx @getalby/hub-cli connect-alby-account --code <code>
```

On success, returns `{ "success": true }`. If the account is already connected, step 1 returns `{ "albyAccountConnected": true, "albyUserIdentifier": "..." }` instead of a URL.
