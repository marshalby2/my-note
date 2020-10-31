We may talk about thread safety as if it were about code, but what we are really trying to do is
protect data from uncontrolled concurrent access.
{: id="20201031103928-6madqs4"}

To ensure thread safety, check-then-act operations (like lazy initialization) and read-modify-write operations (like increment) must always be atomic.
We refer collectively to check-then-act and read-modify-write sequences as compound actions: sequences of operations that must be executed atomically in order
to remain thread-safe
{: id="20201031103935-8k29t97"}

{: id="20201031143750-tovce9d"}

# Atomicity
{: id="20201031143749-ne4dmyn"}

# Locking
{: id="20201031143804-1fmj4l0"}

### Intrinsic locks
{: id="20201031143815-5slc6dh"}

Java provides a built-in locking mechanism for enforcing atomicity: the synchronized block.
{: id="20201031143831-umdvrqi"}

A synchronized block has two parts: a reference to an object that will serve as the lock, and a
block of code to be guarded by that lock
{: id="20201031143940-uqdz1ib"}

Every Java object can implicitly act as a lock for purposes of synchronization;
these built-in locks are called intrinsic locks or monitor locks
{: id="20201031144044-ofb1l1c"}

### Reentrancy
{: id="20201031144405-57zeujo"}

{: id="20201031144408-h7qo404"}

{: id="20201031143810-wtze10z"}
