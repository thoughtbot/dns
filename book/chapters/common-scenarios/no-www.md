## Remove www From a Domain

Back in the 1990s, a convention was started: use a hostname to specify what service a domain represents. For example, an FTP server would put the `ftp` hostname on the front of their domain to create `ftp.example.com`, whereas email servers might use `mail.example.com`, and, of course, servers meant for the World Wide Web would use `www.example.com`.

Many web masters used this convention. It helped the public understand that `www.joespizza.com` on a takeout menu was a website, not a printing error.

But we are now decades beyond the 1990s, and the public is incredibly used to what a website is, yet the `www` remains widespread. There's no real harm in it, but we may want to get rid of it anyway. A more minimal URL can have a nicer aesthetic. Or perhaps we only purchased a TLS certificate for a single domain.

Whatever the case, it's possible to assure that visitors will be taken to the non-`www` URL regardless of what they typed in. The method we choose is dependent on our web server and whether or not we have access to its configuration files.

Note also that every method relies on a [HTTP 301](https://en.wikipedia.org/wiki/HTTP_301) redirect, which is the best way to signal to browsers and search engines that we'd really rather they not use the `www`.

### nginx

If we use nginx and have access to its configuration files, removing the www is relatively easy. Find and open our configuration file, by default located at `/etc/nginx/conf.d/default.conf`.

There will already be a `server` directive for our main website. It should have these lines:

```nginx
server {
  server_name donkeyrentals.com;

  # more configuration down this way...
}
```

This lets nginx know that when a request comes in for `donkeyrentals.com`, do something with it, ideally, serve up the website. Add this separate server directive above it:

```nginx
server {
  server_name www.donkeyrentals.com;
  return 301 $scheme://donkeyrentals.com$request_uri;
}
```

We'll need to change `donkeyrentals.com` to our domain, of course.

This takes requests for `www.donkeyrentals.com` and, instead of serving up the website as normal, redirects (using a standard HTTP 301 redirect) to the non-www version of the site with the whole URL intact.

### Apache

Apache's method is quite similar to nginx's: catch `www` URLs and redirect to the non-`www` versions. Open up our Apache configuration (usually found at `/etc/httpd/conf/httpd.conf`) and insert this directive at the top:

```apache
<VirtualHost *:80>
  ServerName www.donkeyrentals.com
  Redirect 301 / http://donkeyrentals.com/
</VirtualHost>
```

Then, replace `donkeyrentals.com` with our domain.

This, as we might expect, redirects `www` requests to the rest of the website using an HTTP 301 redirect. Apache preserves whatever is after the trailing `/` when using `Redirect`, so deep links will be maintained.

### .htaccess

If we don't have access to our web server's configuration files, an `.htaccess` file can also remove the `www` prefix. Note that this only works if we have an Apache server running, which is very common, especially on shared hosting where we may not have direct configuration access.

Create a file called `.htaccess` in the root of our website's directory, i.e., on the same level as our `index.html` file. If one already exists, we can use that instead. Edit the file to have these lines:

```apache
RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} !^donkeyrentals.com$ [NC]
RewriteRule ^(.*)$ http://donkeyrentals.com/$1 [L,R=301]
```

As usual, replace `donkeyrentals.com` with our domain name.

This looks for any URL that does not begin (`!^`) with `donkeyrentals.com` and redirects (again, using the HTTP 301 redirect) to the non-`www` website. This will only work for web requests, so other protocols like FTP will still work as planned. Other subdomains usually store their content in a separate directory so they won't be affected.
