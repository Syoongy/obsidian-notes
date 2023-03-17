A process does not need all its code and data in the main memory during execution. The OS allocates memory space for a portion of the program based on the runtime behaviour of a process.

Virtual memory is a storage allocation scheme in which secondary memory can be addressed as though it were in main memory to be replaced whe a new page must be brought in
- Simple
	- All pages or segments are in main memory
- Virtual memory
	- Pages or segments are read in as needed
	- Reading a page (segment) into memory may require to write a page (segment) out to disk

## Process Execution
- Os brings only a few pieces of a program into main memory
- Trap is generatedwhen the required piece of program is not in main memory
- OS places the process in a blocking state
- OS issues a disk I/O read request
- Another process is dispatched to run while the disk I/O takes place
- Interrupt is issued when disk I/O is complete, which causes the OS to place the affected process in the ready state

## Advantages
Only part of a program needs to be in memory for execution
- Program no longer constrained by limits of physical memory
- Can a program larger than the memory size?
Each program takes less memory while running
- More programs can reside in the main memory
- More programs can run concurrently
- Increase CPU utilisation

![[virtual_memory_1.png]]

## Demand Paging
Paging: bring in entire process at load time
Demand paging: the needed page only
Pre-paging: some pages other than the one demanded
![[demand_paging_1.png]]

### Advantages
- Less I/O transfer needed

### Address Translation
![[demand_paging_address_translation_1.png]]
![[demand_paging_address_translation_2.png]]
### Page Fault
![[page_fault.png]]

page 12 exercise
3*(64*64)/4 = 3072 page faults

there will be 3 page faults for every 256 instructions. So 3*(64*64)/256 = 48 page faults

## Page size vs Page fault
Smaller page size implies
- Less internal fragmentisation
- More pages required per process
- Larger page table size for more pages
- Page fault rate![[page_fault_rate.png]]
------------------------------
## Replacement Algorithm
Which page to replace when a new page is brought in?
Principle way to minimise page fault rate
- Page least likely to be referenced in the future
Lets consider an optimal algorithm
- Reference pages: 2, 3, 2, 1, 5, 2, 4, 5, 3, 2, 5, 2
![[replacement_algorithm_1.png]]
This is only possible if we know the items that need to be used ahead of time

### LRU: Least Recently Used
Principle of locality
- The page that has not been referenced for the longest time
- Reference pages: 2, 3, 2, 1, 5, 2, 4, 5, 3, 2, 5, 2
![[replacement_algorithm_2.png]]

### FIFO: First-in-first-out
Round robing style
- The page that has been in memory for the longest time
- Reference pages: 2, 3, 2, 1, 5, 2, 4, 5, 3, 2, 5, 2
![[replacement_algorithm_3.png]]

### Clock
Combines FIFO with a tag on the pages (with use bit set to 1) that were recently accessed
- Algorithm
	- Scan the buffer to find a frame with a use bit set to 0 for replacement
	- Each time it encounters a frame with a use bit of 1, it resets that bit to 0 and moves to the next frame
Reference pages: 2, 3, 2, 1, 5, 2, 4, 5, 3, 2, 5, 2
![[replacement_algorithm_4.png]]