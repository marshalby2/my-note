One of the most important steps in designing a program is choosing a good way to represent
the data. In many cases, a simple variable or even an array is not enough. C takes your ability
to represent data a step further with the C structure variables. The C structure is flexible enough
in its basic form to represent a diversity of data, and it enables you to invent new forms
{: id="20201026214440-jn6cgc1"}

# Sample Problem: Creating an Inventory of Books
{: id="20201026214441-qou7yoq"}

{: id="20201026214521-gtjanzp"}

{: id="20201026214647-dg07u5l"}

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
{: id="20201026214501-xcm150v"}

{: id="20201026214647-t71vju5"}

### Setting Up the Structure Declaration
{: id="20201026214639-2zvn0gp"}

{: id="20201026214645-nmsp044"}
