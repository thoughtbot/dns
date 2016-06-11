## Getting a Certificate

Let's walk through creating a private key and certificate signing request (CSR) step by step. We'll upload the CSR to our Certificate Authority (CA) and they will create and sign our certificate. After, we'll cover installing that certificate in a couple of places. By the end of the chapter, we should have ourselves a secure website.

### Create a Working Directory

We're going to be creating a few files, so it's nice to have them contained in a single folder. This folder should eventually be secured, because it will contain private key information that should _never_ be made public. Create a directory with a name like `donkeyrentals-certs` or something equally descriptive. Navigate to that directory inside of your shell.

### Create the Private Key and CSR

Next, we're going to create our private key and CSR. We'll need to enter a bunch of contact information for this. It can be a little overwhelming, so let's do one together. If you messed up, starting over is as easy as deleting the two files it creates and running the command again. I'll run through Donkey Rentals, and you can follow along with your domain:

```shell
$ openssl req -nodes -newkey rsa:2048 -keyout donkeyrentals_com.key \
-out donkeyrentals_com.csr

Generating a 2048 bit RSA private key
.......................................+++
........................................+++
writing new private key to 'donkeyrentals_com.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:Massachusetts
Locality Name (eg, city) []:Cambridge
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Donkey Rentals
Organizational Unit Name (eg, section) []:.
Common Name (e.g. server FQDN or YOUR name) []:donkeyrentals.com
Email Address []:.

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:crouching-domains-hidden-donkeys
An optional company name []:Donkey Rentals
```

We'll go over all those fields in a second. First, we can look at the two files created by the command:

* donkeyrentals_com.key

The private key. Again, this is the thing we need to keep absolutely secret.

* donkeyrentals_com.csr

The certificate signing request. We will be uploading this to our CA. Think of it as the digital paperwork you have to fill out and submit to get your certificate. It contains the public key and the contact information we filled out above.

These names aren't hardcoded; we entered them in the command above. While it doesn't matter what we name the files, it's a good idea to name them in a way that will give us a hint as to what they will be in the future. A convention is naming them similar to the common name, e.g., the `donkeyrentals.com` CSR is named `donkeyrentals_com.csr`.

Let's briefly go over the fields we filled out when creating the key and CSR. Most of these fields should be self-explanatory, but if you're easily intimidated like I am, this should help. To leave a field blank, use a single period (`.`) character.

* **Country Name** -- The two-letter country abbreviation for the certificate's owner.
* **State or Province Name** -- Use the full name here. If you are in a country that doesn't have these divisions, use the full country name instead.
* **Locality Name** -- The City, Township, Hamlet, Ant Colony, etc.
* **Organization Name** -- The company representing the certificate.
* **Organizational Unit Name** -- You can leave this blank (with a period).
* **Common Name** -- We talked about this back in the _Be Prepared_ section. This is the exact domain we want to encrypt. `donkeyrentals.com` vs `www.donkeyrentals.com` is crucial here.
* **Email Address** -- This one can stay blank, too (again, with a period).
* **A challenge password** -- Make this a very strong password, unlike the one I used in the example.
* **An optional company name** -- This can be the same as **Organization Name**.

And that's it for CSR.

### Upload the CSR

The next thing to do is provide the CSR to our CA. It's a text file that looks like a bunch of gibberish with a header and footer. It contains your public key and all the information we just typed in. Your CA will know how to read it. In some cases, we need to upload the .csr file, but in others we resort to copy-and-paste like animals. Your CA will tell you what they want you to do.

Either way, once we get our CA to sign our certificate, they'll send it to us, probably in an email, or make it available on their website. It also may come with a `ca-bundle` file that we will use with the certificate. This usually happens within minutes for a single domain certificate. Once we have the certificate, let's save it to our working directory as `donkeyrentals_com.crt` or your equivalent file name.

Now it's time to install it. If you don't manage your own web server, you'll have to rely on your web hosting provider to provide instructions. If you use nginx or Apache on a server, let's dive in.
