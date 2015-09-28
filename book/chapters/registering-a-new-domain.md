Registering a domain isn't the simplest process. Which like, duh that's probably why you bought this book. But it doesn't have to be rocket science either. We'll need to figure out if our domain is taken, find a registrar (a company that can sell us a domain), buy the domain, and fill out our WHOIS information. Okay, it does sound a little complicated, so let's walk through all the steps.

### Step one – Figure out if the domain is already taken

Let's say we want the domain `petrock.com`. To register that name, we need to know if it's already taken. We could go visit the domain in our web browser and see if a website appears. But even if there's no website, that doesn't necessarily mean it's not registered. Another way is to go to a domain registrar, type in the domain and see if it's taken or not. There's a catch though: _domain name front running_. That is, when a company registers domains after people have used their search tools. Some registrars have [been caught](http://www.domainstate.com/industry-news-6/beware-dont-search-for-names-at-networksolutions-c-85864.html?s=) doing this very thing.

So how can we make sure that doesn't happen? We can skip the registrar all together by using the command line utility `whois`:

```shell
whois petrock.com
```

`whois` (pronouced "who is") is a tool for getting information about who has rights to a domain name. Notice I didn't mention ownership. No one ever actually owns a domain, we just get the ability to rent it for some amount of time. Confusingly, the protocol for getting WHOIS information is also called WHOIS but with uppercase letters. In summary: we can use `whois` to retrieve WHOIS information. Makes sense, right?

Using the command line tool isn't the only way, however. We can also use [Internic's WHOIS service](http://www.internic.net/whois.html). In spite of being updated in 2001, it continues to hold strong to the design aesthetic of the early 90s. It supports domains ending in `.aero`, `.arpa`, `.asia`, `.biz`, `.cat`, `.com`, `.coop`, `.edu`, `.info`, `.int`, `.jobs`, `.mobi`, `.museum`, `.name`, `.net`, `.org`, `.pro`, and `.travel`.

From now on, I'm not going to use the period for `com`, `net`, etc. It's hard to read and isn't totally. If you're curious, check out [TODO: relevant FAQ/appendix to be written].

If `petrock.com` is taken, we have to look for a different domain. Let's try `petrock.dentist` instead. If we're trying to get WHOIS information for a domain that Internic doesn't support, we'll have to use a special WHOIS server. To do that visit the [Root Zone Database](https://www.iana.org/domains/root/db), find the top-level domain we're looking for, and see if they have a WHOIS server. I [looked up](https://www.iana.org/domains/root/db/dentist.html) the whois server for `dentist` domains: `whois.rightside.co`. We can use it with the `-h` option with `whois`:

```
whois -h whois.rightside.co petrock.dentist
```

We'll get back a bunch of text. We're looking for something that in so many words says _We have no record of this domain so therefore it's open for registration._ There's no standard for what WHOIS needs to return. But generally we're looking for something like `No match for "EXAMPLE.COM"` or `No entries found`.

We'll fill out our own WHOIS information later on.

### Step two – Find a Registrar

Now that we know our domain is available, we need a registrar to help us get it. Picking a registrar is mostly a personal preference, here's what I personally look for:

#### Wide selection of top-level domains

With so many top-level domains (TLDs) like `com`, `io`, `co`, and `equipment` we want to make sure our registrar can handle all the domains we might want to register. (If you're looking for business ideas `petrock.equipment` sounds quite promising. But I'm just the idea guy, you'll have to run with it.) Whatever domains we want to register, we want to be able to manage them all from one spot, if possible.

#### A nice control panel

The control panel is where we will spend the most time with a registrar, so it's worth researching. This is super important, but harder to know beforehand. Most sites will have a nice landing page, but some may be hiding a crap control behind it. Ideally we can find screenshots of the control panel or get a demo/trial. There's probably nothing _perfect_ out there, but if it looks like the registrar has never heard of a web designer, we may want to reconsider.

#### Other features

Many registrars offer other features beyond getting a domain name for you. Some offer email, web hosting, or DNS management (technically separate from domain registration). Some offer one-click setup to get your domain setup with your favorite services. There are even websites that just _give_ you a domain for free when you purchase their other services. Other websites will totally scam you. (Note: This is not usually a desired feature.)

Most of these options are personal preference and none of them are critical. It's hard to know exactly what you'll need in the future, but hopefully this gives you an idea of what to look for as you research.

If you're a bit overwhelmed now and just want a suggestion, here are some of my favorites: [TODO: relevant FAQ/appendix list of registrars]

### Step three – Buy the domain

The price for a single domain can range from free, all the way up to $100+/year. Some registrars charge monthly for other niceties. There's no standard and they can charge (or not charge) whatever they want. There are some commonalities among registrars however. Long existing domains like `com`, `net`, and `org` are usually pretty cheap, while newer or specialized domains like `luxury` , `pizza`, and `loans` generally cost more, similar to their real-world counterparts.

### Step four – Complete WHOIS information

After signing up for an account, entering our credit card info, and agreeing to a terms of service we probably should read but didn't, we'll need to enter WHOIS information. It lists a phone number, email, and physical address among other pieces of information for an Administrator, Billing, and Technical contact.

#### Privacy vs legal concerns

We may not want to put that information on the internet, which is understandable. We could use non-personal email addresses, PO boxes, and fake phone numbers, but that sounds like a lot of work for a simple domain name. Many registrars offer what's called WHOIS privacy where they will list obscuring information such as _their_ contact info instead. This can be a nice alternative. One disadvantage is that this info can be used to determine who has rights to a domain, so if our info isn't there, it can be harder to prove that we own it.

For example, there was a registry which shut down because of corrupt leadership. One owner spent thousands of dollars of customer money on liposuction, escorts, and a chihuahua. As ridiculous as that sounds customers who had WHOIS privacy enabled couldn't prove that they had rights to their domains as the site slowly imploded. This is a worst case scenario, but it's important to be aware of the potential tradeoffs of WHOIS privacy.

### Next steps

Now that we have a domain to play with, we can start talking about all the other configuration options available to us. SSL certificates, email, subdomains, etc. Right now, the most important thing we should be focused on is pointing our domain to our content or servers. That is done with DNS records, which is exactly what the next chapter is all about.