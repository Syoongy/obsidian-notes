## Operating Systems
- Software that sits between user program and hardware
- It is a resource manager and allocator
	- Decides between conflicting requests for hardware access
	- Tries to be efficient and fair
- Controls user program execution
- Provides services for system users

### Types
Windows, Linux, BSD

## Computer System
### Processor
- Has access to the registry (Super fast memory access)
- Good at arithmetic operations
### Main Memory
- Holds things in memory that does not need fast access
- Slower than registry
- Still faster than IO storage
### IO Modules
- GFX/USB/Network Cards
### System Bus Interface
- Between memory and IO Modules

## Instruction execution
Processor reads(fetches) instructions and data from memory then executes each instruction
![[instruction_cycle.png]]
- Processor fetches instruction from memory
- Program Counter (PC) holds address of the next instruction to be fetched
	- This is incremented after each fetch
- Instruction is loaded into instruction register
- Processor interprets the instrction and performs the required function

![[w_01_intro_exercise.png]]

- 2^4 = 16
- 2^12
- 16 bit
- Will be slower, there are 2 fetch cycles

![[fetch_execute_diagram.png]]
- 0003 is loaded into AC because from 1940, 1 is the instruction and 940 is where the memory data is located at
- The PC always increments after a fetch

## Interrupt
I/O devices are slower than CPU which results in wasteful use of the CPU while waiting from the device.
An interrupt is a mechanism to _interrupt_ the normal sequencing of the processor. 
An example of this would be an I/O device interrupting and informing the CPU of the completion of an I/O task. Instead of having the CPU poll and wait for I/O completion, the CPU will continue without polling and thus improving processor utilisation.

### Classes of interrupt
- #### Program
	- Illegal Instruction (Divide by 0)
	- Illegal memory space access
- #### Timer
	- Perform functions on a regular basis (Free memory space, update data between memory and disk)
	- Acoounting purposes (Preventing a program from running too long)
- #### I/O
	- Completion of I/O
	- I/O errors
- #### Hardware failure
	- Low battery, Power failure, memory error
### Flow of Control
![[no_interrupts.png]]
![[short_io_wait.png]]
![[short_io_wait_program_timing.png]]
![[long_io_wait.png]]
![[long_io_wait_program_timing.png]]
![[fetch_execute_w_interrupt.png]]
This adds an interrupt stage to our fetch and execute cycle. This checks for whether an interrupt was sent. If an interrupt was sent, we go through the interrupt stage. Otherwise, we fetch and execute as per normal.
![[execution_path.png]]
![[exercise_29.png]]
- A mechanism that informs CPU to stop the current program execution and switch to another task
- Allows the CPU to attend to more important tasks, especially so when multiple requests to allocate CPU arrive simultaneously
- Pre-empt the currently running program by pushing its info into control stack and switching CPU to run on higher priority task
- Let each program occupy the CPU for a fixed amount of time and let timer generate interrupts when a program has been running for too long

## Direct Memory Access (DMA)
Data transfer is performed by a separate module on the system bus or I/O module

When the processor wants to read or write data, it issues a command to the DMA module containing:
- read or write
- address of the I/O device
- Starting location in memory to read/write
- Number of words to be read/written

This DMA module transfers the entire block of data to and from memory without going through the processor
- Processor only involved at the start and end
- Generates an interrupt when transfer is completed
- Processor will execute more slowly during a transfer when access to bus is required
More efficient than interrupt-driven I/O
- Interrupt generated for each byte to be transferred
![[dma_interrupt_timeline.png]]
![[dma_exercise.png]]
- Interrupt
- Yes
- Might be slower when needing to access the bus (Competing with other devices in order to gain access to the memory bus)

## Parallel Vs Concurrency
Parallel means that multiple programs can execute at the same time.
Concurrency means that the programs can run at the same time but will not have access to the same execution power of the CPU