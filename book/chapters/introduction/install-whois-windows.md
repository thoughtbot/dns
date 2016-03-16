## Windows 7/8

* Visit https://technet.microsoft.com/en-us/sysinternals/bb897435.aspx?f=255&MSPPError=-2147217396
* Download
* Unzip
* Go to the `Start` menu > `Computer` > `Local Disk (C:)` > `Program Files`
* Create a new folder called `whois`
* Move whois program inside downloads (not the folder, but the thing inside the folder) to the whois folder created in the last step
* Set the path
	* Start menu > Right click on `Computer` > `Properties` > `Advanced System Settings` > `Advanced` tab > `Environment Variables`
	* Under `System variables`, scroll to find `Path` and click `Edit...`
	* Go to the end of the line, type a semicolon: `;` and then `C:\Program Files\whois`
	* Hit `OK` a bunch of times.
* Close and reopen the Command Prompt
* Type `whois` to confirm

## Windows 10

* Visit https://technet.microsoft.com/en-us/sysinternals/bb897435.aspx
* Download
* Unzip
* Go to the `Start` menu > `Computer` > `Local Disk (C:)` > `Program Files`
* Create a new folder called `whois`
* Move whois program inside downloads (not the folder, but the thing inside the folder) to the whois folder created in the last step
* Set the path
	* Start menu > Click `File Explorer` > Right-click `This PC` > `Properties` > `Advanced System Settings` > `Advanced` tab > `Environment Variables`
	* Under `System variables`, scroll to find `Path` and click `Edit...`
	* Go to the end of the line, type a semicolon: `;` and then `C:\Program Files\whois`
	* Hit `OK` a bunch of times.
* Close and reopen the Command Prompt
* Type `whois` to confirm
