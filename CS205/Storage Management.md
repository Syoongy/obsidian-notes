![[storage_management_1.png]]
There are generally 2 types of storage devices now. Hard drives and Solid state drives
![[storage_management_2.png]]

## Hard Drive
![[hard_drive_1.png]]
### Types of delay
![[hard_drive_2.png]]
### Multi-Platter Disk
![[hard_drive_3.png]]
### Disk Operations
- Large number of sectors (blocks)
	- 512 or 4096 bytes
	- Individual sector writes are **atomic**
	- Multiple sectors writes may be interrupted (torn write)
- Disk rotates at constant speed
- Reading or writing requires the head to be positioned at the desired track and at the beginning of the desired sector on that track
- Read/Write operations are performed as the sector moves under the head
- OS maintains a queue of I/O requests from different processes
	- A request asks for access of a sector
	- Time spent seeking the tracks of the requested sectors will impact the disk performance

### Disk Scheduling Algorithms
#### Issue
Multiprogramming environment results in random data access patterns
- Sector access involves selection of tracks
- If tracks are accessed in random, disk head will be busy moving across tracks, resulting in increase of overall seek time

#### Idea
- Performance can be improved by ordering the request based on the tracks to be accessed
- Turn random access towards sequential access

- #### FIFO: First in First out
	![[hard_drive_fifo.png]]
- SSFT: Shortest Service Time First
	- Can lead to starvation
	![[hard_drive_ssft.png]]
- SCAN
	![[hard_drive_scan.png]]
- C-SCAN: Circular Scan
	![[hard_drive_circular_scan.png]]

### Exercise
![[hard_drive_exercise.png]]
FIFO: 
- 122 + 295 + 182 + 54+ 487 + 422 + 542 + 581 + 1014 + 219
- Total: 3918 tacks
SSTF:
- Order: 1245, 1365, 1678, 1787, 1897, 1045, 932, 878, 750, 664
- Total: 1963 tracks
SCAN: 
 - Order: 1045, 932, 878, 750, 664, 0, 1245, 1365, 1678, 1787, 1897
 - Total: 3064 tracks
C-SCAN
- Total: 3920 tracks

## SSD: Solid State Device
Why not use it for mobile phone?
- Fragile mechanical components can break
- Disk motor is extremely power hungry

Why SSD?
- Resilience against physical damage (Temperature change, no head movement)
- Greatly reduces power consumption (no moving parts)
- No penalty for random access of data
- Faster transfer rate: > 500MB/s vs 200Mb/s for HD

### Flash Memory
![[flash_memory_1.png]]
- No seek time or rotational delay
- Expensive, less capacity, faster and less power hungry
- Read access time is independent of data location
- Write operation is slower
- Two types of technology: NAND, NOR
	- Smartphones uses NAND
#### Challenges
Previously written data should be erased (by an erase operation) to overwrite new data in the same location
![[flash_memory_2.png]]
Flash memory can only be written a fixed number of times. (A device near its end of life due to many erase cycles has much worse performance than a new device)
![[flash_memory_3.png]]
### SSD Controller
- SSDs are complicated internally
- All operations are handled by SSD controller
	- Mapping logical block address to physical page
	- Keep track of free pages
	- Manage garbage collector
	- Perform wear levelling to average out wearing of blocks
- Controller performance is crucial for overall SSD performance
	- Minimally only uses the OS

## Android I/O Scheduler
### NOOP: No operation Scheduler
- Modified FIFO
- Insert the requests into a queue
- Merge adjacent write requests to reduce number of writes and to avoid write amplification
- Serve read requests first to reduce the impact of slow write operations
- Only merging and no sorting of requests is required
	- No seek time so merging(batching is more efficient)

### SIO: Simple I/O Scheduler
- Deal with starvation problem (write requests may be delayed)
- Like NOOP but associating each request with an expiration time
- The requests which are not scheduled by NOOP but have been expired will be dispatched first (also called deadline scheduler)

### CFQ: Completely fair queueing scheduler


- Maintains per process I/O queues with a timeslice for each queue
- Process the queues in a round-robin manner with time quantum
- Dispatcher waits for a short interval for all/most requests of a queue to arrive before dispatching them (aka anticipatory scheduler)
