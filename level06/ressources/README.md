By doing `ls` on home directory we see an executable and a php file, the executable seems to do the same thing as if we do `php level06.php` si I assume it's the same file, compiled, and with more elevated privileges (so we can get the flag).

As those files have the same purpose, we can take a look at the php file to understand what they do.
We can see the php script uses many times preg_replace, so I do my searches and find out it's vulnerable to code injection as one of those preg_replace calls takes directly an entire file passed we can pass to the script. Now I know what to aim for: inject code in the script to make it execute something that can make me get the flag I want (i.e. the command `getflag`(for example (i guess)))

Now that i know what to do, I need to figure out how.
To make the injection I want, I need to pass the code in a file and between '\[x ' and '\]', and so do I, making a file /tmp/input including `[x ]`

After some research, I find that tildes characters makes php execute a shell command, convenient isn't it ?
I am now stuck with a file containing [x \`getflag\`].
The script actually removes the [x and ] so i know the regex is good but can´t inject code yet.
Some more research and thoughts later, I find out php can interpret some code inside a string to ease format strings, and this can help me!
My injection code will then need that syntax to be interpreted ${...}

I finally come out with my file containing [x ${`getflag`}] and it works, the script gave me the flag i was waiting for as i expected!
