# Operating System
## Lec10: Containers and Cloud VMs
### Virtual Machines:
- Run software on top of physical hardware
- Emulate hardware and operating system
- Ideal in data centres to consolidate lots of different OSs (Linux, Windows, Unix) on uniform hardware.
### Containers:
- Containers sit on top of the host and it’s OS.
- It shares the Kernel and (usually) binaries and libraries too.
- Much ‘lighter’ than a VM and start up in a fraction of the time.
- Ideal for packaging and sharing complex applications and their dependencies.
- **To the OS, a container is just an application**
### The case for containers in research
Container technologies can support reproducible(可重复的) computational research by allowing a complete research environment to be scripted and shared.
### The four technical challenges
1. Dependency Hell(极其牛逼大的依赖性)
2. Imprecise Documentation(不精确)
3. Code Rot(腐烂代码???)
   a. But make sure you don’t create rotting code
4. Barriers to adoption(采用) and reuse
### Docker
- Lots of codes already available
- Great for the Cloud and your PC
- BAD for HPC(High performance computer)
  - Many security problems on a shared environment
  - Docker daemon(守护进程) needs to run as root
  - Root escalation(升级) problems
### Singularity
- Container system for HPC
- Fewer security issues
- Singularity daemon runs as user process
  - BUT can be root inside a container
- Can import and read Docker containers
- Can convert Docker containers to native Singularity format