# Contributing to Qcker Extensions

## How to Add Your Extension

### Step 1: Create Extension

Create a directory in `extensions/`:

```
extensions/my-extension/
├── manifest.json
├── README.md
└── (source files or compiled binary)
```

### Step 2: Write manifest.json

```json
{
  "id": "com.qcker.ext.my-extension",
  "name": "my-extension",
  "display_name": "My Extension",
  "version": "1.0.0",
  "api_version": "1.0.0",
  "author": "Your Name",
  "description": "What it does",
  "category": "network",
  "built_in": false,
  "source": "https://github.com/your/repo",
  "license": "Apache-2.0",
  "capabilities": ["NetworkAccess"]
}
```

### Step 3: Write README.md

Document:
- What the extension does
- How to install
- How to use
- Configuration options

### Step 4: Submit Pull Request

1. Fork the repository
2. Create branch: `git checkout -b add-my-extension`
3. Commit changes
4. Submit PR with description

### Step 5: Review Process

- Maintainers review the PR
- Security audit of extension code
- Test against Qcker
- Merge and publish to marketplace

## Extension Development

### Using Rust

```rust
use qcker_ext_api::prelude::*;

#[derive(Default)]
struct MyExtension;

impl Extension for MyExtension {
    fn id(&self) -> &str { "com.qcker.ext.my-extension" }
    fn version(&self) -> &str { "1.0.0" }
    fn name(&self) -> &str { "My Extension" }
    fn description(&self) -> &str { "Does something" }
    fn author(&self) -> &str { "Me" }
    fn api_version(&self) -> &str { "1.0.0" }
    fn capabilities(&self) -> Vec<ExtensionCapability> { vec![] }
    fn on_load(&mut self, ctx: &ExtensionContext) -> Result<()> { Ok(()) }
    fn on_unload(&mut self) -> Result<()> { Ok(()) }
}

qcker_extension!(MyExtension);
```

### Using Other Languages

Extensions can be written in any language that supports:
1. Unix socket communication
2. JSON-RPC protocol

The extension listens on a Unix socket and handles JSON-RPC messages from Qcker.

## Code of Conduct

- Be respectful
- Be constructive
- Follow the license

## Questions?

Open an issue or join the discussion.
