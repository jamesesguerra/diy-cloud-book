# My self-hosting journey

Like most beginner web developers, I started small, just following Youtube tutorials and MOOCs, building little pet projects, and putting them online. At first, that meant the simplest deployment paths: static sites on Vercel and Netlify, and APIs on Heroku paired with MongoDB (yes, I grew up in the generation where MERN apps were the gateway drug into web development).

For a while, that was enough. But when Heroku’s free tier ended in November 2022, I had to look for alternatives. That’s when I found Fly.io. It was cool and easy to use, but it came with limits I quickly ran into.

Around the same time, I landed a job as a software engineer working with .NET and SQL Server. Suddenly, I had a new problem: most PaaS platforms catered to Node.js or Python apps, with PostgreSQL as the default database. Finding a service that supported .NET out of the box was pretty challenging.

I gave those platforms a shot, but another issue surfaced: network latency. From my country (the Philippines), connecting to their servers felt sluggish. That pushed me to try Azure, since I was already using it at work. Azure App Service was honestly great and super easy to set up (I even wrote an [article](https://medium.com/@jamesesguerra025/how-to-deploy-a-net-api-for-free-on-azure-787e95424f0a) about it). The catch, though, was the database pricing. I built a small app for my mom’s job, and even though it didn’t store much data, my Azure SQL bill ballooned to around ₱1,000 (~17 USD) a month. For a side project I wanted to host for free, that felt like burning money.

That frustration led me deeper into DevOps. In September 2024, I bought a mini PC and dove into the world of self-hosting. I saw people online running setups I could barely comprehend. Jellyfin, Nextcloud, Home Assistant, you name it. I started smaller, hosting apps like Glance, Jellyfin, Nginx Proxy Manager, Gitea, and even my own self-hosted runners, all managed with Docker Swarm.

It was addictive. So I soon thought, if I can host all this infrastructure myself, why not my pet projects too? That’s when the question of safety hit me. I didn’t want to expose my home network recklessly. I first discovered Tailscale (a wrapper for WireGuard), which allowed me to connect to my home services remotely. It worked great for personal access, but since devices needed to be on the same tailnet, it wasn’t practical for sharing my projects with others. That’s when I turned to Cloudflare Zero Trust, which finally gave me the security and convenience I needed.

From there, I began piecing together a simple architecture, one where my projects could safely connect to the different services on my mini PC without me constantly worrying about breaking something.

And that’s how this book came to be: the result of documenting that journey, so other budget-conscious developers like me can build their own little cloud at home.