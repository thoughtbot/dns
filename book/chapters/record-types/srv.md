## SRV

SRV (service) records exist to make it easier to connect to a specific service on a specific port. By "service" I mean something other than a website, such as [Minecraft](https://minecraft.net). It uses SRV records to help players to connect to a multiplayer online Minecraft game by typing `play.donkeyrentals.com` instead of `92.112.56.78:9000`. SRV records can also provide server prioritization and load balancing. We'll get into all this below.

Our pretend Minecraft server runs on a machine just like our website does. We can contact it at an IP address `92.112.56.78` and on a specific port `9000`. Normally, players would have to enter that IP address and port number to connect to our server, but all those numbers are a pain to remember. Good thing DNS is, in fact, built to solve this problem.

Instead of an IP address, we'll have our players connect to the server at `play.donkeyrentals.com`. We'll need to set up an [A or AAAA record](#a) for the `play` hostname. We'll set up the SRV record next, but first we need to have a few pieces of information.

When defining how users connect to a service, each developer (in this case, Minecraft) defines certain aspects of the service, such as the **name** and **protocol**. The name for Minecraft is, unsurprisingly, `minecraft`, and the protocol is `tcp`. These pieces of data get an underscore in front of them. Put them together and we get: `_minecraft._tcp`.

Next, we add the first part of the domain we came up with earlier: `play`. This should not have an underscore and comes right after the protocol: `_minecraft._tcp.play`. Are you ready to set up the DNS record yet? Nope. Too bad! We still have two more things to talk about: **priority** and **weight**.

#### Priority and weight

Briefly: priority chooses one server over another and weight distributes the load between multiple servers.

Less briefly: If a service has more than one SRV record for primary and backup servers, **priority** is a way to specify that we want one server used before trying another. For example, normally we want people to just use the primary server. But if it's offline, we can use the backup server instead. We'll start with the lowest number and work our way up until a server responds. Because of this "lowest first" mechanism, priority is often called distance or preference. Priority is a number between 0 and 65535, in case you're a rich person and have 65,000+ servers.

**Weight** is similar, but works differently. Just like priority, it's a number between 0 and 65535. Instead of a server getting used before another, the load will spread out according to the weight value. Weight only applies when there are two or more SRV records with the same priority.

Imagine we have two containers of different sizes for collecting water. They're both perfectly fine containers that we can use at the same time (same priority) but `bucket` is twice the size of `cup`. When we fill them both to capacity, we'll put two drops of water in `bucket` for every drop we put in `cup`. So the **weight** for `bucket` will be `2` and `cup` will be `1`. This is how weights in SRV records work, except instead of drops of water, it's connections to the server. (Water is not great for servers.)

Ok, _now_ we can set up our SRV record:

* **Hostname**: `_minecraft._tcp.play`
* **Record Type**: `SRV`
* **Priority**: `1`
* **Weight**: `1`
* **Port**: `9000`
* **Value**: `play.donkeyrentals.com`

```shell
$ dig +short _minecraft._tcp.play.donkeyrentals.com SRV

1 1 9000 play.donkeyrentals.com.
```

Note the `play` in the **Hostname** relates to the `play` in the **Value**. It isn't always the case that these match up, but it's common. The important part is whatever users type to get to your server (e.g. `play.donkeyrentals.com`), the first part must match up to the last part of the **Hostname**.

In this example, I chose `1` for the **Priority** and **Weight** because, when we only have one server, it doesn't matter which one gets picked first or how often it's used.

This isn't the only way to set up an SRV record, as they can vary widely by service. We'll want to check the documentation from the provider (e.g., Minecraft) to make sure we've set ours up the right way.
