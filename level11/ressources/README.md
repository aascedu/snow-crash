EZ.

Looking at level11.lua we see that the program is a server running on port 5151 of our machine.
That means that we have to connect to it to use it.
We can see as well that the server is a socket server, so we can easily connect with nc.
The command line `nc localhost 5151` prompts for a password, but we don't have any.
Looking back to the server's code we can follow the input to find any path on exploiting it from the input we give.

The password we enter is given to a function named hash. That function actually use popen to use sha1sum on it. as popen litteraly executes a shell command on the machine, we see what to do: code injection inside the password we give.
the executed command is
```sh
echo <password> | sha1sum
```
We just have to replace password with something that complete the command in a way we can exploit it.
here is the command we want the server to execute, so it does not affect the behaviour of the server, but actually prints on all opened tty sessions the flag that the server runner can get.
```sh
echo `getflag` | wall ; echo <password> | sha1sum
```

so we connect to the server over nc and when the password is prompted, we enter: '`getflag` | wall ; '
Comes out that the flag is printed as expected.
