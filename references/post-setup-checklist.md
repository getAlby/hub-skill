# Post-Setup Checklist

A short list of the key things a new user should do to get the most out of their Alby Hub. Treat this as a loose checklist — not a rigid script. **If installation or initial setup is not completed yet - do those first**.

## Items

1. **Open your first channel** — get inbound and outbound lightning capacity. The simplest path is buying a channel from an LSP. See [LSP](./lsp.md).
2. **Link your Alby Account** — unlocks a lightning address, email notifications, encrypted backups, and fiat top-ups. See [Alby Account](./alby-account.md).
3. **Send or receive your first payment** — confirm the wallet works end-to-end. See [Payments](./payments.md).
4. **Connect your first app** — create an NWC app connection so an external client can use the wallet. See [Apps](./apps.md).
5. **Back up your keys** — save the recovery phrase somewhere offline, and (for LDK) keep the static channel backup file safe. See [Backups](./backups.md).

## When to surface this checklist

- **After initial setup** — once `setup` + `start` succeed for the first time, walk the user through this list (item by item, not all at once) and offer to help with each.
- **When the user asks "what should I do next?" / "is there anything to do?" / "anything I'm missing?"** — check which items are done and mention the remaining ones.
- **Occasionally** — if the user has been using the hub for a while and a critical item is clearly missing (e.g. no channels open, no backup taken), you may gently remind them once. Do not nag.

## When NOT to surface it

- Do **not** include the checklist in unrelated responses.
- Do **not** repeat it every session or on every command.
- Do **not** show it if the user is clearly working on something specific — finish that task first.

## Detecting what's already done

Before mentioning an item, check state where possible so you don't suggest something already complete:

- Channels — `list-channels` (skip item 1 if any channel exists).
- Connect Alby account — `get-info` with no args returns `albyAccountConnected: true`.
- First payment — `list-transactions` (skip item 3 if any settled transaction exists).
- Apps — `list-apps` (skip item 4 if any app is listed; ignore the built-in CLI app if present).
- Backup — there is no reliable way to detect this; ask the user if they've stored their recovery phrase safely.

Only mention the items that are still outstanding.
