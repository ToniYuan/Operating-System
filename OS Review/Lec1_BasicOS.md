# Operating System
## Lec1:
### 1. What is an OS?
    A program that act as an intermediary between a user and the computer hardware
    Goals: 
    - Excute user's program and solve the user problem easier.
    - Convenient to use.
    - Use the computer HARDWARE in an efficient manner.
### 2. What OS do?
- Convenience, good performance.
- Don't care about resource utilisation.
### 3. OS Definition
- It is a **resource allocator**
  - Manages all resources
  - Decides between conflicting requests for efficient and **fair** resource use.
- It is a **control program**
  - Controls execution of programs to prevent errors and improper use of computer.
### 4. OS loads at start up
**Boostrap program**(启动程序) is loaded at power-on or reboot.
Typically stored in ROM or EPROM, generally known as **firmware**
- Initialises all aspects(方面) of system
- Loads OS's kernel and starts execution
A computer system is one or more CPUs, **device contollers** connected through common bus(公共总线) providing access to shared memory.
It concurrently(并行地) executes the CPU(s) which compete for memory cycles.
### 5. Computer Systems Operation
- I/O devices and CPUs can execute concurrently.
- Each device controller is in charge of a particular device type
- Each device controller has a local buffer.
- CPU moves data from/to main memory from/to local buffer.
- I/O is from the device to local buffer of controller.
- Device controller informs CPU that it has finished its operation by causing an
**interrupt**
### 6. Interrupts?
- An Interrupt transfers control to the interrupt service routine generally, through the interrupt vector, which contains the addresses of all the service routines(中断一般通过中断向量将控制权转移给中断服务例程，中断向量包含所有服务例程的地址).
- Interrupt architecture must save the address of the interrupted instruction.
- A **trap or exception** is a software-generated interrupt caused either by an error or a
user request.
- **An operating system is Interrupt driven**
### 7. Interrupt Handling
The operating system preserves the state of the CPU by storing **registers and the program counter**
It determines which type of interrupt has occurred: 
- polling
- vectored interrupt system
Separate segments of OS code determine what action should be taken for each type of interrupt.
How do interrupts occur?
Hardware interrupt by one of the devices
Software interrupt (exception or trap):
- Software error (e.g., division by zero)
- Request for operating system service
- Other process problems include infinite loop, processes modifying each other or the
operating system
### 8. Operating System Modes
**Dual-mode operation** allows OS to protect itself and other system components 
- User mode and kernel mode
(Mode bit provided by hardware)
- Provides ability to distinguish when system is running user code or kernel code
- Some instructions designated as privileged(特权定义的), only executable in kernel mode
- A system call changes mode to kernel, return from call resets it to user
### 9. Transition from User to Kernel Mode
Timer to prevent infinite loop / process hogging resources
- Timer is set to interrupt the computer after some time period
- Keep a counter that is decremented by the physical clock.
- Operating system set the counter (privileged instruction)
- **When counter hits zero, we generate an interrupt**
- Set up before scheduling process to regain control or terminate program that
exceeds allotted time
### 10. Processes and Process management
A process is a program in execution. It is a unit of work within the system. A program is a **passive entity**(被动), process is an **active entity**(可以理解为被激活的).
- Process needs resources to accomplish its task
  - CPU, memory, I/O, files
  - Initialization data
Process termination requires reclaim of any reusable resources(Eg: Release the memory)
A Single-threaded process has one program counter **specifying location of next instruction to execute**
Process executes instructions sequentially, one at a time, until completion.
Typically system has many processes, some user, some operating system running concurrently on one or more CPUs

### KEY THINGS CONCLUSION:
- What is an OS?
  - Excute user's program
  - Make PC convenient to use
  - Use hardward in efficient manner
  - Allocate resources automactially
- Interrupts:
  - OS is interrupt driven
  - An interrupt occures when error appears or request from OS or other program request.
- OS modes
  - Dual-mode operation
  - User and kernal
  - Privileged -> kernal
  - System call changes the mode to kernal then return then set mode to user
- Rest all keys.