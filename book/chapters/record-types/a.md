## A

A records are the bread and butter of DNS and probably the least complex. A records always (and only) point toward an IPv4 address such as `93.184.216.34`. A good way to remember this is A for Address.

Here's an example of how we could configure an A record:

* **Hostname**: `@`
* **Record Type**: `A`
* **IP Address**: `93.184.216.34`

The `@` symbol means **apex domain** and has nothing to do with the "at sign" in an email address. It's also called the bare, top, root, or naked domain. It's a fancy way to refer to the domain without any label in front of it. I.e `donkeyrentals.com` as opposed to `www.donkeyrentals.com`. Sometimes, you specify the apex domain by putting simply nothing for the hostname but I'll be using `@` throughout the book.

Once that record set up, we can check our work by using `dig`:

```shell
$ dig donkeyrentals.com A +short

93.184.216.34
```

We've made our domain name point to essentially the same thing as the IP address. In practice this only works one way. Since there might be many websites hosted at that IP address, we aren't guaranteed to get to _our_ website when we visit it. Our server at `93.184.216.34` knows it's getting a request for `donkeyrentals.com` but it must be configured to handle that _specific_ domain, not just the IP address.

We can also use A records with subdomains:

* **Hostname**: `accessories`
* **Record Type**: `A`
* **IP Address**: `93.184.216.34`

This will set up a similar record as above, but for the subdomain `accessories.donkeyrentals.com`:

```shell
$ dig accessories.donkeyrentals.com A +short

93.184.216.34
```

After we have both A records set up, we have an example of more than one website hosted at the same IP address. Our main corporate enterprise's website is `donkeyrentals.com`. For things like diamond-studded donkeyshoes we have our accessories site which is at `accessories.donkeyrentals.com`. We host both websites at `93.184.216.34`, but each have different content.
