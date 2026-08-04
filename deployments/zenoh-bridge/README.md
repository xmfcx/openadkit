# Zenoh Bridge

Edge/cloud bridge for remote visualization and teleoperation.

**Guide (source of truth):**
[Zenoh Bridge docs](https://autowarefoundation.github.io/openadkit/deployments/demos/zenoh-bridge/)

```bash
cp .env.example .env   # set REMOTE_PASSWORD=
../../install.sh sample-data zenoh-bridge
./cloud.sh up -d
./edge.sh up -d
```

Visualizer: `https://localhost:6081/vnc.html`

**Warning:** TCP 7448 has no transport auth/TLS. Keep
`ZENOH_ROUTER_BIND_IP=127.0.0.1` for single-host; multi-host needs a private/VPN
bind and `CLOUD_IP` on the edge (see docs).
