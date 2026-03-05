# Installation

How to get Alby Hub running. Once it's up, use the CLI to manage it — see [Initial Setup](./initial-setup.md) for the first-time setup flow.

## Alby Cloud (Managed Hosting)

See [Alby Cloud](./alby-cloud.md).

## Linux x86_64 (Recommended for Servers)

Installs as a systemd service that starts automatically on boot.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/getAlby/hub/master/scripts/linux-x86_64/install.sh)"
```

Default port: `http://localhost:8029`

To update later: run `./update.sh` in the install directory. Backup data lives in `[install path]/data`.

## Linux aarch64 (ARM64 Servers)

Same approach as x86_64, different script:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/getAlby/hub/master/scripts/linux-aarch64/install.sh)"
```

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
