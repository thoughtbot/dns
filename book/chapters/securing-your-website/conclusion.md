## Wrapping Up

Time to update your résumé, LinkedIn profile, and MySpace page because now you can make your website secure! You sat through chapters about DNS records, technical domain name details, and my bad jokes, so of course you were able to master TLS and the bevy of acronyms found in this chapter.

So what's next, my donkey-renting pupil? Well, you can always learn more about security. [OWASP](https://www.owasp.org/) maintains a tons of information on current security threats, initiatives, and many other resources. [SSLLabs](https://www.ssllabs.com) has some great tools and guides to help you make sure your websites are secure and follow the best practices. They even have [a tool](https://www.ssllabs.com/ssltest/index.html) that will test and grade the security of any website.

A large part of security is keeping up to date with new patches and upgrades for the software you use. If you're using OpenSSL, I would suggest following the [their security vulnerabilities](https://www.openssl.org/news/vulnerabilities.html).

The [W3C](https://www.w3.org) has [lots of great](https://www.w3.org/2001/tag/doc/web-https) information about web security protocols and standards. Finally, if you're a regular to [Hacker News](https://news.ycombinator.com), any major security news inevitably pops up there.

Another good step is finding out what your operating system recommends for security. Any system worth using will have security updates, guides, and best practices. A quick search for `<your operating system> security` should return quite a bit.

Finally, as I noted previously, some people have been switching away from OpenSSL because of its shortcomings. If that sounds like your thing, here's that list again:

* [NSS](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS) by Mozilla.
* [s2n](https://github.com/awslabs/s2n) by [Amazon](https://blogs.aws.amazon.com/security/post/TxCKZM94ST1S6Y/Introducing-s2n-a-New-Open-Source-TLS-Implementation).
* [LibreSSL](http://www.libressl.org) by OpenBSD.
* [BoringSSL](https://boringssl.googlesource.com/boringssl/) by [Google](https://www.imperialviolet.org/2015/10/17/boringssl.html) (not recommended for public use).
