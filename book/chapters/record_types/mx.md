### MX

MX (Mail eXchange – the X looks cool that way) records are for email. The same way A or CNAME records point to a website, MX records tell email where to go on the internet. If you break apart an email address like `eeyore@donkeyrentals.com`, we have two parts: `eeyore` and `donkeyrentals.com`. MX records are only concerned with the second part: `donkeyrentals.com`.

Your email provider (Gmail, Fastmail, etc.) will have a list of servers you need to make MX records for. First, let's try to set one up:

* **Hostname**: `@`
* **Record Type**: `MX`
* **Priority**: `10`
* **Value**: `aspmx.l.google.com`

This is part of the configuration for Gmail. We'll walk through it step by step.

Remember the `@` in the **Hostname** is for the apex domain, and has nothing to do with the `@` in an email address. It represents the domain without anything in front of it. I.e. `google.com` not `www.google.com`. We're saying we want to configure the server for emails that get sent to `<anything>@donkeyrentals.com`. We're not concerned about email sent to other subdomains, just this one.

The **record type** (`MX` in this case) should be pretty obvious. We're talking about `MX` records after all.

**Priority** is the same as in SRV records, a lower number means this server will be used before any other server is tried. There can be multiple mail servers for a particular domain. If one server is down or unavailable, it will try the next one in the list.

The **Value** is finally the domain name of a server. This configuration might look similar to a CNAME record, but the domain name we point to must be an A or AAAA record. I.e. we can't point an MX record to a CNAME or other type of record. It has to go to a domain that points directly to an IP address.

Finally, we can verify it:

```shell
$ dig donkeyrentals.com MX +short

10 aspmx.l.google.com
```
