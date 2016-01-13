## Connecting Your Domain to an External Service

There are tons of web services today that help you set up a website if you're not a web developer. Gone are the days where you have to write your own blog, store, or company website, although some of us with masochistic tendencies tend to make our own anyway.

These services are great, but they often give you a relatively non-personal URL, something like your-name.service.com. It works fine enough for testing, but running a serious business (renting donkeys) needs a professional and trustable domain name.

_I'll try to make this section as generic as possible. There are scores of popular services that let you connect custom domains. It would be impossible to write them all up in detail, but hopefully I can give you the tools to find what you're looking for and troubleshoot if it goes awry._

One solution is that many services will offer to sell you a domain up front. Obviously, domain experts like us don't need that kind of handholding. We want to be in control of our domains! What if we decide to switch services? Or have subdomains that point to other services? For me personally, this isn't flexible enough.

Connecting a domain that you own is usually takes two major steps: adding DNS records to point toward the service, then telling the service about the domain.

There are a few different ways to do the first step. The most common technique I've seen is to point an A or CNAME record toward an IP or hostname owned by the service. Sometimes services force you to switch to their nameservers so they can manage your DNS records. If this is the case, hope that they have good DNS controls if you ever want to set up other subdomains.

Then, you often tell the service about your domain. Usually in some control panel somewhere, you enter it and for the most part, that's it. Sometimes this takes a bit to start working, but it's often pretty immediate.

### Some pointers

Use dig to check your work, and specify a nameserver. This way you can get 100% up-to-date information:

```dig
dig @ns1.example.com shop.yourdomain.com

...
```

The only caveat here is that if you're using the services nameservers, make sure that's what you are, in fact, querying those servers. That's where the updated records will be.

Also, be aware that if you want to use your bare, apex domain, you won't be able to connect it with a  CNAME record unless your DNS provider supports ANAME/ALIAS/etc records. Some services force you to use a CNAME in which case you'll have to use a subdomain like `www`.
