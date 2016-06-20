## Use a CNAME on the Apex Domain

Occasionally, we'll need to use a CNAME record to redirect our domain elsewhere, but we'll want to use it on our apex domain, not `www` or another subdomain. The CNAME is usually the requirement, and the lack of a `www` is a stylistic choice. Some services (I'm looking at you [Heroku](https://devcenter.heroku.com/articles/custom-domains#definitions)) require that we use a CNAME record to point our domain toward their service.

We all know by this point that CNAMEs can't be used on the apex domain, so we're stuck using a subdomain. The common choice is certainly `www`, but, as previously established, maybe that's not what we want.

### ALIAS/ANAME

If our DNS provider offers ALIAS or ANAME records, that's probably our best option. I'm not a huge fan of these because they are non-standard records, but sometimes they're our only choice.

On the upside, they are simple to configure:

* **Hostname**: `@`
* **Record Type**: `ALIAS`
* **Target Host**: `someotherwebsite.com`

And boom, `donkeyrentals.com` now points to another place.

### Forwarding

Unfortunately, sometimes we don't have these special records and we have to use a subdomain like `www`. In this case, I prefer using forwarding to force all apex domains to redirect to their `www` counterparts. We still end up with `www` at the start of our domain, but people can visit either URL and get forwarded to the correct place.

In the last section, I went over detailed instructions on _removing_ the `www` from a domain. We can use those instructions to go the other way and force the `www`. The two basic ways to do this are:

* Configure nginx or Apache to forward the domain.
* Use an `.htaccess` file to forward the domain.

Some DNS providers have tools to forward a domain, which works similarly to the methods above. In this case, we're forwarding it toward the `www` version. For example, if we have `donkeyrentals.com` as our domain, we can forward that to `http://www.donkeyrentals.com`. Then, our CNAME record for `www` can point wherever we need.
