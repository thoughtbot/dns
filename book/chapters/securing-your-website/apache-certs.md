## Installing a Certificate for Apache

### What We Need

This might be a bit obvious, but we'll need access to our server. We'll need to have Apache installed (sometimes referred to only as `httpd`). And, of course, we need the certificate files that our CA sent us:

* `donkeyrentals_com.crt`
* `donkeyrentals_com.ca-bundle`
* `donkeyrentals_com.key`

Additionally, we'll need to have `mod_ssl` and `openssl` installed. We can check for `mod_ssl` by running one of these two commands, depending on which version of Apache we're running:

```shell
# Apache 2
$ apache2ctl -M | grep ssl

# Apache 1
$ apachectl -M | grep ssl
```

If `mod_ssl` is installed, we'll see something like:

```shell
ssl_module (shared)
```

Checking `openssl` is straightforward:

```
$ openssl version

OpenSSL 1.0.2g  1 Mar 2016
```

If we get something back like `openssl: command not found`, then we don't have it installed. If these are missing, our [package manager](#installing-tools) (yum, brew, apt, choco, etc.) should be able to install them for us.

Finally, you'll need to know where your Apache config files are. They are commonly in the `/etc/httpd` directory. If they're not there, a good way to find them on Linux systems is the following command:

```shell
$ sudo find / -name httpd.conf
```

This will locate the main configuration file, `httpd.conf`. From there, we can probably find all the other directories we need like `modules`, `conf.d`, etc. We'll need these directories later.

### Move All the Files

Now that we have all the files we need, we can place them in some sensible directories. If the directories don't exist, we should create them. The `.crt` and `.ca-bundle` files can go in the `/etc/ssl/ssl.crt` directory, and the `.key` file will go in the `/etc/ssl/ssl.key` directory.

We'll also set good permissions on the private key's directory. We want only the root to be able to access the file so no one else can see our private key.

```shell
$ chmod 700 /etc/ssl/ssl.key/
$ chown root /etc/ssl/ssl.key/
$ chgrp root /etc/ssl/ssl.key/
```

### Configure Apache

Next, we need to tell Apache where to find these files and how to act as a secure server. It's possible a configuration may already exist that we can change. Let's search inside our config files to check:

```shell
$ grep -r SSLCertificate /etc/httpd
```

This found the file `/etc/httpd/conf.d/ssl.conf`, which we can modify to our liking. If no file was found, we can build a configuration up from scratch.

A pre-existing file will have hundreds of lines, many of them commented with a `#` at the start of the line. Here's a no-comments version of the relevant part of an example configuration:

```
LoadModule ssl_module modules/mod_ssl.so

<VirtualHost *:443>
DocumentRoot /var/www/donkeyrentals
ServerName donkeyrentals.com
SSLEngine on
SSLCertificateFile /etc/ssl/ssl.crt/donkeyrentals_com.crt
SSLCertificateChainFile /etc/ssl/ssl.crt/donkeyrentals_com.ca-bundle
SSLCertificateKeyFile /etc/ssl/ssl.key/donkeyrentals_com.key
SSLProtocol -all +TLSv1
SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
</VirtualHost>
```

Many of these lines might already exist and need no modification. Some only need to be uncommented from the existing file and tweaked slightly. Some will need to be added entirely. Order doesn't matter too much, as long as all the lines are inside of `<VirtualHost *:443>` and `</VirtualHost>` (except for the first `LoadModule` line). Here's what each line does:

* `LoadModule ssl_module modules/mod_ssl.so`

This tells Apache to load the `mod_ssl` package we installed earlier. The `modules/mod_ssl.so` path is important here. It's relative to the `ServerRoot` directory, which is by default `/etc/httpd`. The full path in the example would be `/etc/httpd/modules/mod_ssl.so`.

* `<VirtualHost *:443>`

We start the `<VirtualHost>` directive off by saying this applies to any IP address, `*`, on port `443`, which is the conventional port for secure connections.

* `DocumentRoot /var/www/donkeyrentals`

The location on this server where we can find our website content like the `index.html` file, images, scripts, etc. is:

* `ServerName donkeyrentals.com`

The name that the server identifies itself as, i.e., our common name, is the same thing we entered when making our CSR.

* `SSLEngine on`

Enable TLS/SSL.

* `SSLCertificateFile /etc/ssl/ssl.crt/donkeyrentals_com.crt`
* `SSLCertificateChainFile /etc/ssl/ssl.crt/donkeyrentals_com.ca-bundle`
* `SSLCertificateKeyFile /etc/ssl/ssl.key/donkeyrentals_com.key`

Where to find our certificate, certificate authority bundle, and private key (these are the same files we moved around previously):

* `SSLProtocol -all +TLSv1`
* `SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH`

Only use TLS version 1 protocol and higher, and use [currently recommended](https://cipherli.st) cipher suites. A full list of ciphers can be seen [here](https://openssl.org/docs/manmaster/apps/ciphers.html). Fancy stuff.

_Side note: Picking which cypher suites to use is tricky. It depends on our server, the client, the current state of security, and many other factors. If you want to learn more, there are [lots](https://cipherli.st) of [resources](https://www.ssllabs.com/projects/best-practices/index.html) that [have](https://httpd.apache.org/docs/2.2/ssl/ssl_howto.html) more [information](http://security.stackexchange.com/questions/76993/now-that-it-is-2015-what-ssl-tls-cipher-suites-should-be-used-in-a-high-securit)._

* `</VirtualHost>`

Finally we make sure to close our `<VirtualHost>` directive.

If you need further customization, check out Apache's [documentation on the SSL](http://httpd.apache.org/docs/current/mod/mod_ssl.html) module.

### Check Our Work

Now that we're configured properly, we can make sure we didn't cause any errors in our Apache configs with one of two commands:

```shell
# Apache 2
$ apache2ctl configtest

# Apache 1
$ apachectl configtest
```

If we see `Syntax OK`, then we're good to go.

Finally, we restart Apache:

```shell
$ sudo service httpd restart
```

You've now configured Apache to use your brand new TLS certificate. High five!

![](../../images/donkeyrentals-certificate-badge.png)
