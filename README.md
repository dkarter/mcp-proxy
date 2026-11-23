# MCP Proxy Server

An MCP proxy that aggregates multiple MCP servers behind a single HTTP entrypoint.

## dkarter fork

This fork retains a regression test for GitHub MCP Server 2.x tool catalogs
with array-valued output schema types, now supported upstream. Release
archives retain the upstream `mcp-proxy` executable name.

Releases from v1.1.4 are immutable and include SHA-256 checksums signed with
keyless Cosign and GitHub build-provenance attestations for each archive.
Release Please opens a version and changelog PR from Conventional Commits.
The repository must allow GitHub Actions to create pull requests and have
immutable releases enabled.
Merging it into `master` builds, signs, and attests the archives before
publishing the draft. If a run leaves a draft behind, run the **Release**
workflow on that release tag to resume publishing:

```sh
gh workflow run goreleaser.yml --ref vX.Y.Z
```

For v1.1.4, download your archive,
`checksums.txt`, and `checksums.txt.sigstore.json` from
<https://github.com/dkarter/mcp-proxy/releases/tag/v1.1.4>, then verify:

```sh
cosign verify-blob \
  --certificate-identity 'https://github.com/dkarter/mcp-proxy/.github/workflows/goreleaser.yml@refs/tags/v1.1.4' \
  --certificate-oidc-issuer 'https://token.actions.githubusercontent.com' \
  --bundle checksums.txt.sigstore.json checksums.txt

# Replace the archive name with the one you downloaded.
gh attestation verify mcp-proxy_1.1.4_darwin_arm64.tar.gz --repo dkarter/mcp-proxy

# Check the archive against the verified checksum file (GNU coreutils).
sha256sum --check --ignore-missing checksums.txt
```

For newer releases, substitute the release tag in the Cosign certificate
identity.

Existing downstream OAuth credentials without issuer metadata may require a
one-time reauthorization after this upgrade. Do not disable issuer validation.

## Features

- Proxy multiple MCP clients: aggregate tools, prompts, and resources from many servers.
- SSE and streamable HTTP: serve via Server‑Sent Events or streamable HTTP.
- Flexible config: supports `stdio`, `sse`, and `streamable-http` client types.
- OAuth client support: authorize once against downstream servers that require interactive OAuth (e.g. Notion), then let the proxy hold and refresh the token for every caller.

## Documentation

- Configuration: [docs/CONFIGURATION.md](docs/CONFIGURATION.md)
- Usage: [docs/USAGE.md](docs/USAGE.md)
- Deployment: [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)
- Claude config converter: https://tbxark.github.io/mcp-proxy

## Quick Start

### Build from source

```bash
git clone https://github.com/tbxark/mcp-proxy.git
cd mcp-proxy
make build
./build/mcp-proxy --config path/to/config.json
```

### Install via Go

```bash
go install github.com/tbxark/mcp-proxy@latest
```

### Docker

The image includes support for launching MCP servers via `npx` and `uvx`.

```bash
docker run -d -p 9090:9090 -v /path/to/config.json:/config/config.json ghcr.io/tbxark/mcp-proxy:latest
# or provide a remote config
docker run -d -p 9090:9090 ghcr.io/tbxark/mcp-proxy:latest --config https://example.com/config.json
```

More deployment options (including docker‑compose) are in [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md).

## Configuration

See full configuration reference and examples in [docs/CONFIGURATION.md](docs/CONFIGURATION.md).
An online Claude config converter is available at: https://tbxark.github.io/mcp-proxy


## Usage

Command‑line flags, endpoints, and auth examples are documented in [docs/USAGE.md](docs/USAGE.md).

## Contributing

Examples for individual third-party or commercial MCP services are not accepted; generic examples live in [docs/CONFIGURATION.md](docs/CONFIGURATION.md).

## Thanks

- This project was inspired by the [adamwattis/mcp-proxy-server](https://github.com/adamwattis/mcp-proxy-server) project
- If you have any questions about deployment, you can refer to  [《在 Docker 沙箱中运行 MCP Server》](https://miantiao.me/posts/guide-to-running-mcp-server-in-a-sandbox/)([@ccbikai](https://github.com/ccbikai))

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
