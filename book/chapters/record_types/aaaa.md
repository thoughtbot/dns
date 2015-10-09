### AAAA

Pronounced like screaming _"AAAAAHHHH!!!!"_, these records are _just_ like A records only they point to an IPv6 address instead. IPv6 addresses look something like this: `2620:0:861:ed1a::1`. Other than being longer and harder to type, they serve pretty much exactly the same function as IPv4; pointing our domain toward a server.

Here's an example configuration:

* **Hostname**: `@`
* **Record Type**: `AAAA`
* **IP Address**: `2620:0:861:ed1a::1`

```shell
$ dig donkeyrentals.com AAAA +short

2620:0:861:ed1a::1
```

As the internet [runs out](http://www.bbc.com/news/technology-19600718) of IPv4 addresses, IPv6 is becoming more and more important. Soon you might not even be able to use an IPv4.
