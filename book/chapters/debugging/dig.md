## dig

So far, we've been using the dig command throughout this book to check our DNS handiwork. It stands for Domain Information Groper (ew) and its sole job is to get information about DNS records. This thing is our Swiss Army knife for DNS debugging.

## Dig basics

The first step with dig is to look up A records:

```shell
$ dig donkeyrentals.com

; <<>> DiG 9.8.3-P1 <<>> donkeyrentals.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 2640
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;donkeyrentals.com.		IN	A

;; ANSWER SECTION:
donkeyrentals.com.	900	IN	A	64.99.80.30

;; Query time: 146 msec
;; SERVER: 208.67.222.222#53(208.67.222.222)
;; WHEN: Wed Oct 21 11:31:04 2015
;; MSG SIZE  rcvd: 51
```

The command breaks down like this:

* `dig` - The command.
* `donkeyrentals.com` - The domain we'd like information for.

The response breaks down like this:

* Header - We can safely ignore this for now. For the curious, this section shows us information about the response such as what type of response it is (`opcode: QUERY`), what flags are present (`flags: qr rd ra;`), and what types of responses we got (`QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0`).
* Question section - Also unimportant. It's only confirming what we asked for: A records for `donkeyrentals.com`.
* Answer section - This is the part we care about because it contains the information we asked for.
* Statistics - Meta information about our request, how long it took, how large it was, what server was queried, etc. Not important for now, but this will come up later.

(Now, I know what you're thinking, "Wow this is captivating reading. Where can I learn even more?!" [RFC 1035](http://www.ietf.org/rfc/rfc1035.txt) from the Internet Engineering Task Force is a great place to start if you really want to dive into the weeds here.)

## Other record types

By default dig looks up A records for our domain (just the apex domain, not any subdomains), and as we can see it returned `64.99.80.30`, the IP address of our apex domain's A record. We can look up other record types as well:

```shell
$ dig message.donkeyrentals.com TXT

; <<>> DiG 9.8.3-P1 <<>> message.donkeyrentals.com TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 55675
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;message.donkeyrentals.com.	IN	TXT

;; ANSWER SECTION:
message.donkeyrentals.com. 900	IN	TXT	"Hello"

;; Query time: 35 msec
;; SERVER: 208.67.222.222#53(208.67.222.222)
;; WHEN: Fri Oct 23 15:13:51 2015
;; MSG SIZE  rcvd: 61
```

Hidden in the response here, we can see the TXT record ("Hello") we added in the previous chapter. Any of the other record types we talked about there are available too.

## Query options

Up until this chapter, I've been using dig with the `+short` query option to just get the bare minimum information we needed. Dig's query options all have a `+` at the start:

```shell
$ dig +short donkeyrentals.com

64.99.80.30
```

_What order these options come in [does matter](http://serverfault.com/questions/431080/dig-show-only-answer#comment-462136). Always put the query option before the domain we're querying for. I've seen some wacky output sometimes the query option comes later._

The [dig manual](http://ftp.isc.org/isc/bind9/cur/9.9/doc/arm/man.dig.html) lists many query options besides `+short` which we can look through at our leisure, but for now I'll point out a few of the more useful ones:

### `+trace`

At the beginning of this chapter, we talked about how DNS queries travel through a chain of servers before finally getting to our domain. This will illustrate that whole process. Try it!

### `+noquestion`, `+noanswer`, `+noadditional`, and `+noauthority`

Query options can also have `no` at the start to remove some functionality. These query options for example are all ways to limit the response dig gives back to us. If we never care about the `QUESTION` section for example, we can simply turn it off and make dig's response much less wordy.

## Common use cases

### Just the answer section

Dig has a query option called `+noall` which as we might expect, turns off all output. It's not very useful by itself, but combined with a different query option such as `+answer`, we can get just the sections we want:

```shell
$ dig +noall +answer donkeyrentals.com A

donkeyrentals.com.	900	IN	A	64.99.80.30
```

### Records without the cache

As we know, there's lots of caching involved in DNS. Since all of our DNS records exist on a nameserver, we can ask that nameserver directly and bypass any caching information:

```shell
$ dig @ns1.hover.com donkeyrentals.com A

; <<>> DiG 9.8.3-P1 <<>> @ns1.hover.com donkeyrentals.com A
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 30822
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;donkeyrentals.com.		IN	A

;; ANSWER SECTION:
donkeyrentals.com.	900	IN	A	64.99.80.30

;; Query time: 68 msec
;; SERVER: 216.40.47.26#53(216.40.47.26)
;; WHEN: Mon Oct 26 12:57:08 2015
;; MSG SIZE  rcvd: 51
```

In this case, we ask the name server `ns1.hover.com` what the A records are for `donkeyrentals.com`. You might think "Isn't this what we've been doing all along?" Yes, and no. The first time we ask for `donkeyrentals.com`, it gets the uncached answer from `ns1.hover.com`. But then our DNS server (or network router, or internet service provider, or myriad other places) stores it in their cache for a certain number of seconds, represented by the `900` (15 minutes) in the answer line. That number by the way is called _Time to live_ or _TTL_.

Theoretically after those 15 minutes pass, we'll get the uncached answer again, or at least the cache will have updated to display more up-to-date information if anything has changed.

To force our domain resolver to get the latest information, we can say: "No, do not ask our caches, ask the server directly for information." We can tell that we got an authoritative answer by looking at the flags in the header: `flags: qr aa rd`. That `aa` stands for **A**uthoritative **A**nswer. Also, in the stats at the bottom, we can see that we queried the server at `216.40.47.26` which is actually what the A record for `ns1.hover.com` points to. If we don't tell it what server to query, it will use the DNS server we have configured for our computer.

### Multiple queries at once

If we have a bunch of queries to make, dig has a batch mode. First we'll need a file with a list of queries. This list will look a lot like our dig commands so far, but there will be no `dig` at the start and each query will have its own line:

*dig.txt*

```text
@ns1.hover.com donkeyrentals.com
www.donkeyrentals.com CNAME
+short donkeyrentals.com NS
```

The, we use dig with the `-f` flag:

```shell
$ dig -f dig.txt

... not gonna paste all the responses here ...
```

This will make all the queries in order. Feel free to use query options here too, like `+short` to make all queries have short responses:

```
$ dig +short -f dig.txt

... no really, pixels are surprisingly expensive ...
```

### Looking up a domain name by it's IP address

So far, we have been looking up domain names to get their IP addresses, but can we do this in the other direction? We can indeed. This is what the `-x` flag is for:

```shell
$ dig -x 66.220.156.2

2.156.220.66.in-addr.arpa. 2360	IN	PTR	edge-star-shv-07-ash4.facebook.com.
```

This returns a PTR record. We didn't cover these in the last chapter because we don't ever get to actually configure them. Briefly, PTR stands for pointer and they _point_ back to the original domain. In this case, we can see that it's a server at `facebook.com`.

Now keep in mind this doesn't point back to a website, but to a server. If `somewebsite.com` is hosted at `somehost.com` with many other websites, a reverse lookup is more likely to show `someserver.somehost.com` rather than `somewebsite.com`. Facebook is so large they host their website on many servers, so they're easier to track down. Since it's not always accurate, I use these reverse lookups as a hint more than an answer.

Another anecdote is that the "reverse DNS lookup" database is hosted at `in-addr.arpa` domain. All lookups happen by reversing the sections of the ip address and prepending the result to `in-addr.arpa`. So if you're trying to look up `12.34.56.78` you can also use `dig 78.56.34.12.in-addr.arpa PTR`.

## Curiosities

### What is the `IN` mean?

In dig responses, we often see `IN` in the response:

```shell
;; QUESTION SECTION:
;donkeyrentals.com.		IN	A
```

This doesn't mean "in" like "A records all up **in** ya donkeyrentals" but is short for "Internet". Turns out all records have a class. Other classes are like an entirely separate internet and have nothing to do with this book. For our uses we are using the IN (Internet) class always. That's also the class that dig defaults to. It can also be CH (Chaos) or HS (Hesiod) but we won't be talking about these no matter how rad they sound.

### Why do records get returned in a different order?

When we ran dig to see all the root servers, they may have come back in a seemly random order. This is called round-robin DNS. When we get back a list of IP addresses from a DNS query, generally a domain resolver will start with the first address in the list. If the first server doesn't respond, it will pick the next one, and so on.

To make sure one server doesn't take all the heat, DNS providers can change the order the records are returned in. This helps distribute requests across multiple servers. Not all DNS providers do this, and it's not always done in the same way, but keep an eye out for it.

### Why does the TTL value change drastically?

While writing this book, this was a common scenario I ran into:

```shell
$ dig somedomain.com A

somedomain.com.	127	IN	A	12.34.56.78

$ dig somedomain.com A

somedomain.com.	125	IN	A	12.34.56.78

$ dig somedomain.com A

somedomain.com.	541	IN	A	12.34.56.78
```

_Dig responses shortened to save pixels. Consider donating to the Save-A-Pixel foundation for America._

What's going on here? We made a request to get the A records at `somedomain.com`. We see the TTL for the first request is `127`. Then, a couple of seconds later, we make the same request and see that the TTL has decreased by 2 seconds to `125`. Seems about right. Finally, after another couple of seconds, we make the request a third time and get `541`. What?!

This is a perfect example of round-robin DNS. Just like I described above, DNS providers change the order of DNS records. So in this case, let's say there were looking at two servers, A and B. We saw the TTL value for server A, and then again for server A after it had decreased slightly. Then we saw server B which has a totally different TTL value.

It's pretty normal to see this so don't let it phase you, but it is certainly jarring and confusing the first time.