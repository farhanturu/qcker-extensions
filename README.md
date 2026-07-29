# Qcker Extensions

Official extension registry for the [Qcker container engine](https://github.com/farhanturu/qcker).

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

**Production by [PaongLabs](https://github.com/farhanturu)**

## How It Works

1. Browse extensions in the TUI Marketplace tab
2. Install with `qcker extension install <name>`
3. Uninstall with `qcker extension uninstall <name>`
4. Request new extensions via [GitHub Issues](https://github.com/farhanturu/qcker-extensions/issues)

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

Want a new extension? Open an issue:

- [Request New Extension](https://github.com/farhanturu/qcker-extensions/issues/new?template=extension_request.yml)
- [Report Bug](https://github.com/farhanturu/qcker-extensions/issues/new?template=bug_report.yml)

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
└── libmyext.so        # Compiled binary
```

### manifest.json Format

```json
{
  "id": "com.qcker.ext.my-extension",
  "name": "my-extension",
  "display_name": "My Extension",
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

| Category | Description | Examples |
|----------|-------------|----------|
| network | Network drivers | bridge, macvlan, cilium |
| storage | Storage backends | overlayfs, zfs, btrfs |
| security | Security scanners | trivy, grype, clair |
| logging | Log drivers | json-file, loki, syslog |
| build | Build strategies | dockerfile, buildkit, nix |
| other | Other extensions | hooks, commands |

## Extension API

### Traits

- `Extension` - Base trait (required)
- `NetworkDriver` - Custom networking
- `StorageDriver` - Custom storage
- `SecurityScanner` - Vulnerability scanning
- `LogDriver` - Custom logging
- `BuildStrategy` - Custom builds
- `HookExtension` - Lifecycle hooks
- `CommandExtension` - Custom CLI commands

### Capabilities

Extensions can declare capabilities:
- `NetworkAccess` - Can make network connections
- `FileSystemAccess` - Can read/write filesystem
- `ContainerLifecycle` - Can manage containers
- `ImageAccess` - Can read/write images
- `Privileged` - Needs root access
- `SystemInfo` - Can read system information
- `RegistryAccess` - Can access registries
- `ProcessSpawn` - Can spawn subprocesses

## Development

### Rust Extension

```rust
use qcker_ext_api::prelude::*;

#[derive(Default)]
struct MyExtension;

impl Extension for MyExtension {
    fn id(&self) -> &str { "com.qcker.ext.my-extension" }
    fn version(&self) -> &str { "1.0.0" }
    fn name(&self) -> &str { "My Extension" }
    fn description(&self) -> &str { "Does something cool" }
    fn author(&self) -> &str { "Me" }
    fn api_version(&self) -> &str { "1.0.0" }
    fn capabilities(&self) -> Vec<ExtensionCapability> { vec![] }
    fn on_load(&mut self, ctx: &ExtensionContext) -> Result<()> { Ok(()) }
    fn on_unload(&mut self) -> Result<()> { Ok(()) }
}

qcker_extension!(MyExtension);
```

### Other Languages

Extensions can be written in any language that supports Unix socket communication and JSON-RPC protocol.

## Links

- [Qcker Engine](https://github.com/farhanturu/qcker)
- [Extension API Docs](https://github.com/farhanturu/qcker/tree/main/crates/qcker-ext-api)
- [Request Extension](https://github.com/farhanturu/qcker-extensions/issues/new?template=extension_request.yml)

## License

Apache 2.0

## Author

**PaongLabs** - [GitHub](https://github.com/farhanturu)
