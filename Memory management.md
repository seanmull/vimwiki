
Types of memory:

- Registers
- Cache
- Main memory
- Electronic Disk
- Etc

Moving up the latter is faster but more volitile
For instance loose power and memory is gone

Memory management roles
- Allocate and de-allocated before and after execution
- Keep track of used memory
- Minimize fragmentation
- Properly utilize memory
- Maintain integrity

Two memory spaces
- Logical - address defined by CPU
- Physicial - defined by the memory managment unit
Logical addresses are mapped to the phyiscal
The physical always remains contant

The loader loads the processes into memory

Static- loads the whole process into memory
Dynammic - only loads when the process is in physical memory

The linker takes object files and combines them into an executable

Static - all combined to a single files
Dynammic - stubs replaces what hasn't been loaded into memory yet

Swapping is the process into another memory type temporarily. This allows more processes to be run that can currently fit in memory

Memory allocation has to do with the placement of processes.  It may be placed using various algo, like best fit, worst fit or first fit.

Processes must be stored in contiguous memory addresses
Fragmentation is when the process block cannot fit is the current used block
Paging is a scheme that eliminates the need for contiguous memory
