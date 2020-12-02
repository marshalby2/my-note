Writing thread-safe code is, at its core, about managing access to state, and in particular to shared,
mutable state.

Informally, an object’s state is its data, stored in state variables such as instance
or static fields. An object’s state may include fields from other, dependent objects;
a HashMap’s state is partially stored in the HashMap object itself, but also in many
Map.Entry objects. An object’s state encompasses any data that can affect its
externally visible behavior

To ensure thread safety, check-then-act operations (like lazy initialization) and read-modify-write operations (like increment) must always be atomic.
We refer collectively to check-then-act and read-modify-write sequences as compound actions: sequences of operations that must be executed atomically in order
to remain thread-safe

# What is thread safety?

# Atomicity

# Locking

### Intrinsic locks

Java provides a built-in locking mechanism for enforcing atomicity: the synchronized block.

A synchronized block has two parts: a reference to an object that will serve as the lock, and a
block of code to be guarded by that lock.

Every Java object can implicitly act as a lock for purposes of synchronization;
these built-in locks are called intrinsic locks or monitor locks.

### Reentrancy

# Guarding state with locks
