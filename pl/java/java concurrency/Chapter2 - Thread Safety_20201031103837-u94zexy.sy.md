We may talk about thread safety as if it were about code, but what we are really trying to do is
protect data from uncontrolled concurrent access.
{: id="20201031103928-6madqs4"}

To ensure thread safety, check-then-act operations (like lazy initialization) and read-modify-write operations (like increment) must always be atomic.
We refer collectively to check-then-act and read-modify-write sequences as compound actions: sequences of operations that must be executed atomically in order
to remain thread-safe
{: id="20201031103935-8k29t97"}

{: id="20201031143750-tovce9d"}

# Atom
{: id="20201031143749-ne4dmyn"}
