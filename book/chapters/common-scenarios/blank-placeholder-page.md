## The Website Is Only a Blank or Placeholder Page

Getting a new domain is fun and all, but it can take some time to set up. A common problem is the website will show up as either nothing or some placeholder page.

Let's say we get a domain from Donkey Domains. With no setup whatsoever, domains often point to a placeholder page with a "website coming soon" message. There are two possible problems.

### Default A Records

First, the A records for the domain haven't been configured yet and are pointing to their default IP addresses. This is an easy fix: point them toward our server. If we don't see the change, we can test our configuration with dig. We'll need a nameserver of the DNS provider. For this example, we'll use `ns1.donkeydomains.com`:

```shell
$ dig @ns1.donkeydomains.com donkeyrentals.com +short

12.34.56.78
```

Compare the IP address that comes back with the IP address of our server. If they're the same, it's likely we need to wait for the DNS to propagate throughout the internet

### Wrong Nameservers

If not, the second thing that could be wrong is our nameservers are set incorrectly. When our computer is looking up (_resolving_) the domain, the domain resolver will be pointed toward the wrong nameservers, then look in those servers for DNS records. If we remember from the _NS Records_ section, this is like being in the wrong phonebook. If someone looks for us in a different city's phonebook, they won't find our number.

Some web hosts require us to use their nameservers instead of our DNS provider's. This is common when a domain comes with our web hosting. I like keeping my DNS records at the DNS provider because it feels nice to have them separated. Also, I suspect that most DNS providers do a better job at, well, managing DNS records than most web hosts. If DNS hosting is your core business, you're more likely to make sure it works well.

But sometimes we have no other choice but to host our DNS records at our web host. To do this, we'll need our web host's nameservers. They often look like `ns1.somedomain.com` or `ns2.somedomain.com`, or something similar, then it's generally as simple as finding the nameserver settings for our domain at the DNS provider. Commonly, these settings are not with our DNS records, but in some other, more general configuration spot.

**Warning**: When you change your nameservers, all of the DNS records at that nameserver become invalid. That's because any domain resolver will be looking for records on a different server now, so any old records at that old server will no longer work. You'll have to enter them all again at your web host.
