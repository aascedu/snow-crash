Getting in level09, we find an executable and a token file.
This time, we have rights to open token, but expectedly the token inside the file is not the password for the flag09 account.
Doing 'cat token' I notice the token contains non-printable chars.

Now, let's take a look at the executable.
Executing it shows us it needs an argument to work, so I pass it the token file. That gives me 'tpmhr', means nothing and does not look like a token.
Lets decompile it then!
Turns out that the program is not waiting for a file name, it only reads and operates on the argument itself.
Executing the program as follows:
```sh
./level09 `cat token`
```
The program outputs is more similar to a token but there's even more non-printable chars. For a moment i'm questionning the fact that the program might be sort of a hash function previously applied to the token, and i'm thinking I need to make the reverse hash function to get the right token back.

Reversing the executable explains us the technique used to transform the entering token into the output it gives.
It's shifting every char in the token by their position in the token itself!
Easy enough to reverse, i'm writing and compiling this C code:
```c
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>

int main(int argc, char **argv) {
    if (argc != 2)
        return (1);
    char buffer[4000];
    int fd;
    fd = open(argv[1], O_RDONLY);
    read(fd, buffer, 100);
    int i;
    i = 0;
    while (i + 1 < strlen(buffer)) {
        buffer[i] -= i;
        i++;
    }
    // buffer[i] = 0;
    printf("\n%s", buffer);
    return (0);
}
```
The output of this code with the hashed token gives me a well formatted token without non-printable chars, therefore I tried this password to connect as flag09 and it worked
