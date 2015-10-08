### TXT

TXT records are pretty simple, but also a bit strange. They're nothing more than an arbitrary string connected to a hostname. For example:

* **Hostname**: `message`
* **Record Type**: `TXT`
* **Value**: `Welcome to Donkey Rentals!`

```shell
$ dig message.donkeyrentals.com TXT +short

"Welcome to Donkey Rentals!"
```

So, what's the point? Why would we want these? Well, sometimes extra metadata is useful. We can use it to prove that you do, in fact, have control over this domain. Email services use TXT records to help prove that email coming from your email address is authentically from you. Spammers can't fake your email address so easily then. Same for SSL/TLS certificates.

Also clever programmers have used TXT records to extend what DNS records can do. Back up in the CNAME section we were talking about how we can't use CNAMEs on the apex domain. ALIAS records (see below) allow us to do this, but ALIAS records aren't standard. It's all a clever use of TXT records.
