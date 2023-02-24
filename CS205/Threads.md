A thread is a unit of execution, while a process is the unit of resource allocation and protection.
- Single-threaded process
	A single trace of instructions executed sequentially
- Multi-threaded process
	Multiple traces of instructions executed concurrently
Each thread has:
- An execution state (Running, Ready, etc.)
- A saved thread context when not running
- An execution stack
- Access to the memory, resources, program and global variables of its processes, shared with all other threads in that process
## Benefits
- Foreground and background work
- Asynchronous processing
- Speed of execution
- Modular program structure
![[threading_benefits.png]]
--------------------------------
# Multithreading
Multiple, concurrent paths of execution within a single process
- The unit of dispatching is referred to as a thread or lightweight process
![[multi_and_single_threading.png]]
-------------------
# Thread Execution State
The key states for a thread are (Running, Ready and Blocked)
- In an OS with thread support, scheduling and dispatching is done on a thread basis
- Suspending a process involves suspending all threads of the process
- Termination of a process terminates all threads within the process
![[thread_execution_state.png]]
Even on a single processor, using threads is still faster
![[thread_execution_2.png]]![[4_exercise_pg_11.png]]
1) A child process will keep a separate copy of program, data and PCB that are duplicated from parent process. All threads share the same address space (global variables and program) and PCB, but keeping different stacks/heaps and having additional thread control blocks. Hence, creation of child process is heavyweight and creation of thread is lightweight.
2i) 2 Threads, 1 method can run in main while a worker thread can run in the other thread
2ii) Cleanliness of code
2iii) You can execute and process the threads at the same time

----------------------
# Type of Threads
- ## Pure user-level
	Management done by user-level threads library. The library provides utilities to create and destroy threads, manage the message passing between threads and scheduling for execution. The kernel is not aware of the thread, and only one thread can occupy one processor at any time.
	One thread being blocked will cause all threads being blocked. A technique known as "jacketing" is needed to bypass this problem
	![[pure_user_level_thread.png]]
	![[pure_user_level_threads_2.png]]
	![[pure_user_level_threads_3.png]]
- ## Pure Kernel-level threads
	Supported by the kernel (e.g. Linux, windows)
	The kernel performs the scheduling at thread level and threads of a process can occupy multiple processors
	The programmer can create and manage as many threads as an application requires. However, we can only have one thread running on a single processor. Multiple threads can run in parallel on multiple processors.
	Creating a user thread requires creating a kernel thread which leads to larger overhead
	Too many kernel threads can also burden system performance
	![[pure_kernel_level_threads_1.png]]
	![[pure_kernel_level_threads_2.png]]
### Exercise: Can a many-to-one multithreaded model achieve better performance on a multiprocessor system than on a single-processor system? Explain your answer.
No. The OS sees only a single process and will not schedule the different threads of the process on separate processors. Only one processor is allocated to the threads of a process on a multiprocessor system.
![[4_exercise_pg_19.png]]
Many-to-many, one-to-one
Java facilitates creation of user threads and these threads will be mapped to kernel threads. The mapping between user and kernel level threads depends on the JVM implementation.

-------------------
# Android
- An android application is the software that implements an app
- Each android application has
	- Activities
	- Services
	- Content Providers
	- Broadcast Receivers
- Each application runs on its own virtual machine

![[android_application.png]]
## Android Terminology
- ### Process
	- An application
	- Main thread/UI thread
- ### Activity
	- Process can have different activities
	- All activities are run under the main thread by default
- ### Task
	- A set of activities
	- The activities can be from different applications
	- The activities are arranged in a stack, called back stack
- ### Thread
	- Programmer can create threads to run tasks concurrently with the main thread

## Zygote
A special process in Android that handles forking of every new application process. It is started when the system is online, where every android application is a clone of zygote process. Every application is therefore a Linux process with a single execution thread.![[zygote.png]]
Because zygote and app share the same memory, they have a **copy-on-write** (vfork()).
- Since both processes share the same memory, starting a new process is almost instantaneous.
	- The kernel does not need to allocate as much memory for the new process and does not need to load in Android framework libraries
- If an app wants to make changes, the "copy-on-write" will allocate new memory and copy the memory page which the new process is writing onto it
![[copy_on_write.png]]
![[zygote_clone.png]]
## Activities
- Every user screen is represented by an activity class (e.g. 3 screens will require 3 activity classes)
- Activity Management (On application switch, the activity instances in the app transition between different lifecycle states)
- Process management
	- Application starts
	- Comes to foreground where user interacts with activities
	- Application close (background process)
	- Application switching
![[android_activity_lifecycle.png]]
## Back Stack
This contains the activities of a task which are arranged in order of which the activities are opened. A new activity is always pushed on the top of the stack and takes focus.
	- The previous activity is stopped and remains in the stack; the system retains the current state of its user interface.
	- When the back button is pressed, the current activity is popped from the top of the stack (destroyed) and the previous activity resumes
![[back_stack_1.png]]![[back_stack_2.png]]
## Android Process
- Foreground: The one which the user is currently interacting with
- Visible: Visible to the user on-screen and is doing work that the user is aware of
- Service: The one holding a service that the user cares about(e.g. download, playing music)
- Background: Processes that user has interacted with previously
- Empty: Processes with no activities, services or broadcast receivers
## Process Priority
Processes will be killed when the OS decides that there is insufficient memory to perform a required task. Killing processes, however, consumes battery power. Thus, Android utilises a **lazy approach** where a process is killed only when necessary.
![[process_priority.png]]
## Main Thread
An application contains a single thread called **main or UI** thread. It is responsible for UI interaction and communication between different components through the UI. (e.g. A screen touch will ask the main thread to dispatch a touch event to the widget)
The main thread is initialised with a **Looper** class that provides data structures to manage a queue of jobs to be executed
## Worker Threads
This is for intensive tasks (e.g. Database query) that should not be handled by the main thread as UI interaction will be blocked. They are also normally created for long-running background jobs.
![[worker_threads.png]]
## Thread Pool
When dealing with threads, we are faced with 2 problems
- Creation and termination of threads take time
- Allowing unlimited threads can resource exhaust system resources
The solution is to create a fixed number of threads on startup and place them into a pool
	- A created worker waits for a thread to be allocated
	- If the pool has no available thread, a worker is queued and waits till a thread is available
	- A worker returns the allocated thread to the pool after completion
Worker threads run concurrently or asynchronously with the main thread so that the main thread will not be blocked/interrupted.
In Android, the **AsyncTask** class is provided to manage worker threads.
![[thread_pool.png]]
## Java Threads
These are managed by the JVM and are typically implemented using the threads model provided by the underlying OS. Java threads are used by the Android OS and can be created by extending a Thread class or implementing the Runnable interface (standard practice)