# Reverse Proxies
Before we move on to hosting more services, let’s address the elephant in the room. You’re probably thinking about how inconvenient it is to keep going back to the Cloudflare dashboard to publish an application route for every new service. It *is* tedious, but I wanted us to go through that process first so we can appreciate just how useful reverse proxies are.

If you’re not familiar with what a [reverse proxy](https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy/) is (or even a regular proxy), the ELI5 version is that it’s a service that receives requests on behalf of another service and forwards them to the right destination. It might not sound all that impressive at first, but reverse proxies offer plenty of benefits, especially in terms of load-balancing, caching, and security.

There are plenty of reasons to use a reverse proxy, but in our case, we’re doing it so we only need to publish one application route on the Cloudflare dashboard. That single route will forward requests to our reverse proxy, which can then decide, based on the URL path, which service in our Docker network to send them to.

## Why Nginx?
For our reverse proxy, I’m choosing to use Nginx. It’s one of if not the most popular technologies that can act as a web server, reverse proxy, load balancer, and content cache all at once. It’s been around for years, with tons of documentation and tutorials available online.

Nginx is also very lightweight in terms of memory usage and achieves high performance through its event-driven, multi-threaded architecture. Sure, there are newer and trendier options out there like [Traefik](https://traefik.io/traefik) and [Caddy](https://caddyserver.com/), but we’ll keep things simple. Nginx is reliable, widely supported, and there’s a very good chance you’ll encounter it in the real world too.

## Setting Up Nginx as a Reverse Proxy
We've already seen how to run Nginx in [Hello, Tunnel!](./hello-tunnel.md). However, running it out of the box like that just makes it a basic web server that serves static files. We’ll need to add a bit more configuration to turn it into a proper reverse proxy.

Nginx is configured by editing its configuration files. To customize them, we have two options:
- **Option 1:** Build a custom Nginx image with our configuration file baked in and mounted. This way, when we run the container, it’s already using our custom setup
- **Option 2:** Run the base Nginx image, enter the container, manually update the configuration file, and restart the Nginx daemon

Between the two, the first option is much more maintainable in the long run, and that’s what we’ll be using. But I have to mention that the second option is still handy when you just want to test configuration changes quickly.



