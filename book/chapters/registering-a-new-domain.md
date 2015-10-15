Registering a domain isn't the simplest process. Which like, duh that's probably why you bought this book. But it doesn't have to be rocket science either. We'll need to figure out if our domain is taken, find a registrar (a company that can sell us a domain), buy the domain, and fill out our WHOIS information. Okay, it does sound a little complicated, so let's walk through all the steps.

### Step one – Figure out if the domain is already taken

Let's say we want the domain `donkeyrentals.com`. To register that name, we need to know if it's already taken. We could go visit the domain in our web browser and see if a website appears. But even if there's no website, that doesn't necessarily mean it's not registered. Another way is to go to a domain registrar, type in the domain and see if it's taken or not. There's a catch though: _domain name front running_. This happens when a company registers a domain as soon as someone has searched for it. Some registrars have [been caught](http://www.domainstate.com/industry-news-6/beware-dont-search-for-names-at-networksolutions-c-85864.html?s=) doing this.

So how can we make sure that doesn't happen? We can skip the registrar all together by using the command line utility `whois`:

```shell
$ whois donkeyrentals.com
```

`whois` (pronounced "who is") is a tool for retrieving information about who has rights to a domain name. Notice I didn't mention ownership. No one ever actually owns a domain, we're just renting it for some amount of time. Confusingly, the protocol for WHOIS information is also called WHOIS, but with uppercase letters. In summary: we can use `whois` to retrieve WHOIS information. Makes sense, right?

Using the command line tool isn't the only way. We can also use [Internic's WHOIS service](http://www.internic.net/whois.html) a site that continues to hold strong to the design aesthetic of the early 90's. The only caveat of the service is it only supports certain domains, mostly the more common domains such as `.com`, `.net`, `.org`, etc.

From now on, I'm not going to use the period for `com`, `net`, etc. It's hard to read and isn't technically accurate. If you're curious, check out [TODO: relevant FAQ/appendix to be written].

If `donkeyrentals.com` is taken, we have to look for a different domain. Let's try `donkeyrentals.dentist` instead. If we're trying to retrieve WHOIS information for a domain that Internic doesn't support, we'll have to use a special WHOIS server. So we go to the [Root Zone Database](https://www.iana.org/domains/root/db), find the top-level domain we're looking for, and see if they have a WHOIS server. I [looked up](https://www.iana.org/domains/root/db/dentist.html) the whois server for `dentist` domains: `whois.rightside.co`. We can either visit that site to look up our domain, or we can use the `whois` tool with the `-h` option:

```shell
$ whois -h whois.rightside.co donkeyrentals.dentist
```

Either way, we'll receive a bunch of text. There's no standard for what WHOIS returns, this could be any text. We're looking for text that in so many words says _We have no record of this domain so therefore it's open for registration._ Common ways to phrase this are: `No match for "EXAMPLE.COM"` or `No entries found`.

We'll fill out our own WHOIS information later on.

### Step two – Find a Registrar

Now that we know our domain is available, we need to rent it from a registrar. Picking a registrar is mostly a personal preference, here's what I personally look for:

#### Wide selection of top-level domains

With so many top-level domains (TLDs) like `com`, `io`, `co`, and `equipment` we want to make sure our registrar can handle all the domains we might want to register. (If you're looking for business ideas `donkeyrentals.equipment` sounds quite promising. But I'm just the idea guy, you'll have to run with it.) Whatever domains we want to register, we want to be able to manage them all from one spot, if possible.

#### A nice control panel

The control panel is where we will spend the most time with a registrar, so it's worth researching. This is super important, but harder to know beforehand. Most sites will have a nice landing page, but some may be hiding a crap control behind it. Ideally we can find screenshots of the control panel or use a demo/trial. There's probably no _perfect_ registrar out there, but if it looks like the registrar has never heard of a web designer, we may want to look elsewhere.

#### Other features

Many registrars offer features beyond domain name administration. Some offer email, web hosting, or DNS management (technically separate from domain registration). Some offer one-click configuration to set up your domain with your favorite services. There are even services that just _give_ you a domain for free when you purchase their other services. Others will totally scam you. (This is not usually a desired feature.)

Most of these options are personal preference and none of them are critical. It's hard to know exactly what you'll need in the future, but this gives you an idea of what to look for as you research.

If you're a bit overwhelmed now and just want a suggestion, here are some of my favorites: [TODO: relevant FAQ/appendix list of registrars]

### Step three – Rent the domain

The price for a single domain can range from free, all the way up to $100+/year. Some registrars charge monthly for other niceties. There's no standard, and they can charge (or not charge) whatever they want. There are some commonalities among registrars however. Long existing domains like `com`, `net`, and `org` are usually pretty cheap, around $10, while newer or specialized domains like `luxury` and `loans` generally cost more, similar to their real-world counterparts.

### Step four – Complete WHOIS information

After signing up for an account, entering our credit card info, and agreeing to a terms of service we probably should have read but didn't, we'll need to enter WHOIS information. It requires among other things a phone number, email, and physical address for an Administrator, Billing, and Technical contact.

#### Privacy vs legal concerns

We may not want to put that information on the internet, which is understandable. We could use non-personal email addresses, PO boxes, and fake phone numbers, but that sounds like a lot of work for a simple domain name. Many registrars offer a service called WHOIS privacy where they will list obscuring information such as _their_ contact info instead. This can be a nice alternative. One disadvantage is that this info can be used to determine who has rights to a domain, so if our info isn't there, it can be harder to prove that we own it.

For example, one registry shut down because of corrupt leadership. One owner spent thousands of dollars of customer money on liposuction, escorts, and a chihuahua. As ridiculous as that sounds customers who had WHOIS privacy enabled couldn't prove that they had rights to their domains as the site slowly imploded. This is a worst case scenario, but it's important to be aware of the potential tradeoffs of WHOIS privacy.

### Next steps

Now that we have a domain to play with, we can start talking about all the other configuration options available to us. SSL certificates, email, subdomains, etc. Right now, the most important task we should be focused on is pointing our domain to our content or servers. That is done with DNS records, which is exactly what the next chapter is all about.
