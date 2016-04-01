## Package Management for Mac OS X

Mac OS X doesn't come with a package manager installed. I highly recommend [homebrew](http://brew.sh) which can be installed with the following command:

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once it completes, you can now use the `brew` command to install, uninstall, update, etc. tons of packages for your system:

```shell
$ brew install whois
$ brew uninstall whois
$ brew search openssl
$ brew upgrade openssl
```

That's it! Now you should be all set to install the tools.
