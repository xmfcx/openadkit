# Zenoh Bridge

Bridges Autoware data from edge to cloud for remote visualization and
teleoperation. Checkout assets live under `deployments/zenoh-bridge/`.

## Security

- noVNC is loopback-bound; set `REMOTE_PASSWORD` in `.env` (required).
- Zenoh TCP **7448 has no transport auth/TLS**. Default bind is `127.0.0.1`.
  For multi-host, bind an exact VPN/private address only and restrict peers.
- Control topics (engage, emergency, teleop cmd) are on the allow-list — treat
  7448 as a vehicle-control plane.

## Setup

```bash
cd deployments/zenoh-bridge
cp .env.example .env
# set REMOTE_PASSWORD=
../../install.sh sample-data zenoh-bridge
```

## Single-host (split topology)

```bash
./cloud.sh up -d
./edge.sh up -d
```

Visualizer: `https://localhost:6081/vnc.html`

## Multi-host

1. **Cloud** — set `ZENOH_ROUTER_BIND_IP` to a private/VPN address in `.env`, then:

```bash
./cloud.sh up -d
```

2. **Edge** — point at the cloud:

```bash
export CLOUD_IP=<cloud-private-ip>
./edge.sh up -d
```

`CLOUD_IP` selects the Zenoh endpoint the edge bridge dials
(`tcp/${CLOUD_IP}:7448`).

## Teleoperation

```bash
./cloud.sh up --with-teleop -d
./edge.sh --no-sim -d   # or default with sim
./run_teleop.sh
```

| Key | Function |
| --- | --- |
| W/S | Throttle / Brake |
| A/D | Steer left / right |
| Z | Toggle Auto/Local control mode |
| M | Cycle STOP → PHYSICS → CRUISE |
| X/C/V | Gear D / R / P |
| Space | Emergency stop / resume |
| R | Reset pose |
| Q | Quit |

## Stop

```bash
./edge.sh down
./cloud.sh down
```

## Notes

- Prefer `./cloud.sh` / `./edge.sh` over raw `docker compose up` (flag allowlists,
  bind guards).
- Map files must exist under `MAP_PATH` before `edge.sh` starts.
