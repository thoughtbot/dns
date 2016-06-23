## Connecting a Domain to an External Service

There are tons of web services today that help us set up a website if we're not web developers. Gone are the days when we have to write our own blog, store, or company website, although some of us with masochistic tendencies tend to anyway.

These services are great, but they often give us a relatively non-personal URL, something like `our-name.service.com`. That works fine enough for testing, but running a serious business (such as renting donkeys) needs a professional and trustworthy domain name.

Sometimes, services will offer to sell us a domain up front. Obviously, domain experts like us don't need that kind of handholding. We want to be in control of our domains! What if we decide to switch services? Or have subdomains that point to other services? For me, this offering isn't flexible enough.

Connecting a domain that we own usually involves two steps: adding DNS records to point toward the service, then telling the service about the domain.

There are a few different ways to do the first step. The most common technique I've seen is to point an A or CNAME record toward an IP or hostname owned by the service. Sometimes, services force us to switch to their nameservers so they can manage our DNS records. If this is the case, hope that they have good DNS controls if we ever want to set up other DNS records.

Next, we tell the service about our domain. Usually, in some control panel, we enter our domain so the service knows what domains to look for. This may take a bit to start working, but it's often immediate.

### Check the Work

If it's not working, we can use `dig` to specify a nameserver. This returns 100% up-to-date information and can confirm that we set the records correctly:

```dig
dig @ns1.example.com donkeyrentals.com

...
```

Make sure you're querying the correct servers. If we're using the service's nameservers, we need to query those servers instead of our DNS provider's servers. That's where the updated records will be.

Also, be aware that if we want to use our bare, apex domain, we won't be able to use a CNAME record with the service unless our DNS provider supports [ANAME/ALIAS](#alias-or-aname). records. Some services force us to use a CNAME, in which case we'll have to use a subdomain like `www`. We'll explore solutions to this problem later.
