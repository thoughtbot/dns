## Package Management for Windows

We'll be installing the software used in this book with a package manager. Unix and Linux based systems often come with a package manager installed. Package managers are great because in addition to installing software, they install supporting packages, keep an up-to-date list of safe software packages, and make it very easy to uninstall software later.

You can think of a package like an application; software written to do a specific set of tasks. The difference is that these packages are used almost always from the command prompt instead of opening up a graphical interface. Installing graphical applications via a package manager is not unheard of however.

Some bad news: Windows does not come with a package manager. But good news; it's pretty easy to install one. In particular, we're going to install [chocolatey](https://chocolatey.org).

Open your Command Prompt by using the Start menu to search for `Command`. When you see the Command Prompt show up, right click it and "Run as administrator".

Now, copy-and-paste this crazy looking command into it. Trust me, don't try to type it out:

```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

This will take some time, on the order of a minute or two for a modern-ish computer. If it's taking significantly longer, try restarting, and make sure you open the Command Prompt as an administrator.

Once it's done, you now have the chocolatey package manager installed on your system. You can use the `choco` tool to issue basic commands, for example:

```shell
$ choco install whois
$ choco uninstall whois
$ choco search openssl
$ choco upgrade chocolatey
```

I also recommend enabling the `allowGlobalConfirmation` feature for chocolatey. If you don't it will ask you every time if you want to install each package:

```
$ choco feature enable -n=allowGlobalConfirmation
```

If you want to disable this feature, you can run:

```
$ choco feature disable -n=allowGlobalConfirmation
```

Now you can install [tons of great packages](https://chocolatey.org/packages)!
