# Logging Simulation

Runs sensing, perception, and localization against a sample rosbag. Checkout
assets live under `deployments/logging-simulation/`.

## Prerequisites

- Host setup via [`install.sh`](../../../getting-started/index.md)
- Autoware artifacts (models under `~/autoware_data`):

```bash
sudo ./install.sh --download-artifacts
```

- Sample map and rosbag:

```bash
./install.sh sample-data logging-simulation
```

## Run (CPU)

```bash
cd deployments/logging-simulation
docker compose \
  --env-file ../base/base.env \
  --env-file logging-simulation.env \
  up -d
```

Play the rosbag (separate profile):

```bash
docker compose \
  --env-file ../base/base.env \
  --env-file logging-simulation.env \
  --profile rosbag \
  up -d rosbag
```

## Run (GPU)

Requires the NVIDIA Container Toolkit. Overlay GPU settings for sensing and
perception:

```bash
cd deployments/logging-simulation
docker compose \
  --env-file ../base/base.env \
  --env-file logging-simulation.env \
  --env-file logging-simulation.gpu.env \
  -f docker-compose.yaml \
  -f docker-compose.gpu.yaml \
  up -d
```

## Visualizer

Open `https://localhost:6080/vnc.html` and use `REMOTE_PASSWORD` from
`deployments/base/base.env`.

## Stop

```bash
cd deployments/logging-simulation
docker compose \
  --env-file ../base/base.env \
  --env-file logging-simulation.env \
  --profile rosbag \
  down
```

## Notes

- The sample rosbag has no camera images (privacy); traffic-light recognition
  and full object detection accuracy are limited.
- Always pass **both** base and deployment env files.
