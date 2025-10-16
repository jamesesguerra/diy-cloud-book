# Moving to Docker Swarm

Now that we're aware of the advantages of Swarm, let’s migrate our Compose setup to Swarm step by step. In each step, we’ll take advantage of Swarm’s features while adapting our existing configuration.

## Making the Compose File Swarm-Ready
Before we can deploy our stack, we need to make our current Compose file Swarm-compliant.
Start by renaming your existing Compose file to something more appropriate for stacks:

```sh
mv docker-compose.yml docker-stack.yml
```

Next, we’ll need to recreate the home network that we originally set up in [Connecting Services with Docker Networking](./connecting-services.md). This is because it used the default `bridge` driver. However, Swarm requires an overlay driver to enable multi-host networking across nodes.

Run the following commands to remove the old network and create a new one for Swarm:
### 
```sh
docker network rm home
docker network create --driver overlay home
```