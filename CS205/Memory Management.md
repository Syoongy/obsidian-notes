In multiprogramming and multiprocessing, processes reside in the memory and run concurrently. Main memory and registers are storage that CPU can access process (process control block, program, data, stack) directly.
![[meomry_management_1.png]]\
### (Re)allocation
(Re)allocate memory resources among competing processes to maximise memory utilisation and system throughput
- A process can be swapped in and out of main memory
- A process may reside in different areas of memory before swapping out and after swapping in

### Address Mapping
Fast translation from logical address (Used by CPU) to physical address (used by memory management)

### Protection
Provide isolation between process, but allow controlled access to shared area of memory
- Memory reference is checked at run time

## Address Translation
![[address_translation_1.png]]

-------------------------------
## Memory Partitioning
### [[Fixed Partitioning]]

### [[Dynamic Partitioning]]

### [[Paging]]

### [[Segmentation]]


