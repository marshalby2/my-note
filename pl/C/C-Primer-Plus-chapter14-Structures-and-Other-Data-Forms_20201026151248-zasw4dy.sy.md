One of the most important steps in designing a program is choosing a good way to represent
the data. In many cases, a simple variable or even an array is not enough. C takes your ability
to represent data a step further with the C structure variables. The C structure is flexible enough
in its basic form to represent a diversity of data, and it enables you to invent new forms

# Sample Problem: Creating an Inventory of Books

```
#include<stdio.h>
#include<string.h>

char * s_gets(char * st, int n);

#define MAXTITL 41  // maximum length of title + 1
#define MAXAUTL 31  // maximum length of author's name

// structure template: tas is book
struct book {
    char title[MAXTITL];
    char author[MAXTITL];
    float value;
};

int main() {
    struct book library; // declare library as a book variable
    printf("Please enter the book title.\n");
    s_gets(library.title, MAXTITL); // access to the title portion
    printf("Now enter the author.\n");
    s_gets(library.author, MAXAUTL);
    printf("Now enter the value.\n");
    scanf("%f", &library.value);
    printf("%s by %s: $%.2f\n",library.title,
            library.author, library.value);
    printf("%s: \"%s\" ($%.2f)\n", library.author,
            library.title, library.value);
    printf("Done.\n");
    return 0;
}

char * s_gets(char * st, int n) {
    char * ret_val;
    char * find;

    ret_val = fgets(st, n, stdin);
    if (ret_val) {
        find = strchr(st, '\n');    // find for newline
        if (find)                   // if the address is not NULL
            *find = '\0';           // place a null character there
        else {
            while (getchar() != '\n')
                continue;           // dispose of rest of line
        }
    }
    return ret_val;
}
```

### Setting Up the Structure Declaration

```c
struct book {
    char title[MAXTITL];
    char author[MAXTITL];
    float value;
};
```

### Defining a Structure Variable

```c
struct book library;
```

### Initializing a Structure

```c
struct book library = {
        "The Pious Pirate and the Devious Damsel",
        "Renee Vivotte",
        1.95
    };
```

### Pointers to Structures

```
#include<stdio.h>

#define LEN 20

struct names {
    char first[LEN];
    char last[LEN];
};

struct guy {
    struct names handle;
    char favfood[LEN];
    char job[LEN];
    float income;

};

int main() {
    struct guy fellow[2] = {
        {
            {
                "Even", 
                "Villard"
            },
            "grilled salmon",
            "personality coach",
            68112.00

        },
        {
            {
                "Rondeny",
                "Swillbelly"
            },
            "tripe",
            "tabloid editor",
            232400.00
        }
    };

    // printf("&fellow[0].income $%.2f\n", fellow[0].income);
    printf("=========== operation by pointer ===========");
    struct guy * him;   // here is a pointer to a structure
    printf("address #1: %p #2: %p\n", &fellow[0], &fellow[1]);

    him = &fellow[0];
    printf("pointer #1: %p #2: %p\n", him, him + 1);
    printf("him->income is $%.2f: (*him).income is $%.2f\n", him->income, (*him).income);

    him++; // pointer to next structure
    printf("him->favfood is %s:  him->handle.last is %s\n", him->favfood, him->handle.last);

    return 0;
}
```

# Telling Functions About Structures

modern implementations give you a choice between passing structures as arguments and
passing pointers to structures as arguments—or if you are concerned with just part of a structure, you can pass structure members as arguments. We’ll examine all three methods, beginning with passing structure members as arguments

### Passing Structure Members

As long as a structure member is a data type with a single value (that is, an int or one of its
relatives, a char, a float, a double, or a pointer), it can be passed as a function argument to
a function that accepts that particular type

```
#include<stdio.h>

struct square {
    int length;
    int width;
};

int area(int, int);

int main() {
    struct square square = {20, 10};
    // Passing Structure Members
    printf("area : %d\n", area(square.length, square.width)); // area : 200
    return 0;
}

int area(int l, int w) {
    return l * w;
}
```

### Using the Structure Address

We will solve the same problem as before, but this time we will use the address of the structure
as an argument

```
#include<stdio.h>

struct square {
    int length;
    int width;
};

int area(const struct square *); // 

int main() {
    struct square square = {20, 10};
    // pass the pointer to function
    struct square * p = □
    printf("area : %d\n", area(p)); // area : 200
    return 0;
}

int area(const struct square * p) {
    return p->length * p->width;
}
```

### Passing a Structure as an Argument

```
#include<stdio.h>

struct square {
    int length;
    int width;
};

int area(struct square s); // 

int main() {
    struct square square = {20, 10};
    // pass structure to function
    printf("area : %d\n", area(square)); // area : 200
    return 0;
}

int area(struct square s) {
    return s.length * s.width;
}
```

### Structures or Pointer to Structures?

Suppose you have to write a structure-related function. Should you use structure pointers as
arguments, or should you use structure arguments and return values? Each approach has its
strengths and weaknesses.

The two advantages of the pointer argument method are that it works on older as well as newer
C implementations and that it is quick; you just pass a single address. The disadvantage is that
you have less protection for your data. Some operations in the called function could inadvertently affect data in the original structure. However, the ANSI C addition of the const qualifier
solves that problem.

One advantage of passing structures as arguments is that the function works with copies of the original data, which is safer than working with the original data
