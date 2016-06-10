## How DNS Works

There are many steps between typing a URL into our browser and seeing the website. It's all very complicated, but there's a method to the madness. To debug our domains, we'll need a quick primer in the deep, dark ways of the domain name system.

### Root Servers

All domains start somewhere, and that somewhere is the root servers. There are 13 root servers labeled `a` through `m`. To see them, simply type `dig +short`:

```shell
dig +short

a.root-servers.net.
b.root-servers.net.
c.root-servers.net.
d.root-servers.net.
e.root-servers.net.
f.root-servers.net.
g.root-servers.net.
h.root-servers.net.
i.root-servers.net.
j.root-servers.net.
k.root-servers.net.
l.root-servers.net.
m.root-servers.net.
```

Told you.

These are nameservers. The order they are in doesn't matter. We can use any of them. Each one stores the information needed to contact all top-level domains like `com`, `net`, `horse`, etc. The `com` nameservers in turn store information about Hover, the DNS provider I use for donkey rentals. Finally, hover has information about donkeyrentals.com.

That's how DNS works: each server looks in its database to find out how to get to the next level below it. To get to any domain, we have to go through all these steps. Well, _we_ don't have to go through all those steps. Software called a resolver does.

### The Resolver

The piece of software that actually makes these requests is called a DNS resolver. Its job is to turn, or resolve, `donkeyrentals.com` into `64.99.80.30` by taking all the steps above. Tools like dig let us see what the resolver sees so we can confirm our DNS settings.

Dig lets us act like a resolver. We can see the whole chain of server interactions laid bare, which then lets us see where things are misconfigured. For example, if we're expecting the nameservers for `donkeyrentals.com` to be `ns1.equestrian-domains.com` and they are, in fact, `ns1.bovinian-domains.com`, we have a problem. If we expect `www.donkeyrentals.com` to be a CNAME that points to `donkeyrentals.com`, but it instead points to `buzzfeed.com`, we have a different problem.

### Caching

The other thing to know about DNS is that each step in the resolution process gets cached. When the resolver asks `com` for information about `donkeyrentals.com`, it gets stored for some amount of time, which can be seconds to days, depending on the server.

The reasoning here is simple: if the whole chain was traced every time anyone in the entire world wanted to go to a website, it would put an enormous load on the root servers. With only 13 root servers, that would be billions of requests a day. In reality, each letter points to multiple servers. But even if there were 500+, that's still hundreds of millions of sites per day. Too much.

That should be enough to get us started with my very favorite debugging tool: dig.
