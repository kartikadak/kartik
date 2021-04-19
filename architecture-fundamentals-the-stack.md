# Architecture fundamentals\(The stack\)

Stack

The Stack is a Last-in-First-out \(LIFO\) block of memory. You can think of the stack as an array used for saving a function’s return addresses, passing function arguments, and storing local variables.

The purpose of the ESP register \(Stack Pointer\) is to identify the top of the stack, and it is modified each time a value is pushed in \(PUSH\) or popped out \(POP\).

The stack grows downward, towards the lower memory addresses.

It was decided that the Heap would start from lower addresses and grow upwards and the Stack would start from the end of the memory and grow downward.

![](.gitbook/assets/image%20%2875%29.png)

PUSH instruction

A PUSH instruction subtracts 4 \(in 32-bit\) or 8 \(in 64-bit\) from the ESP and writes the data to the memory address in the ESP, and then updates the ESP to the top of the stack.

If we do not subtract it, the PUSH operation will overwrite the current location pointed by ESP \(the top\) and we would lose data.

![](.gitbook/assets/image%20%2810%29.png)

POP Instruction

The POP operation is the opposite of PUSH, and it retrieves data from the top of the Stack. Therefore, the data contained at the address location in ESP \(the top of the stack\) is retrieved and stored \(usually in another register\). After a POP operation, the ESP value is incremented, in x86 by 4 or in x64 by 8.

![](.gitbook/assets/image%20%2843%29.png)

It is important to understand that the value popped from the stack is not deleted \(or zeroed\). It will stay in the stack until another instruction overwrites it.

Stack Frames

Functions contain two important components, the prologue and the epilogue. The prologue prepares the stack to be used, similar to putting a bookmark in a book. When the function has completed, the epilogue resets the stack to the prologue settings.

The Stack consists of logical stack frames \(portions/areas of the Stack\), that are PUSHed when calling a function and POPped when returning a value.

When a subroutine, such as a function or procedure, is started, a stack frame is created and assigned to the current ESP location.

When the subroutine ends, two things happen: 

1. The program receives the parameters passed from the subroutine. 
2. The Instruction Pointer \(EIP\) is reset to the location at the time of the initial call.

In other words, the stack frame keeps track of the location where each subroutine should return the control when it terminates.

Example of working of stack frame

![](.gitbook/assets/image%20%2819%29.png)

The first stack frame that needs to be pushed to the Stack is the main\(\) stack frame. Once initialized, the stack pointer is set to the top of the stack and a new main\(\) stack frame is created.

![](.gitbook/assets/image%20%2846%29.png)

Once inside main\(\), the first instruction that executes is a call to the function named a\(\). Once again, the stack pointer is set to the top of the stack of main\(\) and a new stack frame for a\(\) is created on the stack.

![](.gitbook/assets/image%20%2820%29.png)

Similarly

![](.gitbook/assets/image%20%2862%29.png)

When the function completes, the stack pointer is moved to its previous location, and the program returns to the stack frame of a\(\) and continues with the next instruction.

![](.gitbook/assets/image%20%2866%29.png)

Stack frame when it has parameters

![](.gitbook/assets/image%20%2815%29.png)

When the program starts, the function main\(\) parameters \(argc, argv\) will be pushed on the stack, from right to left.

![](.gitbook/assets/image%20%2870%29.png)

Then, the processor PUSHes the content of the EIP \(Instruction Pointer\) to the stack and points to the first byte after the CALL instruction.

This process is important because we need to know the address of the next instruction in order to proceed when we return from the function called.

The caller \(the instruction that executes the function calls - the OS in this case\) loses its control, and the callee \(the function that is called - the main function\) takes control.

![](.gitbook/assets/image%20%2838%29.png)

Now that we are in the main\(\) function, a new stack frame needs to be created. Because we don’t want to lose the old stack frame information, we have to save the current EBP on the Stack

![](.gitbook/assets/image%20%2865%29.png)

The previous step is known as the prologue: it is a sequence of instructions that take place at the beginning of a function. This will occur for all functions. Once the callee gets the control, it will execute the following instructions:

![](.gitbook/assets/image%20%2824%29.png)

1. The first instruction \(push ebp\) saves the old base pointer onto the stack, so it can be restored later on when the function returns.
2. The second instruction \(mov ebp, esp\), copies the value of the Stack pointer \(ESP - top of the stack\) into the base pointer \(EBP\); this creates a new stack frame on top of the Stack.
3. The last instruction \(sub esp, X\), moves the Stack Pointer \(top of the stack\) by decreasing its value; this is necessary to make space for the local variables.

![](.gitbook/assets/image%20%2867%29.png)

Once the prologue ends, the stack frame for main\(\) is complete, and the local variables are copied to the stack.

Since ESP is not pointing to the memory address right after EBP, we cannot use the PUSH operation, since PUSH stores the value on top of the stack

![](.gitbook/assets/image%20%2826%29.png)

![](.gitbook/assets/image%20%2830%29.png)

Looking back at the source code from the second example, we can see that the next instruction calls the function functest\(\).

![](.gitbook/assets/image%20%289%29.png)

When the program enters a function, the prologue is executed to create the new stack frame. When the program executes a return statement, the previous stack frame is restored thanks to the epilogue

The operations executed by the epilogue are the following: 

* Return the control to the caller.
* Replace the stack pointer with the current base pointer. It restores its value to before the prologue; this is done by POPping the base pointer from the stack.
* Returns to the caller by POPping the instruction pointer from the stack \(stored in the stack\) and then it jumps to it.

![](.gitbook/assets/image%20%2814%29.png)

![](.gitbook/assets/image%20%2864%29.png)

* The first instruction in the epilogue is mov esp, ebp. After it gets executed, both ESP and EBP point to the same location.
* The next instruction is pop ebp, which simply POPS the value from the top of the stack into EBP. Since the top of the Stack points to the memory address location where the old EBP is stored \(the EBP of the caller\), the caller stack frame is restored.
* Therefore, ESP now points to the old EIP previously stored.
* The last instruction that the epilogue will execute is ret.
* RET pops the value contained at the top of the stack to the old EIP – the next instruction after the caller, and jumps to that location. This gives control back to the caller. RET affects only the EIP and the ESP registers.

Endianness

Endianness is the way of representing \(storing\) values in memory. Even though there are three types of endianness, we will explain only two of them, the most important ones: big-endian and little-endian.

MSB

The most significant bit \(MSB\) in a binary number is the largest value, usually the first from the left. So, for example, considering the binary number 100 the MSB is 1.

LSB

The least significant bit \(LSB\) in a binary number is the lowest values, usually the first from the right. So, for example, considering the binary number 110 the LSB is 0.

![](.gitbook/assets/image%20%2852%29.png)

![](.gitbook/assets/image%20%2854%29.png)

Let us consider the value 11 \(0B in hexadecimal\).

The example system is using little-endian representation; therefore, the LSB is stored in the lower memory address, or MSB is stored at the highest memory address.

![](.gitbook/assets/image%20%2831%29.png)

![](.gitbook/assets/image%20%2829%29.png)

No Operation instruction \(NOP\)

NOP is an assembly language instruction that does nothing. When the program encounters a NOP, it will simply skip to the next instruction. In Intel x86 CPUs, NOP instructions are represented with the hexadecimal value 0x90.

NOP-sled is a technique used during the exploitation process of Buffer Overflows. Its only purpose is to fill a large \(or small\) portion of the stack with NOPs; this will allow us to slide down to the instruction we want to execute, which is usually put after the NOP ****sled.

The reason is because Buffer Overflows have to match a specific size and location that the program is expecting.



