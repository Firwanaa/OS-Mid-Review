###### **1.** When a process creates a new process using the fork() operation, which of the following states is shared between the parent process and the child process?
a. Stack
b. Heap
**c. Shared memory segments**

###### **2.** Describe the differences among short-term, medium-term, and long-term scheduling.
- **Short-term**: jobs ready to execute, fast, frequent and could be the only job in the system. 
- **Long-term**: selects which processes should be brought into ready queue, Infrequent

###### **3.** Describe the actions taken by a kernel to context-switch between processes.
- It saves the state of the current process and restores it when resume

###### **4.** With respect to the RPC mechanism, consider the “exactly once” semantic. Does the algorithm for implementing this semantic execute correctly even if the ACK message back to the client is lost due to a network problem? Describe the sequence of messages and discuss whether “exactly once” is still preserved.
- server must implement the "at most once" protocol but must also acknowledge to the client that the RPC call was received and executed.

###### **5.** Assume that a distributed system is susceptible to server failure. What mechanisms would be required to guarantee the “exactly once” semantic for execution of RPCs?
- The server should keep a history of information and requests regarding the received RPC operations

###### **6.** Give an example of a situation in which ordinary pipes are more suitable than named pipes and an example of a situation in which named pipes are more suitable than ordinary pipes.  
- If we want to establish communication between two specific processes on the same machine

###### **7.** Consider the RPC mechanism. Describe the undesirable consequences that could arise from not enforcing either the “at most once” or “exactly once” semantic. Describe possible uses for a mechanism that has neither of these guarantees.
- Time stamps


###### **8.** What are the benefits and the disadvantages of each of the following? Consider both the system level and the programmer level.  
a. Synchronous and asynchronous communication  
b. Automatic and explicit buffering  
c. Send by copy and send by reference  
d. Fixed-sized and variable-sized messages

###### **9.** What output will be at Line A?

```C
#include <sys/types.h>  
#include <stdio.h>  
#include <unistd.h>  
int value = 5;  
int main()  
{  
pid t pid;  
pid = fork();  
if (pid == 0) { / **child process** /  
value += 15;  
return 0;  
}  
else if (pid > 0) { / **parent process** /  
wait(NULL);  
printf("PARENT: value = %d",value); / **LINE A** /  
return 0;  
}  
}
```

The output of this program at LINE A will be 5. The child process updates only its copy of value and after than control will be returned to parent process in which the value is 5 hence print statements will print the value as 5. Wait() is used in parent process hence firstly child will end then parents execute. Therefore final value will be from parent process.



###### 11-What are the four components of a process?
- Stack
- Heap
- Data
- Text

###### 12- Provide at least three possible states a process may be in.
- New
- Running
- Waiting
- Ready
- Terminated

###### 13- What is a Process Control Block (PCB) ?
A process represented in an operating system- also called task control block. Contains may pieces of information such as process state, program counter, CPU registers, CPU scheduling information,memory management information, Accounting information, I/O status information

###### 14- What is another term for process?
- Job

###### 15- True or False? Most operating systems allow a process to have multiple threads.
- True

###### 16- What is the role of the process scheduler?
- To switch the CPU among processes so frequently that users can interact with each program while it is running – selects an available process for program execution on the CPU.
###### 17- What is the degree of multiprogramming?
The number of processes in memory- controlled by the long term scheduler.
###### 18- What is the term that describes saving the state of one process, and restoring the state of another?
- Context switch

