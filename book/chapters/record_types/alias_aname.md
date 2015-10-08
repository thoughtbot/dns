### ALIAS or ANAME

There is a way to point the apex domain to a non-address record if we need to. "But didn't you say that the apex domain has to point to an IP address?" Yes. I lied. Sort of. It's technically true; according to [long](http://tools.ietf.org/html/rfc1034#page-15) and [boring](http://tools.ietf.org/html/rfc1034#page-20) documents the apex domain _must_ not use a CNAME record. Despite this, some DNS hosts have started creating new features outside of these rules.

[DNSimple](http://support.dnsimple.com/articles/alias-record/) is using TXT records to point apex domains just like a CNAME would. They call this an ALIAS record. [DNS Made Easy](http://help.dnsmadeeasy.com/managed-dns/records/aname-records/) has a similar feature called ANAMEs. I want to make it clear that these are non-standard uses of DNS technology only available with some registrars. Different registrars call them different things and don't all work the same way. They make me nervous.

Even so, they can be useful. Before I mentioned that [Heroku](https://devcenter.heroku.com/articles/custom-domains#add-a-custom-root-domain). They make use of this feature if you want your apex domain to point toward your Heroku app.

Since these aren't the same across the board I can't promise this is how you'll have to set one up. But it will likely work something like:

* **Hostname**: `@`
* **Record Type**: `ALIAS`
* **Target Host**: `someotherwebsite.com`

And if we want to test it with `dig`, well... we can try:

```shell
$ dig donkeyrentals.com TXT +short

"ALIAS for someotherwebsite.com"
```

Notice I looked for a TXT record here. That might be how you have to find it, but it might be something else entirely! That's the brave new world of non-standard records. Exciting no? _ALIAS records. Coming to a theater near you._
