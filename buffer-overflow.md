# Understanding Buffer Overflow

The term buffer is loosely used to refer to any area in memory where more than one piece of data is stored. An overflow occurs when we try to fill more data than the buffer can handle. You can think an overflow such pouring 5 gallons of water into a 4-gallon bucket.

![](.gitbook/assets/image%20%2826%29.png)

This is where a buffer overflow happens, which is a condition in a program where a function attempts to copy more data into a buffer than it can hold. If you have allocated a specific amount of space in the stack, for example, 10, and you exceed this by trying to copy more than 10 characters, then you have a buffer overflow.

Example:

![](.gitbook/assets/image%20%2849%29.png)

![](.gitbook/assets/image%20%284%29.png)

if the source, argv\[1\], is bigger than the destination, buffer, an overflow occurs. This means that whatever was in the memory location right after the buffer, is overwritten with our input.

In this example, it causes the application to crash. But, an attacker may be able to craft the input in a way that the program executes specific code, allowing the attacker to gain control of the program flow.

There is a safe version of the strcpy function, and it is called strncpy \(notice the n in the function name\). With this knowledge, we can say that a safe implementation of the previous program would be something like this:

![](.gitbook/assets/image%20%2854%29.png)

In the above code, there will be no overflow because the data we can copy is limited. This time the function will only copy 10 bytes of data from argv\[1\], while the rest will be discarded.

Stack representation of strcpy

![](.gitbook/assets/image%20%2833%29.png)

As you can see in this stack representation, this data includes the EBP, the EIP and all the other bytes related to the previous stack frame.

![](.gitbook/assets/image%20%283%29.png)

Since the EIP has been overwritten with AAAA, once the epilogue takes place, the program will try to return to a completely wrong address. Remember that EIP points to the next instruction. An attacker can craft the payload in the input of the program to get the control of the program flow and return the function to a specific memory address location.

Example 2:

goodpwd.cpp

![](.gitbook/assets/image%20%2835%29.png)

![](.gitbook/assets/image%20%282%29.png)

![](.gitbook/assets/image%20%2840%29.png)

From the message box, we can see that the program tried to access the location pointed to 0x41414141 \(0x41 is the hexadecimal value of A\).This means that we have overwritten the EIP with our input, causing the overflow and then crashing the program. The EIP, instruction pointer, tells the program what to run next, but as a result of all of our A’s, that address value is A.

**Objective:**

* We would like to use this buffer overflow to take control of the program execution and be able to execute the function good\_password. The idea is to craft an input that forces the program to jump into the memory address of the function. 

The important thing to remember here is that to perform a buffer overflow, you need to put specific code in specific space in the stack. Our example used a string of A’s that caused it to crash, but was it 20 A’s, 32 A’s, 50 A’s or 100? This is one of the very important questions that we need the answer to. The second question is: what address do we want written in the EIP?

ASM of goodpwd.cpp

![](.gitbook/assets/image%20%2841%29.png)

* bf\_overflow function is at address 00401529
* good\_password function is at address 00401548

What we have to do now is find the EIP. By overwriting the EIP, we can control the application execution flow \(EIP is the return address\).

![](.gitbook/assets/image%20%2816%29.png)

![](.gitbook/assets/image%20%2868%29.png)

you will see the EIP in the reverse order \(0x44434241\) because Windows uses little-endian and thus, the most significant byte comes at the lowest position.

What is happening is that the value ABCD is overwriting the correct EIP in the stack. Now comes the magic. In order to gain control if this program, we have to replace the EIP \(ABCD in our input\) with the address of the good\_password function. We disassembled it previously and discovered the address to be 00401548. By inserting this address to the EIP location, we are forcing the program to return to the good\_password memory address and execute its code.

If we check the input that overwrote the EIP with 0x44434241, it is composed of 22 A characters and then ABCD. Therefore, the helper program will fill the first 22 characters with some junk bytes and then append the address of good\_function \(00401548\).

![](.gitbook/assets/image%20%2831%29.png)

**Notice that we did not add \x00 to the payload since this is a NULL byte. Although we will talk more about NULL bytes in the next section, for now, you just need to know that when functions such as strcpy encounter a NULL byte in the source string, they will stop copying data.**

Let’s now compile the helper and save it in the same path of goodpwd.exe.

![](.gitbook/assets/image%20%2832%29.png)

We successfully called the good\_password function! However, the program might/might not crash after executing the above function. If it does crash, it might be that we have damaged some other registers or data on the stack which might be useful.







