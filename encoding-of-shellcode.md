# Encoding of Shellcode

Shellcodes are generally encoded since most vulnerabilities have some form of restriction over data which is being overflowed.

C language string functions work till a NULL, or 0 bytes is found. If the string2 variable contained the NULL character \x00, then the strcat function would only copy only the data before. Let’s try to edit string2 by adding a NULL character between \x42 and \x43.

![](.gitbook/assets/image%20%2847%29.png)

![](.gitbook/assets/image%20%2825%29.png)

Shellcodes should be Null-free to guarantee the execution. There are several types of shellcode encoding:

* Null-free encoding 
* Alphanumeric and printable encoding

Example of Creating custom Shellcode

-&gt; Create a shellcode that will cause the thread to sleep for five seconds

The sleep functionality is provided by the function Sleep in Kernel32.dll .We can obtain the address in different ways and with different tools. To use Immunity Debugger, we have to open the kernel32.dll file, right-click on the disassemble panel and select Search for &gt; Name in all modules

![](.gitbook/assets/image%20%2863%29.png)

Now that we have the address of the Sleep function, and we know that it requires one parameter, the next step is to create a small ASM code that calls this function. Once we have the ASM code compiled, we can extract \(by decompiling it\) the machine code and use it for our shellcode.

![](.gitbook/assets/image%20%2858%29.png)

Next, we need to compile our ASM code.

![](.gitbook/assets/image%20%2816%29.png)

![](.gitbook/assets/image%20%2877%29.png)

On the left, we have the byte code, while on the right we have the ASM code. Our shellcode is almost done, we just need to do some cleaning up. We need to edit it and remove the spaces and add the \x prefix.

![](.gitbook/assets/image%20%288%29.png)

More Advanced shellcode

This simple code will spawn a new command prompt and will maximize the window.

![](.gitbook/assets/image%20%2839%29.png)

View  [4\_Shellcoding.pdf](file:///D:/e-LearnSecurity/ePTP%20v5/1-%20System%20Security/4_Shellcoding.pdf) for more information

