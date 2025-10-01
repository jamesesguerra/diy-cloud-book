# Connecting Services with Docker Networking

Now that we have the API container up and running, let’s try calling an endpoint that connects to our database service.

Instead of a successful response, we get an error. When we check the logs of the API container with the docker logs command, we can see that it’s unable to connect to the database service.
```sh
docker logs notely-api
```

At this point, beginners might be stumped: *Why did this work when we were running the API locally, but not now that it’s inside a container?*

The reason is that when we ran the .NET API directly on our machine, it could access the database on `localhost` because both processes were *technically* on the same network. I say "technically" because the `cloudflared` process on our machine was just proxying requests to the actual database process running on our VPS. 

However, once we containerized the API, it now runs inside its own isolated Docker network. Inside the container, `localhost` refers to the container itself, not the host machine where the database is running. Don't worry if this sounds confusing at first, this still trips me up to this day :).

There are two ways around this:

1. The quick hack – use `host.docker.internal` instead of localhost to reference the host machine’s network from inside the container

2. The proper solution (what we’ll use) – run the API container in the same custom Docker network as the database service. This way, the API can reach the database directly using its service name, taking advantage of Docker’s built-in DNS and networking features

