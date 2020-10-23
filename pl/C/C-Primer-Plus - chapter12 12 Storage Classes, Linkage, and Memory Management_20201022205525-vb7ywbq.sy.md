C’s memory management system exemplifies that control by letting you determine which functions know which variables and for how long a variable persists in a program
{: id="20201022213840-ep4u3iu"}

# Storage Class
{: id="20201022205527-1wd0l6h"}

### Scope
{: id="20201022210324-7yq54dg"}

Scope describes the region or regions of a program that can access an identifier. A C variable
has one of the following scopes: block scope, function scope, function prototype scope, or file
scope.
{: id="20201022210330-59itslh"}

##### block scope
{: id="20201022210655-00a6j7w"}

the variables cleo and patrick in the following code both have block scope extending to the closing
brace:
{: id="20201022210521-r7kc4bm"}

```c
double blocky(double cleo)
{
double patrick = 0.0;
...
return patrick;
}
```
{: id="20201022210344-des4rkj"}

##### file scope
{: id="20201022205541-3rgdutb"}

A variable with its definition placed outside of any function has file scope. A variable with file
scope is visible from the point it is defined to the end of the file containing the definition. Take
a look at this example
{: id="20201022210716-kp0ysml"}

```
#include <stdio.h>
int units = 0; /* a variable with file scope */
void critic(void);
int main(void)
{
...

```
{: id="20201022210720-dx41igf"}

### Linkage
{: id="20201022211023-eg4gzez"}

Next, let’s look at linkage. A C variable has one of the following linkages: external linkage,
internal linkage, or no linkage. Variables with block scope, function scope, or function prototype scope have no linkage. That means they are private to the block, function, or prototype in
which they are defined. A variable with file scope can have either internal or external linkage.
A variable with external linkage can be used anywhere in a multifile program. A variable with
internal linkage can be used anywhere in a single translation unit.
{: id="20201022211026-a910iie"}

```c
int giants = 5; // file scope, external linkage
static int dodgers = 3; // file scope, internal linkage
int main()
{
...
}
```
{: id="20201022211626-p60bvha"}

### Storage Duration
{: id="20201022211132-fagbb73"}

Scope and linkage describe the visibility of identifiers. Storage duration describes the persistence
of the objects accessed by these identifiers. A C object has one of the following four storage
durations: static storage duration, thread storage duration, automatic storage duration, or allocated storage duration
{: id="20201022211801-41koa2v"}

If an object has **static storage duration**, it exists throughout program execution. Variables with
file scope have static storage duration. Note that for file scope variables, the keyword static
indicates the linkage type, not the storage duration. A file scope variable declared using static
has internal linkage, but all file scope variables, using internal linkage or external linkage, have
static storage duration.
{: id="20201022211839-erynvca"}

**Thread storage duration** comes into play in concurrent programming, in which program execution can be divided into multiple threads. An object with thread storage duration exists from
when it’s declared until the thread terminates. Such an object is created when a declaration
that would otherwise create a file scope object is modified with the keyword _Thread_local.
When a variable is declared with this specifier, each thread gets its own private copy of that
variable.
{: id="20201022212053-hpw56c8"}

Variables with block scope normally have **automatic storage duration**. These variables have
memory allocated for them when the program enters the block in which they are defined, and
the memory is freed when the block is exited. The idea is that memory used for automatic variables is a workspace or scratch pad that can be reused. For example, after a function call terminates, the memory it used for its variables can be used to hold variables for the next function that is called. It is possible, however, for a variable to have block scope but static storage duration. To create such a variable, declare it inside a block and add the keyword static to the declaration:
{: id="20201022212143-k54jc31"}

```c
void more(int number)
{
int index;
static int ct = 0;
...
return 0;
}
```
{: id="20201022212403-xacyexm"}

Here the variable ct is stored in static memory; it exists from the time the program is loaded
until the program terminates
{: id="20201022212245-e4xjbor"}

### Five Storage Classes
{: id="20201022213322-6bdr70z"}

| STORAGE CLASS | DURATION | SCOPE | LINKAGE | HOW DECLARED |
| - | - | - | - | - |
| automatic | Automatic | Block | None | In a block |
| register | Automatic | Block | None | in a block with the keyword register |
| static with external linkage | Static | File | external | Outside of all functions |
| static with internal linkage | Static | File | internal | Outside of all functions with the keyword static |
| static with no linkage | Static | Block | None | In a block with the keyword static |
{: id="20201022213322-v5506h1"}

### Automatic Variables
{: id="20201022213343-fksc5lj"}

A variable belonging to the automatic storage class has automatic storage duration, block scope,
and no linkage. By default, any variable declared in a block or function header belongs to the
automatic storage class.
{: id="20201022213355-9elahop"}

### Register Variables
{: id="20201022213645-3ur83ft"}

Variables are normally stored in computer memory. With luck, register variables are stored
in the CPU registers or, more generally, in the fastest memory available, where they can be
accessed and manipulated more rapidly than regular variables. Because a register variable may
be in a register rather than in memory, you can’t take the address of a register variable. In most
other respects, register variables are the same as automatic variables. That is, they have block
scope, no linkage, and automatic storage duration. A variable is declared by using the storage
class specifier register
{: id="20201022213648-m9rybg2"}

```c
register int quick;
```
{: id="20201022213738-tic48j7"}

### Static Vartiables with Block Scope
{: id="20201023090503-gzd76wj"}

1. Static variables are initialized to zero if you don’t explicitly initialize them to some other value.
{: id="20201023090511-3cq0bsr"}

2. You can’t use static for function parameters:`int wontwork(static int flu); // not allowed`
{: id="20201023090620-kbxpyzj"}

{: id="20201023090725-2ps73tj"}

### Static Variables with External Linkage
{: id="20201023091207-2ogail5"}

1. If a particular external variable is defined in one source code file and is used in a second source code file, declaring the variable in the second file with extern is mandatory.
2. Like automatic variables, external variables can be initialized explicitly. Unlike automatic variables, external variables are initialized automatically to zero if you don’t initialize them. This rule applies to elements of an externally defined array, too. Unlike the case for automatic variables, you can use only constant expressions to initialize file scope variables:
{: id="20201023091206-rumyh7p"}

```c
int x = 10; // ok, 10 is constant
int y = 3 + 20; // ok, a constant expression
size_t z = sizeof(int); // ok, a constant expression
int x2 = 2 * x; // not ok, x is a variable
```
{: id="20201023091233-cutkrqs"}

### Static Variables with External Linkage
{: id="20201023092358-k5g7p4s"}

Variables of this storage class have static storage duration, file scope, and internal linkage. You
create one by defining it outside of any function (just as with an external variable) with the
storage class specifier static:
{: id="20201023092835-s6l7ke6"}

```

```
{: id="20201023092746-gcw8tzj"}
