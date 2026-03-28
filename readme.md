# tidefly-caddy

Custom [Caddy](https://caddyserver.com) build for [Tidefly](https://github.com/tidefly-oss/tidefly) — includes plugins required for automatic HTTPS, TCP proxying, and rate limiting.

## Included Plugins

| Plugin                                                      | Purpose                                                                            |
|-------------------------------------------------------------|------------------------------------------------------------------------------------|
| [caddy-l4](https://github.com/mholt/caddy-l4)               | Layer 4 TCP/UDP proxy — used to expose databases (Postgres, Redis, MySQL) over TLS |
| [caddy-ratelimit](https://github.com/mholt/caddy-ratelimit) | Per-route rate limiting for deployed services                                      |

## Image

```
ghcr.io/tidefly-oss/tidefly-caddy:latest
```

## Usage

This image is used internally by Tidefly. The Caddy Admin API (`2019`) is configured entirely by the Tidefly backend — no Caddyfile needed.

## Building Locally

```bash
docker build -t tidefly-caddy:local .
docker run --rm tidefly-caddy:local caddy list-modules | grep -E "layer4|ratelimit"
```

## License

Apache 2.0 — same as Caddy.