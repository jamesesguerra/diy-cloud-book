# Problems with free tiers

Free tiers are usually the first stop for developers who want to get their apps online. They’re easy to sign up for, quick to deploy on, and feel like a low-risk way to test things out. But if you’re serious about running something long term, free tiers come with problems that you need to be aware of.

## They Expire
The biggest issue with free tiers is that they don’t last forever. Some are trial periods that only run for 30 or 60 days. Others give you a year before you start paying. It feels great at first, but when the clock runs out, you’re suddenly left with a choice: pay for resources you might not actually need, or scramble to migrate your app elsewhere.

## Paying for What You Don’t Need
One of the promises of public clouds is that you “only pay for what you use.” That sounds nice in theory, but the tricky part is knowing what you really need.

In my own case, I once paid for a database that was way overkill. It had way more storage than I’d ever use, but because I didn’t fully understand the pricing model at the time, I kept it running. Even the lowest possible tier was too much for my use case, but I didn't have any other option.

Public cloud pricing can be complicated, often using units like Database Transaction Units (DTUs) that are hard to understand. So if you’re not careful, you might end up paying for performance you don’t actually need.

## Why Public Clouds Exist
It’s worth asking: if free tiers and pricing traps are frustrating, why do public clouds exist at all? The answer is **convenience** and **agility**.

With services like Azure App Service or AWS Elastic Beanstalk, you don’t have to worry about setting up servers, networking, storage, patching, or even basic security. It’s all taken care of for you. That convenience is powerful—especially if you just want to focus on coding.

This setup also gives you agility. You can scale up resources in minutes, experiment with new services quickly, or roll out a proof of concept without touching any infrastructure. For solo developers, that speed is invaluable. It means you can test ideas fast, iterate, and move on if something doesn’t work, all without needing a dedicated ops team.

The problem comes when the free tier runs out. For example, Azure App Service lets you host around 10 apps for free, which sounds great. But once you need a database for example, the costs can shoot up. That’s what happened to me, the app hosting was free, but the database costs quickly made things expensive when my free DB expired on Azure.

So what you’re really paying for isn’t just “cloud space.” You’re paying a convenience fee to let someone else handle the DevOps side of things. If you’re like me and actually enjoy setting up infrastructure yourself, free tiers start to feel limiting instead of freeing.

## PaaS Platforms and Their Limits
There are also Platform-as-a-Service (PaaS) providers that offer a free tier such as Heroku (back in the day when they had a free tier), Render, Fly.io, or Railway. These platforms give you a smoother experience for deploying apps, but they come with hard limits.

For example:
- You can only host a small number of apps
- API calls or compute hours are capped
- Apps can get spun down (go to sleep) if they’re inactive too long, which can turn off recruiters / users if they're impatient

In my case, I still have a Fly.io app connected to a MongoDB Atlas cluster that’s been running for three years with solid performance. But Fly.io limits you to about 2 apps on the free plan, which isn’t much.

The point is: these services are great for learning, experimenting, or running small side projects. But if you plan to scale, or even just run multiple apps without lumping together all of your endpoints in one API project, the limits of free tiers start to show quickly.