## TLS and SSL

You've probably seen that lock next to the URL in your web browser on certain websites. It means you're visiting a website that has proven its identity and established a secure connection with your computer. When that lock is present the data to and from that site is encrypted. No one but you and the website are seeing the data being passing back and forth; data like passwords, credit card numbers, social security numbers, or health information.

If you data is not secure, it can be seen and stolen by malicious hackers. When I talk about data being "secure", I'm talking about two different concepts working together. First, and what you might be thinking, is _encryption_. Software can take any data and scramble it up so it is unreadable. That same software (with appropriate permissions of course) can descramble that information. Second, and arguably more important, is _identity_ or _authenticity_. The ability to de-scramble information should only be given to people we trust, and they can only be trusted if we know who they are. This is what makes the authenticity part of security so important.

TLS (transport layer security) also referred to as SSL (secure sockets layer) makes this encryption and authenticity possible. When it's setup for a website, it shows up as a lock or green badge next to a website's URL and signals to visitors that the website is safe. If visitors enter their private data into the website, snoopers will be able to get at it, even as it's being transferred right in front of their eyes.

The real magic of TLS is that the entire process of proving authenticity and setting up encryption happens out in the open. Even as these digital criminals watch all of the data going back and forth, it's still secure. I say magic, but it's not. It's computer security and we're going to look at how it works later on in this chapter.

Websites and servers aren't configured to use TLS by default. To do so there are some hurdles to jump through: namely proof and money. Getting that lock next to the URL requires paying for a certificate and verification that we own the domain that we're certifying. Don't let the word "money" intimidate you though, free alternatives are starting to pop up.

These roadblocks exist because as we talked about above, security entails some kind of identity or authenticity. For example: you trust the teller at your bank because you trust the bank owners, and they trust their employees. But if the teller came up to you on the street and said "HEY I CAN STORE YOUR MONEY!" you'd probably pretend not to hear them and walk away quickly.

That's the importance of authenticity, but what about encryption? How could data go right in front of hackers without them seeing it? Well, exactly _how_ someone could hack isn't a topic for this book, but we can look at a simplified example of what they would see.

It happens to all of us: You're out in a public place like a coffee shop and you just _have_ to buy that artisanal, small-batch, donkey saddle for your niece's birthday party. Someone in a trench coat and sunglasses with a laptop is sitting nearby watching all the Wi-Fi data go back and forth. They might see something like*:

```
...
User visited donkeyrentals.com
User visited checkout page
User submitted an order with this data:
    Name: Edward A Loveall
    Credit Card Number: 1234-5678-9012-3456
    Expiration Date: 12/99
    CVV: 123
...
```

_*This was only a reenactment. No real data was stolen in the making of this example._

Hackers can see this data flying by and record it. Now they have your credit card number with verification code and everything. No good! In contrast, if you have a secure connection established with TLS, the hacker would see something like this instead:

```
...
DeXZPuvv5btpckqk1feXpmUmLBuCMOrIboeg3WHs1rV8eydrTYVgDDq91u02O9HNijDNo+U
Y01IprNqHu6RAE+Z2vBq7jXgKAOqiHsq71yOnfZKiXJThi5u24kRnh1Rm9zht5lNzQ87yI9
KGPf8p16gplQ1SfTa85LLZWkglZGhfnHkVWNdgPf5rpQIWby24YhTPswG4ZSXw4S/pJKhms
6trB2gSCxJi4zJUPSCmB24V3HpdIL1ZPEIRwAz4EpYir/BEefVenOT8pW6afkyp6wKxInNz
pB/16OE0qzjYYzNXymdIAmlzoglLEMIX1bMpZPTPfs2gLJdCr1oQCJ5z1gfXPL2veyK1PaO
...
```

This is ever-so-slightly less readable. Most nefarious hackers would see this and move on to someone else, but even if they decided to grab this snippet, it would be near impossible to decode, and it's not even guaranteed to be useful. It might just be someone merely _browsing_ donkey saddles.

---

Most of this chapter is about obtaining one of these certificates. In addition, there are some other related topics we'll cover:

* What certificates are and their different types.
* Certificate authorities and how they relate to certificates.
* The information we'll need to correctly set up a certificate.
* Generating a private key and certificate signing request.
* Obtaining a certificate from a certificate authority.
* Installing our certificates with nginx or Apache.

Let's get started!

Fair warning: this is a dense chapter that you may have to read more than once. Make sure you've had a full night's sleep and waited 30 minutes after eating. We're about to go into the deep end.
