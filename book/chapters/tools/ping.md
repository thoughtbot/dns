## ping & ping6

`ping` (and its sibling for IPv6 addresses, `ping6`) is a very simple tool, so this will be a short section. Its most common use case can be summed up as: "Are you there?" Although simple, this utility is useful in automated environments. Computers check to make sure other computers are awake, active, and receiving connections.

Its command line interface looks like this:

```shell
$ ping donkeyrentals.com

PING donkeyrentals.com (104.131.191.2): 56 data bytes
64 bytes from 104.131.191.2: icmp_seq=0 ttl=55 time=15.031 ms
64 bytes from 104.131.191.2: icmp_seq=1 ttl=55 time=21.293 ms
64 bytes from 104.131.191.2: icmp_seq=2 ttl=55 time=12.122 ms
64 bytes from 104.131.191.2: icmp_seq=3 ttl=55 time=12.928 ms
64 bytes from 104.131.191.2: icmp_seq=4 ttl=55 time=12.733 ms
^C
--- donkeyrentals.com ping statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 12.122/14.821/21.293/3.381 ms
```

For IPv6 addresses, `ping6` is the tool to use:

```shell
$ ping6 2620:0:861:ed1a::1

...
```

It will run forever unless instructed to stop by typing the `CTRL-C` interrupt character. To limit the number of times it runs, we use the `-c` flag to set a "count":

```
$ ping -c 5 donkeyrentals.com

...
```

We can mostly ignore the details of the response as they're not particularly important to us. If we run `ping` for an extended period of time, the statistics at the bottom have useful information. Included are percentage of packets lost and combined times that each request took.

But mostly what we're looking for is either a successful response:

```
64 bytes from 104.131.191.2: icmp_seq=0 ttl=55 time=15.031 ms
```

or a failure:

```
Request timeout for icmp_seq 0
```

We can ignore the successes, but failures require attention. Specifically, the site is **down** and we need to work on bringing it back up. `ping` is great for these kinds of monitoring tasks.

