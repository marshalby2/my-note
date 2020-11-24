C’s memory management system exemplifies that control by letting you determine which functions know which variables and for how long a variable persists in a program

# Storage Class

### Scope

Scope describes the region or regions of a program that can access an identifier. **A C variable
has one of the following scopes: block scope, function scope, function prototype scope, or file
scope**.

##### block scope

the variables cleo and patrick in the following code both have block scope extending to the closing
brace:

```c
double blocky(double cleo)
{
double patrick = 0.0;
...
return patrick;
}
```

##### file scope

A variable with its definition placed outside of any function has file scope. A variable with file
scope is visible from the point it is defined to the end of the file containing the definition. Take
a look at this example

```
#include <stdio.h>
int units = 0; /* a variable with file scope */
void critic(void);
int main(void)
{
...

```

### Linkage

Next, let’s look at linkage. A C variable has one of the following linkages: external linkage,
internal linkage, or no linkage. **Variables with block scope, function scope, or function prototype scope have no linkage**. That means they are private to the block, function, or prototype in which they are defined. **A variable with file scope can have either internal or external linkage. A variable with external linkage can be used anywhere in a multifile program. A variable with internal linkage can be used anywhere in a single translation unit.**

```c
int giants = 5; // file scope, external linkage
static int dodgers = 3; // file scope, internal linkage
int main()
{
...
}
```

### Storage Duration

Scope and linkage describe the visibility of identifiers. Storage duration describes the persistence
of the objects accessed by these identifiers. A C object has one of the following four storage
durations: **static storage duration, thread storage duration, automatic storage duration, or allocated storage duration**

If an object has **static storage duration**, it exists throughout program execution. Variables with
file scope have static storage duration. Note that for file scope variables, the keyword static
indicates the linkage type, not the storage duration. A file scope variable declared using static
has internal linkage, but all file scope variables, using internal linkage or external linkage, have
static storage duration.

**Thread storage duration** comes into play in concurrent programming, in which program execution can be divided into multiple threads. An object with thread storage duration exists from
when it’s declared until the thread terminates. Such an object is created when a declaration
that would otherwise create a file scope object is modified with the keyword _Thread_local.
When a variable is declared with this specifier, each thread gets its own private copy of that
variable.

Variables with block scope normally have **automatic storage duration**. These variables have
memory allocated for them when the program enters the block in which they are defined, and
the memory is freed when the block is exited. The idea is that memory used for automatic variables is a workspace or scratch pad that can be reused. For example, after a function call terminates, the memory it used for its variables can be used to hold variables for the next function that is called. It is possible, however, for a variable to have block scope but static storage duration. To create such a variable, declare it inside a block and add the keyword static to the declaration:

```c
void more(int number)
{
int index;
static int ct = 0;
...
return 0;
}
```

Here the variable ct is stored in static memory; it exists from the time the program is loaded
until the program terminates

### Five Storage Classes

| STORAGE CLASS                | DURATION  | SCOPE | LINKAGE  | HOW DECLARED                                     |
| ---------------------------- | --------- | ----- | -------- | ------------------------------------------------ |
| automatic                    | Automatic | Block | None     | In a block                                       |
| register                     | Automatic | Block | None     | in a block with the keyword register             |
| static with external linkage | Static    | File  | external | Outside of all functions                         |
| static with internal linkage | Static    | File  | internal | Outside of all functions with the keyword static |
| static with no linkage       | Static    | Block | None     | In a block with the keyword static               |

### Automatic Variables

A variable belonging to the automatic storage class has automatic storage duration, block scope,
and no linkage. By default, any variable declared in a block or function header belongs to the
automatic storage class.

### Register Variables

Variables are normally stored in computer memory. With luck, register variables are stored
in the CPU registers or, more generally, in the fastest memory available, where they can be
accessed and manipulated more rapidly than regular variables. Because a register variable may
be in a register rather than in memory, you can’t take the address of a register variable. In most
other respects, register variables are the same as automatic variables. That is, they have block
scope, no linkage, and automatic storage duration. A variable is declared by using the storage
class specifier register

```c
register int quick;
```

### Static Vartiables with Block Scope

1. Static variables are initialized to zero if you don’t explicitly initialize them to some other value.
2. You can’t use static for function parameters:`int wontwork(static int flu); // not allowed`

### Static Variables with External Linkage

1. If a particular external variable is defined in one source code file and is used in a second source code file, declaring the variable in the second file with extern is mandatory.
2. Like automatic variables, external variables can be initialized explicitly. Unlike automatic variables, external variables are initialized automatically to zero if you don’t initialize them. This rule applies to elements of an externally defined array, too. Unlike the case for automatic variables, you can use only constant expressions to initialize file scope variables:

```c
int x = 10; // ok, 10 is constant
int y = 3 + 20; // ok, a constant expression
size_t z = sizeof(int); // ok, a constant expression
int x2 = 2 * x; // not ok, x is a variable
```

### Static Variables with External Linkage

Variables of this storage class have static storage duration, file scope, and internal linkage. You
create one by defining it outside of any function (just as with an external variable) with the
storage class specifier static:

```c
static int svil = 1; // static variable, internal linkage
int main(void)
{
```

The ordinary external variable can
be used by functions in any file that’s part of the program, but the static variable with internal
linkage can be used only by functions in the same file

```c
int traveler = 1; // external linkage
static int stayhome = 1; // internal linkage
int main()
{
extern int traveler; // use global traveler
extern int stayhome; // use global stayhome

```

Both traveler and stayhome are global for this particular translation unit, but only traveler
can be used by code in other translation units. The two declarations using extern document
that main() is using the two global variables, but stayhome continues to have internal linkage.

### Mutiple Files

The difference between internal linkage and external linkage is important only when you have
a program built from multiple translation units, so let’s take a quick look at that topic.

### Summary: Storage Classes

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

### Code Example

create two c source code files parta.c and partb.c

**parta.c**

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

**partb.c**

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

**compile and execute**

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

### Storage Classes and Functions

An external function can be accessed by functions in other files, but a
static function can be used only within the defining file

```c
double gamma(double); /* external by default */
static double beta(int, int);
extern double delta(double, int);
```

The functions gamma() and delta() can be used by functions in other files that are part of the
program, but beta() cannot. Because this beta() is restricted to one file, you can use a different function having the same name in the other files. One reason to use the static storage
class is to create functions that are private to a particular module, thereby avoiding the possibility of name conflicts.

# Allocated Memory: malloc() and free()

The storage classes we discussed have one thing in common. After you decide which storage
class to use, the decisions about scope and storage duration follow automatically. Your choices
obey the prepackaged memory management rules. There is, however, one more choice, one
that gives you more flexibility. That choice is using library functions to allocate and manage
memory.

### The malloc() function

The **malloc()** function, which takes one argument: the number of bytes of memory you want. It does return the address of the first byte of that block. Therefore, you can assign that address to a pointer variable and use the pointer to access the memory. If malloc() fails to find the required space, it returns the null pointer.

Let’s apply malloc() to the task of creating an array. You can use malloc() to request a block
of storage as the program is running. You also need a pointer to keep track of where the block
is in memory. For example, consider this code:

```c
double * ptd;
ptd = (double *) malloc(30 * sizeof(double));
```

This code requests space for 30 type double values and sets ptd to point to the location

### The free() function

The free() function takes as its argument an address returned earlier by malloc() and frees up the memory that had been allocated. Thus, the duration of allocated memory is from when malloc() is
called to allocate the memory until free() is called to free up the memory so that it can be reused

**code examples**

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

### The calloc() function

Another option for memory allotment is to use calloc(). A typical use looks like this:

```c
long * newmem;
newmem = (long *)calloc(100, sizeof (long));
```

The first argument is the number of memory cells you want. The second argument is the size of each cell in bytes. In our case, long uses 4 bytes, so this instruction sets up 100  4-byte units, using 400 bytes in all for storage. (The free() function can also be used to free memory allocated by calloc().)

# Storage Classes and Dynamic Memory Allocation

You might be wondering about the connection between storage classes and dynamic memory
allocation. Let’s look at an idealized model. You can think of a program as dividing its available memory into three separate sections: one for static variables with external linkage, internal linkage, and no linkage; one for automatic variables; and one for dynamically allocated
memory.

The amount of memory needed for the **static duration storage classes** is known at compile time, and the data stored in this section is available as long as the program runs. Each variable of
these classes comes into being when the program starts and expires when the program ends.

**An automatic variable**, however, comes into existence when a program enters the block of code
containing the variable’s definition and expires when its block of code is exited. Therefore, as a
program calls functions and as functions terminate, the amount of memory used by automatic
variables grows and shrinks. This section of memory is typically handled as a stack. That means
new variables are added sequentially in memory as they are created and then are removed in
the opposite order as they pass away.

**Dynamically allocated memor**y comes into existence when malloc() or a related function is
called, and it’s freed when free() is called. Memory persistence is controlled by the programmer, not by a set of rigid rules, so a memory block can be created in one function and disposed
of in another function. Because of this, the section of memory used for dynamic memory
allocation can end up fragmented—that is, unused chunks could be interspersed among active
blocks of memory. Also, using dynamic memory tends to be a slower process than using stack
memory.
Typically, a program uses different regions of memory for static objects, automatic objects, and
dynamically allocated objects. Listing 12.15 illustrates this point.

Listing 12.15 The **where.c**  Program

---

```
// where's the memory?

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int auto_store = 40;
int static_store = 30;
const char *pcg = "String Literal";

int main()
{
    int auto_store = 40;
    char auto_string[] = "Auto char Array";
    int *pi;
    char *pcl;

    pi = (int *)malloc(sizeof(int));
    *pi = 35;

    pcl = (char *)malloc(strlen("Dynamic String") + 1);
    strcpy(pcl, "Dynamic String");

    printf("static_store: %d at %p\n", static_store, &static_store);
    printf("  auto_store: %d at %p\n", auto_store, &static_store);
    printf("         *pi: %d at %p\n", *pi, pi);
    printf(" %s at %p\n", pcg, pcg);
    printf(" %s at %p\n", auto_string, auto_string);
    printf(" %s at %p\n", pcl, pcl);
    printf(" %s at %p\n", "Quoted String", "Quoted String");

    free(pi);
    free(pcl);

    return 0;
}
```

---

Here is the output for one system:

```shell
static_store: 30 at 0x556566773014
  auto_store: 40 at 0x7ffc88d8403c
         *pi: 35 at 0x55656795c260
 String Literal at 0x556566572964
 Auto char Array at 0x7ffc88d84050
 Dynamic String at 0x55656795c280
 Quoted String at 0x5565665729c6
```

As you can see, static data, including string literals occupies one region, automatic data a
second region, and dynamically allocated data a third region (often called a memory heap or free
store).

# ANSI C Type Qualifiers

- const
- volatile
- volatile
- Atomic

### The const Type Qualifier

```
#include<stdio.h>
int main() {

    const int month = 12;
    const int age;
    // age = 20;  not allowed
    printf("moths = %d\n", month); // 12
    printf("age = %d\n", age); // 0

    return 0;
}
```

##### Using const with Pointers and Parameter Declarations

Pointers are more complicated because you have to distinguish between making the pointer itself const and making the value that is pointed to const

```c
const float * pf; /* pf points to a constant float value */
```

`pf`points to a value that must remain constant. The value of pf itself can
be changed

```c
float * const pt; /* pt is a const pointer */
```

that the pointer`pt` itself cannot have its value changed. It must always point to the same
address, but the pointed-to value can change

```c
const float * const ptr;
```

that ptr must always point to the same location and that the value stored at the
location must not change.

**In short, a const anywhere to the left of the * makes the data constant; and a const to the right of the * makes the pointer itself
constant.**

### The volatile Type Qualifier
