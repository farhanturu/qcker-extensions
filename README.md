# Qcker Extensions Marketplace

Official extension registry for [Qcker](https://github.com/farhanturu/qcker) — A daemonless, rootless container engine.

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Qcker Version](https://img.shields.io/badge/qcker-v1.1.0-blue)](https://github.com/farhanturu/qcker/releases/tag/v1.1.0)

---

## Overview

This repository contains the official marketplace registry and extension definitions for Qcker. Extensions are compiled as shared libraries (`.so`) that plug into the Qcker runtime.

## Directory Structure

```
qcker-extensions/
├── extensions/              # Extension source code
│   ├── bridge/             # Bridge network driver
│   ├── overlayfs/          # OverlayFS storage driver
│   ├── trivy/              # Vulnerability scanner
│   ├── cilium/             # eBPF networking
│   ├── zfs/                # ZFS storage backend
│   ├── loki/               # Log aggregation
│   └── buildkit/           # Image builder
├── marketplace/
│   └── extensions.json     # Registry manifest
├── API.md                  # Extension SDK documentation
├── CONTRIBUTING.md         # How to create extensions
└── README.md
```

## Installing Extensions

```bash
# From CLI
qcker extension install /path/to/extension
qcker extension enable <id>
qcker extension disable <id>
qcker extension uninstall <id>
qcker extension ls
```

## Available Extensions

| Extension | Category | Status | Description |
|-----------|----------|--------|-------------|
| bridge | network | Built-in | Default bridge networking |
| overlayfs | storage | Built-in | Copy-on-write storage |
| trivy | security | Available | Vulnerability scanning |
| cilium | network | Available | eBPF networking & security |
| zfs | storage | Available | ZFS snapshots & compression |
| loki | logging | Available | Grafana Loki log aggregation |
| buildkit | build | Available | Fast Dockerfile builder |

## Development

See [API.md](API.md) for the extension SDK reference.

```bash
# Clone the SDK
git clone https://github.com/farhanturu/qcker-extensions.git
cd qcker-extensions/extensions/my-extension

# Build
cargo build --release --lib

# Install
qcker extension install .
```

---

**Production by PaongLabs** · [Apache 2.0 License](LICENSE)
