## Deadlock
- Permanent blocking of a set of processes
- Happens when a process is blocked awaiting an event that can only be triggered by another blocked process
- No efficient solution in the general case
![[deadlock_example_1.png]]
![[deadlock_example_2.png]]
![[deadlock_example_3.png]]
If Process P runs first, $P_0$ and $P_1$ are run, locking D. It will then context switch to $q_0$ and $q_1$, locking T. Thus, when the context switch happens again to Process P, $P_2$ will be deadlocked as T is currently locked.

### Resource Allocation Graph
![[resource_allocation_graph_1.png]]
![[resource_allocation_graph_2.png]]
![[resource_allocation_graph_exercise_1.png]]
![[resource_allocation_graph_exercise_2.png]]
**Consider a system consisting of four resource instances that are shared by three processes, each of which needs at most two instances. Is the system deadlock free?**
Yes

### Conditions
#### Necessary
- #### Mutual Exclusion
	- Only one process may use a resource at a time
	- No process may access a resource until that has been allocated to another process
- #### Hold-and-Wait
	- A process may hold allocated resources while awaiting assignment of other resources
- #### No Pre-emption
	- No resource can be forcibly removed from a process holding it
#### Required
- #### Circular Wait
	- Closed chain of processes exists, such that each process holds at least one resource needed by the next process in the chain

### Approaches
There is no single effective strategy to deal with all types of deadlock.
- #### Deadlock Prevention
	- Disallow one of the three necessary condition for deadlock occurrence, or prevent circular wait condition from happening.
	- Mutual Exclusion
		- Only not required for shareable read resources (e.g. Read-only files)
		- Impossible to totally ignore mutual exclusion
	- Hold and wait
		- A process request all of its required resources at one time
		- Blocking the process until all requests can be granted simultaneously
		- Livelock and starvation possible?
	- No Pre-emption
		- Allow incremental request of resources
		- But if a further request is denied, that process **must** release all its allocated resources and request them again
	- Circular Wait
		- Impose a total ordering of all resource types (each resource is assigned a unique number), and require that each process requests resources in an increasing order of enumeration
		- Associate an index with each resource type. Then resource $R_i$ precedes $R_j$ in the ordering if $i < j$.
		- To prove correctness, suppose two processes A and B are deadlocked because A has acquired $R_i$ and requests for $R_j$, and B has acquired $R_j$ and requests for $R_i$. This is impossible because it implies $i < j$ and $j < i$
	- ![[deadlock_prevention_exercise_1.png]]
	- ![[deadlock_prevention_exercise_2.png]]
- #### Deadlock Avoidance
	- Do not grant a resource request if this allocation might lead to deadlock.
	- Allows the three necessary conditions
	- All the processes declare the required resources at the beginning, and then claim the resources incrementally
	- A decision is made dynamically whether the current resource allocation request will, if granted, potentially lead to a deadlock
	- #### Banker's Algorithm
		- Do not grant an incremental resource request to a process if this allocation might lead to a deadlock
		- ![[bankers_algorithm_7.png]]
		- A process makes a request for allocation of resources
			- Simulate resource allocation
				- Calculate allocation matrix A
				- calculate available vector V
			- Test Safe state
				1) Find a process that can run to completion
				2) Update the matrices and vector
				3) Repeat step-1 until unable to proceed
			- Decision to approve the request
				- If all processes can run to the completion
				- Otherwise unsafe, restore to the original values
			![[bankers_algorithm_5.png]]
			![[bankers_algorithm_6.png]]
		- ![[bankers_algorithm_1.png]]
		- ![[bankers_algorithm_2.png]]
		- ![[bankers_algorithm_3.png]]
		- ![[bankers_algorithm_4.png]]
		- ![[bankers_algorithm_exercise_1.png]]
	- ![[deadlock_avoidance_1.png]]
- #### Deadlock detection
	- Grant resource requests when possible, but periodically check for the presence of deadlock and take action to recover.
	- Allow a system to enter a deadlock state
		- No need to declare the required resources
		- A process claims resources incrementally
		- A process is blocked if the requested resources are not available
	- Periodically check whether deadlock currently exists
		- Check whenever a request is made
		- Or check when it is likely for a deadlock to occur
		- Does frequency of checking matter?
	- Apply recovery scheme if deadlock happens
		- Rollback to a safe state
	- ![[deadlock_detection_1.png]]
	- ![[deadlock_detection_2.png]]
	- ![[deadlock_detection_3.png]]
	- #### Recovery Strategies
		- ##### Greedy
			- Abort all deadlocked processes
		- ##### Log the process execution path
			- Back up each deadlocked process to the previously defined checkpoint and restore the system state before the checkpoints
			- Memory/storage expensive
		- ##### Incremental approach
			- Successively abort deadlocked processes until no deadlock
			- Or, successively pre-empt resources until no deadlock
			- Need to run detection algorithm after each step
			- Which process should be killed
	- ![[deadlock_detection_4.png]]
	- Can Banker’s algorithm be modified for deadlock detection?
		- Yes, use Banker's algorithm to test safe state by simply setting something
### Dining Philosophers Problem
![[dining_philosophers_1.png]]
![[dining_philosophers_2.png]]
![[dining_philosophers_3.png]]
## Android
### IPC
Mechanism to transfer data between processes and coordinate activities between processes.
Android however, does not use semaphore for IPC. This is for security purposes. Each process is not allowed to directly access each other's memory for data sharing or communication. 
Instead, it adopts a "detect and recover" for deadlock. This tracks resource allocation and process states. To recover from deadlocks, some processes are restarted to remove them.

### Binder
- #### Data Isolation
	- Android does not allow applications or processes to directly share memory for writing and updating
- An android application runs on a virtual machine. The communication between virtual machines is through remote procedure calls (RPC), called binder
- Binder operates in kernel mode
	- An app that provides service(e.g. email) responds to a request made by third-party applications through binder in a secure way
	- To provide a lightweight remote procedure call that is efficient in memory and processing requirements
	- The RPC uses ioctl system call
	- ![[android_binder_1.png]]
	- ![[android_binder_2.png]]