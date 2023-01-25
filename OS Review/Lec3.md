# Operating System
## Lec3:
### 1. Process: Instance of a running program
A process can have
- A CPU time allocation
- Memory (real or virtual)
- Process ID (pid) ● Threads
Are they aware of the existence of other processes?
- The operating system’s role is to create an “illusion” that a process has all it needs to be executed
- An abstraction of hardware resources
- Each process sees one dedicated processor and one segment of memory (although they are often
shared with others)
- But they can be aware of each other – inter-process communication (IPC)
### 2. Typical memory layout of an executing program
Code or Text
- Binary instructions to be executed
- A clone of the program
- Usually read-only
- Program counter (PC), points to the next instruction
Static Data
- Global/Constant/Static variables - shared between threads
- If not initialized by program, will be zero or null pointer
Heap
- malloc/free
Stack
- Used for procedure calls and return
- Stack Pointer(SP)
- FILO (First In, Last Out)
### 3. The process: an abstraction
Switching between executions means the operating system has to keep track of all the execution context Includes:
- Memory State (code, data, heap and stack)
- CPU state (PC, SP and other registers)
- Also the OS state
Hence the abstraction of the process
- Program usually refers to the instructions that are stored on disk
- Process is the program with execution context
Thread: a lightweight process; a process may have multiple threads which share the same system resources * faster creation, termination, switching and communication
### 4. OS functionality: The Process Control Block
The Process Control Block (PCB) or Task Control Block (TCB) maintains all the relevant information for the process:
- Process ID
- Process state
- PC, SP and other registers (stored)
- Scheduling information (how the running of a process is prioritised)
- Memory management information
- Accounting information
- User information
- Inter-Process Communication (IPC)
PCB is stored in memory and it’s location pointed to by something called the process ID pointer
### 5. So, how is a process created?
- By initialisation, by the request of another process OR by user request
- Each process has a unique ID (pid in Linux- try the top command next time in the lab)
Basic steps:
- Allocate memory for the PCB (and some other structures) and user memory
- Initialise the PCB and memory management
- Link the PCB into the process queue
### 6. If a process is created, it should also be stopped...
- Stopped by the OS/user (why?) or terminate itself
- Handle the output of the process
- Release the resources and reclaim the memory
- Unlink the PCB
In embedded software, some processes may never terminate. Terminating implies a fault
### 7. Process state transition (recap from last week)
- Admit: process is fully loaded into memory and control is established
- Dispatch: scheduler assigns CPU to the process
- Time out: expired or preempted, pushed back to the queue
- Event Wait/Event Occurs: generally requests that cannot be met at the moment, has to wait until something occurs
  - OS not ready for a service
  - Unavailable resource
  - Wait for an input
- Release: release resources and end the process
### 8. Process state
- State information is also recorded by the PCB
- Context switch takes place whenever a process leaves/enters the running state
- Processes may make a transition voluntarily or involuntarily, e.g., end the program vs error
- OS typically maintains queue or queue-like (list) structures for processes in the same states (many pointers in the PCB)
### 9. Context Switching
The PCB makes context switching a bit easier
- Scheduler will start or stop a process accordingly
- Stores necessary information in the PCB to stop
  - Hardware registers
  - Program Counter
  - Memory states, stack and heap
  - State
Similarly, loads necessary information from the PCB on a context switch back.
Notice that context switching does consume time!
- Could be up to several thousand CPU cycles
- Overhead and bottleneck
- Hardware support is also needed