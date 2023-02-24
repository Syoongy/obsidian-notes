![[concurrency_1.png]]
- Sharing of and competing for resources
- Synchronisation of the activities of multiple processes (or threads)
- Communication among processes (or threads)

## Key terms
- ### Race condition
	- Multiple threads or processes read and write a shared data item
	- The final result depends on the relative timing of their execution
	![[race_condition_1.png]]![[race_condition_2.png]]
- ### Critical Section
	- A section of code within a process that requires access to shared data
	An example of this would be a singly linked list where pop and push access the data structure shared by thread
	![[critical_sections_1.png]]![[critical_sections_2.png]]
- ### Atomic operation
	- The sequence of instructions that either executes as a group or not execute at all
	![[atomic_operation.png]]

# Critical Section Problem
- Consider $n$ processes $\{P_0, P_1, ..., P_{n-1}\}$
- Each process has critical section segment of code
	- Process may be changing common variables, updating table, writing files, etc.
	- When one process in critical section, no other may be in its critical section problem is to design a protocol to solve this
- Each process must ask permission to enter critical section in entry section, may follow critical section with exit section, then remainder section
![[critical_section_problem_1.png]]
## Software Solutions
### Solution 1
Using a single global variable to indicate which process can enter the critical section
![[critical_section_software_solution_1.png]]
What happens when it is process 0's turn, but it never enters the critical section? Infinite loop :(

### Solution 2
Use 2 global variables
![[critical_section_software_solution_2.png]]
Mutual exclusion is not preserved as both processes to set `flag[i]` to true
Progress requirement is preserved
Bounded Waiting not guaranteed as they can 

### Solution 3
Use 2 global variables
![[critical_section_software_solution_3.png]]
Mutual exclusion is preserved
Progress Requirement is not possible as a deadlock could happen (Both processes could be waiting for each other to complete (blocking forever))
Bounded waiting not possible due to the same reason

### Solution 4
Use 2 global variables
![[critical_section_software_solution_4.png]]
Mutual exclusion is preserved
Bounded waiting not satisfied
Progress requirement may have no deadlock but...
![[critical_section_software_solution_4_live_lock.png]]
### Dekker's Algorithm
Use both flag and turn variables
![[dekkers_algorithm_1.png]]
![[dekkers_algorithm_2.png]]
### Petersen's Algorithm
![[petersens_algorithm.png]]

--------------------------------
## Hardware Solution
For mutual exclusion, it is sufficient to prevent a process from being interrupted in the critical section. This function to disable and enable interrupts can be implemented at the kernel level, but only works for uniprocessor systems. Because it would stall all other processors.
```
while (true) {
	// Disable interrupts
	// Critical Section
	// Enable Interrupts
	// Remainder
}
```
## Multiprocessor
![[critical_section_hardware_solution_1.png]]
![[critical_section_hardware_solution_2.png]]
![[critical_section_hardware_solution_3.png]]![[mutex_compare_swap_example.png]]
![[mutex_pros_cons.png]]
## Concurrency Mechanism
- ### Mutex
	- Associate with a shared resource or critical section
	- Value: 0 or 1
- [[Semaphore]]
- ### Monitor
	- A programming construct (to make life easy) that provides equivalent functionality to that of semaphores and is easier to control
	- Key elements: mutex + condition variable
	![[Pasted image 20230224084751.png]]
	![[monitor_2.png]]
	This mechanism is still not enough for synchronisation as a thread could still be blocked after entering the monitor and needs to wait until a condition has been met. Thus, a **Conditional Variable** is required.
	Therefore, a combination of mutex and conditional variables is used. A thread is required to obtain the mutex to enter the monitor. Inside the monitor, a thread can `cwait()` for some condition to be satisfied. This will block the thread until the condition is satisfied. Once satisfied, some other thread can use `csignal` to wakeup a waiting thread.
	![[monitor_3.png]]
	If `csignal()` is performed, and there are no waiting threads, the signal is ignored. For a semaphore, `semSignal()` will increment the value of count even with no waiting threads.
	![[monitor_4.png]]
- ### Memory Sharing
	- Processes communicate by sharing variables
	- We create a "shared memory" space that can be accessed by multiple processes.
	- A major issue is to provide a way for user processes to synchronise their actions
	![[memory_sharing_1.png]]
- ### Message passing
	- Inter-process communication
	- Processes communicate without using shared variables
	- Two primitives available
		- `send(destination, message)`
		- `receive(source, message)`
	![[message_passing_1.png]]
	- When two processes communicate
		- A communication link is established
		- Messages are exchanged through `send` and `receive`
	- Implementation Issues
		- How are links established?
		- Can a link be associated with more than two processes?
		- How many links can there be between every pair of communicating processes
		- What is the link capacity
		- Is the max message size of the link fixed or variable
		- Is a link uni or bi directional
	- Direct Communication
		- Processes must name each other explicitly
			- `send(P, message)` - send a message to process P
			- `receive(Q, message)` - receive a message from process Q
		- Properties of communication link
			- Links are automatically established
			- Is associated with exactly one pair of proceses
			- A pair can only have one link
			- It can be unidirectional but is usually bi-directional
	- Indirect Communication
		- Directed and received from **mailboxes**
			- Each mailbox has a unique id
			- Processes can communicate only if they share a mailbox
		- Properties of communication link
			- Can be associated with many processes
			- A pair of processes can share several communication links
			- Links can be both uni and bi directional
		- Primitives
			- `send(A, message)`
			- `receive(A, message)`
		![[message_passing_2.png]]
		![[message_passing_3.png]]
	- #### Readers/Writers Problem
		- A data area is shared among many processes
			- Some processes only read the data (readers), and some only write to the data area (writers)
		- Conditions to be satisfied
			- Any number of readers can simultaneously read the file
			- Only one writer at a time may write to the file
			- If a writer is writing to the file, no reader may read it
		- Readers having priority![[message_passing_4.png]]
		- Writers having priority
		- ![[message_passing_5.png]]
		![[message_passing_6.png]]
		![[message_passing_7.png]]