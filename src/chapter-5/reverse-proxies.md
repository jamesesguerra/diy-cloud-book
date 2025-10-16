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

### Creating a Custom Nginx Image
Let’s start by creating a directory to keep our configuration file and Dockerfile organized.
```sh
mkdir nginx-proxy && cd nginx-proxy
```

Next, create the Nginx configuration file. Run `touch default.conf` then add the following content to it:

```nginx
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
    
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    location /notely-api/ {
        proxy_pass http://notely-api:8080/; 
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

There's quite a bit to unpack here. But let's start with the `server` block. This block defines a single HTTP server that listens for incoming traffic.
```conf
server {
    ...
}
```

Next, we specify which port the server listens on using the `listen` directives. In this configuration, it listens for HTTP traffic on port `80` for both IPv4 and IPv6.
```nginx
listen       80;
listen  [::]:80;
```

Next, we’ll keep the default `location` directives that come with Nginx. These directives define how requests to different paths are handled. Keeping them makes it easy to verify that Nginx is running properly. We’ll also keep the default error pages for now.

```nginx
 location / {
    root   /usr/share/nginx/html;
    index  index.html index.htm;
}

error_page   500 502 503 504  /50x.html;
location = /50x.html {
    root   /usr/share/nginx/html;
}
```

Finally, we add a `location` directive for our Notely API. 

This `location` directive tells Nginx to forward any requests that start with `/notely-api/` to the `notely-api` service running on port `8080`. Once again, we can take advantage of Docker’s built-in DNS capabilities, allowing us to refer to our API by its service name instead of using a hardcoded IP address.

Then the `proxy_set_header` lines ensure that important client and request information (such as the original host, IP address, and protocol) are passed along to our API service.

```nginx
location /notely-api/ {
    proxy_pass http://notely-api:8080/; 
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

### Creating the Dockerfile
Now that our custom Nginx configuration is ready, let’s create a Dockerfile for our image. This part is pretty straightforward. We’ll extend the base Nginx image and copy our custom configuration into it, effectively replacing the default one. First run `touch Dockerfile` and add the contents below:

```dockerfile
FROM nginx

WORKDIR /etc/nginx/conf.d

COPY default.conf .
```

> Tip: If you wanna minimize memory usage and don’t need convenience tools like `curl` or `vim` inside the container, use the Alpine-based images. They're much smaller and more memory efficient.

Next, build the new image by running the command below. Don’t forget to include your Docker Hub username (or any namespace you’re using) as the prefix.
```sh
docker build -t jamesesguerra025/nginx .
```

And push to Docker Hub:
```sh
docker push jamesesguerra025/nginx
```


