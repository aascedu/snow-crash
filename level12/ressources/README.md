In the home directory there is a perl script, opening it, we see it's running on localhost, so we may have to make requests to it in order to exploit it.

As in level04, we have to pass an argument to the curl request on the server, as the server edits our inputs by setting it to uppercase we need to figure out how to call a script in /tmp without naming it '/tmp'
The answer is in the fact that we can call every root directories by calling it '/*' and naming our script with uppercase chars.
As the server is running and we don't have access to it's stdout, we need to figure out a way to get an output from the script. I chose the option to call wall on the output of getflag to flush all opened terminals with the token.
