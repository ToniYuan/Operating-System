# Operating System
## Lec2:
### 1. OS services
- OS provide an environment to execute programs and to provide services to programs and users
- For the user, services like:
  - UI: Command Line, GUI....
  - Program execution: Load program to memory, run it as a process and terminate it
  - Provide I/O operations: access a file or device
  - File system access: r/w/create/delete/search....
  - Communications: proccesses need to exchange data. eg: some software need to access network or some other like adobe photoshop can transport image with pr.
  - Error detection:CPU, memory, process..
- Efficient operation of the computer via resource sharing
  - Resource allocation across processes (CPU, memory, I/O, file storage)
  - Accounting- keeping track of what users use what kind of resource, and how much
  - Protection and Security- especially important in multiuser systems where processes need to be isolated from one another:
  - **Protection** involves ensuring that all access to system resources is controlled
  - **Security** of the system from outsiders requires user authentication, extends to defending external I/O devices from invalid access attempts
### 2. Processes and Programs?
“The program itself is a lifeless thing: it just sits there on the disk, a bunch of instructions (and maybe some static data), waiting to spring into action.”
“It is the operating system that takes these bytes and gets them running, transforming the program into something useful.”
A process then is:
- "An execution stream in the context of a particular process state."
- A more intuitive, but less precise, definition is just a running piece of code along with all the things that the code can affect or be affected by.
- **Process** state is everything that can affect, or be affected by, the process: includes code, particular data values, open files, etc.
- Execution stream is a sequence of instructions performed in a process state.
- Only one thing happens at a time within a process.
### 3. System Calls
- Essentially:
  - Programming interface to the services provided by the OS
  - Typically written in a high-level language
  - **Mostly accessed by programs via a high-level Application Programming Interface (API) rather than direct system call use**
- Think of the OS (programatically) as layered with each layer providing services to the layer above it
  - Classic way in programming of hiding (abstracting) away complex interactions and providing appropriate services to the appropriate user level
  - Even the OS itself is an abstraction!
### 4. System call parameter passing
Three general methods used to pass parameters into the OS:
- Simplest: pass the parameters in registers
  - In some cases, may be more parameters than registers
- Parameters stored in a block, or table, in memory, and address of block passed as a parameter in a register
  - This approach taken by Linux and Solaris
- Parameters placed, or pushed, onto the stack by the program and popped off the stack by the
operating system
### 5. Types of System call
- Process control
  - create process, terminate process
  - end, abort
  - load, execute
  - get process attributes, set process attributes
  - wait for time
  - wait event, signal event
  - allocate and free memory
  - Dump memory if error
  - Debugger for determining bugs, single step execution
  - Locks for managing access to shared data between processes
- Information maintenance
  - get time or date, set time or date
  - get system data, set system data
  - get and set process, file, or device attributes
- Communications
  - create, delete communication connection
  - send, receive messages if message passing model to host name or process name
    - From client to server
  - Shared-memory model create and gain access to memory regions
  - transfer status information
  - attach and detach remote devices
- File management
  - create file, delete file
  - open, close file
  - read, write, reposition
  - get and set file attributes
- Device management
  - request device, release device
  - read, write, reposition
  - get device attributes, set device attributes
  - logically attach or detach devices
- Protection
  - Control access to resources
  - Get and set permissions
  - Allow and deny user access
### 6. System Programs
- System programs provide a convenient environment for program development and execution. They can be divided into:
  - File manipulation
  - Status information sometimes stored in a File modification
  - Programming language support
  - Program loading and execution
  - Communications
  - Background services
  - Application programs
- Most users’ view of the operating system is defined by system programs, not the actual system calls
- File modification
  - Text editors to create and modify files
  - Special commands to search contents of files or perform transformations of the text
- Programming-language support - Compilers, assemblers, debuggers and interpreters sometimes provided
- Program loading and execution- Absolute loaders, relocatable loaders, linkage editors, and overlay-loaders, debugging systems for higher-level and machine language
- Communications - Provide the mechanism for creating virtual connections among processes, users, and computer systems
- Background Services
  - Launch at boot time
  - Some for system startup, then terminate
  - Some from system boot to shutdown
  - Provide facilities like disk checking, process scheduling, error logging, printing
  - Run in user context not kernel context
  - Known as services, subsystems, daemons
- Application programs
  - Don’t pertain to system
  - Run by users
  - Not typically considered part of OS
### 7. Implementing an OS
- Much variation
  - Early OSes in assembly language
  - Then system programming languages like Algol, PL/1
  - Now C, C++, Rust
- Actually usually a mix of languages
  - Lowest levels in assembly
  - Main body in C
  - Systems programs in C, C++, scripting languages like PERL, Python, shell scripts
- More high-level language easier to port to other hardware
  - But slower
- Emulation can allow an OS to run on non-native hardware (eg xv6 is actually implemented on
RISC-V and emulated in x86 via QEMU)

### KEY THINGS CONCLUSION:
