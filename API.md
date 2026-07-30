# Qcker Extensions API Reference

## Extension Types

| Type | Trait | Description |
|------|-------|-------------|
| Network Driver | `NetworkDriver` | Custom container networking |
| Storage Driver | `StorageDriver` | Custom storage backends |
| Security Scanner | `SecurityScanner` | Vulnerability scanning |
| Log Driver | `LogDriver` | Custom log capture |
| Build Strategy | `BuildStrategy` | Alternative build methods |
| Hook Extension | `HookExtension` | Container lifecycle hooks |
| Command Extension | `CommandExtension` | Custom CLI commands |

## Rust SDK

```toml
[dependencies]
qcker-ext-api = "0.1"
```

### Base Extension Trait

```rust
use qcker_ext_api::prelude::*;

#[derive(Default)]
struct MyExtension;

#[async_trait]
impl Extension for MyExtension {
    fn id(&self) -> &str { "com.example.my-ext" }
    fn version(&self) -> &str { "1.0.0" }
    fn name(&self) -> &str { "My Extension" }
    fn description(&self) -> &str { "Does something useful" }
    fn author(&self) -> &str { "Your Name" }
    fn api_version(&self) -> &str { "1.0.0" }
    fn capabilities(&self) -> Vec<ExtensionCapability> { vec![] }
    async fn on_load(&mut self, ctx: &ExtensionContext) -> Result<(), String> { Ok(()) }
    async fn on_unload(&mut self) -> Result<(), String> { Ok(()) }
}

qcker_extension!(MyExtension);
```

### Extension Manifest

```json
{
  "id": "com.example.my-ext",
  "name": "my-extension",
  "display_name": "My Extension",
  "version": "1.0.0",
  "api_version": "1.0.0",
  "author": "Your Name",
  "description": "What it does",
  "category": "network",
  "capabilities": ["NetworkAccess"],
  "repository": "https://github.com/user/repo",
  "license": "Apache-2.0"
}
```

## Capabilities

| Capability | Description |
|------------|-------------|
| `NetworkAccess` | Can make network connections |
| `FileSystemAccess` | Can read/write filesystem |
| `ContainerLifecycle` | Can manage containers |
| `ImageAccess` | Can read/write images |
| `Privileged` | Needs root access |
| `SystemInfo` | Can read system information |
| `RegistryAccess` | Can access registries |
| `ProcessSpawn` | Can spawn subprocesses |

## IPC Protocol

Extensions communicate via JSON-RPC 2.0 over Unix sockets.

### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "network.create",
  "params": { "name": "my-network", "driver": "bridge" }
}
```

### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": { "network_id": "abc123" }
}
```

## CLI Commands

```bash
qcker extension ls
qcker extension install /path/to/extension
qcker extension uninstall <id>
qcker extension enable <id>
qcker extension disable <id>
qcker extension info <id>
```
