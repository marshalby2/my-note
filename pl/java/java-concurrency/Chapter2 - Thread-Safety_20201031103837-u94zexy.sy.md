Writing thread-safe code is, at its core, about managing access to state, and in particular to shared,
mutable state.
{: id="20201102092314-6neznny"}

Informally, an object’s state is its data, stored in state variables such as instance
or static fields. An object’s state may include fields from other, dependent objects;
a HashMap’s state is partially stored in the HashMap object itself, but also in many
Map.Entry objects. An object’s state encompasses any data that can affect its
externally visible behavior
{: id="20201031103928-6madqs4"}

To ensure thread safety, check-then-act operations (like lazy initialization) and read-modify-write operations (like increment) must always be atomic.
We refer collectively to check-then-act and read-modify-write sequences as compound actions: sequences of operations that must be executed atomically in order
to remain thread-safe
{: id="20201031103935-8k29t97"}

# What is thread safety?
{: id="20201102092123-yy0x5oa"}

{: id="20201102093226-safxbj0"}

# Atomicity
{: id="20201031143749-ne4dmyn"}

# Locking
{: id="20201031143804-1fmj4l0"}

### Intrinsic locks
{: id="20201031143815-5slc6dh"}

Java provides a built-in locking mechanism for enforcing atomicity: the synchronized block.
{: id="20201031143831-umdvrqi"}

A synchronized block has two parts: a reference to an object that will serve as the lock, and a
block of code to be guarded by that lock.
{: id="20201031143940-uqdz1ib"}

Every Java object can implicitly act as a lock for purposes of synchronization;
these built-in locks are called intrinsic locks or monitor locks.
{: id="20201031144044-ofb1l1c"}

### Reentrancy
{: id="20201031144405-57zeujo"}

# Guarding state with locks
{: id="20201031145157-kt908xv"}

{: id="20201102082517-0ey59f0"}
