# How the book is structured
This introduction is all about explaining how the book is structured so you can skip to a specific chapter if you like. But if you're starting from almost 0 knowledge it's best to follow the book from cover-to-cover.

**Why Self-Host?** explores why self-hosting can be a better long-term choice compared to free tiers or budget databases, highlighting issues like expiring trials, poor regional network latency, and hidden costs. It also shares my personal journey of turning a mini PC into a reliable home “cloud” using tools like Cloudflare Tunnels and Nginx Proxy Manager to host my pet projects and other self-hosted services.

**The Foundations** lays the groundwork, covering hardware choices such as mini PCs, old laptops, or cloud VMs, along with essential security practices like firewalls. It walks through setting up a Linux OS, installing Docker and Docker Swarm, and introducing basic networking concepts to prepare for hosting.

**Making It Public** focuses on making services publicly accessible without risky port-forwarding. It explains how Cloudflare Tunnels work, guides you through creating an account, configuring DNS, and securing traffic with free SSL certificates.

**Hosting All the Things** dives into hosting applications and databases. It covers how to connect to databases locally, host APIs via Docker Swarm services, set up reverse proxies with Nginx or YARP, and scale workloads until you fully utilize your CPU.

**Developer's Playground** turns the setup into a developer’s playground, showing how to deploy pet projects with Dockerfiles, push them to Docker Hub, and automate service updates. It also includes hosting frontends on GitHub Pages, configuring dev and prod connections, and setting up backups with tools like rclone.

**Beyond the Basics** goes beyond the basics with monitoring and logging using Grafana and Prometheus, as well as exploring additional services you might want to self-host once your foundation is solid.

**Wrapping Up** wraps everything up with a cost breakdown to show the savings, a troubleshooting checklist for common pitfalls, and a collection of templates, configs, and links for further learning.
