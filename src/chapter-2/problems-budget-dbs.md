# Problems with "budget" DBs

When you’re trying to build something on a budget, the database is often where you start feeling the pain. Hosting code can be cheap, sometimes even free, but the database is where the costs, the latency, and the compromises really start piling up.

Take the popular “budget-friendly” PaaS databases that offer free tiers: Supabase, Neon, Planetscale, and others. On the surface, they look like really good options. Free tier storage, easy dashboards, instant provisioning, and sometimes even built-in authentication or APIs. But if you’re outside their main regions (usually in the US or Europe), you’re out of luck. For me, living in Southeast Asia, there’s simply no option closer. That distance translates directly into latency, and you feel it.

I remember using Supabase once and wondering if my API was broken. Every request felt sluggish. But the issue wasn’t my code, it was the database connection. Sure, it “worked,” but it was nowhere near fast enough to keep users around.

The only one that’s worked out decently for me has been MongoDB Atlas. But even then, it’s a document database. Great for those early MERN tutorials everyone starts with, but not always the right fit when you want a traditional relational setup.

On top of that, some providers only give you one database in the free tier. That means if you’re working on multiple pet projects, you have to lump all your tables into that single database. It’s messy, confusing, and can even cause accidental conflicts if you’re not careful.

And then there’s the “spin down” problem yet again. Some of these providers save costs by powering down your database when it’s not in use. That means the first request after a period of inactivity takes forever to wake things up. If you’re a recruiter checking out a demo, or a user testing your app for the first time, that delay is enough to make them bounce. It doesn’t matter how polished the frontend is. If the DB takes ten seconds to respond, it feels broken.
