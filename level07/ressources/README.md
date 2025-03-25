Listing files in home directory of our new user we find an executable 'level07'.
Executing it prints 'level07'
As for level03, I decide to decompile it to see what it really does.

First, I see those lines that are quite explicit
```
asprintf(&var_1c, "/bin/echo %s ", getenv("LOGNAME"));
return system(var_1c);
```
The program seems to execute `/bin/echo $LOGNAME`, it explains why it printed 'level07' when I executed it.
As I can change the environnement variable LOGNAME, I decide to do so and pretend to be 'flag07', because... why not!
Unfortunately, no changes, reexecuting the program gives me 'flag07', and that makes sense.

Rewatching the code, I figure out how to inject a command inside the env variable that is being part of the executed command. so I try something like
```sh
export LOGNAME='`getflag`'
```
I use the single quotes to escape the backticks from my export command so the program does not get the output of getflag but actually echo the output of it's execution of getflag, and bingo, I got the flag I wanted!
