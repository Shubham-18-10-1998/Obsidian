Number of cores -> Number of CPUs


# Concurrency
Running multiple things in parallel, but they run on same core. Appears to be done in paralled but done by context switching



# Parallelism
Running things in pure paralleslism. Each core runs a separate task

![[Pasted image 20260122211702.png]]

# Program, Processes, And Threads
Each application is a program
Each program has many processes
Processes use thread to work.

Thread : light weight execution, each thread gets a stack space. All threads share memory

More Threads is not equall to more performance necessarily due to context switching needed.
For heavy processing we use threads

## Thread Class
- Extends Thread class
- put the code to run, in run() method
- We call start so that it runs in parallel

### Life Cycle of Thread
![[Pasted image 20260122214041.png]]

### Daemon Thread 
Child thread running, killed as soon as parent thread killed

### Non-Daemon Thread
Child has to finish, only then parent allowed to conclude




## Runnable Interface
We implement the class with Runnable
Then we do Thread t = new Thread(ThreadRunnable)

If thread are supposed to join, then the thread it joins with should run first.