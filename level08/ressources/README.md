Entering level08, we do 'ls' again.
This time, two files, an executable named 'level08' and a text file named 'token'.

We don't have the permissions to open token, but we can read and execute level08.
Here's what i do:
```
$> ./level08
./level08 [file to read]
```
the program prompts for a file to read so i decide to give it the token file
```
$> ./level08
you may not access 'token'
```
Seems like we can't do that.
decompiling the executable gives us those interesting lines:
```c
if (strstr(argv[1], "token"))
{
    printf("You may not access '%s'\n", argv[1]);
    exit(1);
}
```
here we can see that if the file we give to that program contains 'token', it won't do anything. Therefore we need to find a way to pass 'token' to that program without naming it 'token'.
I ask myself how could I do that, knowing that I can't copy the file, neither move it.
Then I remember about symlinks, we could create a file that does not contains anything but points directly to our token file, i could name the symlink something else and that's it.

Creating a symlink in the tmp directory that points to the token file in my home directory:
```sh
cd /tmp
ln -s $HOME/token ./my_symlink
cd
./level08 /tmp/my_symlink
```
that last call to ./level08 gave me the token, so I tried to switch to user flag08 with that as a password and it worked. Now I just have to getflag and we're getting access granted.
