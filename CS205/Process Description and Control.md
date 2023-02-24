## What is a process?
It can be defined as:
- A program in execution
- An instance of a running program
- The entity tha can be assigned to, and executed on, a processor
- A unit of activity characterised by a single sequential thread of execution, a current state, and an associated set of system resources
Or just a program or app

It contains multiple parts
- Program code / text section
- Current activity including program counter, processor registers
- Stack containing temporary data
- Data section containing global variables
- Heap containing memory dynamically allocated during runtime
![[process_diagram.png]]![[process_diagram_2.png]]
## Components
A process contains three components:
- An executable program
- The associated data required by the program (variables, work space, buffer, etc)
- Execution context / process state of the program
![[process_components.png]]
# Process Elements
While a program is executing, the process can be characterised by a number of elements![[process_elements.png]]
## Process Control Block (PCB)
This is a data structure created and managed by the OS. It is a key tool that allows support for multiple processes. The OS can interrupt a running process and resume the execution as if the interruption had not occurred.
![[process_control_block.png]]

---------------------
# Process Execution
## Trace
Lists the behaviour of an individual process (e.g. CPU or I/O bound), by listing the sequence of instructions that execute for the process. The behaviour of the CPI can be derived by showing how the traces of various processes are interleaved
## Dispatcher
A small OS program that switches the processor from one process to another
![[process_execution_1.png]]![[process_trace.png]]
![[process_dispatch.png]]
# Process Lifetime
![[process_lifetime.png]]
## Creation
A process is created by another process, which, in turn creates other processes, forming a process tree
![[CS205/images/process_creation.png]]
![[exercise_pg_17.png]]
a -> Identifiers need to be unique

# Two-State Process Model
![[two_state_process.png]]![[two_state_process_2.png]]
# Five-State Process Model
![[five_state_process_1.png]]![[five_state_process_2.png]]![[five_state_process_3.png]]
## When an event occurs, how does OS know which are the processes in the blocked queue to be moved to ready queue?
![[five_state_process_4.png]]
# Suspended Process
This happens when there is not enough memory space to hold the processes in queues
## Solutions
- Moving part of the process from memory to disk
- Move the whole process if there is still not enough space
- These "blocked" processes are in a **suspend queue**
The OS will bring the processes from the suspend queue to the ready queue when there is memory space available or when the ready queue is empty.
Since swapping is an I/O operation (uses storage along with memory), frequent swaps can impact system performance.
![[suspended_process_1.png]]
![[suspend_process_2.png]]![[exercise_pg_27.png]]
![[exercise_pg_27_ans.png]]![[exercise_pg_29.png]]
1) Always dispatch from ready state
	- Swapping is minismised
	- higher prio process will take longer to be served or even starve to be served
2) Always gives preference to the highest-priority process
	- Higher prio is always served first
	- Process in the ready queue may starve
	- Swapping will introduce I/O overhead
3) Dynamic scheme
	A ready/suspend process is chosen next only if it has higher priority than the highest priority ready process by several levels of priority
# Process Description
![[process_allocation.png]]
The OS schedules and dispatches processes for execution, allocates resources to processes
![[os_control_table.png]]
## Memory Table
- Allocation of main memory to processes
- Allocation of secondary memory to processes
- Protection attributes (shared memory)
- Information needed to manage virtual memory
## File Table
- Existence of files
- Location on secondary memory
- Current status
- Other attributes (metadata?)
## I/O Table
- I/O operation status
- Location in main memory being used as the source or destination of the I/O transfer
## Process Table
This table indexes process images which consist of the program, data, stack and attributes. Each process is also associated with a number of attributes that are used by the OS for process control.
The process location is where the program and data is in the main memory. A stack is used to keep track of the execution of a program.
## Process Control Block
	- Process Identification: identifiers of a process an it's parent
	- Processor state information or context: registers, stack pointers
	- Scheduling and state information: state, priority
	- Data structuring: Reference to other process
	- Inter-process communication: Signals and messages
	- Process privileges: E.g. types of instructions that may be executed
	- Memory management: pointers to segments or pages
## Process Identification
Each process is assigned a unique numeric identifier for different tables to use to cross-reference process tables.
## Processor State Information
Consists of the content of processor registers
- Control and status registers
- Stack pointers
- User-visible registers
![[processor_registers.png]]
## Process Control Information
Additional information required by OS to control and coordinate processes (e.g. priority, process state, scheduling-related information, etc.)
![[process_control_information.png]]
![[process_list_structures.png]]
# Process Control
There are two execution modes, user and kernel
![[kernel_mode_execution.png]]
![[process_creation 1.png]]
# Process Switching
Switching a process from running to ready
![[process_switching.png]]
# Mode Switching
This is a switch from user to kernel mode (or vice versa). Here is an example of mode switch with process switch
![[mode_and_kernel_switch.png]]
There can also be a mode switch that does not change the state of a process if serving an interrupt to perform trivial or regular tasks (e.g. acknowledgment to an I/O device)
![[mode_switch.png]]
# Execution of the OS
How are the mode switches implemented?
![[os_execution_1.png]]
![[os_execution_2.png]]![[os_execution_3.png]]