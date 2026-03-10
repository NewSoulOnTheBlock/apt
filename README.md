# Milady APT Repository

Debian/Ubuntu package repository for [Milady](https://github.com/milady-ai/milady) — personal AI assistant built on elizaOS.

## Install

```bash
# Add the repository key and source
curl -fsSL https://apt.milaidy.com/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/milady.gpg
echo "deb [signed-by=/usr/share/keyrings/milady.gpg] https://apt.milaidy.com stable main" | \
  sudo tee /etc/apt/sources.list.d/milady.list

# Install
sudo apt update
sudo apt install milady
```

## Supported Distributions

- Debian 12 (Bookworm) and later
- Ubuntu 22.04 LTS and later
- Linux Mint 22+
- Pop!_OS and other Debian derivatives

## How It Works

Hosted via GitHub Pages at `apt.milaidy.com`. On each release:
1. `publish-packages.yml` in the main repo builds a `.deb` and attaches it to the GitHub Release
2. It dispatches `update-repo.yml` here, which downloads the `.deb` into `pool/`
3. Repository metadata (`Packages`, `Release`, `InRelease`) is regenerated and GPG-signed
4. Changes are pushed to the `gh-pages` branch

## Verifying Signatures

```bash
# Check the signing key
curl -fsSL https://apt.milaidy.com/gpg.key | gpg --show-keys
```

## Running as a Service

After installing, you can optionally run Milady as a background service:

```bash
systemctl --user enable --now milady
systemctl --user status milady
journalctl --user -u milady -f
```
