## nslookup

I like dig. It's a good tool for debugging, probably the best. But one problem with dig is that it's not installed on the Windows operating system by default. That's a bummer if we need to do some quick DNS troubleshooting. Sure you could use one of dig's many online interfaces but it doesn't have that new command line smell.

There's another tool called nslookup. For the most part it does everything dig does, but there are a couple caveats.

Nslookup is a part of [BIND](https://www.isc.org/downloads/bind/), a suite of software tools for running DNS servers. BIND includes a bunch of tools including nslookup and dig. ISC, the company that maintains BIND, states in the [BIND manual](https://kb.isc.org/article/AA-01031), page 9:

>Due to its arcane user interface and frequently inconsistent behavior, we do not recommend the use of nslookup. Use dig instead.

Talk about an authoritative answer! (wink to camera)

That's not all though, nslookup performs other unnecessary queries in the background. Not only are these useless, but they can actually screw up the response that nslookup returns. This won't matter for most requests, but if those initial, unnecessary queries fail, it can stop our query in its tracks.

These flaws are unfortunate, because alternate tools can be very useful. But I'd recommend you'd avoid nslookup altogether. You can read more about the flaws in nslookup [here](http://homepage.ntlworld.com/jonathan.deboynepollard/FGA/nslookup-flaws.html) and [here](http://cr.yp.to/djbdns/nslookup.html).

### Basic usage

Anyway, if you skipped the last few paragraphs let's start with the most basic example, looking up A records for `donkeyrentals.com`:

```shell
$ nslookup
> donkeyrentals.com
Server:  Death-Star
Address:  192.168.1.1

Non-authoritative answer:
Name:    donkeyrentals.com
Address:  64.99.80.30
```

The bigest difference with nslookup is the way you use it. Type `nslookup` and hit enter. This brings up what's called interactive mode. You can type commands here without having to type nslookup first. The command prompt here is indicated with `>` instead of `$`. Type `exit` or hit `ctrl-c` to leave this mode and go back to the terminal.

We can type domain names and get their A records, just like dig. That's the first step. Here are some examples of other queries:

### Getting a little more info

The `debug` setting can give you a more dig-like response including the question and TTL if you want it:

```
> set debug
> donkeyrentals.com
Server:		8.8.4.4
Address:	8.8.4.4#53

------------
    QUESTIONS:
	donkeyrentals.com, type = A, class = IN
    ANSWERS:
    ->  donkeyrentals.com
	internet address = 64.99.80.30
	ttl = 698
    AUTHORITY RECORDS:
    ADDITIONAL RECORDS:
------------
Non-authoritative answer:
Name:	donkeyrentals.com
Address: 64.99.80.30
```

To turn this off, type `set nodebug` at the prompt.

### Look up other record types, such as NS

```
> set type=ns
> donkeyrentals.com
Server:  google-public-dns-b.google.com
Address:  8.8.4.4

Non-authoritative answer:
donkeyrentals.com       nameserver = ns1.hover.com
donkeyrentals.com       nameserver = ns2.hover.com
```

We `set` the `type` to `ns`, or `cname`, or `mx` or any of the other types. We can use `set type=` again to set it to a different type.

### Get an authoritative answer

We can set the server, similarly to how we specify a server with dig:

```shell
> server ns1.hover.com
Default Server:  ns1.hover.com
Address:  216.40.47.26

> donkeyrentals.com
Server:  ns1.hover.com
Address:  216.40.47.26

Name:    donkeyrentals.com
Address:  64.99.80.30
```

This attempts to query a nameserver directly instead of using cached information.

### Looking up a domain name by it's IP address

This one is super simple, just enter the ip address:

```shell
> 66.220.156.2
Server:  google-public-dns-b.google.com
Address:  8.8.4.4

Name:    edge-star-shv-07-ash4.facebook.com
Address:  66.220.156.2
```

So that's nslookup in a nutshell. It can be useful, but I would still avoid it. It's not worth hours of frustration because it interpreted a response wrong or failed when it shouldn't have. Stick to dig if you can.
