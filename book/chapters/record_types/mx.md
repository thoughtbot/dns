### MX

These are for email. Just like how A or CNAME records point to a website, MX records are how email knows where to go on the internet. If you break apart an email address like `sales@donkeyrentals.com`, we have two parts: `sales` and `donkeyrentals.com`. We're just here to concern ourselves with the second part: `donkeyrentals.com`.

Whoever runs your mail server (Gmail, Fastmail, etc.) will have a list of servers you need to make MX records for. First, let's try to set one up:

* **Hostname**: `@`
* **Record Type**: `MX`
* **Priority**: `10`
* **Value**: `aspmx.l.google.com`

This is part of the configuration for Gmail. We'll walk through it step by step.

For **Hostname** remember that `@` is for the apex domain, which is the domain without anything in front of it. I.e. `google.com` not `www.google.com`. It has nothing to do with the "at sign" in an email address. We're saying we want to configure the server for emails that get sent to `<anything>@donkeyrentals.com`. We're not concerned about email sent to other subdomains, just this one.

The **record type** (`MX` in this case) should be pretty obvious. We're talking about `MX` records after all.

**Priority** is the same as in SRV records, the lower the number, the more likely this server will choose it. There can be multiple mail servers for a particular domain. If one server is down or unavailable, it will try the next one in the list.

The **Value** is finally the server. This is going to be a lot like a CNAME record in that we point to a domain name, but _that_ domain name needs to be an A or AAAA record. I.e. we can't point an MX record to a CNAME or other type of record. It has to go to a domain that points directly to an IP address.

Finally, we can verify it:

```shell
$ dig donkeyrentals.com MX +short

10 aspmx.l.google.com
```
