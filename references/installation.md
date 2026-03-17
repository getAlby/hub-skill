# Installation

How to get Alby Hub running. Once it's up, use the CLI to manage it — see [Initial Setup](./initial-setup.md) for the first-time setup flow.

## Alby Cloud (Managed Hosting)

See [Alby Cloud](./alby-cloud.md).

## Linux x86_64 (Recommended for Servers)

Installs as a systemd service that starts automatically on boot.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/getAlby/hub/master/scripts/linux-x86_64/install.sh)" -- -y --skip-verify -s
```

Flags: `-y` non-interactive, `--skip-verify` skip PGP signature verification, `-s` install as systemd service.

Default port: `http://localhost:8029`

To update later: run `./update.sh` in the install directory. Backup data lives in `[install path]/data`.

## Linux aarch64 (ARM64 Servers)

Installs as a systemd service that starts automatically on boot. Same approach as x86_64, different script:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/getAlby/hub/master/scripts/linux-aarch64/install.sh)" -- -y --skip-verify -s
```

Flags: `-y` non-interactive, `--skip-verify` skip PGP signature verification, `-s` install as systemd service.

## Linux x86_64 / aarch64 — HTTP Server Binary (Manual)

For testing or running in a specific folder without systemd. The binary starts an HTTP server you manage yourself.

**Download the latest release:**

```bash
# Find the latest release asset name
gh release view --repo getAlby/hub

# Download (replace FILENAME with the actual asset, e.g. albyhub-Linux-x86_64.tar.bz2)
curl -L -o albyhub.tar.bz2 https://github.com/getAlby/hub/releases/latest/download/FILENAME
tar -xjf albyhub.tar.bz2
```

The binary is at `bin/albyhub`.

**Configuration via `.env` file:**

Hub reads a `.env` file in the working directory automatically — do not pass env vars inline and do not `source` the file manually. Create `.env` before starting.

**Ask the user** whether they want to use the default data directory (`~/.local/share/albyhub`) or keep data in the current folder. If they want data in the current folder, set `WORK_DIR=.` in the `.env`:

```
WORK_DIR=.
# Add any other vars here, e.g. NETWORK, MEMPOOL_API, LDK_ESPLORA_SERVER
```

Setting `WORK_DIR=.` keeps all hub data (database, logs, keys) in the current folder.

**Running the hub:**

Run in the background — the hub manages its own logging:

```bash
./bin/albyhub &
```

Do **not** redirect stdout (e.g. `> albyhub.log`). Logs are written to `{WORK_DIR}/log/nwc.log`.

Default port: `http://localhost:8080`

## Raspberry Pi 4/5 (Experimental)

```bash
/bin/bash -c "$(curl -fsSL https://getalby.com/install/hub/pi-aarch64-install.sh)"
```

Installs to `/opt/albyhub`. Update via `./update.sh`. Official support is limited for this platform.

## Docker

```bash
docker run -v ~/.local/share/albyhub:/data \
  -e WORK_DIR='/data' \
  -p 8080:8080 \
  ghcr.io/getalby/hub:latest
```

Docker Compose file: https://raw.githubusercontent.com/getAlby/hub/master/docker-compose.yml

Default port: `http://localhost:8080`

## Desktop App (Mac / Windows / Linux)

> **Warning:** Do not suggest the desktop app to users working with an agent. Agents cannot control or interact with the desktop GUI. Use one of the server/binary options above instead.

Download the latest release for your platform from https://github.com/getAlby/hub/releases/latest.

Platforms: Mac (arm64), Windows (amd64), Linux (amd64). Designed to run 24/7 on an always-online machine.

## Node Distributions (Umbrel / Start9)

- **Umbrel**: https://github.com/getAlby/umbrel-community-app-store
- **Start9**: https://github.com/horologger/nostr-wallet-connect-startos

Install via your node OS app store.

## System Requirements

| Backend                  | RAM                          | Disk    |
| ------------------------ | ---------------------------- | ------- |
| LDK (default)            | 2 GB (or 512 MB + 2 GB swap) | 1 GB+   |
| External (LND, Phoenixd) | 256 MB                       | Minimal |

lightning port 9735 should be open and reachable for optimal channel connectivity.

## Default Hub URL

After installation, the hub is available at:

- `http://localhost:8080` — Docker, desktop app, manual binary
- `http://localhost:8029` — systemd install scripts
