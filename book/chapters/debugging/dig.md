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

The dig manual lists many query options besides `+short` which we can look through at our leisure, but for now I'll point out a few of the more useful ones:

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

dig @ns1.hover.com donkeyrentals.com A

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
