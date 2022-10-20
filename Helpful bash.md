## Links
-   Start here https://ryanstutorials.net/linuxtutorial/
-   Slightly more advanced https://wiki.bash-hackers.org/scripting/basics
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
- wc - word count
- cut - allows you get columns of text 
- sed - allows find and replace capability of raw text
- jq - does what sed does but with json files
- yq - does what sed does but with yaml files
- uniq - removes duplicate lines

### Grep and Regular Expressions

- grep <string>
- egrep <string or regular expression>

#### Regular expressions
- . (dot) - a single character.
- ? - the preceding character matches 0 or 1 times only.
- * - the preceding character matches 0 or more times.
- + - the preceding character matches 1 or more times.
- {n} - the preceding character matches exactly n times.
- {n,m} - the preceding character matches at least n times and not more than m times.
- [agd] - the character is one of those included within the square brackets.
- [^agd] - the character is not one of those included within the square brackets.
- [c-f] - the dash within the square brackets operates as a range. In this case it means either the letters c, d, e or f.
- () - allows us to group several characters to behave as one.
- | (pipe symbol) - the logical OR operation.
    example: "a|b" no spaces, one string
- ^ - matches the beginning of the line.
- $ - matches the end of the line.

## Pipes and redirections

- STDIN(0) - Standard input.
- STDOUT(1) - Standard output.
- STDERR(2) - Standard error.
- ">" - will take stdout and print it to a file. It will overwrite whatever content is there.
- ">>" - will take stdout and print it to a file. It will append to whatever content is there.
- "<" - send data to standard output
-   example: wc -l < somefile.txt # this will print word count not write to file
- "2>" - will take stderr and print it to a file. It will overwrite whatever content is there.
- "2>>" - will take stderr and print it to a file. It will append to whatever content is there.
 
## Bash utilities

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
