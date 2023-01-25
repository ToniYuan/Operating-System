# Operating System
## Lec8: File Systemns
### So what’s in a file?
- Files are collections of related information defined by their creator. They commonly represent programs and data.
- They are one of the most essential concepts in computing.
- In general, a file is a sequence of bits, bytes, lines or records whose meaning is defined by its creator and user.
- Among other things, files allow us to:
  - Store large amounts of data
  - Allow information to survive the termination of a process
  - Allow multiple processes to concurrently access data
- Operating systems implement the abstract concept of a file by managing mass-storage devices, such as tapes and disks (spinning and SSD).
- Through operating system calls, we can name files, organise files into logical clusters (directories), and easily locate and access files.
- We can also control by whom and in what ways files may be accessed, through the setting of file attributes, i.e. access control.
### File Access
Files can be accessed in two ways:
- Sequential access:
  - Read all bytes/records from the beginning
  - Cannot jump around, but can rewind/back-up
  - Was convenient when the medium was magnetic tape
- Random access:
  - Bytes/records can be read in any order • Essential for database systems
  - Can seek/read or read/seek
### File Operations
- Through operating system calls, we can interact with files in a variety of ways. Here are some:
  - Create
  - Delete
  - Open
  - Close
  - Read
  - Write
  - Append
  - Seek
  - Get attributes
  - Set attributes
  - Rename
### Layered File Systems
- Devices
  - Disk provides in-place rewrite and random access
  - I/O transfers performed in blocks of sectors (usually 512 bytes)
- I/O Control (Interrupts and Device Drivers)
  -  Manage I/O devices at the I/O control layer
  -  Commands like:
        “read drive1, cylinder 72, track 2, sector 10, into memory location 1060”
  - Outputs low-level hardware specific commands to hardware controller
- Basic File System
  - Generic Command like “retrieve block 123”
    translates to device driver
  - Manages memory buffers and caches (allocation, freeing, replacement)
  - Buffers hold data in transit
  - Caches hold frequently used data
- File organisation module
  - Understands files, logical address and physical blocks
  - Translates logical block number to physical block number
  - Remember: logical number is something that maps to a physical location
  - Manages free space, disk allocation
- Logical file system
  - Manages metadata information
  - All file systems structure except the data itself
  - Directory management
  - Protection
  - Translates file name into file number, file handle, location by maintaining file control blocks (inodes Unix)
- Application Programs
  - These (unsurprisingly) use the file system
### Virtual File Systems (VFS)
- A VFS is software that forms an interface between an OS kernel and a more concrete file system
- Same system call interface (API) for different types of file systems e.g.:
- file systems types • network file system
- Then dispatches operation to appropriate file system implementation routines
### What’s an inode?
- No-one actually knows what the ‘i’ is, but probably means ‘index’.
- An inode is a data structure in Linux that stores information about files except the name and data.
- The main role is keeping track of all the blocks that make up a file. Remember that data is stored on disk in fixed-sized blocks. Files often exceed a block in size and in these cases the OS needs to find the next available block to store the data- and track the positions of all of them.
### Info in an inode
Inodes contain the file’s metadata (not actual data), including where all the storage blocks are:
- File size
- Device on which the file is stored
- User and group IDs associated with the file
- Permissions needed to access the file
- Creation, read, and write timestamps
- Location of the data (not filepath)
- Inodes != Filenames
You can copy a single file, rename it and then it still points to the same inode as the original. You get a new inode when you move the file to a new filesystem or modify it.
### There’s a limit to the number of inodes!
...which actually means there’s a hard limit to the number of files your system can store! Once we use all our inodes:
- We can lose data
- Applications might crash
- OS might restart
- Processes don’t restart
- CRON (automated) jobs fail
