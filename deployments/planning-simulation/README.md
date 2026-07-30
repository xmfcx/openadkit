# Planning Simulation

Runs the Autoware planning and control stack with a pre-recorded point cloud
map. See the [deployment documentation](https://autowarefoundation.github.io/openadkit/deployments/samples/planning-simulation/)
for configuration and troubleshooting.

## Source Checkout

```bash
../../install.sh sample-data planning-simulation
docker compose --env-file ../base/base.env --env-file planning-simulation.env up -d
```
