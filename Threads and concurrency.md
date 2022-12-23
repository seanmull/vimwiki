
Process moves from memory through the buses to the CPU
Once it in the CPU it enters a pipeline
The CPU has processers and execution engine
It has a clock to determine the rate it which processes get executed

A group of instructions from a single thread such as adding 4 + 5
A CPU could possibly act on more then one thread through a scheduler.
The switch moves so fast it looks as though is executing both threads (Pre-emptive)
Time slice will tell the interval to which processes changes
Each threads has a proirity that may change

A process can have many threads.  Threads can be spawn many child threads
CPUs
Hypertheading - duplicate the pipeline
Multicore - more queues and execution engine

Great example here of how to use threads in node
https://www.digitalocean.com/community/tutorials/how-to-use-multithreading-in-node-js

Process is a running program
Each one has its own reasources memory cpus etc
Each process has a PID
When processes run a single core they are executed concurrently
It switches between the processes but can only do one at a time
The OS scheduler does this so fast it just looks like it does it in parrellell
If the PC has more then one core it can execute tasks in parrellellll

Threads are different in that they share the same reasources allocated within the same process

Javascript is single threaded but when running a node application it sits on top of the V8 engine which provides access to mmultiple threads.  Node also provides threads for I/O operations.  Every node app has 7 threads

Simple routing is a non-blocking operation.  In other words, it doesn't over utilize the main thread.  However CPU bound tasks do.  In order to make operations non-blocking the CPU task need to be moved off the main thread. 

With more cores you can split CPU intensive tasks and save time



