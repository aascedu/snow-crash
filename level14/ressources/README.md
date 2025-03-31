Entering level14 there is no file in home directory, no files on the machine that we have access to.
We are on a clean VM with nothing more than a brand new one, except getflag
We are now able to reverse binaries, so why not try with getflag.

Doing it gives us the secrets behing all previous levels: all depends on the uid of the user you're logged in.
But, even using GDB I wasn't able to bypass getuid calls so i tried another way.
The binary contains many encrypted flags that we can copy, and the cherry on top, it also contains the function that decrypts those flags.
Using a decompiler (ghidra) I was able to reverse it to pseudo-C and compile it on my machine.
Now that i have the compiled function, I just have to pass it the flag I want.
To find the right one I choose to check /etc/passwd to target the right uid, the uid of flag14.
Turns out it'd 3014, or 0xbc6 in hexadecimal. Searching for 0xbc6 in the decompiled code, i was able to find the right flag to decrypt.
