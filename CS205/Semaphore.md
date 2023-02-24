Generalisation of a mutex
	- Value: an integer
	- Used for signalling among processes or threads
	A variable that has an integer value upon which only three operations are defined:
	1) A semaphore may be initialised to a non negative integer
	2) **semWait**: an atomic operation that waits for semaphore to become positive, then decrements its value by one
	3) **semSignal**: an atomic operation that increments the semaphore value by one and wakes up a waiting thread, if any
	![[counting_semaphore.png]]![[semaphore_example_1.png]]![[semaphore_example_2.png]]
## Binary Semaphore
	![[binary_semaphore.png]]
	![[semaphore_exercise_1.png]]
	There is no big difference
	![[semaphore_exercise_2.png]]
		- Q1: 0, Ready Queue
		- Q2: 
		- Q3:
#### Producer/Consumer Problem
This can be generalised to
	- One or more producers generating data and placing these in a buffer
	- A single consumer taking items out of the buffer one at a time
	- Only one producer or consumer may access the buffer at any one time
	There are however 2 constraints
	- Producer will not add data into the buffer when full
	- Consumer will not remove data from an empty buffer
	![[producer_consumer_1.png]]
	We can use a semaphore to create a critical section
	![[producer_consumer_semaphore.png]]
	![[producer_consumer_semaphore_2.png]]
	![[producer_consumer_finite_buffer.png]]
	![[producer_consumer_semaphore_finite.png]]
	![[producer_consumer_exercise_1.png]]
![[concurrency_exercise_42.png]]
![[concurrency_exercise_43.png]]