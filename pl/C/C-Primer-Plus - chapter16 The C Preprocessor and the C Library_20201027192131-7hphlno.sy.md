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

{: id="20201027194028-766hxvy"}

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

{: id="20201027192736-d2wi2hn"}

Each #define line (logical line, that is) has three parts. The first part is the #define directive
itself. The second part is your chosen abbreviation, known as a macro. Some macros, like these
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
