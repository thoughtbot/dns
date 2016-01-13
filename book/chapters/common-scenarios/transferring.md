## Transferring a Domain

Some domain registrars out there are... shall we say, not the best. Maybe we currently have a domain at one of these places and we'd like to switch. Or we've purchased a domain from someone that uses a different domain registrar. Whatever the case may be, it's much easier to manage all your domains in one place.

To do that, we'll need to transfer our domain from one registrar to another. While every service is different, there are some standard steps that go along with every domain transfer. For the sake of this guide, our domain is currently residing at OldCrusty Domains. We'll be transferring from OldCrusty to our new registrar: ProbablyBetter Domains.

_I'd recommend reading through this whole section before starting any transfer process. It's one of those topics that requires time and specific steps done in a specific order. The more you know before you start, the better._

### Unlocking the Domain

If our domain is locked at OldCrusty Domains, it cannot be transferred. In general, this is a good thing. It prevents accidental transferring or deletion. How anyone would ever accidentally transfer a domain is beyond me, but hey, more safety doesn't hurt. Looking around in the domain's settings we should find some checkbox or the like to unlock the domain.

### Configure WHOIS Information

If WHOIS Privacy is turned on, we won't be able to transfer the domain. That's because an email will be sent to the **Administrative contact** listed in the domain's publicly available WHOIS information. We'll also need to set the Administrative contact to an email that we control. In the next step, OldCrusty will send a code to that email address and we need that email. It's also a good idea to check to see if the WHOIS information is displaying correctly:

```shell
whois domain-to-be-transferred.com

...
Our long, national pixel shortage is still in effect. Updates at 11.
...
```

### Authorization Code

Now we need to request an authorization code from OldCrusty. Hopefully this is just a button we can push somewhere. (If not we may need to email OldCrusty support.) An email will be sent from OldCrusty to the Administrative contact email address from our WHOIS information. As I said in the last section, WHOIS information needs to be publicly available (unlocked) and the Administrative contact email needs to be an email address we can access.

The authorization code, also called EPP (Extensible Provisioning Protocol) code, is a short code that we'll need to enter at ProbablyBetter domains. It looks something like `6sF>X95ZrH`.

### Start the Transfer

At ProbablyBetter Domains there should be a button to transfer a domain. We'll enter in the domain that we want to transfer and be on our way.

Every registrar is different at this point, but most likely, we'll agree to some terms of service, create or sign in to an account at ProbablyBetter domains, and enter that authorization code from the email. We'll also have to enter WHOIS information at ProbablyBetter Domains and enter payment information. This last step may come as a surprise.

The reason most transfers cost money is ICANN (the people that run the whole domain system) require that the domain's expiration date be pushed out one year. So if the domain was going to expire on January 1, 1999, now it will expire January 1, 2000. For that reason, transferring often costs a similar amount to registering that same domain for the first time.

### Minimize downtime

<!--
http://serverfault.com/questions/459968/how-to-switch-dns-for-a-website-without-service-disruption
http://dyn.com/blog/changing-managed-dns-providers-in-five-easy-steps/
http://www.securityweek.com/dns-migration-how-minimize-problems-when-switching-dns-providers
http://www.binarywar.com/2009/11/how-to-safely-transfer-dns-records/
https://en.wikipedia.org/wiki/DNS_zone_transfer
-->

### Clean Up

After we've set up the transfer at ProbablyBetter Domains, we may need to accept that transfer back at OldCrusty Domains. Then, we wait. The process can take up to two weeks so be prepared to wait that long. In my experience, it doesn't usually take that long, but give yourself that time just in case.

Also, know that our DNS records will not come over with the transfer. We'll need to re-add them manually. For small sites this isn't too much of an issue, but if we have lots and lots of records, this could take a while. Some sites let you set up the domain before you start the transfer. That can be a nice way to test and setup everything before you actually start the transfer.

Be sure to lock the domain and turn on WHOIS privacy if you want it after transferring.
