The C language proper is built on the C keywords, expressions, and statements as well as the
rules for using them. The C standard, however, goes beyond describing just the C language. It
also describes how the C preprocessor should perform, establishes which functions form the standard C library, and details how these functions work. We’ll explore the C preprocessor and
the C library in this chapter, beginning with the preprocessor.
{: id="20201027192249-ivlrey7"}

# Manifest Constants: #define
{: id="20201027192716-duxgzfi"}

The #define preprocessor directive, like all preprocessor directives, begins with the # symbol
at the beginning of a line. The ANSI and subsequent standards permit the # symbol to be
preceded by spaces or tabs, and it allows for space between the # and the remainder of the
directive.
{: id="20201027192718-2sjuy2v"}

```
#include<stdio.h>

#define TWO 2
# define OW "Consistency is the last refuge of the unimagina\
tive. - Oscar Wilde"
#define FOUR TWO*TWO
#define PX printf("x is %d.\n", x)

int main() {
    int x = TWO;
    PX;
    x = FOUR;
    // printf(FMT, x);
    printf("%s\n", OW);
    printf("TWO: OW\n");

    return 0;
}
```
{: id="20201027194028-qjqeuh5"}

Each #define line (logical line, that is) has three parts. The first part is the #define directive
itself. The second part is your chosen abbreviation, known as a **macro**. Some macros, like these
examples, represent values; they are called object-like macros. (C also has function-like macros,
and we’ll get to them later.) The macro name must have no spaces in it, and it must conform
to the same naming rules that C variables follow: Only letters, digits, and the underscore (_)
character can be used, and the first character cannot be a digit. The third part (the remainder
of the line) is termed the replacement list or body (see Figure 16.1). When the preprocessor finds
an example of one of your macros within your program, it almost always replaces it with the
body. (There is one exception, as we will show you in just a moment.) This process of going
from a macro to a final replacement is called macro expansion. Note that you can use standard
C comments on a #define line; as mentioned earlier, each is replaced by a space before the
preprocessor sees it
{: id="20201027194026-y1wfqba"}

![16.1.png](assets/20201027194159-hysbzim-16.1.png)
{: id="20201027194042-bzcg61j"}

# Using Arguments with #define
{: id="20201027195217-vhp5ca2"}

```
#include<stdio.h>

#define SQUARE(x) x*x
#define PX(x) printf("x is %d\n", x)

int main() {
    printf("The 2 square is %d\n", SQUARE(2));
    int x = 10;
    PX(x);
    return 0;
}
```
{: id="20201027195219-809yx62"}

Here, SQUARE is the macro identifier, the X in SQUARE(X) is the macro argument, and X*X is the
replacement list
{: id="20201027195822-uqfax2z"}

`#define SQUARE(x) ((x)*(x))`
{: id="20201027195823-ovkbmxn"}

### Macro or Function?
{: id="20201027230407-amqy9m4"}

The macro-versus-function choice represents a trade-off between time and space. A macro
produces inline code; that is, you get a statement in your program. If you use the macro 20
times, you get 20 lines of code inserted into your program. If you use a function 20 times, you
have just one copy of the function statements in your program, so less space is used. On the
other hand, program control must shift to where the function is and then return to the calling
program, and this takes longer than inline code.
{: id="20201027230410-khgo9nu"}

Macros have an advantage in that they don’t worry about variable types. (This is because they
deal with character strings, not with actual values.) Therefore, the SQUARE(x) macro can be
used equally well with int or float.
{: id="20201027230450-bbm261u"}

# File Inclusion: #include
{: id="20201028090613-q987z76"}

When the preprocessor spots an #include directive, it looks for the following filename and
includes the contents of that file within the current file. The #include directive in your source
code file is replaced with the text from the included file. It’s as though you sat down and typed
in the entire contents of the included file at that particular location in your source file. The
#include directive comes in two varieties:
{: id="20201028090924-zsqwj32"}

**#include stdio.h**  Filename directive>> in (angle brackets)> )> (angle)>angle brackets
**#include "mystuff.h"**  Filename in double quotation marks
{: id="20201028091016-qnrjsrl"}

On a Unix system, the angle brackets tell the preprocessor to look for the file in one or more
standard system directories. The double quotation marks tell it to first look in your current
directory (or some other directory that you have specified in the filename) and then look in the
standard places:
{: id="20201028091216-9qv0obf"}

**#include stdio.h**  Searches directive>> system directories
**#include "hot.h"** Searches your current working directory
**#include "/usr/biff/p.h"** Searches the /usr/biff directory
{: id="20201028091253-w2jry9n"}

# Other Directives
{: id="20201028111724-13q8c5r"}

### The #undef Directive
{: id="20201028111726-u0ojhog"}

The #undef directive “undefines” a given #define. That is, suppose you have this definition:
`#define LIMIT 400`
{: id="20201028111735-x3kyghs"}

Then the directive
`#undef LIMIT`
{: id="20201028111902-jomdpr1"}

removes that definition. Now, if you like, you can redefine LIMIT so that it has a new value.
Even if LIMIT is not defined in the first place, it is still valid to undefine it. If you want to use a
particular name and you are unsure whether it has been used previously, you can undefine it to
be on the safe side.
{: id="20201028111909-7x2vtu3"}

### Being Defined—The C Preprocessor Perspective
{: id="20201028111859-41y5ugr"}

The preprocessor follows the same rules as C about what constitutes an identifier: An identifier
can consist only of uppercase letters, lowercase letters, digits, and underscore characters, and a
digit cannot be the first character
{: id="20201028143458-a8fjsok"}

### Conditional Compilation
{: id="20201028143515-bbl4and"}

You can use the other directives mentioned to set up conditional compilations. That is, you
can use them to tell the compiler to accept or ignore blocks of information or code according
to conditions at the time of compilation.
{: id="20201028143934-qqcytxg"}

##### The #ifdef, #else, and #endif Directives
{: id="20201028143908-f23no9v"}

```c
#ifdef MAVIS
#include "horse.h" // gets done if MAVIS is #defined
#define STABLES 5
#else
#include "cow.h" // gets done if MAVIS isn't #defined
#define STABLES 15
#endif
```
{: id="20201028144217-e191wt2"}

The #ifdef directive says that if the following identifier (MAVIS) has been defined by the
preprocessor, follow all the directives and compile all the C code up to the next #else or
#endif, whichever comes first. If there is an #else, everything from the #else to the #endif
is done if the identifier isn’t defined.
{: id="20201028143913-xpg08k2"}

```c
#include<stdio.h>

#define JUST_CHEKING
#define LIMIT 4

// #undef JUST_CHEKING

int main() {
    int i;
    int total = 0;
    for (i = 1; i <= LIMIT; i++) {
        total += 2*i*i + 1;
        #ifdef JUST_CHEKING
        printf("i=%d, running total = %d\n", i, total);
        #endif
    }
    printf("Grand total = %d\n", total);
    return 0;
}
```
{: id="20201028143718-avshwer"}

##### The #ifndef Directive
{: id="20201028144912-21hrt84"}

The #ifndef directive can be used with #else and #endif in the same way that #ifdef is.
The #ifndef asks whether the following identifier is not defined; #ifndef is the negative of
#ifdef. This directive is often used to define a constant if it is not already defined. Here’s an
example:
{: id="20201028144948-ajaxtcv"}

```c
/* arrays.h */
#ifndef SIZE
    #define SIZE 100
#endif
```
{: id="20201028144914-nfhwzo0"}

##### The #if and #elif Directives
{: id="20201028144956-xhzmajn"}

The #if directive is more like the regular C if. It is followed by a constant integer expression
that is considered true if nonzero, and you can use C’s relational and logical operators with it:
{: id="20201028145057-9rie0fu"}

```c
#if SYS == 1
  #include "ibm.h"
#endif
```
{: id="20201028145030-1mn5i5f"}

### Predefined Macros
{: id="20201028145345-o1kq0ix"}

```c
#include<stdio.h>

void why_me();

int main() {
    printf("The file is %s.\n", __FILE__); // The file is predef.c.
    printf("The date is %s.\n", __DATE__); // The date is Oct 28 2020.
    printf("The time is %s.\n", __TIME__); // The time is 14:58:59.
    printf("The version is %s.\n", __VERSION__);
    printf("The line is %d.\n", __LINE__);
    printf("The fuction is %s.\n", __func__);
    return 0;
}
```
{: id="20201028151024-5m4z85d"}

{: id="20201028190223-qdh3ugr"}

### Generic Selection (C11)
{: id="20201028145409-kgv1z0h"}

In programming, the term generic programming indicates code that is not specific to a particular type but which, once a type is specified, can be translated into code for that type
{: id="20201028151027-zkisrbl"}

C11 adds a new sort of expression, called a generic selection expression, that
can be used to select a value on the basis of the type of an expression, that is, on whether the
expression type is int, double, or some other type. The generic selection expression is not a
preprocessor statement, but its usual use is a part of a #define macro definition that has some
aspects of generic programming
{: id="20201028151141-2z4kjc2"}

A generic selection expression looks like this: `Generic(x, int: 0, float: 1, double: 2, default: 3)`
{: id="20201028151230-bn6nrap"}

```c
#include<stdio.h>

#define MYTYPE(x) _Generic((x),\
    int: "int",\
    float: "float",\
    double: "double",\
    default: "other"\
)

int main() {
    int d = 5;
    printf("%s\n", MYTYPE(d));          // int
    printf("%s\n", MYTYPE(2.0 * d));    // double
    printf("%s\n", MYTYPE(3L));         // other
    printf("%s\n", MYTYPE(&d));         // other
    return 0;
}
```
{: id="20201028152007-pj92uwz"}

# The C Library
{: id="20201028190221-7b5qh1h"}

{: id="20201028190222-51hv2ja"}
