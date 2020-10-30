![1.1.png](assets/20201020170008-l68sat3-1.1.png)
{: id="20201020165935-5qdsn0e"}

# 1.1 Information Is Bits + Context
{: id="20201016214742-y4rz57j"}

> The representation of hello.c illustrates a fundamental idea: All information
> in a system—including disk files, programs stored in memory, user data stored in
> memory, and data transferred across a network—is represented as a bunch of bits.
> The only thing that distinguishes different data objects is the context in which
> we view them. For example, in different contexts, the same sequence of bytes
> might represent an integer, floating-point number, character string, or machine
> instruction.
> {: id="20201016215406-mlqjm9d"}
{: id="20201016215405-c1pz6n5"}

# 1.2 Programs Are Translated by Other Programs into Different Forms
{: id="20201016215443-pttl6f4"}

![s1.21.png](assets/20201016220402-ubms4au-s1.2_1.png)
{: id="20201016215105-080hjj7"}

# 1.3 It Pays to Understand How Compilation Systems Work
{: id="20201016220440-uuvl19z"}

# 1.4 Processors Read and Interpret Instructions Stored in Memory
{: id="20201018102451-gzcdkkm"}

![1.4.1.png](assets/20201018102556-g3yi5sw-1.4.1.png)
{: id="20201018102458-tr7xc7h"}

### 1.4.1 Hardware Organization of a System
{: id="20201018102810-stdch8c"}

##### Buses
{: id="20201018102958-otvnewf"}

Running throughout the system is a collection of electrical conduits called buses
{: id="20201018103001-k2ywdqa"}

that carry bytes of information back and forth between the components.
{: id="20201018102649-yck0t1m"}

##### I/O Devices
{: id="20201018103004-wpszskp"}

Input/output (I/O) devices are the system’s connection to the external world. Our
example system has four I/O devices: a keyboard and mouse for user input, a
display for user output, and a disk drive (or simply disk) for long-term storage of
data and programs. Initially, the executable hello program resides on the disk.
{: id="20201020164245-dybxiqi"}

##### Main Memory
{: id="20201020164320-0hts506"}

The main memory is a temporary storage device that holds both a program and
the data it manipulates while the processor is executing the program.Physically,
main memory consists of a collection of dynamic random access memory (DRAM)
chips. Logically, memory is organized as a linear array of bytes, each with its own
unique address (array index) starting at zero.
{: id="20201020164350-nryzbnx"}

##### Processor
{: id="20201020164352-omgibae"}

The central processing unit (CPU), or simply processor, is the engine that interprets (or executes) instructions stored in main memory. At its core is a word-size
storage device (or register) called the program counter (PC). At any point in time,
the PC points at (contains the address of) some machine-language instruction in
main memory
{: id="20201020164430-2hu1dgw"}

### 1.4.2 Running the hello Program
{: id="20201020165449-iai51so"}

![1.5.png](assets/20201020165533-d2btsf3-1.5.png)
{: id="20201020165452-hx4zcji"}

# 1.5 Caches Matter
{: id="20201020165653-l8mtuy9"}

An important lesson from this simple example is that a system spends a lot of
time moving information from one place to another. The machine instructions in
the hello program are originally stored on disk. When the program is loaded,
they are copied to main memory. As the processor runs the program, instructions are copied from main memory into the processor. Similarly, the data string
hello,world\n, originally on disk, is copied to main memory and then copied
from main memory to the display device. From a programmer’s perspective, much
of this copying is overhead that slows down the “real work” of the program. Thus,
a major goal for system designers is to make these copy operations run as fast as
possible.
{: id="20201020165707-gzqovjm"}

![1.6.png](assets/20201020165843-dcj38cv-1.6.png)
{: id="20201020165838-53mkcnm"}

![1.7.png](assets/20201020195445-ilouqlh-1.7.png)
{: id="20201020195440-b4ryzyq"}

![1.8.png](assets/20201020195453-q10jjo8-1.8.png)
{: id="20201020195447-mkwbc85"}

The idea behind caching is that a system can get the effect of both
a very large memory and a very fast one by exploiting locality, the tendency for
programs to access data and code in localized regions. By setting up caches to hold
data that are likely to be accessed often, we can perform most memory operations
using the fast caches
{: id="20201020195645-pp3g7f7"}

![1.9.png](assets/20201020195501-wxpjq9v-1.9.png)
{: id="20201020195455-46l5htu"}

# 1.6 Storage Devices Form a Hierarchy
{: id="20201020195742-1dxoq2y"}

The main idea of a memory hierarchy is that storage at one level serves as a
cache for storage at the next lower level. Thus, the register file is a cache for the
L1 cache. Caches L1 and L2 are caches for L2 and L3, respectively. The L3 cache
is a cache for the main memory, which is a cache for the disk. On some networked
systems with distributed file systems, the local disk serves as a cache for data stored
on the disks of other systems.
{: id="20201020195744-pbjusu5"}

# 1.7 The Operating System Manages the Hardware
{: id="20201020201244-cwpg3m8"}

![1.71.png](assets/20201020201550-8ovzrqd-1.7_1.png)
{: id="20201020201249-ah8hqr6"}

The operating system has two primary purposes: (1) to protect the hardware
from misuse by runaway applications and (2) to provide applications with simple
and uniform mechanisms for manipulating complicated and often wildly different
low-level hardware devices. The operating system achieves both goals via the
fundamental abstractions shown in Figure 1.11: processes, virtual memory, and
files. As this figure suggests, files are abstractions for I/O devices, virtual memory
is an abstraction for both the main memory and disk I/O devices, and processes
are abstractions for the processor, main memory, and I/O devices. We will discuss
each in turn.
{: id="20201020201553-ls7zoxi"}

### 1.7.1 Processes
{: id="20201020201554-ifa6ys1"}

A process is the operating system’s abstraction for a running program. Multiple processes can run concurrently on the same system, and each process appears
to have exclusive use of the hardware.
{: id="20201020201629-lsi5lk0"}

The operating system keeps track of all the state information that the process
needs in order to run. This state, which is known as the context,
{: id="20201020201952-hi5qquf"}

![1.72.png](assets/20201020202523-34q76b5-1.7_2.png)
{: id="20201020202517-i6jrczj"}

There are two concurrent processes in our example scenario: the shell process
and the hello process. Initially, the shell process is running alone, waiting for input
on the command line. When we ask it to run the hello program, the shell carries
out our request by invoking a special function known as a system call that passes
control to the operating system. The operating system saves the shell’s context,
creates a new hello process and its context, and then passes control to the new
hello process. After hello terminates, the operating system restores the context
of the shell process and passes control back to it, where it waits for the next
command-line input.
{: id="20201020202526-g9zefjr"}

### 1.7.2 Threads
{: id="20201020202749-x1cdeyb"}

Although we normally think of a process as having a single control flow, in modern
systems a process can actually consist of multiple execution units, called threads,
each running in the context of the process and sharing the same code and global
data.
{: id="20201020202759-vjhlfn5"}

### 1.7.3 Virtual Memory
{: id="20201020203030-5mmugk0"}

Virtual memory is an abstraction that provides each process with the illusion that it
has exclusive use of the main memory. Each process has the same uniform view of
memory, which is known as its virtual address space.
{: id="20201020203033-das6wt8"}

![1.73.png](assets/20201020202938-emrnb81-1.7_3.png)
{: id="20201020203141-995xs7s"}

### 1.7.4 Files
{: id="20201020211637-58ns3qt"}

A file is a sequence of bytes, nothing more and nothing less. Every I/O device,
including disks, keyboards, displays, and even networks, is modeled as a file. All
input and output in the system is performed by reading and writing files, using a
small set of system calls known as Unix I/O.
{: id="20201020211655-z56spyk"}

# 1.8 Systems Communicate with Other Systems Using Networks
{: id="20201020211828-ocv4mxh"}

With the advent of global networks such as the Internet, copying information
from one machine to another has become one of the most important uses of
computer systems. For example, applications such as email, instant messaging, the
World Wide Web, FTP, and telnet are all based on the ability to copy information
over a network.
{: id="20201021094338-6chay9a"}

![1.14.png](assets/20201021100405-kub3j8t-1.14.png)
{: id="20201021100326-2ekkmob"}

# 1.9 Important Themes
{: id="20201021103329-67yd622"}

### 1.9.1 Amdahl’s Law
{: id="20201021103334-8ahpmxp"}

### 1.9.2 Concurrency and Parallelism
{: id="20201021103344-m11wc1o"}

{: id="20201030150239-dshp1te"}

### 1.9.3 The Importance of Abstractions in Computer Systems
{: id="20201021103401-8xg8n1k"}

The use of abstractions is one of the most important concepts in computer science
{: id="20201021104650-7gmjp7f"}

![1.18.png](assets/20201021104731-invqu6k-1.18.png)
{: id="20201021104708-z4pt1er"}

On the operating system side, we have introduced three abstractions: files as
an abstraction of I/O devices, virtual memory as an abstraction of program memory, and processes as an abstraction of a running program. To these abstractions
we add a new one: the virtual machine, providing an abstraction of the entire
computer, including the operating system, the processor, and the programs.
{: id="20201021104732-qdrwho6"}

{: id="20201030150237-gelvb2r"}
