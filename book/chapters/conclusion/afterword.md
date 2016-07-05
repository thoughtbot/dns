## Afterword

So what's left? You read this book, learned some things about DNS, TLS certificates, and domains in general. Congratulations! I also have a bit of advice for you.

I've spent a lot of time reading through [Server Fault](https://serverfault.com) to understand the particulars of a topic. It's a great Q&A site where you can often find your question has already been asked and answered. If not, you can sign up and ask for free.

I find that I learn best when I'm experimenting. If you have the means, I highly suggest getting a spare domain to play around with. Set up a quick site and just go crazy with different record types. Query them with `dig` and see what you can get out of them. Redirect to other sites with CNAMEs, chat with friends via TXT records, etc. This can help solidify your understanding of the whole domain process.

If you really want to dive into the deep technical details of how DNS or TLS works, [RFCs](http://www.ietf.org/rfc.html) (requests for comments) are the way to go. An RFC document is usually made by a standards committee to decide how certain technology will work. It includes everything a developer would need to create software that works with other like-minded software. RFCs are playbooks that keep distributed systems like DNS working, even when multiple different, often competing, organizations write software for a purpose.

Wikipedia keeps a great list of DNS related RFCs [here](https://en.wikipedia.org/wiki/Domain_Name_System#RFC_documents).

Last, and most importantly, continue to be curious. Curiosity wrote this book, curiosity likely got you through this book, and curiosity will keep you learning, inspecting, and researching to find out more. That is your most powerful tool. Use it to its fullest extent.
