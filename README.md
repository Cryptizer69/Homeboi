# Homeboi

Homeboi installs and wires a self-hosted media stack (Plex/Jellyfin + *arr + download client + request apps) using Docker containers and an Ansible playbook. It also provides:

- A terminal UI (`homeboi`)
- A web dashboard with a setup checklist (`http://<server-ip>:6969`)

## Install

Prereqs: Docker. (Homeboi can install Ansible if needed when you run the CLI.)

```bash
git clone https://github.com/SgtDinosaur/Homeboi.git Homeboi
cd Homeboi
./install.sh
homeboi
```

`./install.sh` creates a `homeboi` command (via a symlink). If you move the `Homeboi/` folder later, re-run `./install.sh`.

## Usage

- Run `homeboi` and choose **Launch Stack**.
- After deployment, open the dashboard: `http://<server-ip>:6969` and follow the **Setup Checklist**.

## Configuration

Homeboi writes local configuration to `settings.env`. This file contains secrets (passwords, VPN creds, API keys) and should never be committed.

- Template: `settings.env.example`
- Local file: `settings.env` (ignored via `.gitignore`)

## Updating

```bash
cd Homeboi
git pull
homeboi
```

## Removing

Use the terminal UI:

- `homeboi` → **Remove Stack**
- When asked, choose whether to also remove configuration files.

To uninstall the `homeboi` command:

```bash
./uninstall.sh
```

## Plex on headless servers

Plex claiming/onboarding can be finicky on headless servers. If Plex is unclaimed (`claimed="0"`) but the web UI shows “Not authorized”, claim it from a “local” browser context via an SSH tunnel:

```bash
ssh -N -L 32400:127.0.0.1:32400 <ssh-user>@<server-ip>
```

Then open:

- `http://localhost:32400/web/index.html#!/setup`
