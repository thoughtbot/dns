**A Record**

An A record or _address record_ is a DNS record type that points a hostname to an _IPv4_ address. Example:

* **Hostname**: `www`
* **IP Address**: `12.34.56.78`

See the section on A records to learn more.

**AAAA Record**

An AAAA record or _quad-A record_ is a DNS record type that points a hostname to an _IPv6_ address. Example:

* **Hostname**: `www`
* **IP Address**: `2620:0:861:ED1A::1`

Note that this IP address example is shortened. See the section on AAAA records to learn more about shortened IPv6 addresses.

**ALIAS Record**

A non-standard record type first used at [DNSimple](https://support.dnsimple.com/articles/alias-record/). It allows CNAME-like redirections on the apex domain, which is not normally allowed. For example, `donkeyrentals.com` could point to `myapp.herokuapp.com` instead of an IP address. Normally, this would need to be done with `www.donkeyrentals.com`.

See the section on ALIAS or ANAME records for more information.

**ANAME Record**

See _Alias Record_

**Apex Domain**

The domain without anything before it. Example: `donkeyrentals.com` but not `www.donkeyrentals.com` or `magical.donkeyrentals.com`.

**Bare domain**

See _Apex Domain_.

**BIND**

Short for _Berkeley Internet Name Domain_, this suite of software is made to run DNS servers. It is widely used across the industry. The BIND software suite includes tools used in this book such as `dig`, `host`, `nslookup`, and many others. More information can be found on BIND's website: [https://www.isc.org/downloads/bind/](https://www.isc.org/downloads/bind/)

**ccTLD**

Country Code Top-level Domains are domains representing a country. Examples include `io` (Indian Ocean), `bz` (Belize), and `fi` (Finland). Some ccTLDs have prerequisites for registration but for the most part, anyone can register a domain at any ccTLD.

See also: _TLD_.

**Certificate Authority (CA)**

Companies that issue certificates. This is where you go to upload a certificate signing request (CSR) and get back a certificate. Examples of these are Comodo, DigiCert, and RapidSSL.

**CNAME Record**

Cannonical Name records or _CNAME records_ are a DNS record type that point a hostname to a domain name, as opposed to an IP address. Example:

* **Hostname**: `redirect`
* **Target Host**: `rabbitrentals.com`

Note: these cannot be used on the apex domain. In the example above, this would point `redirect.donkeyrentals.com` to `rabbitrentals.com`. You cannot use a CNAME to point `donkeyrentals.com` in the same way.

**Common Name**

In regards to TLS certificates, the common name (or CN) is the "place" that the certificate is securing. For example, a certificate for `donkeyrentals.com` will have `donkeyrentals.com` as its common name. The domain being visited and the common name much match exactly. If they don't, it will cause a security warning when a user visits the site.

Wildcard certificates are used if multiple subdomains need to be secure. In this case, the common name can use the `*` character to specify all subdomains, e.g. `*.donkeyrentals.com`. Now users can visit any subdomain such as `secure.donkeyrentals.com` or `www.donkeyrentals.com` and the certificate will be valid.

**dig**

An abbreviation for _domain information groper_, this is a utility used to ask questions and receive answers from DNS servers about their records. For example, we can see the value of the A record for `donkeyrentals.com` with the following command:

```shell
$ dig donkeyrentals.com A
```

Dig is included in the _BIND_ suite of software DNS utilities. It is similar to the _host_ tool, but is far more verbose and explicit.

See also: _BIND_, _host_, _nslookup_.

**DNS**

Short for (the) Domain Name System, the whole network of servers holding records that point to other records or servers. See the rest of this book for more information.

**Domain Name Front Running**

Often, registrar websites will let you search to see if a domain is already taken. You type in the domain name and the registrar says "Taken, sorry." or "It's available! Would you like to register?" If you choose not to register, this domain name should just continue being unregistered until a customer comes along and grabs it.

But some malicious registrars will actually register the domain after it's been searched for, then sell it back to you for a higher price. The nerve! This is domain name front running.

**FQDN**

A fully qualified domain name, which contains all _hostnames_ (including the root zone) combined and separated with a period. Since the root zone does not have any text associated with it like `com`, a FQDN ends with a period.

Example: `shop.donkeyrentals.com.`

**gTLD**

Generic Top-level Domains are, for the most part, domains that are not associated with a country. Examples include `com` (commercial), `org` (organizations), and `dentist` (dental practices). Some gTLDs have prerequisites for registration but for the most part, anyone can register a domain at any gTLD.

See also: _TLD_.

**host**

Host is a tool in the _BIND_ suite of software used to ask questions and receive answers from DNS servers about their records. For example, we can see the value of the A record for `donkeyrentals.com` with the following command:

```shell
host -t A donkeyrentals.com
```

It is similar to _dig_ but attempts to have a much more succinct and readable output.

See also: _BIND_, _dig_, _nslookup_.

**Hostname**

Each individual part of a domain. For example: in `food.donkeyrentals.com`, the hostnames are `food`, `donkeyrentals`, and `com`. Putting these together with dots in between creates a domain.

**ICANN**

The Internet Corporation for Assigned Names and Numbers plays a large part of running the internet as a whole. They run the root name servers where all of the TLDs are found. They also police misbehaving registries, decide what TLDs are allowed to be added, and assign IPv4 and IPv6 addresses.

**InterNIC**

This stands for Network Information Center, with the Inter- prefix presumably for the internet. In the early days of the internet, (1972–1990ish) they handled domain registrations for `com`, `edu`, `gov`, `mil`, `net`, `org`, and `us` domains. InterNIC is now part of ICANN.

**IPv4**

Short for Internet Protocol version 4, this protocol defines addresses as a sequence of four integers (0–255) separated by periods. Examples include `1.2.3.4`, `127.0.0.1`, and `273.115.5.53`.

**IPv6**

Short for Internet Protocol version 6, this protocol defines addresses as a sequence of eight groups of four hexadecimal digits (0–FFFF), separated by colons. Examples include `2620:0000:0861:ED1A:0000:0000:0000:0001` and `2620:0:861:ED1A::1`.

Some IPv6 addresses can also be shortened significantly, as seen in the second example above. See the section in the book on AAAA records to learn more.

**MX Record**

An MX record or _mail exchange record_ is used to route email requests to mail servers. It has an additional priority property which allows multiple records for the same hostname to point to different servers and act as a backup. For example, a record with the priority of `10` will be used before a record with the priority of `20`.

**Nameserver**

The server which stores all DNS records for a particular domain. Think of this as a phonebook where DNS records are listed, instead of people. You can only find the records you're looking for if you look in the right phonebook.

**nslookup**

Short for nameserver lookup, this is a tool used to ask questions and receive answers from DNS servers about their records. Included in the _BIND_ suite of utilities, it is currently deprecated in favor of `dig` and `host`. While it can be used similarly to those tools, it also has an interactive mode:

```shell
$ nslookup
> set type=A
> donkeyrentals.com
```

See also: _BIND_, _dig_, _host_.

**NS Record**

A NS record or _nameserver record_ points to the server that holds all other DNS records for a particular domain.

See also: _Nameserver_.

**PKI**

Public key infrastructure. The system we (the internet) has agreed on to set up and maintain secure certificates. Kind of like how society decided we should fund the government so we use the system of taxes. This system is used by browsers, servers, certificate authorities, and more to ensure we all have safe, secure browsing experiences.

**Private Key**

A long, unique string of random looking numbers and letters that represents someone or something. Maybe that thing is a server, or a website, or your computer. Imagine a physical lock and a key. In public key encryption, the _public key_ is the lock and the _private key_ is the key. Confusing terms, yes, but that's more or less how it works. Never give you private key out or make it visible to the world.

**Public Key**

As opposed to a _private key_, this is a different long, unique string of random looking numbers and letters that represents someone or something. Feel free to give this out to anyone; it does not have to be private. Putting this somewhere else (like a server) usually gives you access, so long as you have the matching _private key_.

**Public-key Encryption**

See _Public-key Cryptography_

**Public-key Cryptography**

The system for creating private and public keys. Imagine some crazy math that can take input like `admin@donkeyrentals.com` and spit out two files of garbage (public and private key). We use these keys as a form of security, which works well even if we don't understand the crazy algorithms behind encryption.

**Quad-A Record**

See _AAAA Record_

**ping**

A tool that makes a simple request to a server with an IPv4 address and returns how long that request took (among other things). It's a useful tool for checking to see if a server is up because if the server is down, it will respond saying the ping timed out.

**ping6**

Just like its sibling _ping_ but uses IPv6 addresses instead.

**Registrar**

This is a company whose job it is to keep records on behalf of customers. As a customer, you talk to the registrar to lease a domain.

**Registry**

A registry manages one or more top-level domains, like `com`, or `co.uk`, or `dentist`. They communicate with registrars to lease domains to customers. Registries themselves do not interact with the general domain-buying public.

**Reverse DNS (RDNS)**

Reverse DNS. This is when you try to get a domain name from an IP address. You can try this easily with dig:

```shell
$ dig +short -x 66.220.158.68

edge-star-mini-shv-07-frc3.facebook.com.
```

**Root domain**

See _Apex domain_.

**Root zone**

The top level of the DNS hierarchy. Similar to how the `donkeyrentals.com` nameserver records are located at the `com` registry, `com`'s nameserver records are located at the registry called the root zone.

There are thirteen root domains (`a.root-servers.net` through `m.root-servers.net`) which represent many servers (500+) around the globe.

**SRV Record**

An SRV record or _service record_ is used to make a specific connection to an IP address using a specific port. Services might include a CalDAV, XMPP, or Minecraft server, among many others.

SRV records also offer two other attributes: priority and weight. When multiple requests are made to the service, they are sent to servers with lower-numbered priority first. When multiple servers have the same priority, requests are distributed across them according to their weight.

**SSL**

Secure sockets layer. This protocol was replaced by _TLS_ (Transport Layer Security) but is still commonly referred to when speaking about secure certificates. Thanks everyone for making it so confusing.

**Subdomain**

A domain that is part of another domain. Example: `shop.donkeyrentals.com` is a subdomain of `donkeyrentals.com` which is a subdomain of `com`. A subdomain is also technically a domain, and all domains (except for the root zone) are technically subdomains. Use subdomain when talking specifically about a domain that is defined by its parent domain.

> Welcome to donkeyrentals.com! Visit our shop at the subdomain shop.donkeyrentals.com.

**TLD**

Top-level Domain. These are the last part of a domain. These include generic TLDs: `com`, `org`, and `dentist`, and country code TLDs: `uk`, `dj`, and `io`.

See the IANA's [Root Zone Database](https://www.iana.org/domains/root/db) for a full list of TLDs.

**TTL**

Short for _time-to-live_, the amount of time left until a DNS record is re-fetched from its authoritative source. I.e. when the records cache will expire.

By the way, _live_ rhymes with _give_ not _dive_, as in "This is how long the data will live."

**TXT Record**

Text records are for storing arbitrary data with a hostname. Example:

* **Hostname**: `message`
* **IP Address**: `Hello`

This may seem like a trivial example, and it is. However real world use cases do exist, such as verifying an email server, or providing proof of ownership for a TLS record.

**WHOIS**

A protocol and tool that retrieves information about who is in control of a domain name. Confusingly, the protocol (WHOIS) and the tool (`whois`) are different: `whois` uses the WHOIS protocol to get domain information.

Basic usage:

```shell
$ whois donkeyrentals.com
```

**X.509**

X.509 is a list of standards that specify public key certificates, certificate revocation lists, attribute certificates, and a certification path validation algorithm. It's like being in a secret club but instead of building a treehouse, you agree to use certain methods to create and structure certificates and how to communicate with certificate authorities. TLS/SSL uses X.509 certificates.

This is opposed to a model like PGP where you get together with all your nerdy friends and sign each others certificates. X.509 certificates rely on being signed by global certificate authorities to be valid, among other formatting requirements.
