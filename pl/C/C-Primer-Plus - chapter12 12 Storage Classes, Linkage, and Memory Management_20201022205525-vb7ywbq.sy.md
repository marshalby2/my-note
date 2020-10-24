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

```c
static int svil = 1; // static variable, internal linkage
int main(void)
{
```
{: id="20201023092746-gcw8tzj"}

The ordinary external variable can
be used by functions in any file that’s part of the program, but the static variable with internal
linkage can be used only by functions in the same file
{: id="20201023092840-w7k55zr"}

```c
int traveler = 1; // external linkage
static int stayhome = 1; // internal linkage
int main()
{
extern int traveler; // use global traveler
extern int stayhome; // use global stayhome

```
{: id="20201023092934-7s3vmz1"}

Both traveler and stayhome are global for this particular translation unit, but only traveler
can be used by code in other translation units. The two declarations using extern document
that main() is using the two global variables, but stayhome continues to have internal linkage.
{: id="20201023092954-mpmmlvc"}

### Mutiple Files
{: id="20201023093138-ovwavcr"}

The difference between internal linkage and external linkage is important only when you have
a program built from multiple translation units, so let’s take a quick look at that topic.
{: id="20201023093054-5n7wo68"}

### Summary: Storage Classes
{: id="20201023093631-vgbdenm"}

**Automatic variables** have block scope, no linking, and automatic storage duration. They are
local and private to the block (typically a function) in which they are defined. Register variables
have the same properties as automatic variables, but the compiler may use faster memory or a
register to store them. You can’t take the address of a register variable.
**Variables with static storage duration** can have external linkage, internal linkage, or no linkage.
When a variable is declared external to any function in a file, it’s an external variable and has
file scope, external linkage, and static storage duration. If you add the keyword static to such
a declaration, you get a variable with static storage duration, file scope, and internal linkage.
If you declare a variable inside a function and use the keyword static, the variable has static
storage duration, block scope, and no linkage.
**Memory for a variable with automatic storage duration** is allocated when program execution
enters the block containing the variable declaration and is freed when the block is exited. If
uninitialized, such a variable has a garbage value. Memory for a variable with static storage
duration is allocated at compile time and lasts as long as the program runs. If uninitialized,
such a variable is set to 0.
A variable with block scope is local to the block containing the declaration. A variable with file
scope is known to all functions in a file (or translation unit) following its declaration. If a file
scope variable has external linkage, it can be used by other translation units in the program.
If a file scope variable has internal linkage, it can be used just within the file in which it is
declared.
{: id="20201023093623-jm7q6ix"}

### Code Example
{: id="20201023095707-klokvwp"}

create two c source code files parta.c and partb.c
{: id="20201023095714-2vvoxve"}

**parta.c**
{: id="20201023095857-h9kgwg4"}

```
// parta.c , compile with partb.c
#include<stdio.h>

void report_count();
void accumulate(int k);
int count = 0; // file scope, external linkage

int main() {
    int value; // automatic variable
    register int i; // register variable

    printf("Enter a positive integer (0 to quit): ");
    while (scanf("%d", &value) == 1 && value > 0) {
        ++count; // use file scope variable
        for (i = value; i >= 0; i--) {
            accumulate(i);
        }
        printf("Enter a positive integer (0 to quit): ");
    }
    report_count();
    return 0;
}

void report_count() {
    printf("Loop executed %d times\n", count);
}
```
{: id="20201023095744-ol0i7ig"}

**partb.c **
{: id="20201023095849-t92dba2"}

```
#include<stdio.h>

extern int count;   // reference declaration, external linkage

static int total = 0;   // static definition, internal linkage

void accumulate(int k);  // prototype

void accumulate(int k) { // k has block scope, no linkage
    static int subtotal = 0;    // static, no linkage

    if (k <= 0) {
        printf("loop cycle: %d\n", count);
        printf("subtotal: %d; total: %d\n", subtotal, total);
        subtotal = 0;
    } else {
        subtotal += k;
        total += k;
    }
}   

```
{: id="20201023095851-wreo3rp"}

**compile and execute**
{: id="20201023095917-037qiyl"}

```shell
# 1. compile
$ gcc parta.c partb.c -o part

# 2. execute
$ ./part       
Enter a positive integer (0 to quit): 10
loop cycle: 1
subtotal: 55; total: 55
Enter a positive integer (0 to quit): 5
loop cycle: 2
subtotal: 15; total: 70
Enter a positive integer (0 to quit): 2
loop cycle: 3
subtotal: 3; total: 73
Enter a positive integer (0 to quit): 0
Loop executed 3 times

```
{: id="20201023095942-lfcfyqv"}

### Storage Classes and Functions
{: id="20201023095938-9r33njz"}

An external function can be accessed by functions in other files, but a
static function can be used only within the defining file
{: id="20201023100059-nk9ko57"}

```c
double gamma(double); /* external by default */
static double beta(int, int);
extern double delta(double, int);
```
{: id="20201023101615-toftx24"}

The functions gamma() and delta() can be used by functions in other files that are part of the
program, but beta() cannot. Because this beta() is restricted to one file, you can use a different function having the same name in the other files. One reason to use the static storage
class is to create functions that are private to a particular module, thereby avoiding the possibility of name conflicts.
{: id="20201023101543-du5nsym"}

# Allocated Memory: malloc() and free()
{: id="20201023101823-6kwf7ni"}

The storage classes we discussed have one thing in common. After you decide which storage
class to use, the decisions about scope and storage duration follow automatically. Your choices
obey the prepackaged memory management rules. There is, however, one more choice, one
that gives you more flexibility. That choice is using library functions to allocate and manage
memory.
{: id="20201023101826-71hoajd"}

### The malloc() function
{: id="20201024173243-sae3l2b"}

The **malloc()** function, which takes one argument: the number of bytes of memory you want. It does return the address of the first byte of that block. Therefore, you can assign that address to a pointer variable and use the pointer to access the memory. If malloc() fails to find the required space, it returns the null pointer.
{: id="20201024172620-j5qt4wj"}

Let’s apply malloc() to the task of creating an array. You can use malloc() to request a block
of storage as the program is running. You also need a pointer to keep track of where the block
is in memory. For example, consider this code:
{: id="20201024173005-abrg7qx"}

```c
double * ptd;
ptd = (double *) malloc(30 * sizeof(double));
```
{: id="20201024172958-rnilprv"}

This code requests space for 30 type double values and sets ptd to point to the location
{: id="20201024172626-rtz6yj4"}

### The free() function
{: id="20201024173046-gqn39ns"}

The free() function takes as its argument an address returned earlier by malloc() and frees up the memory that had been allocated. Thus, the duration of allocated memory is from when malloc() is
called to allocate the memory until free() is called to free up the memory so that it can be reused
{: id="20201024173257-x1i3yje"}

{: id="20201024173303-ik52x4s"}

**code examples**
{: id="20201024173418-x9ft7zc"}

```
#include<stdio.h>
#include<stdlib.h>

int main() {
    double * ptd;
    int max = 0;
    int number;
    int i = 0;

    puts("What is the maximum number of type double entries?");
    if (scanf("%d", &max) != 1) {
        puts("Number not correctly entered -- bye.");
        exit(EXIT_FAILURE);
    }

    ptd = (double *) malloc(max * sizeof(double));

    if (ptd == NULL) {
        puts("Memory allocation failed. Goodbye.");
        exit(EXIT_FAILURE);
    }

    puts("Enter the values (q to quit):");
    while (i < max && scanf("%lf", &ptd[i]) == 1)
        i++;
    printf("Here are your %d enteries:\n", number = i);
    for (i = 0; i < number; i++) {
        printf("%7.2f ", ptd[i]);
        if (i % 7 == 6)
            putchar('\n');
    }
    if (i % 7 != 0) {
        putchar('\n');
    }
    puts("Done.");
    free(ptd);

    return 0;
}
```
{: id="20201024173429-nx4n1i5"}

### The calloc() function
{: id="20201024173837-1ctmfqv"}

Another option for memory allotment is to use calloc(). A typical use looks like this:
{: id="20201024173916-1zjcp29"}

```c
long * newmem;
newmem = (long *)calloc(100, sizeof (long));
```
{: id="20201024173849-n4mk31a"}

The first argument is the number of memory cells you want. The second argument is the size of each cell in bytes. In our case, long uses 4 bytes, so this instruction sets up 1004-byte units, using 400 bytes in all for storage.
{: id="20201024173920-n7uwf5v"}

{: id="20201024174008-p9q2s3h"}
