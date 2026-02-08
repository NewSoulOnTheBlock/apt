# Milaidy APT Repository

Debian/Ubuntu package repository for [Milaidy](https://github.com/milady-ai/milaidy) — personal AI assistant built on ElizaOS.

## Quick Install

```bash
# Add the repository key and source
curl -fsSL https://milady-ai.github.io/apt/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/milaidy.gpg
echo "deb [signed-by=/usr/share/keyrings/milaidy.gpg] https://milady-ai.github.io/apt stable main" | \
  sudo tee /etc/apt/sources.list.d/milaidy.list

# Install
sudo apt update
sudo apt install milaidy
```

## Without GPG (for testing)

```bash
echo "deb [trusted=yes] https://milady-ai.github.io/apt stable main" | \
  sudo tee /etc/apt/sources.list.d/milaidy.list
sudo apt update
sudo apt install milaidy
```

## How it works

This repository is hosted via GitHub Pages. When a new version of Milaidy is released:
1. The `publish-packages.yml` workflow in the main repo triggers this repo's `update-repo.yml`
2. The workflow builds a `.deb` package from the npm release
3. Repository metadata (Packages, Release) is regenerated
4. Changes are pushed to the `gh-pages` branch

## Repository structure

```
├── dists/stable/main/       # Package metadata
│   ├── binary-amd64/
│   ├── binary-arm64/
│   └── binary-all/
├── pool/main/m/milaidy/     # .deb packages
├── gpg.key                  # Repository signing key
└── index.html               # Landing page
```

## Signing

The repository is GPG-signed when `APT_GPG_PRIVATE_KEY` and `APT_GPG_PASSPHRASE` secrets are configured.
See the [publishing guide](https://github.com/milady-ai/milaidy/blob/main/packaging/PUBLISHING_GUIDE.md) for setup instructions.
