# Changelog

## [2.0.1](https://github.com/dkarter/mcp-proxy/compare/v2.0.0...v2.0.1) (2026-11-23)


### Bug Fixes

* **ci:** let Release Please own release notes ([#2](https://github.com/dkarter/mcp-proxy/issues/2)) ([1ebfecd](https://github.com/dkarter/mcp-proxy/commit/1ebfecd3af66ac560d73139ca3bbf5344a9aa16a))

## [2.0.0](https://github.com/dkarter/mcp-proxy/compare/v1.1.4...v2.0.0) (2026-11-23)


### ⚠ BREAKING CHANGES

* **config:** default to streamable-http on both sides

### Features

* add resourceFilter and promptFilter ([0e7f52e](https://github.com/dkarter/mcp-proxy/commit/0e7f52e34061703706c20ea3ad720da15d0f832d))
* **client:** refresh the proxied catalog when a downstream's lists change ([bfebef9](https://github.com/dkarter/mcp-proxy/commit/bfebef9dc88293cbc1cc9b8c3dc3d5bbcabcff9f))
* **config:** default to streamable-http on both sides ([cac0401](https://github.com/dkarter/mcp-proxy/commit/cac0401218eb87034b2d49fbab1c800a22f15988))
* **config:** inherit toolFilter from proxy options, reject empty allow lists and proxy-level disabled ([e84c5f7](https://github.com/dkarter/mcp-proxy/commit/e84c5f7ec5fa210ab086631aef8095e44d44de86))
* **oauth:** add callbackListen for authorizing behind a reverse proxy ([424c082](https://github.com/dkarter/mcp-proxy/commit/424c0828f258c40ca358e08ee9e518fa1b6fe1f3))


### Bug Fixes

* **client:** always run keepalive, stop advertising unimplemented capabilities, log tool errors at WARN ([6370f86](https://github.com/dkarter/mcp-proxy/commit/6370f86fd8ae8b42e9e4ec45960e01500d7d34b6))
* **client:** do not forward per-connection _meta fields downstream ([c84d36b](https://github.com/dkarter/mcp-proxy/commit/c84d36b5ef29feffd39e71c01fc7fa92cbc9fdd1))
* **client:** forward instructions only on first connect to avoid racing initialize ([bfef416](https://github.com/dkarter/mcp-proxy/commit/bfef416873e5caf9f70d4a4abc78fef3a0b408ce))
* **http:** accept the baseURL host behind a same-host reverse proxy ([9f5f4de](https://github.com/dkarter/mcp-proxy/commit/9f5f4deda58733604d2fadab4072d0eabf9a54a3))
* **http:** avoid double client close, build server before client, send proxy version ([6048ef3](https://github.com/dkarter/mcp-proxy/commit/6048ef37a8bc4973280cab338118ddda8d6fb1d5))
* **oauth:** register a new client when redirectUri has changed ([13882e6](https://github.com/dkarter/mcp-proxy/commit/13882e6896be34ed7717e889255d371aa869a8bb))
* **oauth:** save a replacement client only after its token is issued ([4525ba4](https://github.com/dkarter/mcp-proxy/commit/4525ba4251887b646abd329b0952178d9d8e725a))
* sync upstream v1.6.0 and harden build inputs ([324c0b7](https://github.com/dkarter/mcp-proxy/commit/324c0b753799d8f66623e16b455e435bc48eb5dd))
