# Assemblers, debuggers and tools

Assembler

An assembler is a program that translates the Assembly language to the machine code. There are several different assemblers that depend on the target system’s ISA:

* Microsoft Macro Assembler \(MASM\), x86 assembler that uses the Intel syntax for MS-DOS and Microsoft Windows
* GNU Assembler \(GAS\), used by the GNU Project, default back-end of GCC.
*  Netwide Assembler \(NASM\), x86 architecture used to write 16-bit, 32-bit \(IA-32\) and 64-bit \(x86-64\) programs, one of the most popular assemblers for Linux 
* Flat Assembler \(FASM\), x86, supports Intel-style assembly language on the IA-32 and x86-64

When a source code file is assembled, the resulting file is called an object file. It is a binary representation of the program.

Once the assembler has created the object file, a linker is needed in order to create the actual executable file. What a linker does is take one or more object files and combine them to create the executable file. An example of these object files are the kernel32.dll and user32.dll which are required to create a windows executable that accesses certain libraries.

![](.gitbook/assets/image%20%2856%29.png)

Compiler

The complier is similar to the assembler. It converts high-level source code \(such as C\) into low-level code or directly into an object file. Therefore, once the output file is created, the previous process will be executed on the file. The end result is an executable file.

ASM Basics

![](.gitbook/assets/image%20%2861%29.png)

![](.gitbook/assets/image%20%2837%29.png)

Depending on the architectural syntax, instructions and rules may vary. For example, the source and the destination operands may be in different position.

![](.gitbook/assets/image%20%2813%29.png)

As you can see, AT&T puts a percent sign \(%\) before registers names and a dollar sign \($\) before numbers. Another thing to notice is that AT&T adds a suffix to the instruction, which defines the operand size: Q \(quad – 64 bits\), L \(long – 32 bits\), W \(word -16 bits\), B \(byte – 8 bits\).

PUSH Instruction

![](.gitbook/assets/image%20%286%29.png)

POP Instruction

![](.gitbook/assets/image%20%2844%29.png)

Call Instruction

![](.gitbook/assets/image%20%287%29.png)

Debugger

![](.gitbook/assets/image%20%2835%29.png)

* In the first column is the address location 
* In the second column is the machine code 
* In the third column is the assembly language 
* In the fourth column is the debugger comments



