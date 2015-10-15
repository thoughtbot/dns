### AAAA

These records are the same as A records with one exception: they point to an IPv6 address instead of an IPv4. IPv6 addresses look something like this: `2620:0:861:ed1a::1`. Other than being longer and harder to type, they serve the same function as IPv4; to be an address for our server. Technically, these are pronounced as "_quad-A_" records, but I always scream "_AAAAAHHHH!!!!_" in my head.

Here's an example configuration:

* **Hostname**: `@`
* **Record Type**: `AAAA`
* **IP Address**: `2620:0:861:ed1a::1`

```shell
$ dig donkeyrentals.com AAAA +short

2620:0:861:ed1a::1
```

As the internet [runs out](http://www.bbc.com/news/technology-19600718) of IPv4 addresses, IPv6 is becoming more and more important. Soon you might not even be able to use an IPv4.
