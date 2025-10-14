# Docker Swarm

At this point, we’ve successfully deployed our apps using plain Docker commands (`docker run`) and `docker compose`. That’s already a big step toward having a working home cloud setup.

But now that we’ve got the basics down, we can pivot to something a little more advanced and a lot more reliable.

This next part is totally optional, but if you plan to run multiple services, update them safely, or scale beyond one container, you’ll definitely benefit from it. I'm talking about making the move from Docker Compose to Docker Swarm.

## Why Docker Swarm?
If you're not familiar with it yet, [Docker Swarm](https://docs.docker.com/engine/swarm/) is Docker's built-in orchestration tool. You can think of it as sort of like an upgrade from `docker compose`. Instead of just simply just running containers, it manages how they're deployed and what happens if something fails.

In Swarm mode, we’ll be using something called a Docker Stack. It’s very similar to your usual `docker-compose.yml` file, but with a few extra options for scaling, rolling updates, and secrets.
> From this point forward, we’ll be using docker stack deploy instead of docker compose up. The configuration syntax is almost the same, though a few fields behave slightly differently.

## The Benefits of Docker Swarm
### 1. Built-in load balancing
In Docker Compose, if you scale your app to multiple containers, you’ll usually need an external load balancer (like Nginx or Traefik) to distribute traffic between them.

Swarm does this for you automatically. So when you deploy a service with multiple replicas, it exposes it as one single endpoint and load balances requests across all replicas. This is made possible by Swarm’s overlay network, which connects containers across nodes and routes traffic between them through a built-in virtual network layer.

### 2. Blue-Green Deployments
This might not be a big deal if your app doesn't have much users yet, but it's still worth mentioning. Blue-green deployments let you roll out updates more safely through rolling updates. This makes it so that new containers are started before the old ones are stopped, allowing you to test and switch over smoothly. With blue-green setups, both versions can run side by side, and you can easily roll back to the previous one if something goes wrong.

### 3. Secrets Management
Up until now, we’ve hardcoded things like our database connection strings directly in the environment variables section. This obviously isn't good from a security standpoint, but I did this intentionally to show how we can address it with Docker Swarm secrets.

Basically, you can store credentials, API keys, and any other secret, securely in the Swarm cluster and just inject them into a container at runtime.

### 4. Automatic Rollbacks
If an update fails, Swarm can automatically rollback to the last working version. This is incredibly helpful when testing new features or making big changes to your deployment.



