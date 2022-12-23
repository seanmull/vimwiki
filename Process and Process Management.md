
- When an application is loaded into memory it becomes a process
- It has a program counter
- Processes have:
    - text - code of the program
    - data - global variables
    - stack - temporary variables
    - heap - dynammic runtime memory

- Every element is uniquely identified
- On OS abstraction is address spaces
- Virtual addresses map to actual physical addresses
- The page table is what stores this mapping
- Two process can possible share the same memory by swapping some portion to disk
- The source code is compiled which is the process of converting the code to a set of binary instructions
- CPU register stores the address of the next instruction.  This is called a program counter.
- The Process control block (PCB) is what manages all the procresses. It maintains program counter, stack pointer, CPU registry

A process may ask for more resources and the OS may give it more and update values in the PCB

The status of process are stored in the PCB.  Interrupts will cause a context switch when you move from process p1 to p2.  This is an expesive operation since all values are stored in memory.  It could be in memory (slow) of cache (fast)

Process is in the following states:
- New - Allocated PCB to process
- Ready - Waiting in queue to be assigned to processer
- Running - Assigned a processer.   Can be interrupted and moved to ready state.  It could also be put in the ready state if its long running. When its done process will terminated with an exit code
- Terminated

Processes come a single roots.  Everything is spawned from the root to child.
Fork: creating new child process by copying PCB values from root to child
Exec: replaced childs image and loads a new program

CPU scheduler determines which process in the ready queue will be sent to the cpu for execution.  When the cpu picks a process it interrupts the currect process and saves the current context. It runs an algo to determine which one gos first.  Then it dispatches the process to the cpu.

Interprocess communication is for transfering data between address spaces without sacrificing the abstraction and isolation the OS provides.

IPC mechanism choices:
- Message - provides read/write from channel and has API.  however must copy memory into a shared space and back to the sending process
- Shared memory - OS creates shared memory channel/space.  OS is not involved in the communtication but it provides no API


