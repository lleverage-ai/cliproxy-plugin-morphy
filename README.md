# Morphy CLIProxyAPI plugin

Public registry and immutable release assets for the [Morphy](https://github.com/lleverage-ai/morphy) CLIProxyAPI plugin.

## Add this store source

Morphy is third-party in CLIProxyAPI. Review the source and release details before accepting the Management Center confirmation prompt. For a self-hosted CLIProxyAPI instance, add the raw registry URL and enable plugins globally:

```yaml
plugins:
  enabled: true
  store-sources:
    - "https://raw.githubusercontent.com/lleverage-ai/cliproxy-plugin-morphy/main/registry.json"
```

The built-in official source remains enabled. Install `morphy` from the plugin store after reloading this configuration. Store installation selects the host platform asset, verifies its SHA-256 entry from `checksums.txt`, writes the versioned library and plugin configuration, and asks the running host to load it.

Supported release platforms:

- Linux x86-64 (`linux/amd64`), GNU libc 2.17 or newer
- Linux ARM64 (`linux/arm64`), GNU libc 2.17 or newer
- macOS x86-64 (`darwin/amd64`)
- macOS Apple silicon (`darwin/arm64`)
- Windows x86-64 (`windows/amd64`)

## Safety and current scope

CLIProxyAPI plugins are trusted native libraries loaded in process. Only install assets you trust. Morphy is mandatory fail-open: malformed input, unsupported formats, compression errors, and panics leave the request body unchanged; a configuration that sets `fail_open: false` is rejected while the prior configuration remains active. Authentication headers and credentials are not exposed to the plugin request-interceptor payload.

Version 0.3.1 has a conservative subscription-auth posture because the current host metadata identifies the selected credential but not its authentication kind. Codex-format requests are passed through unchanged. Model-backed and embedding-heavy features are disabled: semantic cache is off, embeddings use the non-downloading hash backend, LLMLingua is off, and ACON uses its heuristic compressor.

## Release contract

The registry version has no leading `v`. Release tags are immutable `v<semver>` tags. The release contract for version `0.3.1` is tag `v0.3.1` with exactly:

- `morphy_0.3.1_linux_amd64.zip`
- `morphy_0.3.1_linux_arm64.zip`
- `morphy_0.3.1_darwin_amd64.zip`
- `morphy_0.3.1_darwin_arm64.zip`
- `morphy_0.3.1_windows_amd64.zip`
- `checksums.txt`

Each ZIP contains one platform library at its root (`morphy.so`, `morphy.dylib`, or `morphy.dll`). `checksums.txt` contains sorted SHA-256 entries for all five ZIPs.
