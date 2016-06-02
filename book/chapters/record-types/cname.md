## CNAME

I want you to know going into this section that CNAMEs are odd and hard to understand. They have their uses, which we'll get into below, but don't worry if at first read you are as confused as I was when I began learning about CNAMEs. So saddle up on your rental donkey and let's get moving.

CNAME records are the other side of the coin from A and AAAA records. Instead of pointing toward an IP address, they can only point toward another domain. You can think of CNAMEs as making one domain accessible from another domain. For example, a common configuration is to point `www` toward our apex domain so both addresses display the same website:

* **Hostname**: `www`
* **Record Type**: `CNAME`
* **Target Host**: `donkeyrentals.com`

```shell
$ dig +short www.donkeyrentals.com CNAME

donkeyrentals.com.
```

Now `www.donkeyrentals.com` will point to `donkeyrentals.com`.

That's not all. You can point a CNAME record at any domain, even one that isn't ours:

* **Hostname**: `redirect`
* **Record Type**: `CNAME`
* **Target Host**: `rabbitrentals.com`

```shell
$ dig +short redirect.donkeyrentals.com CNAME

rabbitrentals.com.
```

Now when people try to visit `redirect.donkeyrentals.com`, they get _hopped_ over (see what I did there?) to our competitors site.

### When To Use CNAMEs

Why would we use a CNAME record instead of an A? Well, for the most part, you wouldn't. A records are highly preferred because they are much more direct. When your browser sees an A record, it gets an IP address. That's it. Requesting a CNAME record is different. It looks up the record, sees that it's a CNAME, looks what the record is pointing toward, and then _restarts_ the request. This will make requests take longer to get to our final, glorious IP address.

CNAMEs also have limits. For example, we can't use a CNAME record on the apex (`@`) domain. If you want to point the plain `donkeyrentals.com` to another domain with DNS, you're out of luck (with the exception of ALIAS records, see below). Also CNAME records can never exist with other record types for the same hostname. Imagine our `www` pointing to `rabbitrentals.com` with a CNAME record, and _also_ to our server's IP address with an A record. We have no way of knowing whether to use the CNAME record or A record, and each could have different outcomes.

For the most part A records are the way to go when we want to connect a domain to a website or service. But sometimes CNAMEs are the better (or only) choice. If we want an honest to goodness alternate name for the same domain, CNAMEs are it. Or for services like [Heroku](https://devcenter.heroku.com/articles/custom-domains#configuring-dns-for-subdomains) we need to use a CNAME to point our domain to an app we created. Heroku hosts lots of websites on many servers where the IP addresses can change at any time, so there's no IP address where we can point an A record.

### CNAMEs vs Subdomains

There's a lot of confusion about the difference between a CNAME and a subdomain (at least there was for me when I started learning). They are two separate concepts, and it's important to understand both of them.

We might hear `www` talked about as a subdomain of `donkeyrentals.com` or as a CNAME record for the `donkeyrentals.com` domain. But which one is it?

Technically, `www` by itself is a hostname (referred to in the [RFC 882](https://tools.ietf.org/html/rfc882#page-9) with a space as in "host name"). Hostnames are not subdomains or CNAME records. The [subdomain](https://tools.ietf.org/html/rfc882#page-7) is the full `www.donkeyrentals.com` and `www` is the hostname at the beginning. (It's common to call `www` the subdomain even if that's technically incorrect.)

There's _also_ the `www` entry in our domain's DNS records. It's not unusual for this to be a CNAME record but it doesn't need to be. We can have `www` be an A record, or NS record, or any kind of record. Speaking of NS records...
