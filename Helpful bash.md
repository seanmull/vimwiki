## Links

-   Start here https://wiki.bash-hackers.org/scripting/basics
-   Basic commands: https://wiki.bash-hackers.org/syntax/basicgrammar
-   Defensive-bash-programming https://web.archive.org/web/20180917174959/http://www.kfirlavi.com/blog/2012/11/14/defensive-bash-programming
-   Main list -https://github.com/awesome-lists/awesome-bash
-   Explain shell to find out what the command is doing

## Basic commands

### Wildcards
- "*" for wildcard search no place holder
-   ls ap* will pick up apple.txt
- ? for wildcard which is place holder specific
-   ls ??l will pick up aal.txt but not aap.txt
- [] for wildcards with ranges
-   ls "*[0-9]*" will pick up foo1 foo2 ...
- ^ for what doesn't meet a condition
-   ls ^a will pick up ball but not apple

### Permissions

- If you want to give a file of folder full permissions
```bash
chmod 777 <some dir>
```

### Filters

- head - prints the first of some text
- tail - prints the last part of the text helpful with -f to follow the file
- sort
- nl - number of lines

## Bash utils

-   ranger - good for searching for files
-   htop - for getting the utils of a system
-   speedread - may want to try this for reading large amounts of text. See if I can get
-   books in raw text format.
-   neofetch - to get basic details for system
-   trash - to keep things in trash can
-   sudo!! - runs the last command as sudo
-   killall -9 <process> it kills all the processes
-   uptime- how long the system has been up
-   background processes
-   ctrl-z to minimize
-   fg to put it foreground

## Syntax

use :Shfmt : May want to hot key this when I start writing in bash
