# Operating System
## Lec6 Scheduling:
### Why CPUs need scheduling?
Processes go through multiple phases of CPU-IO over their lifetime.
Maximum CPU utilization through multiprogramming.
When processes wait for IO, CPU can be used for something.
What to run next? There is a need for scheduling.
### CPU Scheduler
CPU utilization
- When CPU becomes idle, OS finds work (waiting process queue).
CPU scheduler selects a process from the ready queue and allocates CPU to it.
Queue may be ordered in various ways.
CPU scheduling decisions may take place when a process changes state:
1 running → waiting,
2 running → ready,
3 waiting → ready,
4 terminates.
For 1 and 4, scheduling is nonpreemptive (run as long as needed) while for 2 and 3 preemptive (may interrupt a running process).
### Challenges with Preemptive Scheduling
A few scenarios that cause problems:
    1 Process 1 is writing data, is preempted by process 2 that reads the same data.
    2 Process 1 asks kernel to do some important changes, process 2 interrupts while they are being done.
Disabling interrupts
    Irrespective of the challenges, most modern operating systems are fully preemptive when running in kernel mode, but disable interrupts on certain small areas of code.
### Dispatcher
Dispatcher gives control of the CPU to the scheduled process.
Switching context.
    Switching to user mode (kernel tasks in supervisor mode).
    Jumping to the proper location in the previously interrupted user program (set the Program Counter register).
Dispatch latency
    Time it takes for the dispatcher to stop one process and start another running.
### Scheduling Criteria
**CPU utilization**—reduce amount of time CPU is idle.
**Throughput**—number of processes completed per time unit.
**Turnaround time**—amount of time to execute a particular process.
**Waiting time**—amount of time a process has been waiting in the ready queue.
**Response time**—amount of time it takes from when a request was submitted until the first response is produced, not output (for time-sharing environment).
When designing a scheduler
    It is desirable to maximize CPU utilization and throughput and to minimize turnaround time, waiting time, and response time.
### First-Come, First-Served (FCFS) Scheduling
Issue with FCFS
Convoy effect—short jobs can be held waiting by long jobs.
### Shortest-Job-First (SJF)
- Append each process with the length of next CPU burst. Schedule jobs with shortest time.
- SJF is optimal, but difficult to know future CPU burst lengths.
- Ties broken with FCFS scheduling.
- Better name shortest-next-CPU-burst.
### Shortest-remaining-time-first
If we allow SJF to be preemptive, it can interrupt a currently running process if it would run longer than some new process.
### Priority Scheduling
Priority scheduling
    Shortest-job-first is a specific case of general scheduler that decides by priorities.
- A priority (integer) associated with each process.
- CPU allocated to a process of highest priority.
- Starvation—low priority processes may not execute.
- Aging—increase the priority proportional to waiting time.
- Internal priorities—time limits, memory requirements, ratio of average I/O burst.
- External priorities—importance of the process, type and amount of funds being paid for the CPUs, who is asking to run the process, and other.
Preemptive priority scheduling
    Priorities may change while a process is running.
### Round Robin (RR) Scheduling
- Time quantum (q) is defined.
- CPU scheduler assigns the CPU to each process for an interval of up to 1 quantum.
- Queue treated as First-In-First-Out.
- Interrupts every quantum to schedule next process.
- RR is therefore preemptive.
- No process allocated for more than q in a row (unless there is only one).
- If there are n processes waiting, each process is guaranteed to get 1/n of CPUs time in chunks of time quantum q.
- Each process must wait no longer than (n − 1) × q time units until its next turn to run.
- Turnaround time depends on the size of the quantum.
- However, it does not necessarily improve with the size of q.
### Multilevel Queue Scheduling
With previous algorithms, it takes O(n) to search the queue. Assign processes to different queues, by priority.
Can also assign to queues by process types:
    1 Queue for background processes (for example, batch processing)
    2 Queue for foreground processes (interactive)
Each queue can have different scheduling algorithms, depending on needs.
Scheduling may be required among queues: commonly fixed-priority preemptive scheduling.
Example queues in decreasing priority level:
    1 Real-time precesses
    2 System processes
    3 Interactive processes
    4 Batch processes
Multilevel priority queue
    No process in a lower priority queue runs while there are processes waiting in the higher priority queues.
    High priority queues preempt lower priority ones.
Time slicing
    Another possibility is to allocate time among queues. Example: 80% to foreground queue and 20% to the background queue.
### Multilevel Feedback Queue Scheduling
Dynamic queueing
    Instead of fixing processes to queues, allow them to move.
    Multilevel feedback queue defined by
- number of queues,
- a scheduling alg. for each queue,
- a method to upgrade a process to higher priority queue,
- a method to downgrade a process, and
- a method to determine which queue to assign process at the start.
Multilevel feedback queue
    Most general CPU scheduling algorithm due to many parameters in the definition.
### Advantages and Disadvantages of Scheduling Algorithms
|Algorithm                  |        (dis)advantages            |
|:--------------------------:|:---------------------------------:|             
|FCFS                       |Convoy effect a problem—long jobs hold the queue. |
|SJF                        |Need to predict future CPU burst lengths.|
|Preemptive SJF             |Better average waiting time than SJF.|
|Priority scheduler         |Starvation.|
|RR                         |Need to tune time quantum to avoid expensive con- text switch.|
|Multilevel queue           |Faster search than O(n).|
|Multilevel feedback queue  |Configuration can be expensive. Starvation.|
### Multi-Processor Scheduling
Traditionally term multi-processor referred to systems with multiple physical cores. Now we use it to describe systems with either several physical or virtual cores/threads.
One approach to scheduling is to have one master processor handling scheduling (assymetric multiprocessing). Master becomes potential bottleneck.
Another is symmetric multiprocessing (SMP)—each processor handles its scheduling. Most common (Windonws, Linux, macOS, Android, iOS).
Two approaches in SMP
  1) Common ready queue—each processor takes processes/threads from that queue (potential clashes).
  2) Each processor has its own queue.
### Multicore Processors
- Relatively recent trend is to place multiple cores on chip (multicore).
- Speed and energy efficiency.
- Memory stall—cores spend significant amount of time for memory (since these days cores are much faster than memory).
- Multithreading—hardware assisted mutliple threads per core.
- When one thread is in memory stall, work on another.
- OS sees different hardware threads as separate CPUs.
### Load balancing
With SMP we need to utilize all CPUs efficiently.
Load balancing attempts even distribution.
Only necessary on systems with separate queues for each CPU.
Push migration—a task checks the load on each CPU and moves threads from CPU to CPU to avoid imbalance.
Pull migration—idle processor pulls waiting tasks from busy processors.
### Processor Affinity
- When a thread runs a processor, the cache is “warmed up” for that thread.
- We say that a task has affinity for the processor it’s running on.
- When a task is moved, say due to load balancing, we have a big overhead in terms of cache.
- Invalidating and repopulating caches is expensive.
- Soft affinity—OS will attempt to keep the process on the same core, but load balancing can move it.
- Hard affinity—processes specify a list of processes on which to run.
- Usually both methods are available.
Implications on scheduling
    Load balancing and processor affinity both may have implications on scheduling.
### Real-Time CPU Scheduling
Real-time systems categorized into two:
    1 Soft real-time: guarantee preference for critical processes.
    2 Hard real-time: guarantee completion by deadline.
Two types of latencies affect performance:
    1 Interrupt latency: time from arrival to interrupt service routine.
    2 Dispatch latency: time for dispatcher to stop current process and start another.
Hard real-time systems
    Various latencies should be bounded to meet the strict requirements of these systems.
### Priority-Based Scheduling
Real-time systems
    It is essential to have a priority-based preemptive scheduling for real-time systems. Usually real-time processes have highest priority.
Priority-based preemptive scheduling gives us soft real-time functionality.
Additional scheduling features required for hard real-time.
Some definitions:
    Processes are periodic—require CPU at constant intervals. Processing time t, deadline d, period p. Here 0 ≤ t ≤ d ≤ p.
Admission control
    Schedulers take advantage of these details and assign priorities based on deadlines and period. Admission control algorithm may reject the request as impossible to service by the required deadline.
### Rate-Monotonic Scheduling
    Upon entering the system, each periodic task assigned priority ∝ 1/P .
    Rationale: prioritize processes that require CPU more often.
### Earliest-Deadline-First Scheduling