# homelab

This repo contains configuration for my homelab setup.
 
# Details

The moving parts of my homelab are documented below.

## Services
### [opnsense](https://opnsense.org)

Open source router and firewall platform. Auxillary configuration stored at [./opnsense](opnsense).

### docker01

* [portainer](https://portainer.io): Container dashboard to manage and monitor docker machines.

* [traefik](https://traefik.io): Reverse proxy.

* [grafana](https://grafana.com): Analytics and monitoring interface.
  * [prometheus](https://prometheus.io): Monitoring backend.
  * [node-exporter](https://github.com/prometheus/node_exporter): Hardware and OS metrics exporter.
  * [cadvisor](https://github.com/google/cadvisor): Container metrics aggregation.
  * [loki](https://grafana.com/oss/loki/): Logging backend.
  * [promtail](https://grafana.com/docs/loki/latest/clients/promtail/): Log exporter.

### docker02

* [portainer_agent](portainer/docker-compose.agent.yml): Agent container to remotely manage Docker host.

* Grafana Stack:
  * [node-exporter](https://github.com/prometheus/node_exporter): Hardware and OS metrics exporter.
  * [promtail](https://grafana.com/docs/loki/latest/clients/promtail/): Log exporter.

# Usage

The [bootstrap script](script/bootstrap) will install general services and setup the environment (zsh, vim, etc.). Tested on both amd64 and arm64 hosts.

## docker01

To copy all files needed to launch [docker01 services](dockerfile.docker01.yml) from Portainer, run [script/setup-docker01](script/setup-docker01).
Next, login to the host and run `cd /homelab/portainer && docker-compose up -d` to deploy Portainer.
Stacks can now be deployed remotely via the Portainer interface to docker01. Stacks need the following enviornment variables added in order to run properly:
* grafana-server
  * POSTGRES_USER
  * POSTGRES_PASSWORD
  * GRAFANA_SERVER_ROOT_URL
  * GRAFANA_GITHUB_CLIENT_ID
  * GRAFANA_GITHUB_CLIENT_SECRET
  * GRAFANA_GITHUB_ALLOWED_ORGS
  * GRAFANA_ADMIN_PASSWORD
* traefik
  * DOMAIN_DIRECTORY

## docker02

Run [script/setup-docker01](script/setup-docker01) to copy the portainer agent file. Then run `cd /homelab/portainer_agent && docker-compose up -d` to start the agent.
Add the agent via the Portainer server UI to deploy stacks remotely.