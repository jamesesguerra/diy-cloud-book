# Setting expectations
Before we dive into the hands-on work of self-hosting, let’s establish what this book is (and isn’t). By the end, you’ll know exactly what you can expect to learn and what assumptions I’ll make about prior knowledge.

## What You Will Learn
This book is written for the budget-conscious developer who wants more control over their projects than free tiers allow, without breaking the bank. You’ll learn how to run as many pet projects as you need for the cost of a domain name and a mini PC or virtual machine.

Here’s what we’ll cover:
- **Choosing your hardware**  
    How to pick a mini PC or cloud VM that’s powerful enough to run your apps, but still cost-effective.
- **Securing your host**  
    Setting up firewalls, SSH, and basic hardening so you’re not leaving your front door open to the internet.
- **Owning your domain**  
    Walking through how to buy your own domain and why it’s worth it in the long run.
- **Cloudflare Tunnels**  
    How to create secure Cloudflare Tunnels and connect them to your mini PC or VM so you don’t need messy router port forwarding.
- **Running APIs and databases on Docker Swarm**
    - Writing Dockerfiles for your apps
    - Publishing your images to Docker Hub
    - Running your apps as Swarm services for easy scaling and resilience
    - We’ll focus on deploying .NET APIs, but the concepts are the same for Node.js, Python, or any other stack. Once you see the process, you’ll be able to replicate it for your language of choice.
- **Hosting frontends and connecting them to APIs**  
    Serving Angular, React, or any frontend alongside your backend services.
- **Essential Docker commands**  
    A small toolkit of the Docker commands you’ll use most often (nothing overwhelming).
- **Reverse proxies**  
    Using YARP or Nginx to route requests to the right service without exposing everything directly.
- **Monitoring and logging**  
    Adding just enough observability so you can quickly identify if something’s wrong, and which service is the culprit.

## What You Won’t Learn

Just as important as what we’ll cover is what this book won’t try to do.

- **Not a full Docker course**  
    I won’t re-teach Docker from scratch. If you’re already familiar with containers, even at a beginner level, you’ll be fine. If not, going through a beginner Docker course [^1] will give you the foundation you need.
- **Not a Linux command guide**  
   While you’ll inevitably touch the Linux terminal, this isn’t the place to master shell commands. There are far better resources [^2] for learning Linux.
- **Not networking basics**  
    Basic networking concepts (and Docker networking) aren’t covered here. While you can get by without them, not knowing the fundamentals can make troubleshooting frustrating.
- **Not enterprise-scale DevOps**  
    We’ll focus on lightweight, practical setups that work for indie developers, hobbyists, and small projects. This isn’t a Kubernetes handbook. We won't even be using Kubernetes, just Docker Swarm.
- **Not a security Bible**  
    We’ll implement reasonable security practices, but this isn’t a penetration testing or advanced ops book. Think “safe enough for personal projects,” not “hardened enterprise infrastructure.”

[^1]: [Complete Docker Course by DevOps Directive](https://www.youtube.com/watch?v=RqTEHSBrYFw)
[^2]: [Learn Linux - The Full Course by Boot dev](https://www.youtube.com/watch?v=v392lEyM29A)