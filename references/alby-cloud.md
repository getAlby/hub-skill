# Alby Cloud

Alby Hub hosted on Alby Cloud — no server required.

## Setup (Human Step Required)

The human must subscribe to Alby Cloud at https://getalby.com/subscription/new and then complete the onboarding wizard themselves. Do not run `setup` — Alby Cloud onboarding replaces it.

## CLI Authentication

1. Human must find their Alby Cloud hub name (e.g. `nwcxxxxxxxxxx`) at https://my.albyhub.com/settings/developer
2. Save it once:
   ```bash
   echo "nwcxxxxxxxxxx" > ~/.hub-cli/alby-cloud.txt
   ```
3. The CLI auto-uses `https://my.albyhub.com` and sets the required routing headers. Use `start`/`unlock` as normal:
   ```bash
   npx -y @getalby/hub-cli@0.4.0 hub-cli start --password YOUR_PASSWORD --save
   npx -y @getalby/hub-cli@0.4.0 hub-cli balances
   ```

To override the hub name for a single invocation, set the `ALBY_HUB_NAME` env var.
