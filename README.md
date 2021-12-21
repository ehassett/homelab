# homelab

This repo contains configuration for my homelab setup.
 
# Details

The moving parts of my homelab are documented below.

## Services
### [opnsense](https://opnsense.org)

Open source router and firewall platform. Auxillary configuration stored at [./opnsense](opnsense).

### docker01

* [portainer](portainer): Container dashboard to manage and monitor docker machines. See [its README](portainer/README.md) for more info.

* [traefik](https://traefik.io): Reverse proxy.

# Usage

To copy all files needed to launch docker01 services from Portainer, run [script/bootstrap-docker01](script/bootstrap-docker01).
Next, login to the host and run `cd /homelab/portainer && docker-compose up -d` to deploy Portainer.