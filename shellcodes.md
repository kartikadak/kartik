# Shellcodes

Once an attacker has identified a vulnerable application, his first objective is to inject shellcode in the software.

The shellcode can work two ways; it can get sent through the network \(remote buffer overflows\) or through the local environment.

But, the EIP is not the only method for execution of shellcode. It is possible for a shellcode to execute when an SEH \(Structured Exception Handling\) frame activates. The SEH frames store the address to jump to when there is an exception, such as division by zero. By overwriting the return address, the attacker can take control of the execution

Types of shellcode

* Local shellcode 
* Remote shellcode

A Local shellcode is used to exploit local processes in order to get higher privileges on that machine. These are also known as privilege escalation shellcodes and are used in local code execution vulnerabilities.

A remote shellcode is sent through the network along with an exploit. The exploit will allow the shellcode to be injected into the process and executed. Remote Code Execution is another name for this kind of exploitation.

Remote shellcodes can be sub-divided based on how this connection is set up: 

* Connect back 
* Bind shell 
* Socket Reuse

A connect back shellcode initiates a connection back to the attacker's machine.

 A bind shell shellcode binds a shell \(or command prompt\) to a certain port on which the attacker can connect. 

A socket reuse shellcode establishes a connection to a vulnerable process that does not close before the shellcode is run. The shellcode can then re-use this connection to communicate with the attacker. However, due to their complexity, they are generally not used

Staged shellcode

Staged shellcodes are used when the shellcode size is bigger than the space that an attacker can use for injection \(within the process\). 

In this case, a small piece of shellcode \(Stage 1\) is executed. This code then fetches a larger piece of shellcode \(Stage 2\) into the process memory and executes it. 

Staged shellcode may be local or remote and can be sub-divided into 

* Egg-hunt shellcode
* Omelet shellcode

Egg-hunt shellcode is used when a larger shellcode can be injected into the process but, it is unknown where in the process this shellcode will be actually injected. It is divided int0 two pieces: 1. A small shellcode \(egg-hunter\) 2. The actual bigger shellcode \(egg\) The only thing the egg-hunter shellcode has to do is searching for the bigger shellcode \(the egg\) within the process address space. At that point, the execution of the bigger shellcode begins.

Omelet shellcode is similar to the egg-hunt shellcode. However, we do not have one larger shellcode \(the egg\) but a number of smaller shellcodes, eggs. They are combined together and executed. This type of shellcode is also used to avoid shellcode detectors because each individual egg might be small enough not to raise any alarms but collectively they become a complete shellcode.



