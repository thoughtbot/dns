## ALIAS or ANAME

These records are a special case. As of this writing, very few DNS providers implement them. When they are implemented their names and implementations vary wildly. So why are we even talking about them? Because they let us do a very special thing: point the apex domain to a non-address record.

"But didn't you say that the apex domain has to point to an IP address?" Yes. I lied. Sort of. It's technically true; according to [long](http://tools.ietf.org/html/rfc1034#page-15) and [boring](http://tools.ietf.org/html/rfc1034#page-20) documents, the apex domain _must_ not use a CNAME record. Despite this, some DNS hosts have started creating new features outside these rules.

[DNSimple](http://support.dnsimple.com/articles/alias-record/) is using TXT records to point apex domains just like a CNAME does. They call this an ALIAS record. [DNS Made Easy](http://help.dnsmadeeasy.com/managed-dns/records/aname-records/) has a similar feature called ANAMEs. I want to stress again that these are _non-standard_ uses of DNS technology only available through limited DNS providers. Each providers' implementation is entirely different. They make me nervous.

Even so, they can be useful. For example I mentioned that [Heroku](https://devcenter.heroku.com/articles/custom-domains#add-a-custom-root-domain) makes use of this feature to let us point our apex domain our Heroku app.

Since these aren't the same across the board I can't promise this is how we'll have to set one up. But it will likely work something like:

* **Hostname**: `@`
* **Record Type**: `ALIAS`
* **Target Host**: `someotherwebsite.com`

When we want to test our setup, if we're lucky, our DNS provider will let us ask it about ALIAS or ANAME records directly:

```shell
$ dig donkeyrentals.com ALIAS +short

82.144.121.97
```

But again, these are _non-standard_ record types, so we may have to result to alternate methods:

```shell
$ dig donkeyrentals.com TXT +short

"ALIAS for someotherwebsite.com"
```

Notice we looked for a TXT record here. That's how DNSimple does it but it might work some other way entirely! That's the brave new world of non-standard records. Exciting no? (ALIAS records. Coming to a theater near you.)
