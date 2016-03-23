## Windows 7/8

Source: http://nil.uniza.sk/windows/windows-7/how-install-dig-dns-tool-windows-7

* https://www.isc.org/downloads/
* Click `BIND`
* Click `Download` next to the version with the Status of "Current"
* Pick your architecture
* 32 or 64 bit?
	* Open the start menu
	* Right click on `Computer` and click `Properties`
	* In the System section, `System type` should say 32- or 64-bit Operating System
* Unzip the files
* Right-click `BINDInstall.exe` and `Run as administrator`
	* Target Directory: `C:\Windows\SysWOW64\dns`
	* Service Account Name: `named`
	* Options:
		* [x] Tools Only
		* [ ] Automatic Startup
		* [ ] Keep Config Files After Uninstall
		* [ ] Start BIND Service After Install
	* `Install`
* Set the path
	* Start menu > Right click on `Computer` > `Properties` > `Advanced System Settings` > `Advanced` tab > `Environment Variables`
	* Under `System variables`, scroll to find `Path` and click `Edit...`
	* Go to the end of the line, type a semicolon: `;` and then `%SYSTEMROOT%\SysWOW64\dns\bin`
	* Hit `OK` a bunch of times.
* Close and reopen the Command Prompt
* Type `dig` to confirm


## Windows 10

Source: http://nil.uniza.sk/linux-howto/how-install-dig-dns-tool-windows-10

* https://www.isc.org/downloads/
* Click `BIND`
* Click `Download` next to the version with the Status of "Current"
* Pick your architecture
* 32 or 64 bit?
	* Right click on the Windows/Start menu
	* Click `System`
	* In the System section, `System type` should say 32- or 64-bit Operating System
* If the files don't download (0kb)
	* Make sure you aren't using Microsoft Edge. It can't yet connect to FTP sites to download. Pretty much any other browser should work fine.
* Unzip the files
* Right-click `BINDInstall.exe` and `Run as administrator`
	* Target Directory: `C:\Program Files\ISC BIND 9`
	* Service Account Name: `named`
	* Options:
		* [x] Tools Only
		* [ ] Automatic Startup
		* [ ] Keep Config Files After Uninstall
		* [ ] Start BIND Service After Install
* Set the path
	* Use the search box (next to the start/windows menu) and type in `environment`
	* Click on `Edit the system environment variables`
	* Click `Environment Variables...` at the bottom
	* Under `System variables`, scroll to find `Path` and click `Edit...`
	* Go to the end of the line, type a semicolon: `;` and then `C:\Program Files\ISC BIND 9\bin`
	* Hit `OK` a bunch of times.
* Close and reopen the Command Prompt
* Type `dig` to confirm
