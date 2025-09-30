# Setting up a Cloudflare account + Domain

## Why Cloudflare?
First, I have to mention why I chose to register my domain with Cloudflare. It's mainly because it gives me free, automatic HTTPS out of the box. That means the moment I map a service to my domain, Cloudflare issues and manages SSL/TLS certificates for me, with no manual setup or renewal required. For a DIY setup where I can't be bothered fiddling with Let’s Encrypt or OpenSSL configuration, this is a huge win (yes, there are tools to make it easier, but nothing beats doing nothing). Managing your own certificates and dealing with HTTPS in general can quickly become a headache and a roadblock for beginners.

Another advantage is that since we’ll be using Cloudflare Tunnels, registering the domain with Cloudflare simplifies everything. All configuration changes can be handled from a single dashboard, reducing context-switching and making management much smoother.

## Cloudflare Account
Before we set up a Cloudflare Tunnel, we first need a Cloudflare account. You can create an account for free on the [Cloudflare website](https://www.cloudflare.com/).

Once you have and account and are signed in, head on over to the [Cloudflare Dashboard](https://dash.cloudflare.com) if not already opened.

## Registering a Domain
The first thing we need is a domain. This might be the only thing you’ll actually be spending on if you’re using a mini PC to self-host. And yes, it’s mandatory. We need our own domain that our apps and other people can use to access our services. You register it with a DNS provider like Cloudflare so you can point it to a specific IP address or another domain. Think of it as giving your server a recognizable name that anyone on the internet can use.

You can use this domain for other things, such as pointing it to Vercel's servers if you're hosting your portfolio there. But in our case, we need it so that we have a name that we can use to connect to the Cloudflare tunnel we will be making in the next chapter.




