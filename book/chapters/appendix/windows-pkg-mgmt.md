## Package Management for Windows

The bad news? Windows does not come with a package manager. The good news? It is pretty easy to install one. In particular, we are going to install [chocolatey](https://chocolatey.org).

Open your Command Prompt by using the Start menu to search for `Command`. When you see the Command Prompt, right click it and "Run as administrator."

Now, copy and paste the following crazy looking command into it (trust me, don't even try to type it out):

```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

This will take some time, perhaps a minute or two for a modern-ish computer. If it takes significantly longer, try restarting, and make sure you open the Command Prompt as an administrator.

Once it is done, you will have the chocolatey package manager installed on your system. Use the `choco` tool to issue basic commands. For example:

```shell
$ choco install whois
$ choco uninstall whois
$ choco search openssl
$ choco upgrade chocolatey
```

I also recommend enabling the `allowGlobalConfirmation` feature for chocolatey. If you do not, it will ask if you want to install each package every time:

```
$ choco feature enable -n=allowGlobalConfirmation
```

To disable this feature, run:

```
$ choco feature disable -n=allowGlobalConfirmation
```

Now you can install [tons of great packages](https://chocolatey.org/packages)!

### Additional installation

This book makes heavy use of the [BIND suite](https://www.isc.org/downloads/) of tools, like `dig`, `host`, and `nslookup`. Chocolatey can install them, but they will also need some additional supporting software. Specifically, the succinctly named _Visual C++ Redistributable for Visual Studio 2012 Update 4_.

Installation is pretty simple:

1. Visit [this website](https://www.microsoft.com/en-us/download/details.aspx?id=30679).
2. Download the x64 or x86 version of the software based on your system architecture. If you are not sure what system architecture you have, follow these steps:  
    a. On Windows 7, open the Start menu and right-click on `Computer`, then click `Properties`
    b. On Windows 10, right click the Start menu and click `System`
    c. In the System section, `System type` should say **32-** or **64-bit Operating System**.
    d. Download x64 for 64-bit systems and x86 for 32.
3. Double click the installer and let it do it's thing.
4. `dig`, `host`, and `nslookup` should work without issue.
