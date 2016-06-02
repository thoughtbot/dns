## How To Read This Book

Considering you are reading this part with your eyes, this might be a confusing section to come across. I'll assume you're literate, but perhaps not familiar with my particular conventions.

### New terminology

First up, new terms I will try to define as I go. There is however a high chance that I will assume (wrongly) a term is well known enough that I don't need to explain it on the spot. I might also accidentally forget to define something. If you find yourself confused and needing a quick reminder or introduction to a term, check the [glossary](#glossary). Hopefully I've defined all the technical terms that you're curious about.

### Literal text

In the case where I'm trying not to use words to describe things, but to show something exact, I'll specify it in a monospaced font `like this`. You'll see this scattered throughout the book where there's a small piece of text (i.e. one line or less) that I expect you to type into a field or configuration file.

When we need to use a command line tool like `dig`, it's often useful to show an example of the command and its response. In those situations, I'll be using code block formatting, like so:

```
$ some command

some response

...
```

I also use this formatting when I'm showing multiple lines of text, like in a configuration file.

### Truncation

Three dots `...` will represent some kind of truncated response. It's not that I couldn't copy and paste something, but seeing a large block of what looks like gibberish is draining to read. If something is important, don't worry, I'll include it.

### Shell commands

Also, you may have noticed the dollar sign at the start of the command. This represents a command I expect you to copy and paste into your shell if you want to follow along and see a similar response. They also serve to separate commands from responses.

Note that the dollar sign is _not_ included in the command. It's what we call the "prompt". You'll probably see something like your computer name, current folder, and/or username, followed by the dollar sign in your prompt. For brevity, we can just shorten to the single symbol.

So in a case like this:

```
$ hello
```

I just expect you to type the five letters "hello", not "$ hello".

### Short `dig` responses

I also use the command line tool `dig` liberally throughout the book, as it's extremely useful for inspecting existing domains. It has a relatively verbose response by default. To try and reign in these responses, I use the `+short` option on most `dig` commands:

```
$ dig +short example.com

104.131.191.2
```

Note that you most definitely can leave off the `+short` part if you want the full, lengthy response from `dig`.

### The example domain

Finally, inevitably, we're going to talk about domains in this book about the domain name system. Instead of trying to stay abstract, I've picked a domain we'll use in examples: [donkeyrentals.com](https://donkeyrentals.com).

Why donkey rentals? Mostly it makes the book a bit more fun to read. I couldn't type `example.com` for five-or-so chapters and keep my sanity.

It's also a real domain that works. As much as possible I've tried to make all the example `dig` queries the same as they are in the book so we can see them in action! Feel free to query the domain as much as you like to try and get the hang of any of the concepts in the book. It's there for you, dear reader.
