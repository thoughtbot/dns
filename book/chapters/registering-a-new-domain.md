Registering a domain isn't the simplest process. Which, like, duh, that's probably why you bought this book. But it doesn't have to be rocket science either. We need to figure out if our domain is taken, find a registrar (a company that can sell us a domain), buy the domain, and, finally, fill out our WHOIS information. Okay, it does sound a little complicated, so let's walk through each of the steps.

### Step One – Figure Out if the Domain Is Already Taken

Let's say we want the domain `donkeyrentals.com`. To register that name, we need to know if it's already taken. We could go visit the domain in our web browser and see if a website appears, but even if there's no website, that doesn't necessarily mean it's not registered. Another way is to go to a domain registrar, type in the domain, and see if it's taken. There's a catch, though: _domain name front running_. This happens when a company registers a domain as soon as someone has searched for it. Some registrars have [been caught](http://www.domainstate.com/industry-news-6/beware-dont-search-for-names-at-networksolutions-c-85864.html?s=) doing this.

To make sure that doesn't happen, skip the registrar altogether by using the command line utility `whois`:

```shell
$ whois donkeyrentals.com
```

`whois` (pronounced "who is") retrieves information about who has rights to a domain name. Notice I didn't mention ownership of a domain name. No one ever actually owns a domain. We're just leasing it for a certain amount of time. To confuse things even further, the protocol used by whois to get its information is also called WHOIS, but with uppercase letters. In summary: we can use `whois` to retrieve WHOIS information. Makes sense, right?

Using the command line tool isn't the only way. We can also use [Internic's WHOIS service](http://www.internic.net/whois.html), a site that continues to hold strong to the design aesthetic of the early 1990s. The only caveat of the service is it only supports certain domains, mostly the more common ones such as `.com`, `.net`, and `.org`.

From now on, I'm not going to use the period for common domains since it's hard to read and isn't technically accurate, so you'll see `com`, `net`, etc. instead.

If `donkeyrentals.com` is taken, we need to look for a different domain, so let's try `donkeyrentals.dentist` instead. If we're trying to retrieve WHOIS information for a domain that Internic doesn't support, we have to use a special WHOIS server. So we go to the [Root Zone Database](https://www.iana.org/domains/root/db), find the top-level domain we're looking for, and see if they have a WHOIS server. For this step, I [looked up](https://www.iana.org/domains/root/db/dentist.html) the whois server for `dentist` domains and found `whois.rightside.co`. We can either visit that site to look up our domain, or we can use the `whois` tool with the `-h` option:

```shell
$ whois -h whois.rightside.co donkeyrentals.dentist
```

However, using either method returns a bunch of text. Because there is no standard for what WHOIS returns, this could be any text. We're looking for text that, in so many words, says _We have no record of this domain so therefore it's open for registration._ Common ways to phrase this are: `No match for "EXAMPLE.COM"` or `No entries found`.

We'll fill out our own WHOIS information later on.

### Step Two – Find a Registrar

Now that we know our domain is available, we need to lease it from a registrar. Picking a registrar is mostly a personal preference, so here's what I look for:

#### Wide selection of top-level domains

With so many top-level domains (TLDs) like `com`, `io`, `co`, and `equipment`, available, we have to make sure our registrar can handle all the domains we might want to register. (If you're looking for business ideas, `donkeyrentals.equipment` sounds quite promising. But I'm just the idea guy, so you'll have to run with it.) Whichever domains we want to register, we need to be able to manage them all from one spot if possible.

#### A nice control panel

The control panel is where we will spend the most time with a registrar, so it's worth researching. This is super important, but harder to know beforehand if the control panel is good before you sign up with that registrar. Most sites will have a nice landing page, but some may be hiding a crap control behind it. Ideally, we can find screenshots of the control panel or use a demo/trial. There's probably no _perfect_ registrar out there, but if it looks like the registrar has never heard of a web designer, we may have to look elsewhere.

#### Other features

Many registrars offer features beyond domain name administration. Some offer email, web hosting, or DNS management (which is technically different from domain registration). Some offer one-click configuration to set up your domain with your favorite services. There are even services that just _give_ you a domain for free when you purchase their other services. Others will totally scam you (this is not usually a desired feature).

Most of these options are personal preferences, but none of them are critical. It's hard to know exactly what you'll need in the future, but this gives you an idea of what to look for as you research.

If you're a bit overwhelmed now and just want a suggestion, [here are some of my favorites](#recommended-registrars).

### Step Three – Lease the Domain

The price for a single domain ranges from free all the way up to $100+/year. Some registrars charge monthly for other niceties like [WHOIS privacy](#privacy-vs-legal-concerns), email, or website hosting. There's no standard, so they can charge (or not charge) whatever they want. There are some commonalities among registrars, however. Long-existing domains like `com`, `net`, and `org` are usually pretty cheap--around $10--while newer or specialized domains such as `luxury` and `loans` generally cost more, just like their real-world counterparts.

### Step Four – Complete WHOIS Information

After signing up for an account, entering the credit card info, and agreeing to a terms of service we probably should have read but didn't, we need to enter WHOIS information, including, among other things, a phone number, email, and physical address for administrator, billing, and technical contacts.

#### Privacy vs legal concerns

We may not want to put sensitive information on the internet, which is understandable. We could use non-personal email addresses, PO boxes, and fake phone numbers, but those sound like a lot of work for a simple domain name. Many registrars offer a service called WHOIS Privacy that lists obscuring information such as _their_ contact info instead. This can be a nice alternative, but the same info can also be used to determine who has rights to a domain, so if our info isn't there, it can be harder to prove that we own it.

In one case, a registry shut down because its owner spent thousands of dollars of customer money on liposuction, escorts, and a chihuahua. As ridiculous as this sounds, customers who had WHOIS Privacy enabled couldn't prove that they had rights to their domains as the site slowly imploded. This is a worst case scenario, but it's important to be aware of the potential tradeoffs of WHOIS privacy.

### Next Steps

Now that we have a domain to play with, we can start talking about all the other configuration options available to us, such as SSL certificates, email, and subdomains. Right now, the most important task we should be focused on is pointing our domain to our content or servers. That is done with DNS records, which is exactly what the next chapter is all about.
