## Installing tools

We'll be installing the software used in this book with a package manager. Unix and Linux operating systems often come with a package manager installed. Package managers are great because in addition to installing software, they install supporting packages, keep an up-to-date list of safe software packages, and make it very easy to uninstall software later.

You can think of a package like an application; software written to do a specific set of tasks. The difference is that these packages are used almost always from the command prompt instead of opening up a graphical interface. Installing graphical applications via a package manager is not unheard of however.

Tools used in this book (`dig`, `host`, `openssl`, `nslookup`, and `whois`) are all available via a package manager. While this is incredibly convenient, even _more_ convenient is often, many of these tools are already installed.

From your shell or command prompt, you can use the `which` command to see if a tool is installed:

```shell
$ which dig

/usr/bin/dig
```

or the `where` command on Windows:

```shell
$ where dig

C:\ProgramData\chocolatey\bin\dig.exe
```

You can replace `dig` with any of the following:

* `host`
* `openssl`
* `nslookup`
* `whois`

If the tool is installed, it will return its location on the system. If not, it will say `<command> not found`. If that's the case, you can use your package manager to install it, described below.

### Mac and Windows

Neither Mac OS X nor Windows comes with a package manager. Luckily, this is pretty easy to resolve. If you're using either of these systems, check out the _Package Management for Mac OS X_ or _Package Management for Windows_ section before moving on to the next section.

### Installation

Below are the basic commands to install each tool on seven different operating systems. For the purposes of this book, and perhaps the world at large, this is all you will need.

### BIND (which includes dig, host, and nslookup)

* Arch Linux: `pacman -S bind`
* Centos: `yum install bind`
* Debian: `apt-get install bind9`
* Gentoo: `emerge -atv net-dns/bind`
* Fedora: `yum install bind`
* Mac OS X: `brew install bind`
* Ubuntu: `apt-get install bind9`
* Windows: `choco install bind-toolsonly`

### whois

* Arch Linux: `pacman -S whois`
* Centos: `yum install whois`
* Debian: `apt-get install whois`
* Gentoo: `emerge -atv net-misc/whois`
* Fedora: `yum install whois`
* Mac OS X: `brew install whois`
* Ubuntu: `apt-get install whois`
* Windows: `choco install whois`

### OpenSSL

* Arch Linux: `pacman -S openssl`
* Centos: `yum install openssl`
* Debian: `apt-get install openssl`
* Gentoo: `emerge -atv dev-libs/openssl`
* Fedora: `yum install openssl`
* Mac OS X: `brew install openssl`
* Ubuntu: `apt-get install openssl`
* Windows: `choco install openssl.light`

_Note for OpenSSL on Windows: You'll also need to add OpenSSL's `bin` directory to your path. Copy-and-paste the following in the Command Prompt:_

```
$ setx path "%PATH%;C:\Program Files\OpenSSL\bin"
```

### Installation check

After these are installed, do a quick `which <command>` or `where <command>` to determine if these are installed. A slightly more involved check would be to invoke the command in its simplest form:

* dig: `dig -v` - Displays the current version of the dig command.
* host: `host` - Displays list of command options.
* openssl: `openssl version` - Display the current version of the openssl command.
* nslookup: `nslookup` - Enter interactive mode, type `exit` to close.
* whois: `whois` - Displays list of command options.
