# Why not port-forward?
Now that we have a server up and running, the next step is figuring out how to make the services on it accessible from the internet. 

It might be tempting to simply expose your services by opening ports on your home router and pointing them to your server. However, this approach comes with several problems. First, it significantly increases your attack surface. By poking holes through your router, you’re effectively making your home network accessible to anyone on the internet, including malicious people who create scripts that actively scan for open ports. Even if your apps are password-protected, brute force attempts and vulnerabilities in the software can quickly put your entire network at risk.

Another drawback is that port-forwarding often isn’t reliable. Some ISPs use [Carrier-Grade NAT (CGNAT)](https://en.wikipedia.org/wiki/Carrier-grade_NAT), which means your public IP address is actually shared with other customers. In this case, you won’t even be able to forward ports from your router to the wider internet, because you don’t truly control the external address.

For these reasons, port-forwarding is not recommended for securely exposing self-hosted services. Let's see how we can solve this in the next section.
