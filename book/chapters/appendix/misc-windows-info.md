## Windows - What's my architecture?

At a very low level, every computer processor deals with integers as "bits"; ones or zeros, which are grouped into "words". Many CPUs these days use words made up of 64 bits, but many still use 32. This is broadly considered your computer's "architecture". Every program is compiled for either 32-bit or 64-bit integers. If your CPU's architecture doesn't match the program's architecture, weird and bad things can happen, so make sure you get the right version of the program.

To check your CPU architecture, do the following:

### Windows 7

1. Open the start menu
2. Right click on `Computer` and click `Properties`
3. In the System section, `System type` should say 32- or 64-bit Operating System.
4. And now you know.

### Windows 10

1. Right click on the Windows/Start menu
2. Click `System`
3. In the System section, `System type` should say 32- or 64-bit Operating System.

## Windows - How do I set my path?

In the command prompt, when you type a command like `dig`, it usually knows you want to execute that command, and how to find it. The way this works, is there are a list of places (directories) it knows to look for commands. This list is called the "path". You can check your current path by typing (you'll never guess) `path` in your command prompt.

Imagine, for example, that `dig` is located at `C:\Folder One\dig`, but your path is only `C:\Program Files;C:\Folder Two`. The command prompt won't be able to find it! It will report something like _'dig' is not recognized as an internal or external command, operable program or batch file._ That's because it doesn't know to look for dig inside of Folder One (and also apparently doesn't know about the oxford comma). We need to add "C:\Folder One" to our path.

The path is a "system environment variable" which means the whole path is represented as a single, long string. Multiple directories in the path are separated with semicolons (`;`).

To set or edit your path, do the following:

### Windows 7

1. Open the Start menu.
2. Right click on `Computer` > `Properties` > `Advanced System Settings` > `Advanced` tab > `Environment Variables`.
3. Under `System variables`, scroll to find `Path` and click `Edit...`
4. Go to the end of the textfield, type a semicolon to separate what you're about to type from the other directories: `;`
5. Add the path.
6. Hit `OK` a bunch until all the windows are gone.

### Windows 10

1. Right click on the Windows/Start menu.
2. Click on `Control Panel`.
3. Navigate to `System and Security` > `System` > `Advanced system settings` (sidebar).
4. Click `Environment Variables...` at the bottom.
5. Under `System variables`, scroll to find `Path` and click `Edit...`
6. Go to the end of the textfield, type a semicolon to separate what you're about to type from the other directories: `;`
7. Add the path.
7. Hit `OK` a bunch until all the windows are gone.

