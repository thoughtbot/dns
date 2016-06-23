## My Old Website Is Showing Up

Let's say we've recently moved to to a different web host, or, for whatever reason, need to point our domain to a different server. This can be tricky because there's not a great way to test our records before we move. The best way I've found is to have a spare domain lying around that we can configure without fear of screwing anything up.

But that isn't always the case. So what can we do if it's not working?

### Check the Nameservers

One very common problem is a domain's [nameservers](#ns) are set incorrectly. Remember, the nameservers are like the phonebook and all our other DNS records are like the people listed inside it. If someone is looking in the wrong "phonebook," they won't be able to find the right DNS records.

Some web hosts will manage a domain's individual DNS records, and the DNS provider is only responsible for administrative tasks like domain renewal and whois information. In a situation like this, we use the DNS provider to point our domain's NS records toward our web host, and the web host handles all other records.

Let's say we used Donkey Domains for our domain name and Horse Hosting to host our website. Over at Donkey Domains, we would set our NS records to the nameservers provided by Horse Hosting:

* **Nameserver 1**: `ns1.horsehosting.com`
* **Nameserver 2**: `ns2.horsehosting.com`
* **Nameserver 3**: `ns3.horsehosting.com`

Then, all other records (A, MX, CNAME, etc.) will be created through Horse Hosting's control panel.

### Check the Records With dig

If we think we've set everything up correctly but our website is still not showing the correct data, we can check the records directly using `dig`.

First, we can check to make sure nameservers are what we expect them to be:

```shell
$ dig +short donkeyrentals.com NS

ns2.horse-hosting.com.
ns1.horse-hosting.com.
ns3.horse-hosting.com.
```

Then we can check individual records:

```shell
dig +short donkeyrentals.com A

104.131.191.2
```

We can also check the nameserver directly for any record:

```shell
$ dig +short @ns1.horse-hosting.com donkeyrentals.com A

104.131.191.2
```

If these match but we're not seeing the website in our browser, it's possible that DNS resolvers around the world haven't updated to the latest set of data yet. This is why we see warnings like "changes may take up to 48 hours."

However, if they don't match, that means we may have set the individual DNS records in the wrong place. Looking at the queries above, there are two types: one uses our DNS resolver, while the other queries the nameserver directly.

If the query using the nameserver is correct but the query using the resolver isn't, it's still possible that a resolver somewhere along the line is using old, cached information. This should sort itself out within hours or, at most, a couple of days.

However, if the direct nameserver query has the incorrect records, it's likely that the nameserver is still pointing toward the old domain host. Make sure the domain's NS records point toward the new server.
