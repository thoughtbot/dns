## Install OpenSSL on Windows

We'll be using OpenSSL in the Securing Your Website chapter, so you'll want to make sure you have it installed. Let's make sure you don't already have it installed:

1. Open your Command Prompt by using the Windows/Start menu to search for `Command Prompt`.
2. Right-click and run it as an administrator
3. After the black window opens, type `openssl version`
4. If OpenSSL is not installed, the command prompt will say: _'openssl' is not recognized as an internal or external command, operable program or batch file._

If, by some miracle, it is installed, it will show it's version number; something like `OpenSSL 1.0.2g  1 Mar 2016` and you're good to go. If not, check out the steps below.


1. First, visit [this site](http://slproweb.com/products/Win32OpenSSL.html).
2. Scroll down and find the latest "Light" version for your architecture (Win32 or Win64). For example, if your computer is 64bit, you might download _Win64 OpenSSL v1.0.2g Light_. If you're not sure what your architecture is, check the _Windows - What's my architecture_ section.
3. Extract and open the installer.
    * Accept the installer's agreement.
    * Install to `C:\Program Files\openssl`.
    * Add to Start menu as `OpenSSL`.
    * Copy OpenSSL DLLs to `The OpenSSL binaries /bin directory`.
    * Click Install.
4. You'll then need to add `C:\Program Files\openssl\bin` to your path. If you don't know how to do that, check the _Windows - How do I set my path?_ section.
5. Check to make sure it's installed by closing and reopening the Command Prompt. Then type `openssl version`. If everything went correctly, it should report back `OpenSSL 1.0.2g  1 Mar 2016`.
