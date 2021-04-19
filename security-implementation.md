# Security Implementation

* Address Space Layout Randomization \(ASLR\)
* Data Execution Prevention \(DEP\)
* Stack Cookies \(Canary\)

ASLR

The goal of Address Space Layout Randomization \(ASLR\) is to introduce randomness for executables, libraries, and stacks in the memory address space; this makes it more difficult for an attacker to predict memory addresses and causes exploits to fail and crash the process.

When ASLR is activated, the OS loads the same executable at different locations in memory every time. It is important to note that ASLR is not enabled for all modules. This means that, even if a process has ASLR enabled, there could be a DLL in the address space without this protection which could make the process vulnerable to the ASLR bypass attack.

DEP

Data Execution Prevention \(DEP\) is a defensive hardware and software measure that prevents the execution of code from pages in memory that are not explicitly marked as executable. The code injected into the memory cannot be run from that region; this makes buffer overflow exploitations even harder.

Stack cookies \(Canary\)

The canary, or stack cookie, is a security implementation that places a value next to the return address on the stack. The function prologue loads a value into this location, while the epilogue makes sure that the value is intact. As a result, when the epilogue runs, it checks that the value is still there and that it is correct.

