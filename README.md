# Qcker Extensions

Official extension registry for the Qcker container engine.

## How It Works

1. Browse extensions in the marketplace
2. Install with `qcker extension install <name>`
3. Uninstall with `qcker extension uninstall <name>`
4. Request new extensions via GitHub Issues

## Available Extensions

| Extension | Category | Status | Description |
|-----------|----------|--------|-------------|
| bridge | network | Built-in | Default bridge networking |
| overlayfs | storage | Built-in | Default overlayfs storage |
| trivy | security | Available | Vulnerability scanning |
| cilium | network | Available | eBPF-based networking |
| zfs | storage | Available | ZFS storage backend |
| loki | logging | Available | Grafana Loki logging |
| buildkit | build | Available | BuildKit compatible builder |

## Installing Extensions

```bash
# Install from registry
qcker extension install trivy

# Install from local path
qcker extension install /path/to/extension.so

# List installed
qcker extension ls

# Uninstall
qcker extension uninstall trivy
```

## Requesting Extensions

Want a new extension? Open an issue using our templates:

- [Request New Extension](https://github.com/qcker/qcker-extensions/issues/new?template=extension_request.yml)
- [Report Bug](https://github.com/qcker/qcker-extensions/issues/new?template=bug_report.yml)

## Contributing Extensions

1. Fork this repository
2. Create your extension in `extensions/<name>/`
3. Add `manifest.json` with metadata
4. Submit a pull request
5. After review, it will appear in the marketplace

### Extension Structure

```
extensions/my-extension/
├── manifest.json      # Extension metadata
├── README.md          # Documentation
├── src/               # Source code (optional)
│   └── lib.rs
├── Cargo.toml         # Rust project (optional)
└── libmyext.so        # Compiled binary (or build instructions)
```

### manifest.json Format

```json
{
  "id": "com.qcker.ext.my-extension",
  "name": "My Extension",
  "version": "1.0.0",
  "api_version": "1.0.0",
  "author": "Your Name",
  "description": "What this extension does",
  "category": "network|storage|security|logging|build|other",
  "capabilities": ["NetworkAccess", "FileSystemAccess"],
  "repository": "https://github.com/user/repo",
  "license": "Apache-2.0"
}
```

## Extension Categories

- **network** - Network drivers (bridge, macvlan, cilium, etc.)
- **storage** - Storage backends (overlayfs, zfs, btrfs, etc.)
- **security** - Security scanners (trivy, grype, etc.)
- **logging** - Log drivers (json-file, loki, syslog, etc.)
- **build** - Build strategies (dockerfile, buildkit, nix, etc.)
- **other** - Other extensions

## API

Extensions communicate with Qcker via JSON-RPC over Unix sockets.

### Available Traits

- `Extension` - Base trait (required)
- `NetworkDriver` - Custom networking
- `StorageDriver` - Custom storage
- `SecurityScanner` - Vulnerability scanning
- `LogDriver` - Custom logging
- `BuildStrategy` - Custom builds
- `HookExtension` - Lifecycle hooks
- `CommandExtension` - Custom CLI commands

### Extension SDK

```toml
[dependencies]
qcker-ext-api = "0.1"
```

## License

Apache 2.0
