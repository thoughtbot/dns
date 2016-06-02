## MX

MX (Mail eXchange – the X looks cool that way) records are for email. The same way A or CNAME records point to a website, MX records tell email where to go on the internet. If you break apart an email address like `eeyore@donkeyrentals.com`, we have two parts: `eeyore` and `donkeyrentals.com`. MX records are only concerned with the second part: `donkeyrentals.com`.

Your email provider (Gmail, Hotmail, Fastmail, etc.) will have a list of servers you need to make MX records for. First, let's try to set one up:

* **Hostname**: `@`
* **Record Type**: `MX`
* **Priority**: `10`
* **Value**: `aspmx.l.google.com`

This is part of the configuration for Gmail. We'll walk through it step by step.

Remember the `@` in the **Hostname** is for the apex domain, and has nothing to do with the `@` in an email address. It represents the domain without anything in front of it. I.e. `google.com` not `www.google.com`. We're saying we want to configure the server for emails that get sent to `<anything>@donkeyrentals.com`. We're not concerned about email sent to other subdomains, just this one.

The **record type** (`MX` in this case) should be pretty obvious. We're talking about `MX` records after all.

**Priority** is the same as in SRV records, a lower number means this server will be used before any other server is tried. There can be multiple mail servers for a particular domain. If one server is down or unavailable, it will try the next one in the list.

The **Value** is finally the domain name of a server. This configuration might look similar to a CNAME record, but the domain name we point to must be an A or AAAA record. I.e. we can't point an MX record to a CNAME or other type of record. It has to go to a domain that points directly to an IP address.

Finally, we can verify the record:

```shell
$ dig +short donkeyrentals.com MX

10 aspmx.l.google.com
```

### How email uses MX records

Let's take a second to talk about how email uses these records. When an email server needs to deliver to `donkeyrentals.com`, it looks up MX records for that domain. We just did the same thing for our domain. Let's pretend there are a bunch of servers instead of just one. This is a much more common scenario:

```shell
$ dig +short donkeyrentals.com MX

5 gmail-smtp-in.l.google.com.
10 alt1.gmail-smtp-in.l.google.com.
20 alt2.gmail-smtp-in.l.google.com.
30 alt3.gmail-smtp-in.l.google.com.
40 alt4.gmail-smtp-in.l.google.com.
```

The mail server first tries the record with the lowest priority on the list, `gmail-smtp-in.l.google.com.` and looks up its IP address. Remember that all MX records must point to an A or AAAA record so they will always resolve to an IP address:

```
$ dig +short gmail-smtp-in.l.google.com A

173.194.205.27
```

Then it tries to send the email data. If it fails, it moves on to the item with the next server `alt1.gmail-smtp-in.l.google.com.` which is next lowest priority. The mail server tries server after server until one succeeds or they all fail.

It might seem weird to use the server with the _lowest_ priority first. For that reason, priority is often called **distance**. That way we can think of it like starting with closer servers first and moving outward. Of course, this has nothing to do with the physical location of the servers. It's only a mental model to help remember what that number is for.
