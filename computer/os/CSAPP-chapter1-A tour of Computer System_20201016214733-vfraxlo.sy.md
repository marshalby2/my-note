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

{: id="20201020164320-0hts506"}
