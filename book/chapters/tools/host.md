## host

`host` is kind of like a simplified version of `dig`. In fact, it's developed by the [same company](https://www.isc.org) that makes `dig` and `nslookup`. This will be a quick section since there's not much to the `host` tool, but it's a nice thing to have if you are looking for friendlier responses. Here's what I mean:

```shell
$ host donkeyrentals.com

donkeyrentals.com has address 104.131.191.2
```

Hard to be more friendly than that. That's the A record for `donkeyrentals.com` in simple English words. It can even interpret more complex responses:

```shell
$ host facebook.com

facebook.com has address 173.252.120.68
facebook.com has IPv6 address 2a03:2880:2130:cf24:face:b00c::25de
facebook.com mail is handled by 10 msgin.vvv.facebook.com.
```

### Types

Of course, if we need to look up something other than A records, we can specify type with the `-t` option:

```shell
$ host -t CNAME www.donkeyrentals.com

www.donkeyrentals.com is an alias for donkeyrentals.com.
```
```shell
$ host -t NS donkeyrentals.com

donkeyrentals.com name server ns1.hover.com.
donkeyrentals.com name server ns2.hover.com.
```

### Reverse Lookups

`host` can also do reverse IP lookups just like dig:

```shell
$ host -i 173.252.120.68

68.120.252.173.in-addr.arpa domain name pointer edge-star-mini-shv-12-frc3.facebook.com.
```

### A Little More Info

Sometimes we do want a little more information than just a sentence. The `-v` option is helpful here:

```shell
$ host -v donkeyrentals.com

Trying "donkeyrentals.com"
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 49015
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;donkeyrentals.com.		IN	A

;; ANSWER SECTION:
donkeyrentals.com.	900	IN	A	104.131.191.2

Received 51 bytes from 192.168.128.1#53 in 37 ms
Trying "donkeyrentals.com"
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 65416
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;donkeyrentals.com.		IN	AAAA

;; ANSWER SECTION:
donkeyrentals.com.	900	IN	AAAA	2620:0:861:ed1a::1

Received 63 bytes from 192.168.128.1#53 in 35 ms
Trying "donkeyrentals.com"
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 44277
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2

;; QUESTION SECTION:
;donkeyrentals.com.		IN	MX

;; ANSWER SECTION:
donkeyrentals.com.	900	IN	MX	10 aspmx.l.google.com.

;; ADDITIONAL SECTION:
aspmx.l.google.com.	35	IN	A	209.85.201.27
aspmx.l.google.com.	267	IN	AAAA	2607:f8b0:400d:c04::1a

Received 110 bytes from 192.168.128.1#53 in 38 ms
```

Wait a second! This looks very familiar. In fact, it looks like they're just using `dig`! That makes some sense because, again, the same company developed both. In this case, we could probably just stick with `dig`, but it's good to know we have this option if we want it.

### Why I Chose `dig` Instead

So, I like `host` enough to include a section about it. It feels nice to use sometimes when you want a quick answer, but I believe `dig` gives us more authentic information. It shows us in the response itself that something is an A record, or a CNAME, or NS, etc. This book is about learning those concepts, so it made the most sense to use `dig`. It's also the tool I see most used online in guides, tutorials, and Q&A sites. I hope familiarity with `dig` will help you continue to learn on your own after using this book.

However, `host` does pop up from time to time, and it can be a really nice alternative for something quick, but only when you first understand what it's telling you. `donkeyrentals.com has address 104.131.191.2` may look nice, but it doesn't give us a lot of information to work with.
