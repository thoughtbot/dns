## Be Prepared

So what do we need before we setup a TLS certificate on our website?

### A Certificate Authority

We talked about this in the previous section, but this is who you will buy your certificate from. There are many certificate authorities to choose from; searching for `buy SSL certificate` will find plenty. Some to check out are:

* [Comodo](https://ssl.comodo.com/comodo-ssl-certificate.php)
* [DigiCert](https://www.digicert.com/welcome/ssl-plus.htm)
* [RapidSSL](https://www.rapidssl.com) (one of the least expensive paid CAs I've found)

And one that offers free DV certs:

* [Let's Encrypt](https://letsencrypt.org)

One thing you'll notice when shopping around is paid certificates are often much more expensive than domain names. For example, the certificate for donkeyrentals.com cost $230.85 for three years, or $76.95 per year. The domain cost $13.17 for one year. Security can be expensive.

That said, there are free alternatives like Let's Encrypt if you only need a DV certificate. "How is Let's Encrypt free?" I hear you asking. Well, they are funded by [a bunch of tech companies](https://letsencrypt.org/sponsors/) to promote the adoption of digital certificates. I'm not head-over-heels for Let's Encrypt yet because they're a bit too new for my taste. Their public beta started in December 2015 (I'm writing this chapter in early 2016), so I'd like to give them some time to prove themselves before I support them whole-heartedly, although from what I've seen so far, the service is very promising.

### OpenSSL

[OpenSSL](https://www.openssl.org) is software that implements these TLS standards we've been talking about. OpenSSL has a ton of functionality, and we're going to use it to generate our server keys, create our certificate signing request (CSR), and debug our certificate.

Make sure the `openssl` tool is [installed](#installing-tools) before continuing. It's often (but not always) installed on Unix/Linux systems. You'll probably have to install or update it on Windows and Mac OS X. Open up a terminal or command line and type `openssl version`. If you get something like `OpenSSL 1.0.2g  1 Mar 2016`, you're all set. If not, you'll need to install it. If you have an old version, I'd recommend updating it.

Also, I'll note here that OpenSSL has been the cause of some security bugs in the last couple of years. Since it is a very popular implementation of TLS standards, any bug found is able to be exploited across a large number of websites. You may have heard of [heartbleed](http://heartbleed.com), a bug that allow hackers to access server data, including the server's _private key_. Like any piece of software, this is one of many bugs that happen in the course of development. Unlike any piece of software, bugs in OpenSSL are more extreme because they can jeopardize server and customer security.

Because of these bugs, other companies have started to make their own implementations:

* Mozilla has created [NSS](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS).
* [Amazon](https://blogs.aws.amazon.com/security/post/TxCKZM94ST1S6Y/Introducing-s2n-a-New-Open-Source-TLS-Implementation) is taking a stab at modernizing OpenSSL with [s2n](https://github.com/awslabs/s2n).
* OpenBSD created [LibreSSL](http://www.libressl.org).
* Google [created](https://www.imperialviolet.org/2015/10/17/boringssl.html) a version called [BoringSSL](https://boringssl.googlesource.com/boringssl/), but they don't recommended it for public use.

If you'd rather use these, then great! However, for the rest of this book I'm going to be using OpenSSL commands. Make sure you translate any commands as necessary if you're going to follow along with a different tool.

### A Common Name

This is the full domain that we'll be securing. I say "full" because, for a certificate, just as in DNS, `www.donkeyrentals.com` and `donkeyrentals.com` are different. If you're purchasing a wildcard certificate, this will probably be the equivalent of `*.donkeyrentals.com` to cover all first level subdomains. For a single DV certificate, you'll have to pick your apex domain or a subdomain. This could be `www.donkeyrentals.com`, or `secure.donkeyrentals.com`, or `donkeyrentals.com`, etc. You can't change this without getting another certificate, so choose wisely.

### A Web Server

This might seem obvious, but the web server that you use matters quite a bit. If you're setting a web server up manually, it's likely that you're using Apache, Nginx, or IIS. Any web server worth using supports TLS certificates. You'll also need access to the configuration files of these web servers.

If you're using shared hosting (Dreamhost, Bluehost, etc.) or a service (Tumblr, Squarespace, Shopify, etc.) to host your website, check with that service to make sure they support TLS/SSL and allow you to configure enough of your web server to set up a certificate. Some do, some don't. Some have restrictions on the kinds of certificates you can use or how you use them. Some only let you configure a small part of your web server. I can't give any more advice here than to contact the service or do some very extensive research to find out what the restrictions might be.
