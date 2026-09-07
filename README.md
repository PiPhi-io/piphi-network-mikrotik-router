# Piphi Network Mikrotik Router

Generated PiPhi integration runtime.

## Run locally

```bash
pdm install -G dev
pdm run uvicorn piphi_network_mikrotik_router.main:app --reload --port 4218
pdm run pytest
pdm run python scripts/validate.py
```

The runtime listens on port `4218` by default and exposes the common PiPhi runtime route contract:

- `GET /health`
- `GET /diagnostics`
- `POST /discover`
- `POST /config`
- `POST /config/sync`
- `POST /deconfigure`
- `POST /deconfigure/{config_id}`
- `GET /state`
- `GET /contract`
- `GET /entities`
- `GET /events`
- `POST /events/device/{config_id}/example`
- `POST /telemetry/example`
- `POST /telemetry/device/{config_id}/example`
- `POST /command`

## Capability coverage

`capability-catalog.json` inventories the reviewed RouterOS system health,
interfaces, traffic, clients, DHCP, wireless, LTE, routing, firewall, VPN,
services, logs, maintenance, and administrative boundaries. Every entry is
classified as implemented, planned, or excluded, and contract tests ensure
that only implemented entries are advertised.

Router monitoring remains planned until secure API transport, least-privilege
permissions, RouterOS/version fixtures, counter normalization, redaction, and
transition tests exist. Arbitrary console, REST, and configuration mutation is
explicitly excluded. The starter runtime exposes only connectivity and refresh.

## Manifest

`manifest.json` is a starter manifest. Before publishing, update:

- `image`
- `version`
- capabilities and commands
- config fields and identity fields
- entity metadata

## Docker

```bash
docker build -t docker.io/piphinetwork/piphi-network-mikrotik-router:0.1.0 .
docker run --rm -p 4218:4218 docker.io/piphinetwork/piphi-network-mikrotik-router:0.1.0
```
