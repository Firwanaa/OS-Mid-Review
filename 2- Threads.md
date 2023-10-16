###### 1-True or False? Concurrency is only possible with parallelism.
- False 


###### 2- What are the two general types of parallelism?
1. Data parallelism  
2. Task parallelism

###### 3- List the three common ways of mapping user threads to kernel threads.
1. Many-to-one  
2. One-to-one  
3. Many-to-many

###### 4- True or False? PThreads is only a specification, not an implementation.
- True

###### 5-Which of the following components of program state are shared across threads in a multithreaded process?

      a. Register values

   b. Heap memory

   c. Global variables

      d. Stack memory 
- Heap memory 
- Global variables shared

###### 6-As we discussed Google’s Chrome browser and its practice of opening each new tab in a separate process. Would the same benefits have been achieved if, instead, Chrome had been designed to open each new tab in a separate thread? Explain. 

###### 7- Consider the following code segment:
![](Pasted%20image%2020231015203408.png)
a. How many unique processes are created?
 - 6 unique processes
b. How many unique threads are created?
- 2 unique threads will be created.


###### 8-. What would be the output from the following program at LINE C and LINE P?
```C
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int value = 0;
void *runner(void *param);/*the thread*/ 

int main(int argc, char *argv[]) {
  pid_t pid;
  pthread_t tid;
  pthread_attr_t attr;
  pid = fork();
  if (pid == 0) {/*child process*/ 
    pthread_attr_init(&attr);
    pthread_create(&tid, &attr, runner, NULL);
    pthread_join(tid, NULL);
    printf("CHILD: value = %d", value);/*LINE C*/
  } else if (pid > 0) {/*parent process*/
    wait(NULL);
    printf("PARENT: value = %d", value);/*LINE P*/
  }
}


void *runner(void *param) {
  value = 5;
  pthread_exit(0);
}

```
- Child = 5, parent = 0