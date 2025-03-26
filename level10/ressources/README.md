```sh
echo 'token' > tk && ln -nsf tk token ; ln -nsf $HOME/token token && $HOME/level10 token localhost
```
This command when executed in /tmp on the VM, creates a file 'tk' that we can access, then it creates a symlink named token to this file.
The second part of the command is gonna run two commands at once, allowing for race conditions. The ln command will redirect the existing symlink to the token in $HOME we can't access, while the level10 program will check the same symlink.
