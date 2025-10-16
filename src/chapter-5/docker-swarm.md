# Docker Swarm

At this point, we’ve successfully deployed our apps using plain Docker commands (`docker run`) and `docker compose`. That’s already a big step toward having a working home cloud setup.

But now that we’ve got the basics down, we can pivot to something a little more advanced and a lot more reliable.

This next part is totally optional, but if you plan to run multiple services, update them safely, or scale beyond one container, you’ll definitely benefit from it. I'm talking about making the move from Docker Compose to Docker Swarm.

## Why Docker Swarm?
If you're not familiar with it yet, [Docker Swarm](https://docs.docker.com/engine/swarm/) is Docker's built-in orchestration tool. You can think of it as sort of like an upgrade from `docker compose`. Instead of just simply just running containers, it manages how they're deployed and what happens if something fails.

In Swarm mode, we’ll be using something called a Docker Stack. It’s very similar to your usual `docker-compose.yml` file, but with a few extra options for scaling, rolling updates, and secrets.
> From this point forward, we’ll be using docker stack deploy instead of docker compose up. The configuration syntax is almost the same, though a few fields behave slightly differently. If you plan to stick with Compose, things might not work as expected if you reuse my Swarm configurations as-is.

## The Benefits of Docker Swarm
### 1. Cluster-Wide Replication
If needed, you can replicate container instances to achieve horizontal scaling. While Compose supports scaling as well, it only works on a single host. The advantage of Swarm replication is that it distributes replicas across multiple nodes, even on different machines. This provides better availability and reliability with no single point of failure. This might be overkill for smaller projects, but it’s still worth setting up for the added resilience if your memory allows it.

### 2. Built-in load balancing with replicas
In Docker Compose, if you scale your app to multiple containers, you’ll usually need an external load balancer (like Nginx or Traefik) to distribute traffic between them.

Swarm does this for you automatically. So when you deploy a service with multiple replicas, it exposes it as one single endpoint and load balances requests across all replicas. This is made possible by Swarm’s overlay network, which connects containers across nodes and routes traffic between them through a built-in virtual network layer.

### 3. Self-Healing
Another powerful feature of Swarm is its ability to automatically recover from container failures. You can configure how Swarm should respond when a container exits unexpectedly using a restart policy. 

### 4. Blue-Green Deployments
This might not be a big deal if your app doesn't have much users yet, but it's still worth mentioning. Blue-green deployments let you roll out updates more safely through rolling updates. This makes it so that new containers are started before the old ones are stopped, allowing you to test and switch over smoothly. With blue-green setups, both versions can run side by side, and you can easily roll back to the previous one if something goes wrong.

### 5. Secrets Management
Up until now, we’ve hardcoded things like our database connection strings directly in the environment variables section. This obviously isn't good from a security standpoint, but I did this intentionally to show how we can address it with Docker Swarm secrets.

Basically, you can store credentials, API keys, and any other secret, securely in the Swarm cluster and just inject them into a container at runtime.

### 6. Automatic Rollbacks
If an update fails, Swarm can automatically rollback to the last working version. This is incredibly helpful when testing new features or making big changes to your deployment.

## Why Not Kubernetes?
You’ve probably heard of Kubernetes. Everyone has. Yes, it’s way more powerful and has more features than Docker Swarm. But for most pet projects or small self-hosted apps, it’s complete overkill. In fact, you probably don’t even need Swarm. Docker Compose alone is often more than enough.

That said, I still think Swarm is worth adding because of how easy it is to set up. You get simple scaling, load balancing, and self-healing, all with a simple command and without the steep learning curve that comes with Kubernetes.

Kubernetes definitely has its place in large-scale or enterprise environments where teams manage complex, distributed systems. But for personal or small-scale deployments, it’s a whole 'nother beast that’ll just slow us down from getting our projects up and running quickly.

