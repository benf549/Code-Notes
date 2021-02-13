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

###### User Input (`printf `and `scanf`)

`scanf()` is another function from `stdio.h`. Usage:

```c
int i;
printf("Please enter an integer: ");
scanf("%d", &i); //YOU HAVE TO USE THE POINTER TO I (for some reason we will see later.)
prinf("the number you entered was %d", i);
```

The output of `scanf` can tell you if the input went correctly. Returns 0 if the input was invalid for the specified type. `EOF`is returned which is generally equal to `-1` if no input was available meaning the end of file was reached. The `scanf` returns the number of successful matches. If you're scanning for 2 matches, a successful scan returns 2

### Git

Main takeaways were put `*.c` and executable files in `.gitignore`. 

### Submitting Files

`zip zipped_files.zip file1.c file2.c file3.c` to bundle files together

`unzip -l zipped_files.zip` to unzip without unpacking (-l)

![image-20210129120910801](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210129120910801.png)

### Logical Operators and Control Flow

These are the operators for Boolean expressions in C.

- `&&` is logical and
- `||` is logical or
- `!` is logical not 

```c
#include <stdio.h>

int main()
{
    int a = 5, b = 5, c = 10, result = 0;
    result = (a == b) && (c > b);
    printf("result equals to %d \n", result); // evals to 1
}
```

###### Decision Statements

```c
if (a) {
    printf("a is true\n");
} else {
    printf("a is false\n");
}
```

```c
switch (integer_expression) {
   	case c1: stmnt1;
  	case c2: stmnt2;
  			 break;
    case c3: 
    case c4: stmnt3;
    		 stmnt4;
    default: stmtlast;
}
```

If switch cases aren't given break statements between cases, the code below until a break or default clause will execute. For example in the above example if `c1` occurs, then `stmnt1` and `stmnt2` will execute. If `c2` occurs, then `stmnt2` will execute. If `c3` or `c4` occur, `stmnt3`, `stmnt4`, and `stmntlast` will execute. 

The switch statement for `c3` and `c4` are essentially creative ways to implement logical or. 

###### Example of Switch statement

```c
int main(){
    char grade = 'B';
    switch (grade) {
        case 'A':
            printf("Excellent\n");
            break;
        case 'B':
        case 'C':
            printf("Well Done\n");
            break;
        case 'D':
            printf("You passed\n");
            break;
        case 'F':
            printf("Better try again\n");
            break;
        default:
            printf("Invalid grade\n");
    }
    printf("Your grade is %c\n", grade);
}
```

Switch statements can only be used with integer statements, but since characters in C are just the ascii placeholders for integers, the switch statement works. 

###### Compound Expressions

Exist and work the same way as in other languages

`c += 1` takes the current value of c and sets c equal to that value +1

Other expressions:

`-=`

`*=`

`/=`

`%=`

######  Increment and Decrement

preincrement vs postincrement:

`++a` increments a by 1 then uses the new value of a in the expression in which a resides

`a++` uses the current value of a, then increments a by 1

The same logic applies to the `--a` and `a--` operators.

pre-incrementing has higher precedence than post-incrementing. 

```c
int main()
{
    int a = 10;
    printf("%d", a++); // Prints 10
}
```

```c
int main()
{
    int a = 10;
    printf("%d", ++a);
}
```

### Looping

There are 3 types of loops in c. There are while loops, do-while loops, and for loops.

The loops have the keywords `break` and `continue`. Using `break` immediately exits the loop. `continue` immediately skips to the next execution of the loop.

###### While Loops

```c
while (boolean_expression) {
    statements;
}
```

A while loop iterates a minimum of 0 times. The loop occurs for as long as the boolean expression is true and never occurs if the boolean expression is not true going into the loop

###### Do-While Loop

```c
do {
    statements;
} while (boolean_expression)
```

A do-while loop will always execute at least once regardless of whether the boolean expression is true going into the loop. After the first execution, the while loop is checked and each subsequent iteration occurs if the boolean expression is true.

###### For Loop

```c
for (initialize; boolean_expression; update) {
    statements;
}
```

In a for loop, an initialization step occurs first setting an index variable to some value. If the boolean expression based on the index variable evaluates to true, the loop executes and after execution, the update expression is applied and the boolean is reevaluated. 



###### While Loop for Reading in Values Until No More Available

```c
#include <stdio.h>

int main(){
    int sum = 0
    int addend;
    while (scanf("%d", &addend) == 1) {
        sum += addend;
    }
    //output the sum
    printf("%d\n", sum);
    return 0;
}
```

When you use `scanf` it will wait patiently for you for inputs. This continues to scan even when you press enter until the End of Input signal is given. To give the end of input signal, press `ctrl+D` (possibly twice)



### Arrays and Ascii

###### Arrays

An array variable is a collection of elements laid out consecutively in memory. All elements are of the same type as declared when the array is initialized. Elements are accessed with `[]` as in python. The actual value of the variable assigned to be an array is the memory address of the array.

`int array[10]` creates an integer array of size 10.

Arrays are zero-indexed like in python. **The last valid index in the array is one less than the size of the array.**

When an array is created, the elements inside the array are not initialized. If you access them before initializing them, you get undefined behavior. To initialize the array, just loop through the indices and set each index to something. 

```c
int c[12]; //initializes with undefined values
for (int i = 0; i < 12; i++){
    c[i] = i; //sets each value to its index.
}
```

Another way to initialize an array is to use curly braces:

```c
int c[5] = {1, 2, 3, 4, 5};
int c[] = {1, 2, 3, 4, 5}; //This is also valid because c can figure out the size of the array from the initialization
```



Using an array within an array:

```c
int data[10] = {2, 1, 1, 1, 2, 0, 1, 2, 1, 0};
int freq[3] = {0, 0, 0}

for (int i = 0; i < 10; i++) {
    freq[data[i]]++; //counts the frequencies of  0, 1, and 2 in the data array.
}
```

If you had a 3 in the data array, you would get an error because `freq` can only count 0, 1, and 2s.



###### Ascii

The Ascii table maps characters to their integer values. 

It is useful to know that uppercase letters come before lowercase letters and that character sets are continuous. 

If you know that `'A' = 65`, you know that `'Z'` must be 26 numbers greater.

The digits come before the letters and most symbols come before the digits.

The char `'0' = 48` in Ascii table. 



Useful character functions can be found in the `#include <ctype.h>` file. 

`isalpha` returns T/F if char is alphanumeric

`isdigit` returns T/F if char is numeric

`islower` checks if the char is lowercase or not

`isspace` checks if the char is whitespace or not

`tolower` converts char to lowercase

`toupper` converts char to uppercase



### Strings

###### Strings in C

In C, there are no strings as types separate from arrays. Strings are simply arrays of `chars`.

The last item in the array must always be the null character `\0`, this is the first character in the ascii table corresponding to 0.

```c
char day[] = "monday"; //initialize a string without specifying length similar to curly braces.
//alternatively
const char *day_ptr = "monday"; //we will perhaps use this later.
char day2[] = {'m', 'o', 'n', 'd', 'a', 'y', '\0'}; //manually setting the array is allowed but must remember null character!
```

Because strings are arrays, indexing is the same as for arrays. 

```c
char str[] = "hello";
//char str_copy[5]; we cannot use an array of length 5, need length 6 to accomodate the null character. 
char str_copy[6];
for (int i = 0; i < 6; i++) {
	str_copy[i] = str[i];
}
printf("%s\n", str); // %s is the string format specifier. 
printf("%s\n", str_copy);
```

You can pass the null terminator into the middle of the string to cleave the subsequent characters. You have to be careful when manually setting the location of the `\0` character.

###### String Methods

Useful functions can be imported by using `#include <string.h>`

`strlen()` returns the number of characters before '\0'

`sizeof()` returns the amount of space in bytes occupied by the variable. Includes the `\0` while `strlen` does not. Regardless of the data in the array will tell you what the array length was defined as. This function works on any type in c and returns the number of bytes that that type is taking. `char` types are only one byte. `int` types are 4 bytes. To calculate the length of a non-char array, you can use `sizeof(array) / sizeof(type)` where type is the variable type like `int`.

Both of the above functions return `%lu` (unsigned long) values so have to be passed into `printf` as such.

`strcmp(s1, s2)` compares the two strings according to character ascii values. Performs a character by character comparison of each array. If the two match it moves to check the next character. If the first mismatched character in s1 is less than its counterpart in s2, returns a negative value. If the first mismatched character in s1 is numerically greater than s2, a positive number is returned. The number returned corresponds to the distance between the mismatched values on the ASCII table. 

`strcpy(s1, s2)` copies s1 to s2 as long as s2 is large enough.

`strcat(s1, s2)` concatenates like string addition in python. 



### File IO

###### Reading and Writing Files

We have worked only with `printf` and `scanf` to do standard input and standard output.

We may want to be able to read and write to files. Especially when we have very larger outputs. 

`fprintf()` and `fscanf()` 

```c
fopen("output.txt", "w") // opens file in writing mode
```

Possible read/write modes are:

 `r` which opens the file for reading

 `r+` which opens the file for reading and writing

 `w` which opens the file for writing

`w+` which opens the file for reading and writing. 

Both w and w+ mode will overwrite a file if it already exists. 

The `fopen()` command returns a `FILE*` which is a pointer to a `FILE` struct

If the file open fails, returns `NULL`

`feof(fileptr)` returns non-zero if we have already read past `EOF`

`ferror(fileptr)` returns non-zero if the file is in an error state. An example of when this would happen is if the file was opened for writing and reading was attempted.

`rewind(fileptr)` returns a file pointer to the beginning of the file. Rewinds the read/write operation to the beginning. 

```c
#include <stdio.h>
int main() {
    FILE* input = fopen("numbers.txt", "r");
    if (input == NULL) {
        printf("Error: could not open input file\n");
        return 1;
    }
    int a = 0, b = 0;
    int numCollected = fscanf(input, "%d%d", &a, &b);
    while (numCollected == 2){
        printf("%d\n", a+b);
        numCollected = fscanf(input, "%d%d", &a, &b);
    }
	if (ferror(input)) {
        printf("Error: error indicator ");
        printf("was set for input file \n");
    	return 2;
    } else if (numCollected != EOF) {
        printf("Error: could not parse line \n");
        return 3;
    }
    
    fclose(in=put);
    return 0;
}

```

Remember to close a file whenever you open one!

###### Standard Streams

The following are considered standard streams. They are the object used by `printf` and `scanf` and are defined in `<stdio.h>`. They do not have to be closed, probably because they are read in before the main function executes but I'm not sure about that. 

`stdin` 

`stdout`

`stderr`

Because these are basically files, we can read from the standard in with `fprintf`

```c
#include <stdio.h>
fprintf(stdout, "Hellow, World\n");
```



### Assertions

`assert(boolean_expression)`

Assertion statements help us to catch bugs as close to the source as possible. 

`#include <assert.h>`

The `boolean_expression` is an expression that should be true if everything is OK. If the boolean_expression is false, the program immediately exits with an error message indicating an assertion has failed. 

Assert is used to create test cases.

Example:

```c
#include <assert.h>
int sum = a*a + b*b;
assert(sum >= 0);

if (isalpha(c)) {
    assert(c >= 'A');
    printf("%d\n", c - 'A');
}
```



Assert statements should not be used for typical error checking. Assert statements should be used for checking that your programming has not introduced an error. 

We want to use return statements with non-zero integers that indicate that the program has returned an error when the error is on the fault of the user. We use assert statements to set up test cases that we want to ensure are correct while editing the code. 

### Math

`#include <math.h>`  gives us access to useful math functions. 

`-lm` must be included when compiling to ensure that the functions work. For example we would then have to call `gcc -Wall -Wextra -pedantic -std=c99 -lm file.c`  this is the link flag that links the `math.h` when compiling our program.

`sqrt()`, `pow(x, y)`, `exp(x)`, `log(x)`, `log10(x)`, `ceil(x)`, `floor(x)`, `sin(x)` 

and more!

The arguments of math functions are doubles, however, you can pass in ints, floats, or doubles.



### Functions

```c
int foo(char c, int i){
    return i;
}
```

To define a function, specify the return type, the name, then its typed arguments in parentheses. When functions communicate with eachother, we use parameters to go into one function and return values to get information out of the function. Another option is to use global variables, but this is a bad practice when programming. 

If you want to have a function that doesn't return anything return type should be void.

```c
void bar(char c){
    printf("%c", c);
}
```

Writing functions allows us to break our larger problem into smaller, more easily solvable subproblems. 

When deciding to write a function, if the function has a clear goal, does not require too many variables to be passed in, and the code has a single result or perhaps a couple results a function is a good call.

###### Pass by Value

When you pass arguments into the function, you are passing a copy of the variable into the function. Reassigning the variable will not change the variable outside of the scope of the function. 

### Command Line Arguments

```c
#include <stdio.h>

int main(int argc, char* argv[]) {
    printf("argc = # arguments + 1: %d\n", argc);
    for (int i = 0, i < argc; i++) {
        printf("argv[%d] = %s\n", i, argv[i]);
    }
    return 0;
}
```

Rather than having void or empty parameters in main, we pass in the `argc` and `argv` parameters. These values are set automatically when the main function is called at execution time. 

The executable's name is always the first index of the `argv` array like the `sys.argv` function in python.

Rather than `char* argv` you could also see `char argv[][]` or `char **argv`. These are all different ways of saying the same thing. 

### Function Declarations

When calling functions, we need to make sure that the function is defined before it is called in the file. 

```c
float func1(){}

int main() {
    func1();
}
```



###### Compilation Step

First the preprocessor reads the file and brings all code and include statements together. Then the compiler takes the source code (human readable) to the machine code. Then the linker connects the include statements. 

If we want to do the implementation of a function after the main function, we can declare first and then do the implementation later.

```c
float func1(int a, int b) //declaration
    
int main() {
    float a = func1(4, 5)
}

float func1(int a, int b) { //implementation
    return (float) a / b
}
```



### Pass By Reference Arrays

When arrays are passed to functions, the pointer to the array is passed so the function has access to change the original array rather than a copy of the array. 

It is useful to pass the length of an array to a function that will need it to loop through it.

What about returning arrays? We actually don't have the tools we need to do this quite yet. You cannot return a pointer to a local variable. To get around this, we can just use the pass-by-reference nature of the array to ensure that the modifications are kept. 



### Recursion

When you need to repeatedly do something. Break a larger problem into repeated smaller subproblems. The function then needs to call itself. 

In C when you call a function, the function call is added to the stack frame. This is an area of memory where variables and temporary values for a function call are stored as well as the return address indicating the code location where the function call will return to once it resolves. Each recursive call  adds to the stack frame and if the recursion does not break, you exceed the size of the call stack.

The size of the call stack is proportional to the size of n.



### Multiple Source Files

To compile  one executable from one source file, we can put information in header files to specify declarations and definitions that different files will need to use. Recall that we just need to tell the program that functions exist before they are called and then the actual implementation can be written in a c file.

When calling a custom header file, we use `#include "functions.h"`

```c
functions.c
__________________
#include "functions.h"

float func1 (int x, float y) {
    return x+y;
}

int func2 (int a) {
    return 2*a;
}

__________________
functions.h
__________________
float func1 (int x, float y);
int func2 (int a);

__________________
mainFile.c
__________________
#include <stdio.h>
#include "functions.h"
int main() {
    printf("%.2f %d", func1(2, 3.0), func2(4));
    return 0;
}
```

Once we have the file structure set up, we can call 

`gcc std=c99 -pedantic -Wall -Wextra mainFile.c functions.c`

and then we can simply call `./a.out` as usual



#### Compiling, Linking and Separate Compilation

Compiling translates `.c` files to `.o` files. 

Linking combines `.o` files into one executable into `a.out`

The linking ensures that if only one compiled file is changed, we don't have to recompile unchanged files. We wouldn't want to call the above `gcc` command every time. 

![image-20210210114910053](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210210114910053.png)

You can use the `gcc -c` flag to specify that you only want to compile that file. Previously compiled files that were not edited do not need to be recompiled. You can first compile the changed file and then link the changed file and unchanged files. 



### Make and Makefile

`make` keeps track of which files were changed and need to be recompiled. Saves time by not having to recompile things unnecessarily. 

Just need to set up a configuration file called a Makefile, then we can carefully specify which files require other files and which commands to use to create them. 

Simply create a makefile. A makefile differentiates between tabs and spaces. We can have different targets which creates different commands that do different things when called. 

```makefile
Makefile:
_________________
CC=gcc
CFLAGS=-std=c99 -pedantic -Wall -Wextra
    
main: mainFile.o functions.o
	$(CC) -o main mainFile.o functions.o

mainFile.o: mainFile.c functions.h
	$(CC) $(CFLAGS) -c mainFile.c

functions.o: functions.c functions.h
	$(CC) $(CFLAGS) -c functions.c

clean:
	rm -f *.o main
```

To use a makefile, we can just run `make functions.o` or `make mainFile.o` or `make`

Just running `make` will run main and all below things.



### Header Guards

When making our own `.h` files, we will include header guards which are used when the header contains definitions. It prevents definition duplications when multiple `.c` files use the same `.h` file. 

```c
rectangle.h
_____________
//include likes like this at the top; change the all-caps name to match the file name, rectangle.h in thic case. 
#ifndef RECTANGLE_H
#define RECTANGLE_H

struct rectangle { //we haven't discussed structs yet in c. 
    int height;
    int width;
};

// include this line at the bottom. 
#endif
```

Doing this ensures that if you have a main that includes `a.h and b.h` and in `a.h` you include `b.h` then technically, you have already included `b.h` from main.



### `sizeof`

A default function that returns the size of a type in bytes. 

A char is one byte, an int is 4 bytes, a float is 4 bytes, and a double is 8 bytes

`sizeof(a)/sizeof(type_of_a)` gives the length of an array of a types.



### Multidimensional Arrays

C arrays are really easy to turn into matrices.

`int arr[10][10]` creates a 10x10 matrix. The first bracket is number of rows, the second bracket is the number of columns.

`int table[2][4] = { {1,2,3,4}, {5,6,7,8}}` These arrays are laid out as one continuous block of memory. When you want to access a value in the array, you index with `table[i][j]`

We can write functions that handle multidimensional arrays but as with regular arrays, we get passed the pointer to the array, so we need to pass one or both array sizes in with the function parameter. 

```c
void sum_matrix(int list[][4], int numRows);
```



### GDB

Stands for GNU debugger. This is helpful for identifying bugs in our code. Helps us run the program in a way that allows us to flexibly pause and resume the code, print out value in the middle of execution, and see where errors like `segmentation faults` are occuring. 

When using `gdb`, compile the program with `-g`. This flag includes the source code in the executable for GDB to read. 

To run call `gdb ./executable`

Within gdb, `break main` sets a break point at the main function. then `run` will progress the program by one line. We can then use `next` to execute one like at a time. If you use `step` rather than `next`, `gdb` will step inside the function. `print var` will print the value of a variable

`n` is an abbreviation for next

`p` is an abbreviation for print

