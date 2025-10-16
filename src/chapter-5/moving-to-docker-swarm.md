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

After that, we can make our Stack file compliant with the standard format. The only section we need to update is ports, since Stack files use a different syntax.

So intead of:
```yml
ports:
  - "5432:5432"
```

We write:
```yml
  ports:
    - target: 5432
      published: 5432
      protocol: tcp
      mode: host
```

This is because Stack deployments require explicit definitions for each port mapping, including the target, published port, protocol, and mode.

To test it out, we can now deploy the stack using the following command. In this case, `home` is the name of the stack:

```sh
docker stack deploy -c docker-stack.yml home
```

