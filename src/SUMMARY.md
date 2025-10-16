# Summary

# Introduction
- [What this book is about and who it's for](./chapter-1/what-this-book-is-about.md)
- [How the book is structured](./chapter-1/how-book-is-structured.md)
- [Setting expectations](./chapter-1/setting-expectations.md)

# Why Self-Host?
- [Public Cloud Pitfalls](./chapter-2/public-cloud-pitfalls.md)
- [Problems with free tiers](./chapter-2/problems-free-tiers.md)
- [Problems with "budget" DBs](./chapter-2/problems-budget-dbs.md)
- [My self-hosting journey](./chapter-2/my-journey.md)

# The Foundations
- [Choosing Your Self-Hosting Setup](./chapter-3/self-hosting-setup.md)
  - [Why a Mini PC for Self Hosting](./chapter-3/self-hosting-setup/mini-pc.md)
  - [Why VMs for Self Hosting](./chapter-3/self-hosting-setup/vm.md)
- [Choosing your hardware](./chapter-3/choosing-hardware.md)
- [Choosing your OS](./chapter-3/choosing-os.md)
- [Setting up your Server](./chapter-3/server-setup.md)
  - [Server Hardening](./chapter-3/server-setup/hardening.md)
  - [SSH](./chapter-3/server-setup/ssh.md)
  - [Installing Docker and Docker Swarm](./chapter-3/server-setup/docker.md)
- [Section Recap](./chapter-3/section-recap.md)

# Making It Public
- [Why not port-forward?](./chapter-4/no-port-forward.md)
- [Cloudflare Tunnels](./chapter-4/cloudflare-tunnels.md)
- [Setting up a Cloudflare account + Domain](./chapter-4/cloudflare-account-and-domain.md)
- [Creating a Cloudflare Tunnel](./chapter-4/cloudflare-tunnel-setup.md)
- [Section Recap](./chapter-4/section-recap.md)

# Hosting All the Things
- [Hello, Tunnel!](./chapter-5/hello-tunnel.md)
- [Introducing Our Sample App](./chapter-5/intro-sample-app.md)
- [Databases](./chapter-5/databases.md)
  - [Exposing for Local Access](./chapter-5/databases-local.md)
- [APIs](./chapter-5/apis.md)
- [Connecting Services with Docker Networking](./chapter-5/connecting-services.md)
- [Docker Swarm](./chapter-5/docker-swarm.md)
  - [Moving to Docker Swarm](./chapter-5/docker-swarm/moving-to-docker-swarm.md)
- [Reverse Proxies](./chapter-5/reverse-proxies.md)
  - [Using the Proxy](./chapter-5/reverse-proxies/using-the-proxy.md)
- [Object Storage](./chapter-5/object-storage.md)

# Developer’s Playground
- [Deploying pet projects](./chapter-6/deploying-pet-projects.md)
  - [CI/CD with GitHub Actions](./chapter-6/ci-cd-github-actions.md)
  - [Automating updates in Docker Swarm](./chapter-6/auto-updates-swarm.md)
  - [Hosting frontends on Vercel](./chapter-6/vercel-frontends.md)
- [Dev & prod connections](./chapter-6/dev-prod-connections.md)
- [Backups with rclone](./chapter-6/backups-rclone.md)

# Beyond the Basics
- [Monitoring and logging](./chapter-7/monitoring-logging.md)
- [Caching](./chapter-7/caching.md)
- [What else to host?](./chapter-7/what-else-to-host.md)

# Wrapping Up
- [Cost breakdown](./chapter-8/cost-breakdown.md)
- [Troubleshooting checklist](./chapter-8/troubleshooting.md)
- [Templates and config](./chapter-8/templates-config.md)
- [Links for further learning](./chapter-8/further-learning.md)
