# Deployments

A **deployment** is a running instance of Open AD Kit, a specific combination of Autoware components configured to achieve a particular task, such as a simulation or a full autonomous driving stack.

Runnable Compose assets live under `deployments/<name>/` in the repository.
Each directory has a short README that points here for the full guide.

Shared base services and env defaults: `deployments/base/` (`base.env` +
`docker-compose.yaml`). From a checkout, always pass both env files:

```bash
docker compose --env-file ../base/base.env --env-file <name>.env up -d
```

Fetch maps/rosbags with `./install.sh sample-data <name>` (see
[Getting Started](../getting-started/index.md)).

## Samples

Recommended for **learning and development**.

- [CARLA Simulation](samples/carla-simulation/index.md) — `deployments/carla-simulation/`
- [Planning Simulation](samples/planning-simulation/index.md) — `deployments/planning-simulation/`
- [Scenario Simulation](samples/scenario-simulation/index.md) — `deployments/scenario-simulation/`
- [Logging Simulation](samples/logging-simulation/index.md) — `deployments/logging-simulation/`

## Demos

Use-case specific topologies.

- [Zenoh Bridge](demos/zenoh-bridge/index.md) — `deployments/zenoh-bridge/` (edge/cloud remote viz + teleop)
