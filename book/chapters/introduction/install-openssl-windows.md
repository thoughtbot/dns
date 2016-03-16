Source: http://blog.didierstevens.com/2015/03/30/howto-make-your-own-cert-with-openssl-on-windows/

## Windows 7/8

* Visit http://slproweb.com/products/Win32OpenSSL.html
* Download latest version for your architecture
* Run installer
    * Accept agreement
    * Install to `C:\Program Files\openssl`
    * Add to Start menu as `OpenSSL`
    * Copy OpenSSL DLLs to `The OpenSSL binaries /bin directory`
    * Click Install
* Set the path
	* Start menu > Right click on `Computer` > `Properties` > `Advanced System Settings` > `Advanced` tab > `Environment Variables`
	* Under `System variables`, scroll to find `Path` and click `Edit...`
	* Go to the end of the line, type a semicolon: `;` and then `C:\Program Files\openssl\bin`
	* Hit `OK` a bunch of times.

## Windows 10

* Visit http://slproweb.com/products/Win32OpenSSL.html
* Download latest version for your architecture
* Run installer
    * Accept agreement
    * Install to `C:\Program Files\openssl`
    * Add to Start menu as `OpenSSL`
    * Copy OpenSSL DLLs to `The OpenSSL binaries /bin directory`
    * Click Install
* Set the path
	* Use the search box (next to the start/windows menu) and type in `environment`
	* Click on `Edit the system environment variables`
	* Click `Environment Variables...` at the bottom
	* Under `System variables`, scroll to find `Path` and click `Edit...`
	* Go to the end of the line, type a semicolon: `;` and then `C:\Program Files\openssl\bin`
	* Hit `OK` a bunch of times.
