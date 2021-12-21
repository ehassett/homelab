# portainer

This is sectioned off as it is deployed before anything else. Portainer is then used to deploy docker-compose stacks on the appropriate hosts via source control.

* [server](docker-compose.server.yml): Deploys the Portainer server and creates the `homelab` network.

* [agent](docker-compose.agent.yml): Deploys the Portainer agent and creates the `homelab` network.