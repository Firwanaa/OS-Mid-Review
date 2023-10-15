
# Week 1
## Computer System:
- Hardware
- OS: control and coordinate hardware and applications
	- Resource allocator
	- Control program 
- Application programs: define the ways in system resources can be used to solve computing problem
- Users: ppl, machines and other computers
![](Pasted%20image%2020231008120916.png)


### Kernal: The one program running all the time
- Everything else is either:
	- System program (comes with the OS)
	- Application program

## Os Startup (Bootstrapping) or Booting
#### Booting: 
Procedure that transfers the OS from mass storage (permanent) into main memory volatile.

#### Bootstrap: Program in ROM (firmware)
- Run by CPU when power is on (PC starts at predefined address when power applied)
- Transfers OS from mass storage to main memory
- Executes jump to OS

### Interrupts
- Transfer control to interrupt service through interrupt service routines
- Trap or exception is a software-generated interrupt caused either by error or user request

## Operating System Structure
#### Multi programming (Batch systems) 
#### Timesharing (Multitasking)



slide #2023-05-09 ![](Pasted%20image%2020231008133854.png)

### Memory Management
### Storage Management
### I/O Subsystem
- Buffering: Storing data temporarily while it is being transferred
- Caching: Storing parts if data in faster storage for performance
- Spooling: The overlapping of output of one job with input of other job
### Protection and security
### Computing Environments - Traditional
### Computing Environments - Mobile
### Computing Environments - Distributed
### Computing Environments - Client-Server
### Computing Environments - Peer-to-Peer
	- Does not distinguish clients and servers, instead all nodes are considered peers. 
	- Napster, Gnutella and VOIP
### Computing Environments - Visualisation
### Computing Environments - Cloud Computing
### Computing Environments - Real-time Embedded Systems

## Open Source Operating Systems

## SYSGEN
- what CPU is used
- available memory
- available devices
- desired OS options 
## Firmware 
- Readonly
- EPROM : erasable programmable read only memory 
## System Boot
Starting computer by loading the kernel

### Bootstrap program or loader, locates the Kernel
This program in Read-Only memory (ROM), because RAM is in an unknown state. ROM is convenient because it needs no initialisation and can not be infected by viruses.  

# Week 2 (starting slide 31)
### Process Management
- Process is a program in execution
	- Program is passive entity Process is active entity
	`slide 31`![](Pasted%20image%2020231008134811.png)

<hr>

# Week 3 - Module 2,6,8

## Process Concept
#### Process: 
a program in execution; process execution must progress in sequential fashion. 

#### Thread: 
A unit of execution within a process, a process can have one or more threads. 
`slide 1`
![](Pasted%20image%2020231008194620.png)
- Program is passive entity stored in disk (executable file), process is active
	- Program becomes process when executable file loaded into memory.
- One program can be several processes
- Consider multiple users executing same program

### Process in Memory
![](Pasted%20image%2020231008195044.png)
### Process State
- **New**: process created 
- **Running**: instruction executed
- **Waiting**: The process is waiting for some event to occur
- **Ready**: The process is waiting to be assigned to a processor
- **Terminated**: process finished execution
![](Pasted%20image%2020231010160224.png)
### Process Control Block (PCB)
> also called Task Control Block
![](Pasted%20image%2020231008195426.png)

- Process state
- Program counter: Address of next instruction (line)
- CPU registers: contents of all process-centric registers
- CPU scheduling information 
- Memory management information
- Accounting information: resources used by process
- I/O status information: input/output devices used by process

### Process Scheduling (Intro)
The objective of **Multiprogramming** is to have some process running **All the time**, to maximize CPU utilization. 

The objective of **Time Sharing** is to switch the CPU among processes **so frequently** that user interact with each program while it is running.

To meet these objectives, the process scheduler selects an available process for program execution in the CPU. 

#### Scheduling Queues
**Job Queue**: As the process enter the system they are put into a job queue, which consists of all the processes in the system. 

**Ready Queue**: Processes in the main memory and are ready and waiting to execute kept on this list. 

**Device Queue**: Set of processes waiting for an I/O device

- Processes migrate among the various queues. 

![](Pasted%20image%2020231010164500.png)

#### Schedulers
##### Short-term scheduler (CPU)
- Select which process should be executed next. 
- Maybe the only the scheduler in the system. 
- short-term scheduler invoke **frequently** (milliseconds) => Must be fast
##### Long-Term scheduler: 
- Selects which processes should be brought into ready queue.
- Invoked **infrequently** (seconds, minutes) => (may be slow)
- It controls the level of multiprogramming
###### Processes can be described as either:
- I/O-bound process - spends more time doing I/O than computations, many short cpu bursts. 
- CPU-bound process - spends more time doing computations; few very long CPU bursts

## Context Switch
The interrupts cause the operating system to change a CPU from it's current task and to run in kernel routine. 

Such operation happen frequently on general-purpose systems. 

When the interrupt happen, the system needs to save the current **Context** of the process currently running in the CPU so it can restore that context when its processing is done. Essentially suspending the process and them resuming it. 

The context is represented in the PCB of the process. 
- State save
- State restore

- Context-switch time is pure **overhead**, because the system does no useful work while switching.
- Its speed varies from machine to machine

### Operations on Processes 
#### Process Creation
- A process may create several new processes, via create-process system call. 
- Parent process create children process. 

###### Address space:
- child duplicate of parent
- child has a program loaded into it
###### Unix examples:
- `fork()`: system call create new process
- `exec()`: system call used after `fork()` to replace the process memory space with a new program. 

#### Process Termination
- `exit()`  system call, asks OS to delete it.
- Returns status value (typically an integer), to its parent process (via wait() system call).
- All resources deallocated by the OS.
- Parent may terminate execution of children process using `abort()` system call. 
- Some operating systems does not allow child to exist if its parent terminated: cascade termination.
- Parent wait termination of child using `wait()` 
	- `pid = wait(&status)`
- If no parent waiting (did not invoke wait()), process is **Zombie** 🧟
- Parent may kill child process for many reasons:
	- Child exceed its usage of some of the resources
	- The task assigned to child no longer required
	- The parent exiting and the OS does not allow zombie🧟 processes

#### Multiprocess Communication
`slide 26`
![](Pasted%20image%2020231010181346.png)


### Interprocess Communications (IPC)
- Processes may be **Independent** or **Cooperating**:

#### Independent process:
Can not affect or be affected by the execution of another process
#### Cooperating process
Can affect or be affected by other processes, including sharing data. Needs **IPC**
##### Reasons for cooperating processes:
- Information sharing
- Computation speedup
- Modularity
- Convenience
##### Two Models of (IPC)
- Shared memory
	- Region of memory that is shared by cooperating processes is established.
	- Processes can then exchange information by reading and writing data to shared region. 
- Message passing
	- Messages exchanged between cooperating processes to synchronize their actions
	- without resorting to shared variables
	- IPC provides two operations:
		- send(message)
		- receive(message)
	- ##### Communication Link
		- ###### Physical 
			- Shared memory
			- Shared Bus
			- Network
		- ###### Logical:
			- Direct / Indirect
			- Synchronous or asynchronous
			- Automatic or explicit
#### Direct / Indirect
##### Direct:
Explicitly name the recipient or the sender of the communication.
- send(P, message) # send message to process P
- receive(Q, message) # receive message from process Q
- ###### Properties of communication link
	- established automatically
	- only on pair of processes
	- Between each pair exists one link
	- The link maybe unidirectional, but usually bidirectional
##### Indirect:
Messages are directed and received from a mailbox (also referred as ports)
- Each mailbox has a unique id
- Processes can communicate only if they share a mailbox
	- `send(A, message) # 'A' is the name of mailbox `
	- `receive(A, message) # 'A' is the name of mailbox `
- ###### Properties of communication link
	- established only if processes share a common mailbox
	- link may be associated with many processes
	- share two or more several communication links
	- Unidirectional or bidirectional
	- **Problem**: `P1, P2 and P3` share a mail box A, `P1` sends; P2 and P3 receive. Who gets the message?
		- **Solution**:
			- allow like to have only two process
			- allow only one process to receive()
			- allow the system to decide, send notify who is the receiver. 

#### Synchronous / Asynchronous
- ##### Blocking -> Synchronous
	- **Blocking Send**: the sender is blocked until the message received. 
	- **Blocking Receive**: the receiver blocked until a message available 
- ##### Unblocking -> Asynchronous
	- **Non-blocking send**: the process sends the message and resume operation
	- **Non-blocking receive**: The receiver receives:
		- A valid message or
		- Null message
#### Automatic / Explicit buffering
- Direct or indirect: messages exchanged using temporary queue:
	- **Zero capacity**: No message queued. 
	- **Bounded Capacity**: finite length n messages, sender must wait if link is full
	- **Unbounded Capacity**: infinite length, sender never waits

#### Slides (44 - 49):
##### Examples of IPC systems:
- POSIX shared memory
- Mach Message passing
- Windows
- Pipes

![](Pasted%20image%2020231010191934.png)
![](Pasted%20image%2020231010192018.png)

#### Shared Memory Systems:
- Typically, shared memory region resides in the address space of the process creating the shared-memory segment. 
- other process must attach it to their address space. 

#### Producer-Consumer Problem 
producer process produce information and consumer process consume information 🤯.
- Using Buffer
	- Unbounded-buffer: no practical limit on the size
	- bounded-buffer: assumes there is a fixed buffer size.


## Threads 🧵
![](Pasted%20image%2020231008220530.png)
#### Using Terminal
#### `gcc -g -pthread main.c -o main`
#### Using VScode
![](Pasted%20image%2020231008221851.png)

## Mutex vs Semaphore
 provides synchronisation service also known as synchronisation primitives.
 **Mutex**: Mutual exclusion to specific portion of the code. It uses priority inheritance mechanism to avoid **priority inversion** issues.
 **Semaphore**: is a non-negative integer variables that shared between various threads. It uses two atomic operations 
 - Wait (P)
 - Signal (V)

|                                                                 Mutex                                                                 |                                                                           Semaphore                                                                          |
|:-------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                                                         A mutex is an object.                                                         |                                                                  A semaphore is an integer.                                                                  |
|                                                Mutex works upon the locking mechanism.                                                |                                                              Semaphore uses signaling mechanism                                                              |
| Operations on mutex: Lock Unlock                                                                                                      | Operation on semaphore: Wait Signal                                                                                                                          |
|                                                    Mutex doesn’t have any subtypes.                                                   | Semaphore is of two types: Counting Semaphore Binary Semaphore                                                                                               |
|                        A mutex can only be modified by the process that is requesting or releasing a resource.                        |                                         Semaphore work with two atomic operations (Wait, signal) which can modify it.                                        |
| If the mutex is locked then the process needs to wait in the process queue, and mutex can only be accessed once the lock is released. | If the process needs a resource, and no resource is free. So, the process needs to perform a wait operation until the semaphore value is greater than zero.  |


<hr>

# Week 4 - Module 2,6,8 (5-60) , Module 3 (1-16)
## Sockets
- Endpoint for communication
- Pair of processes communicating over the network



# Week 6 - Module 4 (till slide 18)