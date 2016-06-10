## AAAA

These records are the same as A records, but with one exception: they point to an IPv6 address instead of an IPv4. IPv6 addresses look something like this: `2620:0000:0861:ed1a:0000:0000:0000:0001`. That's eight sets of four hexadecimal digits, which is way too long. However, they can be severely shortened: `2620:0:861:ed1a::1`.

Here's how to shorten your very own IPv6 address:

* Drop the leading zeros in each section: `2620:0:861:ed1a:0:0:0:1`
* Replace consecutive groups of all zeros with two colons: `2620:0:861:ed1a::1`

Also:

* If there are more than one group of all zeros, replace the longest group.
* If other groups are the same length, replace the left-most group.

Other than being longer and harder to type, they serve the same function as IPv4: to be an address for our server. Technically, these are pronounced as "_quad-A_" records, but I always scream "_AAAAAHHHH!!!!_" in my head.

Here's an example configuration:

* **Hostname**: `@`
* **Record Type**: `AAAA`
* **IP Address**: `2620:0:861:ed1a::1`

```shell
$ dig +short donkeyrentals.com AAAA

2620:0:861:ed1a::1
```

As the internet [runs out](http://www.bbc.com/news/technology-19600718) of IPv4 addresses, IPv6 is becoming more important. Soon you might not even be able to use an IPv4 address.

If you want to visit these addresses in your browser, surround them with brackets: `http://[2620:0:861:ed1a::1]`. This should work for any length of IPv6 address. In practice I found that these urls are often blocked or not recognized, so your mileage my vary. If they don't work for you, ask around to see if someone can try the address for you.
