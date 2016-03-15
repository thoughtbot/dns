## Installing dig, host, and nslookup on Windows

First up, let's make sure you don't already have these tools installed.

1. Open your Command Prompt by using the Windows/Start menu to search for `Command Prompt`.
2. Right-click and run it as an administrator
3. After the black window opens, type each of these followed by the enter key:
    * `dig` - If installed, it will list all of the root servers like `a.root-servers.net`, `b.root-servers.net`, etc.
    * `host` - If installed, this will list all available options we can use to change host's output.
    * `nslookup` - If installed, this will open the nslookup command prompt. You'll see simply an `>` and a blinking cursor. To exit out of this mode, type `exit` and hit enter.
4. If any of these are not installed, a message like this will be displayed: _'command' is not recognized as an internal or external command, operable program or batch file._
5. If any of these three return that message, move on to the next section. If all three are installed, you're good to go!

---

1. First, download BIND here: [isc.org/downloads](https://www.isc.org/downloads/).
    * Click `BIND`
    * Click `Download` next to the version with the Status of "Current"
    * Pick the version that has your architecture (win 32-bit or win 64-bit). If you're not sure, check the _Windows - What's my architecture_ section.
2. Extract the files open the folder
3. Right-click `BINDInstall.exe` and click `Run as administrator`
4. When it's open, fill out each field like this:
  * Target Directory: `C:\Program Files\dns`
  * Service Account Name: `named`
  * Options:
    * [x] Tools Only
    * [ ] Automatic Startup
    * [ ] Keep Config Files After Uninstall
    * [ ] Start BIND Service After Install
5. Then click the **Install** button.
6. You'll then need to add `C:\Program Files\dns\bin` to your path. If you don't know how to do that, check the _Windows - How do I set my path?_ section.
7. After that, close reopen your Command Prompt and try the same commands from before:
    * `dig` - If installed, it will list all of the root servers like `a.root-servers.net`, `b.root-servers.net`, etc.
    * `host` - If installed, this will list all available options we can use to change host's output.
    * `nslookup` - If installed, this will open the nslookup command prompt. You'll see simply an `>` and a blinking cursor. To exit out of this mode, type `exit` and hit enter.

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
