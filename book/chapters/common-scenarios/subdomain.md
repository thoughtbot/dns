## Creating a Subdomain

Hopefully, creating a subdomain is simple. If we have some kind of managed web hosting, there is often a control panel just for this purpose. The basic idea here is to create an A record that points to a server, exactly like our main website.

### Subdomain for a Service

If this is for a service like an FTP server, we can point the `ftp` hostname to our FTP server using an A record. Anyone connecting over the file transfer protocol can use `ftp.donkeyrentals.com`. If we host our FTP server elsewhere, or we change where it's located, we can update that A record and the same domain will work.

### Subdomain for the Web

The process is not too different from a service. If our hosting provider does not provide us with an easy way to make subdomains, we'll have a little more configuration to do.

The DNS setup is the same: we create an A record pointing to the IP address of a server. It's common, but not at all mandatory, to use the same server as our main website.

Once the request makes it to the server, our web server software--for this, we'll look at nginx and Apache--will take over and figure out what to do.

Let's say we're creating `store.donkeyrentals.com`. If we're using nginx, our server will need additional configuration to route requests to the store. Edit the nginx configuration for our website. Mine is located at `/etc/nginx/conf.d/default.conf`.

Each domain is divided up into a `server` directive. The directive for the store will look like this:

```nginx
server {
  server_name store.donkeyrentals.com;
  root /var/www/donkey_store;
}
```

This short and sweet configuration can go above or below existing configurations. The `server_name` looks for requests coming in for that domain, and `root` specifies the directory to serve files from.

Apache is similar. Find our Apache configuration files (by default at `/etc/httpd/conf/httpd.conf`) and add a new `<VirtualHost>` directive:

```apache
<VirtualHost>
  ServerName store.donkeyrentals.com
  DocumentRoot /var/www/donkey_store
</VirtualHost>
```

We'll see striking similarities to the nginx configuration. `ServerName` will look for requests for `store.donkeyrentals.com`, and `DocumentRoot` will route those requests to files inside `/var/www/donkey_store`.

After either configuration, we'll need to restart nginx or Apache, respectively. Once that's done, our DNS can now work along side our web server. The A record points to an IP address, and the web server software will direct it to the correct files.
