## WHOIS

Let's clear up one thing real fast: WHOIS in all caps is a protocol, while `whois` in all lowercase is a command line tool. They are related but not the same thing. The `whois` tool uses the WHOIS protocol to retrieve information about a domain. We'll be interacting with `whois` directly and WHOIS indirectly.

The information we get using `whois` is different for every domain. The most common and useful pieces include contact information for the person or company that registered the domain and/or the expiration date of that domain. The catch is that this information has no standard to it. It can be any information, in any format. As we'll see, this can make working with WHOIS incredibly annoying.

Let's take a look at a response. It's a long one:

```
Whois Server Version 2.0

Domain names in the .com and .net domains can now be registered
with many different competing registrars. Go to http://www.internic.net
for detailed information.

   Domain Name: DONKEYRENTALS.COM
   Registrar: TUCOWS DOMAINS INC.
   Sponsoring Registrar IANA ID: 69
   Whois Server: whois.tucows.com
   Referral URL: http://www.tucowsdomains.com
   Name Server: NS1.HOVER.COM
   Name Server: NS2.HOVER.COM
   Status: clientTransferProhibited https://www.icann.org/epp#clientTransferProhibited
   Status: clientUpdateProhibited https://www.icann.org/epp#clientUpdateProhibited
   Updated Date: 20-jan-2016
   Creation Date: 23-sep-2015
   Expiration Date: 23-sep-2016

>>> Last update of whois database: Wed, 20 Jan 2016 18:09:25 GMT <<<

For more information on Whois status codes, please visit
https://www.icann.org/resources/pages/epp-status-codes-2014-06-16-en.

NOTICE: The expiration date displayed in this record is the date the
registrar's sponsorship of the domain name registration in the registry is
currently set to expire. This date does not necessarily reflect the expiration
date of the domain name registrant's agreement with the sponsoring
registrar.  Users may consult the sponsoring registrar's Whois database to
view the registrar's reported date of expiration for this registration.

TERMS OF USE: You are not authorized to access or query our Whois
database through the use of electronic processes that are high-volume and
automated except as reasonably necessary to register domain names or
modify existing registrations; the Data in VeriSign Global Registry
Services' ("VeriSign") Whois database is provided by VeriSign for
information purposes only, and to assist persons in obtaining information
about or related to a domain name registration record. VeriSign does not
guarantee its accuracy. By submitting a Whois query, you agree to abide
by the following terms of use: You agree that you may use this Data only
for lawful purposes and that under no circumstances will you use this Data
to: (1) allow, enable, or otherwise support the transmission of mass
unsolicited, commercial advertising or solicitations via e-mail, telephone,
or facsimile; or (2) enable high volume, automated, electronic processes
that apply to VeriSign (or its computer systems). The compilation,
repackaging, dissemination or other use of this Data is expressly
prohibited without the prior written consent of VeriSign. You agree not to
use electronic processes that are automated and high-volume to access or
query the Whois database except as reasonably necessary to register
domain names or modify existing registrations. VeriSign reserves the right
to restrict your access to the Whois database in its sole discretion to ensure
operational stability.  VeriSign may restrict or terminate your access to the
Whois database for failure to abide by these terms of use. VeriSign
reserves the right to modify these terms at any time.

The Registry database contains ONLY .COM, .NET, .EDU domains and
Registrars.
Domain Name: DONKEYRENTALS.COM
Registry Domain ID: 1962822874_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.tucows.com
Registrar URL: http://tucowsdomains.com
Updated Date: 2015-09-23T18:00:04Z
Creation Date: 2015-09-23T18:00:04Z
Registrar Registration Expiration Date: 2016-09-23T18:00:04Z
Registrar: TUCOWS, INC.
Registrar IANA ID: 69
Registrar Abuse Contact Email: domainabuse@tucows.com
Registrar Abuse Contact Phone: +1.4165350123
Reseller: Hover
Domain Status: clientTransferProhibited
Domain Status: clientUpdateProhibited
Registry Registrant ID:
Registrant Name: Contact Privacy Inc. Customer 0141386251
Registrant Organization: Contact Privacy Inc. Customer 0141386251
Registrant Street: 96 Mowat Ave
Registrant City: Toronto
Registrant State/Province: ON
Registrant Postal Code: M6K 3M1
Registrant Country: CA
Registrant Phone: +1.4165385457
Registrant Phone Ext:
Registrant Fax:
Registrant Fax Ext:
Registrant Email: donkeyrentals.com@contactprivacy.com
Registry Admin ID:
Admin Name: Contact Privacy Inc. Customer 0141386251
Admin Organization: Contact Privacy Inc. Customer 0141386251
Admin Street: 96 Mowat Ave
Admin City: Toronto
Admin State/Province: ON
Admin Postal Code: M6K 3M1
Admin Country: CA
Admin Phone: +1.4165385457
Admin Phone Ext:
Admin Fax:
Admin Fax Ext:
Admin Email: donkeyrentals.com@contactprivacy.com
Registry Tech ID:
Tech Name: Contact Privacy Inc. Customer 0141386251
Tech Organization: Contact Privacy Inc. Customer 0141386251
Tech Street: 96 Mowat Ave
Tech City: Toronto
Tech State/Province: ON
Tech Postal Code: M6K 3M1
Tech Country: CA
Tech Phone: +1.4165385457
Tech Phone Ext:
Tech Fax:
Tech Fax Ext:
Tech Email: donkeyrentals.com@contactprivacy.com
Name Server: NS1.HOVER.COM
Name Server: NS2.HOVER.COM
DNSSEC: unsigned
URL of the ICANN WHOIS Data Problem Reporting System: http://wdprs.internic.net/
>>> Last update of WHOIS database: 2015-09-23T18:00:04Z <<<

Registration Service Provider:
    Hover, help@hover.com
    +1.8667316556
    http://help.hover.com


This domain's privacy is protected by contactprivacy.com. To reach the domain contacts,
please go to http://www.contactprivacy.com and follow the instructions.

The Data in the Tucows Registrar WHOIS database is provided to you by Tucows
for information purposes only, and may be used to assist you in obtaining
information about or related to a domain name's registration record.

Tucows makes this information available "as is," and does not guarantee its
accuracy.

By submitting a WHOIS query, you agree that you will use this data only for
lawful purposes and that, under no circumstances will you use this data to:
a) allow, enable, or otherwise support the transmission by e-mail,
telephone, or facsimile of mass, unsolicited, commercial advertising or
solicitations to entities other than the data recipient's own existing
customers; or (b) enable high volume, automated, electronic processes that
send queries or data to the systems of any Registry Operator or
ICANN-Accredited registrar, except as reasonably necessary to register
domain names or modify existing registrations.

The compilation, repackaging, dissemination or other use of this Data is
expressly prohibited without the prior written consent of Tucows.

Tucows reserves the right to terminate your access to the Tucows WHOIS
database in its sole discretion, including without limitation, for excessive
querying of the WHOIS database or for failure to otherwise abide by this
policy.

Tucows reserves the right to modify these terms at any time.

By submitting this query, you agree to abide by these terms.

NOTE: THE WHOIS DATABASE IS A CONTACT DATABASE ONLY.  LACK OF A DOMAIN
RECORD DOES NOT SIGNIFY DOMAIN AVAILABILITY.
```

Hello. Welcome to, like, three pages later.

There's a lot to this response, as we can see. Most of it is legal disclaimer because WHOIS information has been the source of a lot of legal trouble over the years. The act of publicly displaying a customer's personal information has (surprise!) caused a lot of problems.

There's also some meta-information about the servers that were contacted to get this information, and also some pseudo-advertisements. For the most part, you can ignore these.

Toward the middle is the information we're probably looking for: to whom the domain is registered and when it expires. This can give us leads for who to contact if there's a problem or when the domain might go up for sale.

### Different TLDs

Above is just one example of what a `com` domain will return but, as I said, each TLD is different. Here's a different response from a `gov` domain:

```shell
$ whois nasa.gov

% DOTGOV WHOIS Server ready
   Domain Name: NASA.GOV
   Status: ACTIVE

>>> Last update of whois database: 2016-01-20T19:12:13Z <<<
Please be advised that this whois server only contains information pertaining
to the .GOV domain. For information for other domains please use the whois
server at RS.INTERNIC.NET.
```

Much shorter! This is because there's no guide or specification that dictates what WHOIS information needs to include or how it should be formatted. What a great "standard" this is!

### Different WHOIS Servers

Another aspect to consider: since all this information is stored on different servers (all TLDs are run by different companies), occasionally we'll need to specify which server to use. For example, if we try to look up a `dentist` domain, we get:

```shell
$ whois donkey.dentist

whois: dentist.whois-servers.net: nodename nor servname provided, or not known
```

It can't find the right server. Luckily the [root zone database](https://www.iana.org/domains/root/db) list all TLDs and their WHOIS server info. Clicking on the dentist domain gives us a bunch of information about the TLD and, at the bottom, a WHOIS server: `whois.rightside.co`. Now we can make our WHOIS query using the `-h` option:

```
$ whois -h whois.rightside.co donkey.dentist

Domain not found.

...
```

Be right back. I need to go register a domain real quick.

### Multiple Domains

This is a tricky one, but sometimes `whois` isn't smart enough to figure out what you mean. For example, if you try to get WHOIS information for a popular domain:

```shell
$ whois google.com

Aborting search 50 records found .....
GOOGLE.COM.AFRICANBATS.ORG
GOOGLE.COM.ANGRYPIRATES.COM
GOOGLE.COM.AR
GOOGLE.COM.AU
GOOGLE.COM.BAISAD.COM
GOOGLE.COM.BEYONDWHOIS.COM
...
```

What is all this? Did we mistakenly type only a subdomain from `africanbats.org`? Unlikely. It seems like WHOIS just isn't that smart at figuring out what we mean. So how do we get the information for just `google.com`?

Maybe you tried this out yourself and saw this piece of text in the gigantic domain list:

>To single out one record, look it up with "xxx", where xxx is one of the
records displayed above. If the records are the same, look them up
with "=xxx" to receive a full display for each record.

But if we try that advice, one of two things happen. If we try surround it in quotes, we get the same result. If we use the `=` "trick" it shows us WHOIS information for _all_ of the domains on that list:

```shell
$ whois "=google.com"

Aborting search 50 records found .....
   Server Name: GOOGLE.COM.AFRICANBATS.ORG
   Registrar: TUCOWS DOMAINS INC.
   Whois Server: whois.tucows.com
   Referral URL: http://www.tucowsdomains.com


   Server Name: GOOGLE.COM.ANGRYPIRATES.COM
   IP Address: 8.8.8.8
   Registrar: NAME.COM, INC.
   Whois Server: whois.name.com
   Referral URL: http://www.name.com

...
```

This does get us the information we want, but come on. Really, WHOIS!? We don't want to see any of that. Can't we just get the single domain we asked for?

Turns out that if you prepend `domain` onto the front of the domain you want and put it all in quotes, this works:

```shell
$ whois "domain google.com"

Whois Server Version 2.0

Domain names in the .com and .net domains can now be registered
with many different competing registrars. Go to http://www.internic.net
for detailed information.

   Domain Name: GOOGLE.COM
   Registrar: MARKMONITOR INC.
   Sponsoring Registrar IANA ID: 292
   Whois Server: whois.markmonitor.com
   Referral URL: http://www.markmonitor.com
   Name Server: NS1.GOOGLE.COM
   Name Server: NS2.GOOGLE.COM

...
```

But fair warning here: this **doesn't work with all domains**. (There's no standard for WHOIS, remember? It can be anything! What a great syst–. Uhg, I can't finish that sentence with a straight face.)

There are alternatives, such as [jwhois](https://www.gnu.org/software/jwhois/), that a lot of people really like. There are also web-based tools that help get around these issues. I recommend using one of those instead.

---

Honestly, the more I look into WHOIS, the less I am a fan of it. It can be useful for checking to see if a domain is registered, but overall, it's a mess. The Internet Engineering Task Force (which wins the _Best Company Name In This Book_ award) and ICANN both [recognize](https://tools.ietf.org/html/rfc3912#section-5) that WHOIS is flawed and are [trying to replace it](https://www.icann.org/en/system/files/files/initial-report-24jun13-en.pdf).

Hopefully, we'll see this happen, but for now WHOIS is all we have.
