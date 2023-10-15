###### 1- What are the two bursts that CPU schedulers are designed around?
- CPU burst
- I/O burst


###### 2-True or False? Under preemptive scheduling, when a process switches from the running to the ready state, it may lose control of the CPU.
- False, This is an example of cooperative or nonpreemptive scheduling

###### 3- List at least three different criteria for designing a CPU scheduling algorithm. 
- CPU utilization
- Throughput 
- Turnaround time

- Waiting time
- Response time

###### 4- What scheduling algorithm assigns the CPU to the process with the highest priority?
- Priority Scheduling

###### 5- True or False? The multilevel feedback queue scheduling algorithm allows processes to migrate between different queues.
- True

###### 6- What scheduling algorithm assigns the CPU to the process that first requested it?
- First Come First Serve

###### 7- What scheduling algorithm assigns the CPU to a process for only its time slice (or time quantum?)
- Round Robin

###### 8- What scheduling algorithm assigns the CPU to the process with the shortest burst?
- Shortest Job First (Job)
###### 9- What are the two types of contention scope for thread scheduling?
- process-contention scope
- system-contention scope

###### 10- What are the two general hardware instructions that can be performed atomically?
- test_and_set()
- compare_and_swap()

###### 11- What is more common on current systems, asymmetric or symmetric multiprocessing?
- Symmetric multiprocessing (SMP) 

###### 12- What are the two forms of processor affinity?
- Soft affinity
- Hard affinity

###### 13- What are the two general approaches for load balancing?
- Push migration
- pull migration

###### 14- What are the two ways to multithread a processing core?
- Core grained
- fine-grained

###### 15- What are the two general types of real-time scheduling?
- Soft real-time systems
- Hard real-time sytems

###### 16- What real-time scheduling algorithm uses deadline as its scheduling criteria?
- Hard real-time systems

###### 17- What real-time scheduling algorithm is used for scheduling periodic tasks with static priorities?
- Rate-monotonic

###### 18- What is the name of the default scheduling algorithm for current Linux systems?
- Completely Fair Scheduler (CFS)
###### 19-True or False? A Windows thread is assigned both a priority class and a relative priority within that class.
- True

###### 20- If a thread on a Solaris system exhausts its time quantum, will it later be assigned a higher or lower priority?
- Lower

###### 21- True or False? Deterministic modeling and simulations are similar strategies for evaluating scheduling algorithms.
- True

###### 22-Consider the following set of processes, with the length of the CPU burst given in milliseconds:

Process Burst Time Priority

P1          5                4

P2          3                1

P3          1                2

P4          7                2

P5          4                 3

The processes are assumed to have arrived in the order P1 , P2 , P3 , P4 , P5 , all at time 0.

a. Draw four Gantt charts that illustrate the execution of these processes using the following scheduling algorithms: FCFS, SJF, non-preemptive priority (a larger priority number implies a higher priority), and RR (quantum = 2).

b. What is the turnaround time of each process for each of the scheduling algorithms in part a?

c. What is the waiting time of each process for each of these scheduling algorithms?

d. Which of the algorithms results in the minimum average waiting time (over all processes)?