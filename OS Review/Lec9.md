# Operating System
## Lec9:Virtuallisation
### So what is virtualisation then?
In OS virtualisation, the operating system is altered so that it operates like several different, individual systems.
The virtualised environment accepts commands from different users running different applications on the same machine.
The users and their requests are handled separately by the virtualized operating system.
We see this many places, especially in Cloud services where VMs allow us to run many more services than we have physical servers.
### What can we virtualise?
Although we normally talk about virtualisation in terms of operating systems, we can also virtualise:
- applications (with containers)
- networks
- even storage
### Key terms
Virtual Machine (VM):
- a representation of a real machine in software
Guest OS:
- The OS that runs inside the VM
Host OS:
- The OS that runs on the host machine (the one the VMs sit on top of)
Hypervisor (Virtual Machine Monitor)(管理程序):
- The software layer that provides the virtualisation
- Sits between real machine and the VMs.
### Why should we virtualise?
1. It lets us maximise the use of (expensive) resources
2. Reduced the amount of physical hardware we need (thus reducing the space needed in data centres...)
3. Reduce energy consumption footprint (and costs, carbon etc.)
4. If configured correctly, easier to automate: it’s all scriptable.
### Examples:
Virtual Memory, supported by memory and disk
- Virtual Disk System, supported by an array of disks (e.g. RAID)
- Virtual File System, supported by distributed file sub-systems
- Virtual Computing System, supported by multiple, distributed servers
### Benefits
- Freedom of choice for operating system (i.e. testing environment)
- Consolidates server and infrastructure
- It saves time and money
- Makes it easier to manage and secure desktop environments
- Isolates “unsafe” programs into VM
- Can copy VMs from one machine to another
- Can setup copies of the same OS/Software setup quickly
### Disadvantages
- Cost alot
- Something is hard to virtuallize
- Performance overhead is large
### Hypervisor Types
**Type 1: Hypervisor**
- Sits on the bare metal computer
- All the guest operating systems are a layer above the hypervisor.
- Hypervisor is the first layer over the hardware
**Type 2 - Hosted Hypervisor**
- Run over a host operating system
- Is the second layer over the hardware
- Guest operating systems run a layer over the hypervisor
### Hypervisor Properties
Equivalence:
Programs should behave identically to direct execution on equivalent hardware
Resource Control:
Hypervisor must have complete control over virtual resources
Efficiency:
A significant proportion of machine instructions must be executed without interference by the Hypervisor