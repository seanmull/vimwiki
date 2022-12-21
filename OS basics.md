# Sys arch

Overview doc
C:\Downloads\ch1.pptx

1. Hardware - CPU, memory, I/O
2. Operating system - controls the hardware among applications
3. Application programs - define the way system resourses are used
4. User - people, machines, other computers

Features of computer system operation

1. I/O devises can operate at the same time
2. Each device has a local buffer
3. Each device has a device driver for the OS
4. CPU moves data to/from main memory to local buffers
5. Device controller tells CPU its done with a process by causing interrupt
6. With interrupt handling the OS perserves the state of CPU by storing registers and program counters

A bootstrap program is typically stored on the OS that is firmware.
It usually loads the OS and starts execution

Memory storage -
1. Main memory that is volitile, but fast
2. Secondary storage which is safer but slow

Usually the smaller the capacity the faster the access time
ex. hard-drive vs ram

How modern computers work

1. CPU fires a thread of exec 
2. This sends I0/requests or data
3. Or device can send interrupt to skip over to another part of the regestry
4. Memory stores the exec cycle of all threads

Sequence of OS

1. Bootstrap program starts
2. Kernel loads
3. System daemons are fired up.  Daemons are services provided outside of the kernel
4. Interrupts are sent from software and hardware.

On page 30
