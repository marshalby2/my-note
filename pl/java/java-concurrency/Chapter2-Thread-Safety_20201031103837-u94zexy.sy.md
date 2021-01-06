Writing thread-safe code is, at its core, about managing access to **state**, and in particular to **shared** ,
**mutable state**.
{: id="20210106092029-xxv5i8f"}

Informally, an object’s state is its data, stored in state variables such as instance
or static fields. An object’s state may include fields from other, dependent objects;
a HashMap’s state is partially stored in the HashMap object itself, but also in many
Map.Entry objects. An object’s state encompasses any data that can affect its
externally visible behavior.
{: id="20210106092029-onihn0c"}

By **shared** , we mean that a variable could be accessed by multiple threads; by
**mutable** , we mean that its value could change during its lifetime. We may talk
about thread safety as if it were about code, but what we are really trying to do is
protect data from uncontrolled concurrent access.
{: id="20210106160353-bj383n8"}

To ensure thread safety, check-then-act operations (like lazy initialization) and read-modify-write operations (like increment) must always be atomic.
We refer collectively to check-then-act and read-modify-write sequences as compound actions: sequences of operations that must be executed atomically in order
to remain thread-safe.
{: id="20210106092029-ppaa5a3"}

# What is thread safety?
{: id="20210106092029-phdqmn0"}

# Atomicity
{: id="20210106092029-ja0b5gw"}

# Locking
{: id="20210106092029-27r2fda"}

### Intrinsic locks
{: id="20210106092029-ibv5va0"}

Java provides a built-in locking mechanism for enforcing atomicity: the synchronized block.
{: id="20210106092029-lnc92fx"}

A synchronized block has two parts: a reference to an object that will serve as the lock, and a
block of code to be guarded by that lock.
{: id="20210106092029-tp3z3ob"}

Every Java object can implicitly act as a lock for purposes of synchronization;
these built-in locks are called intrinsic locks or monitor locks.
{: id="20210106092029-pzemxbb"}

### Reentrancy
{: id="20210106092029-ixnbxbi"}

# Guarding state with locks
{: id="20210106092029-8eg3pbb"}
