### TXT

TXT (text) records are incredibly simple. They're a string of text connected to a hostname. But since they are so simple and their purpose is undefined, they are very much the "other" type of record. For example:

* **Hostname**: `message`
* **Record Type**: `TXT`
* **Value**: `Welcome to Donkey Rentals!`

```shell
$ dig message.donkeyrentals.com TXT +short

"Welcome to Donkey Rentals!"
```

So, what's the point? Why would we want these? Sometimes extra metadata is useful. We can use it to prove that we do, in fact, have control over this domain. Email services use TXT records to help prove that email coming from our email addresses is authentically from us. Spammers can't fake our email address so easily then. Same for SSL/TLS certificates.

Another example: clever programmers have used TXT records to extend what DNS records can do. In the CNAME section above we were talking about how we can't use CNAMEs on the apex domain. ALIAS records (see below) allow us to do this, but ALIAS records aren't standard. It's all a clever use of TXT records.
