# Finding Buffer Overflows

Before studying how to exploit buffer overflows and execute payloads, it is important to know how to find them. Any application that uses unsafe operations, such as those below \(there are many others\), might be vulnerable to buffer overflows.

![](.gitbook/assets/image%20%2871%29.png)

Any function which carries out the following operations may be vulnerable to buffer overflows: 

* Does not properly validate inputs before operating 
* Does not check input boundaries

However, buffer overflows are problems of unsafe languages, which allow the use of pointers or provide raw access to memory. All the interpreted languages such as C\#, Visual Basic, .Net, JAVA, etc. are safe from such vulnerabilities.

buffer overflows can be triggered by any of the following buffer operations: 

* User input 
* Data loaded from a disk 
* Data from the network

Fuzzing

Fuzzing is a software testing technique that provides invalid data, i.e., unexpected or random data as input to a program. Input can be in any form such as: 

*  Command line 
*  Parameters 
* Network data 
* File input 
*  Databases 
* Shared memory regions 
* Keyboard/mouse input 
* Environment variables

This technique basically works by supplying a random data to the program, and then the program is checked for incorrect behavior such as: 

* Memory hogging 
* CPU hogging 
* Crashing

Finding buffer overflows in binary programs

Example : cookie.c

![](.gitbook/assets/image%20%2852%29.png)

First, we will go through the process of understanding the code, and then we will exploit it.

ASM

![](.gitbook/assets/image%20%2875%29.png)

![](.gitbook/assets/image%20%2850%29.png)

![](.gitbook/assets/image%20%2844%29.png)

In this sample, the message you win! is never printed on screen because the cookie variable is set to 0 and never changes.

However, since the function gets can be overflowed, we will demonstrate that we can:

* Easily control program flow using variable control 
* Buffer overflows can even be controlled via keyboard-inputs \(though it's hard to type shell-code using hand, but nonetheless, it can be done\)
* Find overflows in binaries

Stack Frame of cookie

![](.gitbook/assets/image%20%2847%29.png)

**Also, note that since ESP points to the top of the stack, things such as local variables and function arguments can also be accessed using the \[ESP + x\] combination. As you already know, the square brackets are an assembly language notation used to indicate that we are pointing to the memory. This means we are pointing to data stored at memory location \[EBP + x\] and not the value EBP + X.**

Now that you can convert the program to pseudo-code, you can easily tell that the user-input is not verified and therefore, has a buffer overflow vulnerability. We can say this because, the function gets never verifies the length of the data \(also note stack space is limited\) and in this case, user has full control over the data. Therefore, it is susceptible to an overflow.

Looking at the stack, you should notice that if \[EBP-4\] can be controlled, then we can reverse the jump and thus control the program flow.

