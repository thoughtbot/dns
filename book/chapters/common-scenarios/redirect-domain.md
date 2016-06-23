## Redirect One Domain to Another

Sometimes we move on from a domain. Perhaps a company is rebranding, or we sold the domain for a tidy profit. Or maybe we've grown apart from the domain. The domain doesn't "get" us anymore and we've found a new, fresher, more happenin' domain.

Whatever the case, we want to make sure previous visitors to our domain can get to us at the new one, even if they visit the old one. Let's look at a few options on how to do this.

### Our DNS Provider Might Do This for Us

If we're no longer using any part of the domain (e.g., no subdomains, email accounts, etc.), sometimes our domain host can redirect the entire domain for us. This is often called **forwarding** or **redirecting** the domain. We can check in the DNS provider's control panel for an option to forward or redirect.

If we have the option, the best thing to use is a [301 or permanent redirect](https://en.wikipedia.org/wiki/HTTP_301). This will tell search engines and browsers alike to use the new domain instead of the old one. This technical detail may not be apparent in our control panel, but if we see it, we'll know we're doing it right.

### If We Have Access to the Server

If we're using some part of our domain, but still want to redirect traffic, we can configure the web server to use a 301 redirect.

For an **nginx** server, we'll need to find the configuration file, by default located at `/etc/nginx/conf.d/default.conf`. Find the `server` directive for our website that has our old domain listed next to `server_name`, then change it to look like this:

```nginx
server {
  server_name donkeyrentals.com;
  return 301 https://newdomain.com;
}
```

For **Apache**, find its configuration file, by default located at `/etc/httpd/conf/httpd.conf`. Find the `<VirtualHost>` directive that has our site listed next to `ServerName`. Add a `Redirect` line to it:

```apache
<VirtualHost *:80>
  ServerName donkeyrentals.com
  Redirect 301 / https://newdomain.com
</VirtualHost>
```

We can see these both use 301 redirects.

If we don't have access to the direct Apache configuration files, but we do have access to the files on our server, we can use an `.htaccess` file to redirect. Place or edit an `.htaccess` file in the same directory where our `index.html` page is. We may have to show invisible files if it doesn't show up.

Add this to the file:

```apache
Redirect 301 / https://newdomain.com
```

This looks very similar to our Apache configuration, and it does pretty much the same thing.

### If We Don't Have Access to the Server

If the domain is the only thing we have access to, then the above is not an option. As long as we can create new DNS records, we can use a [CNAME](#cname).

This is a book about DNS, so it might seem odd that I put the DNS solution last. That's because there's one big caveat: CNAMEs [cannot exist on the apex domain](#when-to-use-cnames). You might remember this from the [Types of DNS Records](#types-of-dns-records) chapter.

If we were using `www` or some other subdomain as our main URL, this will work great. Make a new CNAME record that looks like this:

* **Hostname**: `www`
* **Record Type**: `CNAME`
* **Target Host**: `newdomain.com`

Unfortunately, if our domain has no prefix, the only other option is an ANAME/Alias record, which our DNS host may or may not support.

### Check Our Work

Obviously, we can visit the old website and see if the new one shows up instead. If we want to inspect further, we can use a command called `curl`. Open up a shell and type the following using the old domain:

```shell
$ curl -I donkeyrentals.com

HTTP/1.1 301 Moved Permanently
Location: httpw://newdomain.com
Date: Mon, 11 Apr 2016 17:51:57 GMT
Server: lighttpd/1.4.28
```

The `curl` command makes a request to whatever domain we tell it, like typing a URL into a web browser would do. The `-I` flag says that we want to see the HTTP headers that come back as a result of the request. In this case, we can see we got the `301 Moved Permanently` status code, which is exactly what we want. Go us!
