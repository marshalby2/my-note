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

{: id="20201028091347-yrccb9w"}

# Other Directives
{: id="20201028111724-13q8c5r"}

###
{: id="20201028111726-u0ojhog"}
