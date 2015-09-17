Registering a domain isn't the simplest process. Which like, duh that's probably why you bought this book. But it doesn't have to be rocket science either. Here are the common steps:

### Safely figure out if the domain is taken

Let's say we want the domain `petrock.net`. To register that name, we need to know if it's taken. We could go visit the domain in our web browser, but that isn't necessarily the whole story. Another way is to go to a domain registrar, type in the domain and see if it's taken or not. There's a catch though: Some registrars have [been caught](http://www.domainstate.com/industry-news-6/beware-dont-search-for-names-at-networksolutions-c-85864.html?s=) domain name front running. That is, registering a domain after someone has used their tools to search for it.

So how can we make sure that doesn't happen? We can skip the registrar all together by using the command line utility `whois`:

```shell
whois petrock.net
```

We can also use [Internic's WHOIS service](http://www.internic.net/whois.html). It supports `aero`, `arpa`, `asia`, `biz`, `cat`, `com`, `coop`, `edu`, `info`, `int`, `jobs`, `mobi`, `museum`, `name`, `net`, `org`, `pro`, and `travel` domains. Despite being updated in 2001 it continues to hold strong to the design aesthetic of the early 90s.

If we're trying to get WHOIS information for a domain that Internic doesn't support, we may have to use a special whois server. To do that visit the [Root Zone Database](https://www.iana.org/domains/root/db), find the top-level domain we're looking for, and see if they have a WHOIS server. I [looked up](https://www.iana.org/domains/root/db/dentist.html) the whois server for `dentist` domains, `whois.rightside.co`. We can use it with the `-h` option:

```
whois -h whois.rightside.co petrock.dentist
```

We'll get back a bunch of text, which can be anything really. There's no standard for what WHOIS needs to return. But usually we're looking for something like `No match for "EXAMPLE.COM"` or `No entries found` or something that in so many words says _We have no record of this domain so therefore it's open for registration._

### Find a Registrar

This is mostly a personal preference, but we'll need some kind of registrar for our domain. Here what I personally look for in a registrar:

#### Wide selection of TLDs

With so many TLDs like `com`, `io`, `co`, and `equipment` we want to make sure our registrar can handle it all. (If you're looking for a new business idea `petrock.equipment` is probably a good bet. But I'm just the idea guy, you'll have to run with it.) Whatever domains that we want to register, it's nice to be able to manage them all from one spot.

#### A nice control panel

This is super important, but harder to know before hand. Most sites will have a nice landing page but some can be hiding a crap control panel underneath. This is where we spend the bulk of our time with a registrar, so its worth looking in to. If we can find screenshots of the control panel or get a demo/trial that will help a lot. There's probably nothing _perfect_ out there, but if they look like they've never heard of a web designer, we may want to reconsider.

#### Other features

Many registrars offer other features besides just getting a domain name for you. Some offer email, or web hosting, or DNS management (technically separate from domain registration). Some offer one-click setup to get your domain pointing toward your favorite services. There are websites that just _give_ you a domain for free when you purchase their other services. Other websites will totally scam you. Note: This is not usually a desired feature.

It's hard to know exactly what you'll need in the future, but hopefully this gives you an idea of what to look for as you research.

### Buy the domain

Prices generally range from $6/year all the way up to $100+/year or more. Some registrars charge monthly for other niceties. There's no standard and they can charge (or not charge) whatever they want. There are some commonalities between many registrars however. Long existing domains like `com`, `net`, and `org` are usually pretty cheap where as newer or specialized domains like `luxury` , `pizza`, and `loans` generally cost more, similar to their real-world couterparts.

### WHOIS

After signing up for an account, filling out our credit card info, and agreeing to a terms of service we probably didn't read, we'll need to enter WHOIS information. WHOIS is a way to determine the current proprietor currently in control of a domain. It lists a phone number, email, and physical address among other pieces of information for an Administrator, Billing, and Technical contact.

We may not want to put that information on the internet, which is understandable. Many registrars offer what's called WHOIS privacy where they will list obscuring information such as _their_ contact info instead. This can be a nice alternative. One thing to keep in mind however is that this info can be used to determine who has rights to a domain, so if our info isn't there, it can be harder to prove that we own it.

For example, there was a registry who shut down because of corrupt leadership. One owner spent thousands of dollars of customer money on liposuction, escorts, and a chihuahua. As ridiculous as that sounds customers that had WHOIS privacy enabled couldn't prove that they had rights to their domains as the site slowly imploded. This is very much a worst cast scenario, but it's good to be aware of the potential downsides of WHOIS privacy.

### Name Servers

Now that we have a domain we'll need to point it somewhere. The first step is the Nameservers or NS records. We'll talk more in detail about NS records later, but for now just know that they are the first step in finding all things related to our domain. Wherever our nameserver points to, that's where all of our other records need to be.

Imagine someone is looking up our home address in an outdated address book. It might have been a valid address for us at one time, but it's since changed. That's no good. We'll have to make sure they look in a different, updated address book. This is similar to what would happen if someone looked up our domain at the wrong nameserver. The address book here is the nameserver, and each person is a record. Wrong nameserver, wrong records.

### Next steps

Now that we have a domain to play with, we can start talking about all the other configuration options available to us. SSL certificates, email, subdomains, etc. Right now, the most important thing we should be focused on is pointing our domain to our content or servers. That is done with DNS records, which is exactly what the next chapter is all about.
