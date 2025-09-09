# Installing Docker and Docker Swarm

## Docker
The reason why we're using Docker to run our apps is because it provides strong isolation between different runtimes. It’s also very quick to spin up and tear down containers. Furthermore, Docker is widely adopted, so you benefit from a huge ecosystem of images, documentation, and community support. If you have an app in mind that you wanna run, chances are there's a Docker container for it.

I followed this guide [^1] from the official Docker docs to set it up. Be sure to double-check that you're following the instructions for your distro.

1. Set up Docker's `apt` repository
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$UBUNTU_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

2. Install the Docker packages
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

3. Verify that the Docker installation is successful
```sh
 sudo docker run hello-world
```

4. Add the current user to the `docker` group to avoid having to use `sudo` when executing Docker commands
```sh
sudo usermod -aG docker $USER
```

5. Restart the PC if still not working.

6. Check Docker version (client and server), as well as Docker info
```sh
docker version
docker info
```

## Docker Swarm
Docker Swarm helps us overcome the limitations of running plain Docker containers. With it, we can:
- automate the container lifecycle
- scale instances up / down
- replace containers without downtime
- manage and access secrets

In short, Swarm is Docker’s built-in clustering solution. It’s beginner-friendly and easier to get started with than Kubernetes, though less feature-rich.

It isn’t enabled by default, so the first step is to initialize Swarm mode to create a single-node swarm:
```sh
docker swarm init
```

[^1]: [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)