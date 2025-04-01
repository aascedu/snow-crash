Now on level13, we just have a binary file, as usual we put it in a decompiler.

First we see a token passed to a function 'ft_des' but that token is not exploitable.
That token might be encrypted and could be decrypted with the ft_des call.
Asking other students for an idea, someone tell me that i could exploit the binary using GDB.
GDB can open the binary, place breakpoints and jump to some instructions.

Second we see that the only requirement to pass the binary's tests is to be a certain uid, not exploitable there but using GDB we could skip that condition.

To do so we need to set a breakpoint on the if instruction and to run the program. The program stops on the if and we can now tell GDB to jump to the printf(ft_des...) instruction we see in the decompiler.
Entering 'jump *0x080485e9' does the job.
And voilà: the flag we wanted is printed on the output of our program.
