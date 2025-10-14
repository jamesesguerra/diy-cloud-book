# Connecting Services with Docker Networking

Now that we have the API container up and running, let’s try calling an endpoint that connects to our database service.

```sh
curl https://tunnel.james-esg.com/notely-api/notes
```

Instead of a successful response, we get an error. When we check the logs of the API container with the docker logs command, we can see that it’s unable to connect to the database service.
```sh
docker logs notely-api
```

At this point, beginners might be stumped: *Why did this work when we were running the API locally, but not now that it’s inside a container?*

The reason is that when we ran the .NET API directly on our machine, it could access the database on `localhost` because both processes were *technically* on the same network. I say "technically" because the `cloudflared` process on our machine was just proxying requests to the actual database process running on our VPS. 

However, once we containerized the API, it now runs inside its own isolated Docker network. Inside the container, `localhost` refers to the container itself, not the host machine where the database is running. Don't worry if this sounds confusing at first, this still trips me up to this day :).

There are two ways around this:

1. The quick hack – use `host.docker.internal` instead of localhost to reference the host machine’s network from inside the container

2. The better solution (what we’ll use) – run the API container in the same custom Docker network as the database service. This way, the API can reach the database directly using its service name, taking advantage of Docker’s built-in DNS and networking features

To do this solution, we'll need to create a new Docker network since the default bridge network doesn't have this DNS superpower. This command creates a network called `home` using the default `bridge` driver.

```sh
docker network create home 
```

Once we have our new network created, the first thing we can do is use the service name of our DB in place of `localhost` in our database connection string. And build a new image after making this edit.

```json
"ConnectionStrings": {
    "DefaultConnection": "Host=db;Port=5432;Database=postgres;Username=postgres;Password=postgres"
}
```

Next, we need to have both our database service and our API service to run in our `home` Docker network.

To do that, we can just add our API service to the Compose file we made earlier for our DB service. They can be in separate Compose files if you want, but I generally like to have all services in the same network inside the same file.

We then add a `networks` section and tell Docker that we want the services to be in our `home` network. We say `external: true` because we want Docker to know that we've already created a Docker network called `home` and so it won't make a new one.

```yml
services:
  db:
    image: postgres
    restart: always
    shm_size: 128mb
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    ports:
      - "5432:5432"
    networks:
      - home

  notely-api:
    image: jamesesguerra025/notely-api
    restart: always
    ports:
      - "8080:8080"
    networks:
      - home

networks:
  home:
    external: true
```

Now we can run `docker compose up -d` once again to spin up the services. If all goes well, the API should now be able to communicate with the DB service.

A quick way to check this is by running `docker logs` on the API container. If there are no exceptions indicating that it couldn’t connect to the database, that means it’s successfully communicating through the Docker network as expected.

To fully verify, we can run curl `localhost:8080/notes` or `https://tunnel.james-esg.com/notely-api/notes`, which should return the list of note records.



