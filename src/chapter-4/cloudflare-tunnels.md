# Cloudflare Tunnels
Cloudflare Tunnels let you securely connect your home server to the internet without ever exposing it directly. Instead of opening up ports on your router, your server creates an outbound, encrypted connection to Cloudflare’s global network. Once that tunnel is established, Cloudflare handles all the incoming traffic for you and routes it safely back to your server.

And because the connection is outbound, there’s no need for risky port-forwarding or complex router setups. This completely sidesteps the problems of attack surface, brute-force attempts, and even ISP restrictions like CGNAT. In short, you can make your local services publicly available while keeping your home network safe.

For more information (and I highly encourage you to read their docs), you may refer to their documentation [^1]. Cloudflare Tunnels are really a clever piece of tech that makes things much easier for us. It is an abstraction, but for the purposes of getting our services out in the open safely, it's the best solution I've found.

[^1]: [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/)