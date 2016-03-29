## Installing whois on Windows

Let's make sure whois isn't already installed. Open your Command Prompt by using the Windows/Start menu to search for `Command Prompt`. Once it opens, type `whois`. If installed, whois will print out a brief list of usage instructions like so:

```shell
$ whois

usage: whois [-aAbdgiIlmQrR6] [-c country-code | -h hostname] [-p port] name ...
```

If instead you get _'whois' is not recognized as an internal or external command, operable program or batch file._ you'll need to install whois.

1. First, visit [this site](https://technet.microsoft.com/en-us/sysinternals/bb897435.aspx?f=255&MSPPError=-2147217396).
2. There are three identical download links on the page. Pick whichever you feel you have the most emotional connection to and click it to download the whois installer.
3. Extract the downloaded file. Note the `whois` program inside the resulting folder.
4. Create a new folder at `C:\Program Files\whois`
5. Move the `whois` program (not the extracted folder, but the program inside the folder) to the whois folder created in the last step.
6. Add `C:\Program Files\whois` to your path. If you don't know how to do that, check the _Windows - How do I set my path?_ section.
7. Check if it was installed correctly by closing and reopening the Command Prompt.
8. Type `whois` to confirm. If you see usage instructions, it's been installed correctly!
