## Transferring a Domain

Some domain registrars out there are... shall we say, not the best. Maybe we currently have a domain at one of these places, and we'd like to switch. Or we've purchased a domain from someone who uses a different domain registrar. Whatever the case, it's much easier to manage all our domains in one place.

To do that, we'll need to transfer our domain from one registrar to another. While every service is different, there are some standard steps that go along with every domain transfer. For the sake of this guide, our domain is currently residing at OldCrusty Domains. We'll be transferring from OldCrusty to our new registrar: ProbablyBetter Domains.

_I'd recommend reading through this whole section before starting any transfer process. It's one of those topics that requires time and specific steps done in a specific order. The more you know before you start, the better._

### Unlocking the Domain

If our domain is locked at OldCrusty Domains, it cannot be transferred. In general, this is a good thing. It prevents accidental transferring or deleting. How anyone would ever accidentally transfer a domain is beyond me, but hey, more safety never hurts.

However, to transfer the domain, we'll have to unlock it. Some registrars require us to call or email them to unlock a domain, but some are nice and give us a checkbox or setting in the control panel.

### Configure WHOIS Information

If WHOIS Privacy is turned on, we also won't be able to transfer the domain. That's because an email will be sent to the **Administrative contact** listed in the domain's publicly available WHOIS information, and WHOIS Privacy blocks that email.

We'll also need to make sure the Administrative contact is an email that we can check. In the next step, OldCrusty will send a code to that email address, and we need that email. It's also a good idea to check if the WHOIS information is displaying correctly:

```shell
whois donkeyrentals.com

Domain Name: DONKEYRENTALS.COM
Admin Email: admin@donkeyrentals.com
...
```

### Authorization Code

Now we need to request an authorization code from OldCrusty. Hopefully this is just a button we can push somewhere (if not, we may need to email or call OldCrusty support). An email will be sent from OldCrusty to the Administrative contact email address from our WHOIS information. As I said in the last section, WHOIS information needs to be publicly available (WHOIS Privacy turned off), and the Administrative contact email needs to be an email address we can access.

The authorization code, also called EPP ([Extensible Provisioning Protocol](https://en.wikipedia.org/wiki/Extensible_Provisioning_Protocol)) code, is a short code that we'll need to enter at ProbablyBetter domains. It looks something like `6sF>X95ZrH`.

### Start the Transfer

At ProbablyBetter Domains we can start transferring in a domain. Every registrar is different at this point, but most likely, we'll enter our domain, agree to some terms of service, create or sign in to an account at ProbablyBetter domains, and enter that authorization code from the email. We'll also have to enter WHOIS information at ProbablyBetter Domains and enter payment information. This last step may come as a surprise.

The reason most transfers cost money is ICANN (the people who run the whole domain system) require the domain's expiration date be pushed out one year. So if the domain was going to expire on January 1, 1999, now it will expire January 1, 2000. For that reason, transferring often costs a similar amount to registering that same domain for the first time.

### Minimize Downtime

Downtime is bad, and no one wants it, but it can be tricky to avoid when transferring a domain. Because of the way DNS works, servers often hold onto DNS data over long periods of time, even if we change our records.

This is normally not a problem because your DNS records don't change much. But when we transfer a domain we're essentially changing _all_ the records. At any one point in time, DNS servers have records that are anywhere from 1 second to 48 hours old.

One way to work with this constraint, [outlined here](http://dyn.com/blog/changing-managed-dns-providers-in-five-easy-steps), is to create identical records at ProbablyBetter Domains and _then_ transfer the domain over. That way if visitors access the new DNS records or outdated ones, it won't matter because they are the same.

This does require you to be able to create DNS records without transferring the domain first, which many registrars don't support.

Another way is to reduce the time servers hold onto old information. This is called the TTL value. It's the number of seconds before DNS servers refresh their data. The problem is, all servers that have your DNS data (potentially a lot) need to have this value updated also.

[This answer](http://serverfault.com/questions/459968/how-to-switch-dns-for-a-website-without-service-disruption/459970#459970) on ServerFault shows the following steps:

> 1. Change the zone TTL to minimum - in most cases it's 300 seconds (5 minutes). Do not change any records at this stage.
> 2. Wait 48 hours.
> 3. [Transfer the domain]. It will take just 5 minutes to propagate the changes.
> 4. Revert TTL to standard 48 hours.

This is pretty clever. Most of the time, you want your TTL to be a long period of time so that if something _does_ go wrong, it can't happen immediately to everyone. Also, this allows DNS servers not to have to be in near constant communication with each other, as that would be much harder to scale to the world-wide system that it is today.

### Clean Up

After we've set up the transfer at ProbablyBetter Domains, we may need to accept that transfer back at OldCrusty Domains. Then, we wait. The process can take up to two weeks, so be prepared to wait that long. In my experience, it doesn't usually take that long, but we should give ourselves that much time just in case.

Also, know that our DNS records will not come over with the transfer. We'll need to re-add them manually if we haven't already. For small sites, this isn't too much of an issue, but if we have lots and lots of records, this could take awhile. Some sites let us set up the domain before we start the transfer. That can be a nice way to test everything.

Be sure to lock the domain and turn on WHOIS privacy if we want it after transferring.
