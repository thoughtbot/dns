## NS

Nameserver (NS) records are the first point of contact to the outside world that we as domain administrators are responsible for. In fact, the `dig` command we've been using is asking the nameservers to get its information. NS records are often neglected when setting up or changing a domain. Most people just skip right to those attractive and charismatic A and CNAME records.

So what do NS records point to? Each one points to a server that holds all the records we create. Usually we'll configure two or more nameservers when setting up a domain. That way if one is offline, the other can pick up the slack. Here's how it might look:

* **Nameserver 1**: `ns1.example.com`
* **Nameserver 2**: `ns2.example.com`
* **Nameserver 3**: `ns3.example.com`

Nameservers are usually in the form of `nsX.example.com` where `X` is a number starting at 1, and `example.com` is the website where you registered your domain. This isn't a standard, just a convention. If you had to guess what the nameservers are, start here.

In all the domain tech support I've done, wrongly set nameserver records are the most common source of confusion for newcomers. Since the nameserver finds all the other records in your domain, if they're set wrong, nothing will work. If you find that your domain points to some placeholder page, it's likely that your name servers are wrong.

Imagine you were looking someone up in a phone book for the wrong town. You wouldn't be able to find that person. The phonebook here is the nameserver, and each person here is a record. Wrong nameserver, wrong records.

We can check our configuration with `dig`:

```
$ dig +short donkeyrentals.com NS

ns1.hover.com
ns2.hover.com
```

This isn't as useful as you might think. Since `dig` uses the nameservers to get information, asking for those nameservers is a bit cyclical. It's like calling someone up to ask them for their phone number. Looking up NS records with `dig` is still useful to find out if your nameservers are incorrect, but it's not useful for figuring out the right ones.
