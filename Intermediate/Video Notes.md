# Video Notes

### Hello World In C

```c
#include <stdio.h>

int main(void) {
    printf("Hello, World!\n");
    return 0;
}
```

and compile in bash with `gcc hello_world.c -std=c99 -pedantic -Wall -Wextra; ./a.out`

Every function needs a `main()` function which returns the `int` 0 if the program executes correctly and some non-zero value otherwise. `prinf()` is contained in the `stdio.h` header file that comes by default with the c installation. Header files are used to declare things like useful functions. 

We want to use the switches included above to make sure we have all the warnings and make the compiler as verbose as possible. `a.out` is the default name for a compiled c program. 

Comments are started with `//` as well as `/* comment */`

### C Basics

###### Preprocessing, Compiling, and Linking

**Preprocessing:** substitutes the content from lines like `#include` and `#define` into the files.

**Compiler**: Converts the source code into the assembly language. 

**Linking:** Fixes up and chooses final code details required for the code to execute such as determining memory address ranges and combining different files into a single executable.

![image-20210127122024522](C:\Users\benfy\AppData\Roaming\Typora\typora-user-images\image-20210127122024522.png)





###### `printf()`

A function used to print to the terminal. Can be used to print strings, and also to feed variables into the string. 

> `printf("there are %d students in class", 36);`

Valid substitutions:

- d - decimal (integer) [ use ld for long ints]
- u - unsigned (integers that disallow negative values) [lu for long unsigned]
- f - floating point numbers [lf for double]
- c - character
- s - character array

###### Variables

First variable gets its type declared to allocate memory location and then the value is assigned. The value may change but the type may not.

Types:

- Int: signed integer (usually 32 bits)
  - unsigned: only positive integers
  - long: larger ints
- Floating Point:
  - float: single-precision fp
  - double: double-precision fp
- Character:
  - char: holds a 1-byte character, 'A', 'B', 'C'
  - chars are integers that correspond to an ASCII value
- Boolean:
  - 1: true
  - 0: false
    - if you don't want to define custom symbolic constants/vars can `#include <stdbool.h>`

Assignment is done with `=`

> You can declare and assign at the same time
>
> `int num_students = 32;`

 `const int base = 32` is a way to make a variable a constant without defining a symbolic constant. 



###### Operators

- Addition with `+`
- Subtraction with `-`
- Multiplication with `*`
- Division with `/`
  - If passed integers, will perform integer division. One float makes it a float operation
- Modulus with `%`

> Operator Precedence:
>
> ![image-20210127115449089](C:\Users\benfy\AppData\Roaming\Typora\typora-user-images\image-20210127115449089.png)

Multiplication and Division have higher precedence than addition and subtraction. 

Note above, postincrement and preincrement have different precedence.

###### User Input

`scanf()` is another function from `stdio.h`. Usage:

```c
int i;
printf("Please enter an integer: ");
scanf("%d", &i); //YOU HAVE TO USE THE POINTER TO I (for some reason we will see later.)
prinf("the number you entered was %d", i);
```

The output of `scanf` can tell you if the input went correctly. Returns 0 if the input was invalid for the specified type. `EOF`is returned which is generally equal to `-1` if no input was available meaning the end of file was reached.

