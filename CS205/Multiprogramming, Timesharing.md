A _Program_ that controls the execution of application programs (Like a manager). It is also an interface between applications and hardware.
The main objectives of an OS are:
- Convenience
- Efficiency
- Ability to evolve (Not having to reinstall OS after changing hardware is nice :D)

![[hardware_software_diagram.png]]
# Kernel
The one program running at all times on the computer. It can never be stopped, or the operating system would stop working.
The kernel handles:
- Device management (CPU, memory, disk, ...)
- Scheduling (Loading and execution of programs)
- System calls and APIs
- Protection and fault tolerance (Program crashes shouldn't crash the machine (haha nvidia drivers lul))
- Security

## Types
### Microkernel
Mostly for embedded systems that contain only essential functionalities
- #### Research kernels
	Mach, L4, GNU Hurd
- #### Embedded System kernels
	QNX
![[microkernel.png]]
The kernel will only hand out and give access to instructions. It has no knowledge of whichever program is accessing it. All this knowledge stays in the user space.
### Hybrid Kernel
Most functionalities are compiled into the kernel and some functions are loaded dynamically
- #### Types
	Windows, MacOS
![[hybrid_kernel.png]]
### Monolithic Kernels
All functionalities are compiled into the kernel. All codes will run in the kernel space.
- #### Types
	Android, Linux
![[monolithic_kernel.png]]
## Modes of Operation
### User Mode
A user program will execute in user mode where certain memory areas are protected from user access and some instructions may not be executed
### Kernel Mode
The OS will execute in kernel mode where protected areas of memory can be accessed, and privileged instructions can be executed. This is not the same as `sudo`/root. 
![[virtual_memory_excercise.png]]
Answer: The processor could keep track of what locations are associated with each program and limit access to locations that are outside a program's extent. Information regarding the extent of a program's memory could be maintained by using base and limits registers and by performing a check for every memory access.
![[virtual_memory_exercise.png]]

## Uniprogramming
The program will run until its end before the next program can start. Everything is committed to the singular program. (Inefficient)
![[uniprogramming.png]]
## Multiprogramming
The programs can run concurrently to optimise CPU usage. This is also known as multitasking.
Memory should also be large enough for thee, four, or more programs and allow context switch among all  of them.
![[multiprogramming.png]]

![[programming_types_exercise.png]]
- They run in multiprogramming mode (Playing music in the background while scrolling through images)
- Single user, UI, multiple tasks (foreground and background), multiple cores/CPUs
![[processing_jobs_exercise_1.png]]
![[processing_jobs_exercise_2.png]]
![[processing_jobs_exercise_ans.jpg]]
## Time Sharing System
- Can be used to handle **multiple interactive jobs**
- Processor time is shared among **multiple users**
- Multiple users can access the system simultaneously, with the OS interleaving execution of each user program in a short burst or quantum of computation
- Pure multiprogramming aims to maximise CPU utilisation
- Multiprogramming + time sharing aims to minimise user response time
### Time slicing technique
This is an older system where the system clock or timer generates interrupts at a rate of approximately one every 0.2 seconds. The OS regains control at each clock interrupt and assigns the processor to another user. The current user program and data are written out to disk and the new user program and data are restored in main.
Modern time slicing utilises virtual memory management to allow multi user programs to reside in memory
![[timesharing_exercise.png]]![[timesharing_exercise_2.png]]
- 22s
- $(0 + 2 + 4 + 6)/3 = 3s$
- $(14+8+14+12)/4 = 12s$

-------------------------------------
# Android
Android is a software stack that utilises the Linux kernel. It has it's own inter-process communication and power management which differs largely from Linux.
It is written primarily in C/C++ but the kernel is called through Java interfaces (JNI)

## Application Framework
High level building blocks exposed through standardised through API's. (e.g. Activity Manager, Window Manager, Package Manager, Telephony Manager, ...)

## Runtime
Most Android software is mapped into **bytecode format** which the transforms into native instructions on the device itself.
Early releases of android uses _Dalvik_ which targets single core CPUs while more modern releases (as of 4.4) utilise Android Runtime (ART). ART is fully compatible with Dalvik's existing format for backwards compatibility. However, ART converts bytecode to machine code during app installation (compiling once to machine code is more efficient than having to compile on every run).

## Power Management
- ### Power Collapse
	- Makes the system enter sleep mode while being able to respond to external stimuli (e.g. phone call, button press)
	- Provides wake-up service for apps
- ### Component-level power management
	- Shut down individual components (e.g. screen, audio subsystem, etc...)
- ### Wakelocks
	- Provides flexibility to prevent systems from entering power collapse (e.g. during app install)
	- An app can hold different kinds of wakelocks to turn individual components on or off