## Installing tools on Unix, Linux, and Mac OS X

Luckily, the tools for this book (dig, host, openssl, nslookup, and whois) are all available via a built-in (or very easy to install) package manager. While this is incredibly convenient, even _more_ convenient is often, many of these tools are already installed.

From your shell, you can type the following command to see if a tool is installed:

```shell
$ which dig

/usr/bin/dig
```

You can replace `dig` with any of the following:

* `host`
* `openssl`
* `nslookup`
* `whois`

If the tool is installed, it will return its location on the system. If not, it will say `<command> not found`. If that's the case, you can use your package manager to install it, described below.

### Mac OS X and homebrew

Mac OS X doesn't come with a package manager installed. I highly recommend [homebrew](http://brew.sh) which can be installed with the following command:

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now you should be all set to install the tools.

---

Below are the basic commands to install each tool on seven different operating systems. For the purposes of this book, and perhaps the world at large, this is all you will need.

### BIND (which includes dig, host, and nslookup)

* Arch Linux: `pacman -S bind`
* Centos: `yum install bind`
* Debian: `apt-get install bind9`
* Gentoo: `emerge -atv net-dns/bind`
* Fedora: `yum install bind`
* Mac OS X: `brew install bind`
* Ubuntu: `apt-get install bind9`

### whois

* Arch Linux: `pacman -S whois`
* Centos: `yum install whois`
* Debian: `apt-get install whois`
* Gentoo: `emerge -atv net-misc/whois`
* Fedora: `yum install whois`
* Mac OS X: `brew install whois`
* Ubuntu: `apt-get install whois`

### OpenSSL

* Arch Linux: `pacman -S openssl`
* Centos: `yum install openssl`
* Debian: `apt-get install openssl`
* Gentoo: `emerge -atv dev-libs/openssl`
* Fedora: `yum install openssl`
* Mac OS X: `brew install openssl`
* Ubuntu: `apt-get install openssl`

After these are installed, do a quick `which <command>` to determine if these are installed. A more robust check would be to invoke the command in its simplest form:

* dig: `dig -v` - Displays the current version of the dig command.
* host: `host` - Displays list of command options.
* openssl: `openssl version` - Display the current version of the openssl command.
* nslookup: `nslookup` - Enter interactive mode, use ctrl-D to exit.
* whois: `whois` - Displays list of command options.
