# C Notes

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
    
    fclose(input);
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
float func1(int a, int b); //declaration
    
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



### Pointer Basics

Suppose we want to mutate the actual values of arguments of functions. We can use pointers to make the parameters of a function pass by reference. To understand this, we need to talk about execution stacks and stack frames (activation record). Variables declared in a function are in memory in the stack. When a function is called, a new stack frame is made and put on top of the stack in memory with all local variables copied. Subsequent function calls get added on top of the stack. Once a function returns the return value is passed into the frame below it, and the stack gradually collapses until main finishes executing. 

Local variables are lost when the stack frame is collapsed. By using pointers, we can pass variables between stack frames. 

A pointer is a variable that can store a memory address. Every pointer has a specified data type that it points to. To declare add an asterisk in front of the variable name as in `*p`. To assign a pointer of something else, we use the address of operator `&x` which returns the address of x. The dereferencing operator `*p` returns the value at that memory location. 

```c
int x = 1;
int y = 2;

int *ip; //Initialize pointer called ip

ip = &x; //point ip to x.

y = *ip; //sets y to the value contained at the location of x.

*ip=0; //sets the location containing x to zero (sets x to zero)
```

To improve the swap function to actually change the variables around:

```c
void swap(int *px, int *py) {
    int temp;
    temp = *px; //set temp to value held in x
    *px = *py; //set x to value held in y
    *py = temp;  //copy value held in temp to value at y address.
}
```

`*ip` can do anything that the normal variable can. The pointer operators have 'unary operator precedence'. You want to be careful with incrementation because `*ip++` will first increment the memory address and then will get the value at that address which probably isn't what you want. Rather, we want to write `(*ip)++` to ensure that we first get the value at `ip` and increment that. 

### Dynamic Memory Allocation

When we define a 2D array, the memory is allocated in one large block. The first row followed by the second followed by the third and so on. 

There is a way to write a function that returns an array. The problem with this is that anything defined in the function is local. Once the function is exited, you lose access to those variable from that stack frame. Furthermore, declaring arrays that are too large will run out of memory. 

Dynamic allocation allows us to get around these limitations. We no longer define our variable on the stack as we have been doing. We can do things on the 'heap' which is a lot larger than the stack. Defining a variable on the heap is also persistent between stack frames. The problem with doing this is that we need to collect our garbage-we need to de-allocate that memory or else we cause a memory leak. 

We use the `malloc()` function to allocate memory. 

```c
int main(){
    int *ip = malloc(sizeof(int)); //define an integer pointer that points to memory for one int
    if (ip == NULL){
        return 1; //an error occurred (maybe size was too large.)
    } else {
     	return 0;   
    }
}
```

We can also use `malloc` to allocate memory for arrays like this:

```c
int main() {
    int n = 35;
    int *a = malloc(sizeof(int) * n); //define array for 35 integers on heap.
}
```

the array can then be indexed as normal. 

To deallocate memory once we no longer need it, we use the `free` command. We call it on the pointer that we defined earlier. 

```c
int main(){
    int *ip = malloc(sizeof(int)); //define an integer pointer that points to memory for one int
    if (ip == NULL){
        free(ip)
        return 1; //an error occurred (maybe size was too large.)
    } else {
        free(ip)
        ip = NULL
        return 0;   
    }
}
```

Allocation and deallocation of memory do not have to occur in the same function. They can occur wherever dynamically but you NEED to free allocated memory to avoid memory leaks. 

```c
int* createArray(int size) {
    int *a malloc(sizeof(int)*size); //put the array on the heap
    if (a == null) {return NULL} //if it doesnt work return nothing
    //You want to also initialize the array to some values here. 
    return a;
}

int main() {
    int *list = createArray(10); //call to function that returns a pointer must store a pointer
    if (!list) {return -1;} //check error
    for (int i = 0; i < 10; i++){
        printf("%d ", list[i]); //print array contents (uninitialized at the moment)
    }
    free(list); //FREE THAT MEMORY
    list = NULL; //This is unnecessary because the program is ending, but it's a best practice. 
	return 0;
}
```

More functions for dynamic memory allocation:

`realloc` if you want to resize an area of memory. It may move the initial memory address elsewhere so you need to handle this. Needs to keep everything continuous. `realloc(prev_pointer, sizeof(int)*100)` 

`calloc` is similar to `malloc`, but it initializes all bits to 0 which is pretty useful! `calloc(10, sizeof(int))` will initialize all the bits for 10 integers worth of memory to zero and return the pointer to that array. 

### Valgrind

A debugging tool that helps find memory related issues like leaks, invalid reads. Again, need the `gcc -g` flag like gdb. To use valgrind we run:

`valgrind --leak-check=full ./myFile <arg1> <arg2> ...`

first thing to look at is **error summary**. Then if 'all heap blocks were freed'. Helps find memory leaks, invalid writes and reads. 



### Pointer Arithmetic

There are four different things you can do with pointers. There are operations on pointers, there is pointer arithmetic for arrays, and string operations, and a special subtraction operations. 

#### Pointer Assignment

When you assign a pointer to another pointer of the same type, only the memory address held in ptr2 is copied. They reference the same memory location. 

`ptr1 = ptr2;` results in the two pointers referring to the same unnamed memory location. If you were to then do `*ptr1 = 10;` then `*ptr2 = 10` as well. 

#### Pointer Comparison

We can compare pointers to see if they point to the same memory address as in `ptr1 == ptr2` and `ptr1 != ptr2`. We can check if a pointer is assigned with the `NULL` keyword. `ptr == NULL` will check if `ptr` is set to zero which is a good value to initialize pointers to. 

We can also use pointer comparison with `ptr < ptr2` which compares the locations in memory which can be useful for when you have an array and want to see where in it an item is. 

#### Pointer Arithmetic

Operators `-, +, +=, and -=` can all be used to manipulate pointers. You can subtract two pointers or add/subtract integers to pointers. This is most useful for pointers to arrays. Rather than adding that integer to the address, it adds that number times how many bytes each element takes up. So, we don't need to multiply by the `sizeof` operator. C will automatically move us the base data type's byte size. This is just a different way to index arrays. 

`a[10]` is really just 10 data types past the address of `a[0]`. Writing `a[0]` is actually the same as writing `&a[0]`. 

Similarly, writing `a[3]=20` is the same thing as writing `*(a+3) = 20` puts the value 20 at the memory address offset three from pointer to the start of the array. 

#### Pointer Difference

Use a special type to hold the difference between pointers. This type is `ptrdiff_t` which is defined in the `stddef.h` file. Essentially just works as a long int. 

Pointer difference can be used to find the size of an array if you know the first and last element. 



```c
char string[] = "hello"
char* ptr = string;
ptr += 3;
printf("%s\n", ptr);
// prints 'lo'
```

Using pointers can process substrings. 

#### Common Arithmetic Errors

```c
char str1[] = "original";
char * str2;
```

If you try to use `strcpy(str2, str1)`, you will get an error because no memory was allocated for `str2`. For this to work we would have to do `str2 = malloc(strlen(str1)+1);`

`str1 += 3` will not work because we cannot change the address stored in a statically declared array variable. You can't change the pointer to the first element because this would lose values.

`str2 = str1` only copies the memory address stored in str1 not the whole array. This just points str2 to where the array is but since str2 is not an array and is a pointer, the assignment is just a pointer. 

### Dynamically Declared Arrays, `Const` Pointers

Arrays are laid out in memory by row. First the entire row, then the next row. Because the array is stored in memory this way, we can use pointer arithmetic to get to different array locations without double indexing. 

#### Dynamically Allocating a 2D array

If we know we want 5 rows by 2 elements, we could just allocate a length 10 array. 

Another approach we could do would be to allocate an array of pointers to pointers. 

```c
int **a = malloc(sizeof(int*) * num_rows);

for (int i = 0; i < num_rows; i++) {
    a[i] = malloc(sizeof(int) * num_cols);
}

a[2][1] = 17; //this works

for (int i = 0; i < num_rows; i++) {
    free(a[i]);
}
free(a); //need to free both allocated indices and the memory allocated for the indices.
```

Essentially what this is doing is that we are allocating 3 integer blocks per index in a. Interestingly, this probably won't allocate each block sequentially but indexing like a normal array still works! We have to be conscious of freeing each of the indices and the array to those pointers as well.

Regardless of whether the array is statically allocated or dynamically allocated, we can use rows of 2D arrays as one dimensional arrays. 

It is possible to dynamically allocate rows for a 2D array that are not all the same length. This is probably not that useful. This would be considered a non-uniform or jagged 2D array. Could be useful to create a parallel array that holds the lengths of each row to index to keep track if you ever need to do this. 

#### `const` keyword

We can use the type modifier `const` to make the variable non-modifiable. When working with constant variables, and passing them to functions, the variable parameter must also be defined as a constant type as well. 

`const int * pointer` protects the thing the pointer points to (mutable pointer)

Using `const` with pointers. What gets stored in the pointer is not allowed to be changed but the pointer itself can be changed. Once the value that the pointer points to is assigned, it cannot be changed at that memory address. You CAN reassign the pointer to another value. 

`int * const pointer` makes it so that the pointer cannot be changed but the contents inside the array can be. The address must be set at declaration time if you want this to be useful or could be in the parameter of a function declaration. Prevents assignments that would change the address stored in the pointer. 

`const int * const pointer` would make the address of the pointer and the value at that memory immutable. 

### Lifetime/Scope

The lifetime of a variable is the period of time in which a variable is alive in memory. The scope is the blocks of code that the variable is accessible. Local variables' lifetimes begin when we enter a function and end when we exit a function. Local variables are allowed out of scope when we pass them as arguments to other functions. 

A variable can be in scope and temporarily hidden when an inner scope declares a variable with the same name.

```c
int main() {
    int i = 12;
    for (int i = 0; i < 10; i++)
        printf("%d", i);
    printf("%d", i);
}
```

#### Static Variables

declared using the static keyword. Have scope similar to local variables, but have a longer lifetime. They are automatically created and initialized to zero but are not destroyed at the end of a block of code. The next time that same block of code is executed, the value of the variable is retained. 

```c
int addInt(int x, int y) {
    static result;
    result += x + y;
    return result
}

int main() {
    printf("add %d + %d = %d", 3, 4, addInt(3, 4)); //returns 7
    printf("add %d + %d = %d", 3, 4, addInt(3, 4)); //returns 14
 	return 0;
}
```

#### Global Variables

Automatically created when the function is begins executing. If can be accessed within any function in a file. They have universal scope. We don't allow global variables because they make the debugging process much harder than it needs to be. 

#### Storage

Static and Global variables live in the Data Segment which his a region of memory that is filled when the program executes. 

### Structure Data Type

In C a `struct` is a bunch of variables grouped together in one bundled variable. We don't have classes in C so we cannot have functions associated with `structs` we can only have values. 

```c
struct checkers_piece {
    int x;
    int y;
    int black;
};

int main() {
    struct date {
        int year;
        int month;
        int day;
    };
    
    struct date purchase_date;
}
```

`sizeof()` a struct is the sum of the size of its fields. When you pass an array into a function, it decays into a pointer and `sizeof ` will return the size of an address. Passing the struct as a wrapper around arrays will make copies of the arrays making them pass by value and the `sizeof` operator will accurately get the size of the array.

The size of the struct might be bigger than the size of its fields. Sometimes the C compiler will add padding between its fields. This may happen when you have attributes with different types. 

`struct`s can be passed in as parameters and returned as return types. 

`struct`s are **pass by value** so we need to return a struct changed in a function or take in the pointer to the struct and make changes to that. 

There is a special operator that combines dereferencing with the `.` operator. This is useful when we pass a pointer to a struct as a function argument. To use this we can replace `(*date).day` with `date->day` we are incentivized to use pointers as struct parameters as we can make changes anywhere in the program that has access to the struct. If we have the structs in the struct, updates will propagate throughout.

You can also type an array to hold structs. To assign values to each item of the array just index and use the `.` operator to access each value. 

You can also have arrays inside structs. 

#### `typedef`

If we don't want to keep writing the struct keyword when using a lot of structs

```c
typedef struct {
	float amount;
	char cc_number[16];
} cc_receipt;

cc_receipt hello; //don't have to prefix with struct anymore. 
```

#### Nested Structures

```c
typedef struct {
    struct {
        int r;
        int g;
        int b;
    } color;
    struct  {
        int x;
        int y;
    } position;
} pixel;

int main() {
    pixel p;
    p.color.r = p.color.g = p.color.b = 255;
    p.position.x = 40;
    p.position.y = 50;
    printf("[%d, %d. %d] at (%d, %d)\n", p.color.r, 
           p.color.g, p.color.b, p.position.x, p.position.y);
    return 0;
}
```

In the above example, we don't name the sub-structs, they are created only when defining the color and position names. 

### Random Numbers

In C, `rand()` will return a value between 0 and RAND_MAX in the uniform distribution. 

We can seed the random number generator with the `srand(unsigned int)` function. If `srand` is not specified, the program runs `srand(1)`. If you want a unique sequence of random numbers every time the function is run, we can pass the function the epoch time: `srand(time(0))` after `#include <time.h>`

This will create a new random number sequence as long as the program isn't being called more than once per second. 

We can use the modulus operator to constrain the values of the modulus operator and we can also shift the values with subtraction once we constrain the values:

![image-20210222121905492](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210222121905492.png)

We can generate floating point numbers with the following code:

```c
((rand() % 100000) / 100000.0) // which generates an inclusive range from 0.0 to 0.99999
((rand() % 100001) / 100000.0) //which generates from 0.0 to 1
```

Increasing the integer and float being modulo-d increases the resolution of the random numbers. The hard maximum of the random number resolution (granularity) from zero to one is

```c
rand() / (double) (RAND_MAX - 1)
```

### Binary File I/O

Working with the bits and bytes directly rather than text. Anything that isn't a text file is a binary file. Storing data in binary is much more efficient than storing them in text format.

To store `255` as text, it is treated as 2, 5, and 5 as characters and thus takes 3 bytes. If we convert it to binary, it can be represented as only one byte.

To read and write to binary files:

```c
FILE *fp = fopen("data.dat", "rb"); //opens the file in binary read mode
fread(where_to, size_of_elements, num_elements, fp); //first is an array to store values, second is size of elements, third self ex. 
fwrite(where_from, size_of_elements, num_elements, fp);
```

for example:

```c
int main(){
    int SIZE = 100;
    int arr_write[SIZE];
    for (int i = 0; i < SIZE; i ++)
	    arr_write[i] = i * 10;
    File *fp = fopen("data.dat", "wb");
    fwrite(arr_write, sizeof(arr_write[0]), SIZE, fp);
    fclose(fp);
    
    int arr_read[SIZE];
    fp = fopen("data.dat", "rb");
   	int num_of_ints = fread(arr_read, sizeof(arr_Read[0]), SIZE, fp);
    
    for (int i = 0; i < 100; i++){
        printf("arr_read[%d] = %d\n", i, arr_read[i]);
    }
    fcose(fp);
}
```

### Bitwise Operations

Manipulates values at the bit levels in binary. Syntax is single operator rather than double operator. 

#### AND Operator

AND between two bits is done with one ampersand: 

`12 = 00001100`

`25 = 00011001`

`12 & 25 = 00001000 = 8` which is the value when each bit is compared and only set to 1 when they are  both 1

#### OR Operator

Performs logical or across all bits as AND

`12 = 00001100`

`25 = 00011001`

`12 | 25 = 00011101 = 29` which is the logical or of each bit compared. 

#### Bit Shifting

`x << n` shifts the bits of x to the left N positions. N 0s are shifted in at the right hand side and N bits fall off the left hand side

`25 = 00011001`

The bitwise shift of `25 << 5` introduces 5 zeros on the right:

`25 << 5 = 1100100000 = 800`

When you shift bits to the left you are basically multiplying the number by two. For example, shifting 25 to the left 5 bits, results in 2^5^ * 25 = 800

`x >> n` shifts the bits of x to the right N positions analogously

This is essentially (floor) division by powers of 2: 

`25 = 00011001`

`25 >> 4 = 00000001 = 1` which is the same as doing floor(25/2^4^)

#### Convert an Integer to its Binary Representation in A String

```c
int num = 53;
char bin_str[33] = {'\0'}; //make a 32 bit string with every position null
int tmp = num;
for (int i = 0; i < 32; i++) {
    if ((tmp & 1) != 0){ //check if rightmost bit is 1 or zero.
        bin_str[31 - i] = '1';
    } else {
        bin_str[31 - i] = '0'
    }
    tmp >>=1; // shift right by 1
}
printf("%d in binary is %s\n", num, bin_str);
```

#### Other Operators

There is also `^` for XOR and `~` which flips every bit in the number from 0 to 1 and 1 to 0.

### Number Representation and Type Casting

Integers in C use the two's complement system to represent a signed value. To be able to represent both negative and positive value, we have 4 bits:

All positive numbers have the fourth bit equal to zero. All negative numbers have the fourth bit equal to 1. 

When you flip the bits and add 1, you convert the number to its negative/positive inverse. 

When a four bit integer over flows such as adding 1 to 0111 we get 1000 which would be -8. This wraps around to the integers. One plus the largest maximum value gives the minimum maximum value. 

Floats on the other hand have an expensive conversion as they have bits that hold the sign, the mantissa, and the value. 

#### Type Conversion

When you write an integer, the type is determined based on its value. When a number is too big for an integer, you should assign it to a long which has more associated bits.

Any floating point number is by default a double, not a float (4 bytes). A double has (8 bytes) and greater precision. If you specifically want to denote a float number you have to specify with a trailing f: `float a =  3.14f`

You can also use scientific notation for very small numbers such as in `double b = -1.1e-12`

Floats and doubles can also be overflown. The compiler will issue an error and the type is set to inf. 

Type conversions happen automatically behind the scenes in C sometimes. There are two important terms: promotion and narrowing. Promoting is going from a smaller to a type value to a larger one like setting a float equal to an integer. Promoting raises the lower type to the same type as the other number/expected type. Narrowing is going from a larger type to a smaller type such as setting an int variable with a float. Narrowing generally chops off whatever extra bits are left after the conversion. 

Remember that dividing two integers only performs integer division. If you want a float, you need to cast one of the numbers to a float or double.

When narrowing conversions are applied, no compiler warnings are thrown.

Passing a float as a parameter to a function that has type int will not throw any errors. The decimal just gets truncated.

When printing, you may get compiler warnings if what you're expecting to print is not the type you pass printf. Things like floats cannot be used as array indices. 

##### Type Hierarchy

> char < int < unsigned < long < float < double

The best practice is to cast the type of the input to the desired output. It is better to have explicit control of the type rather than leaving it up to hierarchy. Same as using parentheses in complicated operations. 

### Linked Lists

A data structure that we can use to store variables of some type. Comparable to arrays but has different pros and cons. Each element in a linked list can be stored in a different location in memory. Rather than one contiguous block of memory like in an array. The linked list is better for enormous arrays. However, indexing them is harder because you cant just look one integer down. 

Called a linked list because each node in the list has an associated pointer to the next item. This is an added price because the list must store the value and the pointer while an array only has to store the value. 

A linked list takes more memory in total but it is more flexible. 

Each linked list has a starting node and a final node. The last node's pointer will point to NULL so we know it is the last node. The head is a pointer to a node which happens to be the first node in the list.

Unlike an array, you cant use pointer arithmetic to jump to another element. In a linked list, you have to follow the pointers until you find your desired element of the null pointer. 

![image-20210301114106897](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210301114106897.png)

if you need to access the elements of the list frequently, you might want to use an array rather than a linked list because if you have a million elements to get to the last one, you have to traverse every single element to get there.

Linked lists have the potential to be dynamic though because you can delete an element by reassigning the previous nodes' pointers.

Linked lists are really good tools for practicing pointers and dynamic memory allocation. 

#### Example Implementation

```c
typedef struct _node {
    char data;	//this could be any type
    struct _node * next; //every node contains a reference to another node
} Node;

Node * create_node (char ch) {
    Node * node = (Node *) malloc(sizeof(Node));
    node -> data = ch;
    node -> next = NULL;
    return node;
}

void print(const Node * cur){
    //traverse list until you hit null printing value at each node.
}

void length(const Node * cur) {
    //advvance node by node through the list and increment a counter on each new node.
}

void add_after(Node * node, char val) {
    //create a new node, hold previous node's pointer and set to self pointer, then point previous node to new node. 
}
```

### Linked List Advanced Operations

Here are some common operations that you might want to use linked lists:

clear - deallocates all nodes in the list and sets the head pointer to null

add_front - add a new node in front of the head pointer. 

clear_list - free all nodes

remove_after - removes all nodes after a given node.

remove_front - removes all nodes before a given node.

remove_all - remove all occurrences of a given data value.



Some of these operations might require reassigning the head pointer on the stack. If you want to do this inside a function, you'd have to pass the function the pointer to the pointer that holds the address of the first element of  the linked list (the head). So, this is an application of a double pointer. 

Like other data types, pointers are also pass by value. So if we want to change the value in the pointer, we need to pass the function the address at which the pointer resides. 

```c
void add_front(Node ** list_ptr, char val) {
    Node * n = create_node(val);
    n->next = *list_ptr; //new node gets next address of current first node
    *list_ptr = n; //head pointer gets address of new node.
}
```



# C++ Notes

### Introduction  to C++

C++ is not a superset of C, it is actually a completely different language but there is interplay between the two. Unlike C, C++ supports object oriented programming so this half of the class focuses on that more

###### Types

int, char, float, double, pointer, bool are all default

Operators, number properties, arrays, pointers, etc work the same as in   c.

Control structures: if/else, switch/case, for, while, do/while all work the same as in C

Functions are pass by value and can be made pass by address with pointers. 

There is an analogous stack, heap, scope, and lifetime of variables.

Structs are similar with slight modifications to be more object oriented. 

###### Tools

`git`, `make`, `gdb`, and `valgrind `also work with C++ file execution.

###### Hello World

```c++
#include <iostream>

using std::cout;
using std::endl;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

and compile with `g++ std=c++11 -pedantic -Wall -Wextra -c hello_world.cpp` followed by `g++ hello_world.o -o hello_world`

Again we edit our source code, preprocess, compile, link,  and execute our code.  

Notice that default header files do not get the `.h` extension. If we define our own header files we do it the same as in C.

Command line arguments are the same as well:

```c++
#include <iostream>
#include <cassert> //assert - c modules can be imported usually with a c prefix

using std::cout; //this syntax declares cout as an alias for std::cout
using std::endl;

int main(int argc, char **argv) {
    assert(argc > 1);
    cout << "Hello " << argv[1] << "!" <<  endl;
    return 0;
}
```

###### Namespaces

If two things had the same name in C, we would get errors during compilation and sometimes undefined behavior. In C++, items with the same name can be safely placed in namespaces that distinguish them. This is like modules in python. 

`using std::cout;` imports the fully qualified name `std::cout;` as `cout`

You should **never** use the `using` keyword in a header file, only in `.cpp` files as files that import that header might not know the default namespace has been changed. Also never do this `using namespace std` this is like importing an entire python module.

###### Text I/O

As we saw, the most basic form of I/O is done with:

```c++
cout << "Hello world!" << endl;
```

where `cout` is the standard output, and `<<` is the insert operator so it inserts the thing to the left into the thing to the right. You can chain inserts together to build up  complex statements. Notice, when doing this, we don't need to specify a format specifier like in printf. The program just prints whatever is is passed. 

The `<<` operator is also the bit shift operator. C++ looks at the operands to decide if you want to bit shift. Both operands would have to be integers.

You can use `printf` by `#include <cstdio>` which imports the standard IO library from `C`

If we want to collect input, we can use `cin`

```c++
#include <iostream>
#include <string> //there is a library for strings

using std::cout;
using std::cin;
using std::endl;
using std::string; //define strings from the std namespace

int main() {
    cout << "please enter your first name: ";
    string name; //string now works as a type
    cin >> name;
    cout << "Hello, " << name << "!" << endl;
    return 0;
}
```

where `>>` is the extraction operator in `c++`

The way `cin >>` works is by reading a word at a time where each word is defined as characters separated by white space. 

```c++
#include <iostream>
#include <string>

using std::cout;
using std::cin;
using std::endl;
using std::string;

int main() {
    //prints the word that is alphabetically smallest
    string word, smallest;
    while(cin >> word) {
        if (smallest.empty() || word < smallest) { //types now have methods!
            smallest = word;
        }
    }
    cout << smallest << endl;
    return 0;
}
```

Relational operators work with strings because they have been overloaded to be defined for string comparison.

```c++
#include <iostream>
#include <cctype>

using std::cout;
using std::cin;
using std::endl;

int main() {
    //converts input string to uppercase.
    char ch;
    while(cin.get(ch)) {
        ch = toupper(ch);
		cout << ch;
    }
    cout << endl;
    return 0;
}
```



### Strings

In C, strings are null-terminated arrays of characters. In C++, strings are objects and behave more like they do in java and python. 

To use them we `#include <string>` and use `using std::string` to alias the string type.

```c++
string s1 = "world"; //same as C
string s2("hello"); //calls the string constructor (more later)
string s3(3, "a"); //replicates "a" 3 times
string s4; //empty string
string s5(s2); //copies s2 into s5.
```

When strings are defined, they are defined on the heap by C++ automatically. Therefore, strings can be arbitrarily long. 

```c++
s = "wow"; //assign string
cin >> s; //put a single whitespace delimited word into s
cout << s; //write s to std out
getline(cin, s); //read to end of line from standard in and store in s
s1 = s2; //copy contents of s2 into s1
s3 = s1 + s2; //concatenates s1 with s2
s1 += s2; // concatenates s2 to s1
== != < > <= >= //the relational operators are all valid to work with strings
```

###### Methods

`s.size()` prints the number of characters in the string. returns an unsigned int called `size_t`

`s.capacity()` returns the number of bytes allocated for the string

`s.substr(offset, howmany)` gives a substring starting at offset for `howmany` characters

`s.c_str()` returns a c-style array of characters. You can then use C library functions like `strlen` on this as a normal character array.

`s.at(5)` returns the 6^th^ element of the string, but unlike `s[5]` does a bounds check to ensure that the address is not out of bounds!

### STL - Standard Template Library

It is a built-in library of useful data structures and algorithms in C++. 

Composed of iterators, containers, and algorithms. Allows us to avoid reinventing the wheel every time we want to implement something. For example, sorting algorithms, stacks, linked lists, etc are all built in.  

A template is the way of writing an object or function such that they can work with any type. Defining a template is simultaneously defining a family of related objects/functions. 

```c++
template<typename T>
struct Node {
    T payload; //'T' is placeholder for type, want a generic linked list with any type
    Node *next;
}

template<typename T>
void print_list(Node<T> * head) {
    Node<T> * cur = head;
    while (cur != NULL) {
        cout << cur->payload << " ";
        cur = cur->next;
    }
    cout << endl;
}
```

now we have one node struct that works for any type T and a corresponding print function that also works for any node type. The generic type convention is to name it a single capital letter. 

To create an instance of the newly defined generic type we use angle brackets to specify what type we want to use

```c++
int main() {
    Node<float> f3 = {95.1f, NULL};
    Node<float> f2 = {48.7f, &f3};
    Node<float> f1 = {24.3f, &f2};
    print_list(&f1);
    
    Node<int> i2 = {239, NULL};
    Node<int> i1 = {114, &i2};
    print_list(&i1);
    return 0;
}
```

There are also common built in types in c++:

```c++
vector<std::string>;
vector<float>;
map<std::string, int>;
```

a vector takes a generic type like we defined above, a map requires two type variables. 

`array` - fixed length array.

`vector` - dynamically-sized array.

`set` - mathematical set where elements may only appear once

`list` - a linked list

`map` - associative list or dictionary

`stack` - last-in first out data structure (LIFO)

`deque` - double-ended queue, flexible combo of LIFO/FIFO

If you want to use a vector, you have to include it into your code. Again, a vector is an array that automatically grows and shrinks as you use more or less room. It is indexed with brackets and allocation, deallocation, resizing etc is all handled by C++. Similar to lists in python.

`#include <vector>` is needed to use it and once you have it imported, the name vector belongs to the standard name space so you need to alias it with `std::vector<char>`

To declare a vector: 

```c++
using std::vector;
vector<std::string> names;
```

To add elements to the back of the vector:

```c++
names.push_back("Alex Hamilton");
names.push_back("Ben Franklin");
names.push_back("George Washingon");
```

To print the number of items in a vector, first and last items:

```c++
cout <<  "Size =" << names.size() << ", first =" << names.front()
    << ", last = " << names.back() << endl;
```

To print every item in a vector wit indexing:

```c++
for (size_t i = 0; i < names.size(); i++) {
    cout << names[i] << endl;
}
```

To print every item in a vector with an *iterator*

```c++
for(vector<string>::iterator  it = names.begin();  it  != names.end(); ++it) {
    cout  << *it  << endl;
}
```

where **an iterator is sort of like a pointer** where it points to each element in the vector and can be incremented and dereferenced like a pointer.

To print every item in reverse order with a reverse iterator:

```c++
for (vector<string>::reverse_iterator it = names.rbegin(); it != names.rend(); ++it) {
    cout << *it << endl;
}
```

this is **a reason why we cant say that iterators are literally pointers because the incrementation works backwards in this case**. The operator is overloaded to give the desired effect. 

### Maps

Maps are like dictionaries in python. They are collections of key-value pairs. The value may be of any arbitrary type. The key must be a type that can be used for binary comparison like all numeric types, char, `std::string` and more.

```c++
#include <map>
#include <iostream>
#include <string>

using std::map;
using std::string;
using std::endl;

int main() {
    map<int, string> id_to_name;

    const int k = 92394;
    id_to_name[k] = "Alex Hamilton";
    id_to_name[k] = "George Washington";
    cout << "Key=" << k << ", Value=" << id_to_name[k] << endl;
    return 0;
}
```

One to one: One key relates to only one value and reassignment occurs if you reindex. 

`mapname.size()` gives the number of keys in the map

To check if a map contains a given key we can do this:

```c++
if (id_to_name.find(92394) != id_to_name.end()) {
    cout << "Found it" << endl;
} else {
    cout << "Did't Find it" << endl;
}
```

which if find does not succeed, it returns an iterator to one past the last element of the map which is the `.end()` iterator. We can check if this was returned and handle the error appropriately.

To visit all of the elements of a map, we can use an iterator like we could with arrays:

```c++
for(map<int, string>::iterator it = id_to_name.begin(); it != id_to_name.end();  ++it) {
    cout << " " << it->first << ": " << it->second << endl;
}
```

where `it->first` gives you access to the key while `it->second` gives you access to the value.

This is because when you dereference a map iterator, you get a `pair` type which contains  `first` and `second` elements. 

Maps do not preserve order they were inputted, the iterator sorts the elements in the map by the keys.

###### Pairs and Returning Multiple Values

We can have functions return two values a few different ways. We could pass pointers to the function that we dereference and set to the return values of the function call:

```c++
void divmod(int a, int b, int *quo, int *rem)  {
    *quo = a/b;
    *rem = a%b;
}
```

Another way would be to define a struct that is designed to contain the functions return type:

```c++
using std::cout; std::endl;

struct quo_rem {
    int quotient;
    int remainder;
};

quo_rem divmod(int a, int b) {
    quo_rem result = {a/b, a%b};
    return result;
}

int main() {
    cout << divmod(10, 0).quotient << endl;
    cout << divmod(10, 0).remainder << endl;
    return 0;
}
```

notice you don't have to repeatedly use the struct keyword to instantiate a `quo_rem`

The STL solution would be to use a **pair** which allows us to return the two items at the same time very simply:

```c++
#include <iostream>
#include <utility> //includes pair and make pair.

using std::pait;
using std::make_pair;
using std::cout;
using std::endl;

pair<int, int> divmod(int a, int b) {
    return make_pair(a/b, a%b);
}

int main() {
    pair<int, int> test = divmod(10, 5);
	cout << "first: " << test->first << endl;
    cout << "second: " << test->second << endl;
    return 0;
}
```

Pair types can be compared with pairwise operators such as in `make_pair(2, 3) < make_pair(3, 2)` is true because it first checks first elements and then checks second elements. 

###### typedef for STL Containers

When using things like iterators, we can end up needing to repeatedly use really long/complicated expressions. The `typedef` operator lets us avoid rewriting things and reduce clutter. 

```c++ 
typedef map<int, string> TMap; //define the map type as TMap
typedef TMap::iterator TMapItr; //define TMap iterator as TMapItr
```

For example  we can save space by using this in the following example:

```c++
typedef vector<int>::iterator TItr;

void prefix_sum(TItr begin, TItr end) { // takes in the start and end iterators
    int sum=0;
    for(TItr it = begin; it != end; ++it) { //loop through value range
        *it += sum;
        sum += *it;
    }
}
```

this example calculates the "prefix sum" which seems to work like a cumulative sum.

A `const_iterator` works exactly the same but does not allow modifications to the elements of the object the iterator operates on. This would break the above example because we are dereferencing the `it` variable and reassigning which would be forbidden. 

There are four types of iterator total:

1. iterator
2. const_iterator
3. reverse_iterator
4. const_reverse_iterator

Which pretty much work as expected with desired forward and reverse behavior.

###### Tuples

Tuples work the same as for pairs but with as many elements as you want. 

```c++
#include <tuple>

using std::tuple; using std::make_tuple;

tuple<int, int, float> divmod(int a, int b) {
    return make_tuple(a/b, a%b, (float) a/b);
}
```

To index the tuple, we can use `get<N>(tuple_name)` where N is the n^th^ element of `tuple_name` rather than  using the first and second keywords like in pairs.

There also exist `unordered_maps` which are more like hash tables. 

### STL - Algorithms

There are algorithms built into the STL library. They are contained in `#include <algorithm>`. 

A common algorithm in STL to implement is a sort algorithm:

```c++
#include <algorithm>
#include <vector>
#include <iostream>

using std::vector; using std::endl; using std::cout; using std::sort; using std::cin; 
using std::sort;

int main() {
vector<float> grades;
    float cur_grade;
    while(cin >> cur_grade) {
        grades.push_back(cur_grade);
    }
    sort(grades.begin(), grades.end());
    cout << "Median Grade Was " << grades[grades.size() / 2] << endl;
    return 0;
}
```

Another commonly imported algorithm is `find` which searches a vector for an element:

```c++
int main() {
    int arr[] = {1, 20, -2, 4};
    int * p;
    p = std::find (arr, arr+4, 30);
    if (p != arr + 4) //for a vector use != vector.end() to do same thing
        cout <<  "value found at idx " << *p << endl;
    else
        cout << "value 30 not found in arr" << endl;
}
```

Another commonly imported algorithm is `count` which counts the frequency of a given element in an array:

```c++
int main() {
    int arr[] = {10, 20, 30, 30, 20, 10, 10, 20};
    int mycount = std::count (arr, arr + 8, 10);
    cout << "10 appears " << mycount << " times in arr.\n";
    //To use with a vector
    std::vector<int> vec (arr, arr + 8);
    mycount = std::count (vec.begin(), vec.end(), 20);
    cout << "20 appears " << mycount << " times in vec.\n";
    return 0;
}
```

Another one is `is_permutation` which tells you if two vectors are permutations of the same set:

```c++
int main() {
    array<int, 5> foo = {1, 2, 3, 4, 5};
    array<int, 5> bar = {3, 1, 4, 5, 2};
    
    if (std::is_permutation (foo.begin(), foo.end(), bar.begin()) )
        cout << "foo and bar contain the same elements." << \n;
    return 0;
}
```

### I/O Overview

As we know, we can use `<<` to write `cout` and `>>` to read from `cin`. There is more we can do with the `#include <iostream>` module though

###### Standard I/O

In addition to `using std::cin`, `using std::cout`, `using std::endl` we can also use `using std::cerr` for writing to standard error. We call `<<` the insertion operator and `>>` the extraction operator. 

###### File I/O

To do file I/O in C++, we use `std::ofstream` and `std::ifstream` which are contained in the `#include fstream` where `ofstream` is for file writing and `ifstream` is for file reading. `fstream` can be used to both read and write from a file. The insertion and extraction operators are used analogously to `cin` and `cout`

All the file I/O imports are objects that need to be created to target a file. 

Writing to a file:

```c++
#include <iostream>
#include <fstream>

int main() {
    std::ofstream ofile("hello.txt"); //creates hello.txt and writes to it.
    ofile << "Hello, World!"  << endl;
    return 0;
}
```

Reading From A File:

```c++
std::ifstream ifile("hello.txt");
std::string word;
while(ifile >> word) //while there is a word to read in, do so and write to console.
	std::cout << word << endl;
```

To be able to read and write to a file, we can use an `fstream`.

```c++
const std::ios::openmode mode = std::ios_base::in | std::ios_base::out
    | std::fstream::app
    
std::fstream fs;
fs.open("hello.txt", mode);
fs << "Hello CS 220" << std::endl;
fs.clear(); //resets the status.. not sure what that means
fs.seekg(0); //resets to beginning of file. 
```

Where app mode allows appending rather than overwriting. 

###### String Manipulation (I/O)

Instead of writing to a console or file, we can read and write to a temporary string in the program. 

```c++
std::stringstream ss;
ss << "Hello, world" << std:endl;
std::cout << ss.str();  //convert to a string and write to console.
```

Doing this creates a buffer so we can process the string and manipulate it before using it for our program or before writing to the console. This is great for string processing applications. The `.str()` method converts the buffer to a string object. 

A buffer creates a sequence of characters that can be read or written to like a file. The constructor `std::stringstream ss(string_name)` creates the `ss` buffer prefilled with the contents of `string_name`

String streams also have read and write specific versions. To create a string stream that can only be read from you can use `istringstream`. To create a string stream that can only be written to you can use `ostringstream`. Generally through a regular string stream is fine for most use cases. 

### Object Oriented Programming

C++ is an object oriented programming language. It features classes that can include methods unlike C structures. Another difference between classes and structs is that the classes allow `protection levels` for fields and functions like setting a function to private to hide data from users.   

`constructors` are special functions used to initialize class objects. `destructors` are special functions used to perform clean-up operations just before a class instance's lifetime ends.

Classes also allow inheritance for class extending and overloading. 

The File I/O functions we discussed in the previous section are examples of class inheritance. Inheritance is when class A inherits from class B if every class A object is also a class B object. The base class of all I/O functions is the `ios ` where `istream ` and `ostream ` inherit from. `ifstream ` inherits from `istream`, `ofstream  ` inherits from `ostream ` and `iostream ` inherits from both. The `>>` operator is defined for all `istreams`  and the `<<` operator is defined for all `ostreams`. Since `fstream` and `stringstream` both inherit from `iostream` both operators are defined. 

Again, using the example of the I/O stream functions, the `ofstream` function has a constructor that allows us to specify a filename  which is essentially calling `fopen` with the `w` flag. There is then a destructor that is run at the end of the `ofstream`  lifetime which closes the file for us. 

### References

References in C++ are very similar to pointers in C. A reference is an alias for an existing variable (memory location). Allows two names to separately refer to the same variable. References are like pointers but are safer. They cannot be `NULL` they must be initialized immediately upon declaration. Once the alias is set to a variable, it cannot be set to alias  another variable later in the code

To declare a reference to an integer we would write `int & ` which is reminiscent of the address-of operator but they are not the same.

```c++
int a = 5;
int & b = a; //now b is just another name for a
int * c = &a; //while c is a pointer to address of a

std::cout <<  "&a=" << &a << std::endl; //prints memory address: 0x01
std::cout << "&b=" << &b << std::endl; //prints same mem address: 0x01 
std::cout << "&c=" << &c << std::endl; //prints the address of pointer: 0x02
std::cout << "c=" << c << std::endl;  //prints address of original: 0x01
```

References allow us to pass the reference *by reference* like a pointer would be as a function parameter. In addition to this, they allow us to avoid the dereferencing syntax within that function. 

For example to write a swap function we can do this:

```c++
void swap(int & a, int & b) {
    int tmp = a;
    a = b;
    b  = tmp;
}
```

so no dereferencing is needed because we aren't using pointers. 

References allow us to do read in standard input line by line with `std::cin.get` without inputting the address of to the get function:

```c++
char ch;
while(std::cin.get(ch))
    std::cout << toUpper(ch);
```

The problem with references is that we don't know whether a parameter is by reference or by value just by looking at it. We just have to be careful about what variable is doing what especially because we can combine reference parameters with regular pass by value parameters. For example:

```c++
void divmod(int a, int b, int& quo, int& rem){
	//quo and rem are passed by reference so retain their value outside function scope.
    quo = a/b;
    rem = a%b;
}

int main() {
    int a = 10, b = 3, quo, rem; //initialize two ints and dont init the others
    divmod(a, b, quo, rem);
}
```

As a general rule, we should use references but pointers are available to us if we really need them for some obscure reason. 

References can be returned like pointers as well. Here is an example:

```c++
int& minref(int& a, int& b) {
    if (a < b) {
        return a;
    } else {
        return b;
    }
}
int main() {
    int a = 5, b = 10;
    int& min = minref(a,b); //sets min to be an alias to the actual variable a or b
    min = 12;
    cout << "a=" << a << ", b=" << b << ", min=" << min << endl;
    //prints a=12, b=10, min=12
}
```

the parameters to `minref` above must be references themselves otherwise, we would get an error because we would be returning a local variable that gets destroyed upon completion of the function call.

References can be made `const` which is useful because it will prevent us from changing that variable via the reference but unlike regular `const` types, that variable may still be able to change if the original variable was not `const`. 

When you want to save memory when manipulating large vectors, we can choose to replace `int sum(vector<int> vect)` with `int sum(const veector<int>& vect)`. The latter does not make a copy of the original vector in memory and instead performs its operation with the original vector. In both cases manipulations cannot be made or do not matter so there isn't really a difference between the two other than saving memory.

### Dynamic Memory Allocation

The C++ equivalents to `malloc` and `realloc` are `new` and `delete` respectively. There are some notable differences between the C and C++ functions however, 

`new` calls the appropriate constructor if used on a class type. 

`new` and `delete` are built-in keywords in the C++ language so we don't need to use parentheses to instantiate a new object.

```c++
int *iptr = new int;
*iptr = 10;
cout << "value of iptr " << iptr << endl;
cout << "value in iptr  " <<  *iptr << endl;
delete  iptr;
```

When we want to allocate a block of memory, rather than having to multiply the size of the type by the number of elements, we can do the following:

```c++
T * fresh  = new T[n]; //an array of size n
/** use the array **/
delete fresh; //don't need to specify the size.
```

if T is a built-in type, then all the values in the array are not initialized just like a malloc call. If T is a class, then the default constructor is called when the memory is allocated.

``` c++
int main() {
    double  *d_array =  new double[10];
    for (int i = 0; i < 10; i++)
        cout << (d_array[i] = i*2) << " ";
    cout << endl;
    delete[] d_array;
    return 0;
}
```

### Classes

###### Defining a Class with Methods

Like structs, classes bring together many variables but can also implement functions:

```c++
class Rectangle {
public:
    double width;
    double height;
    
    //the trailing const modifier indicates the function wont be modifying any of the object's fields
    //it is best practice to add this.
    void print() const {
        std::cout << "width=" << width << ", height=" << height << std::endl;
    }
    
    void area() const {
        return width * height
    }
};

int main()  {
    Rectangle r = {30.0, 40.0};
    r.print();
    std::cout << "area=" << r.area() << std::endl;
    return 0;
}
```

The best practice for writing classes in C++ is to put their **definitions** in `.h` files that wee can then import when needed. Functions can be declared and defined within the class definition but we should only do so when the function is very short which is referred to as "in-lining" the definition of the function. Otherwise, we put the function prototype in the class definition and define the member function in a `.cpp` file. To do this you have to specify the scope as in  `Classname::function(){}` within  the `.cpp`

Method definition within header file:

```c++
//rectangle.h
#ifndef RECTANGLE_H
#define RECTANGLE_H

class Rectangle {
    ...
    double area() const {
        //short function definition
        return width * height;
    }
    ...
};
#endif


```

Method and Class definition in separate files:

```c++
//rectangle.h ---------------------------------------------
#ifndef RECTANGLE_H
#define RECTANGLE_H

class Rectangle {
    double area() const;
}
#endif 

//rectangle.cpp ---------------------------------------------
#include "rectangle.h"
double Rectangle::area() const {
    //definition outside class
    return width * height;
}
```

###### Public vs Private

Fields in C++ classes can be public or private or protected. These protection statements define whether members of the class are public or private. Everything is `private` by default. C++ also has `structure` types where everything you define is `public` by default.  

A `public` field or method can be accessed freely by any code with access to the class definition (ex. contains the `.h` file)

A `private`  field or method can only be accessed by other member functions and variables in the object itself but not by a user of the class. We could have made the width and height variables private in the earlier example because we didn't use them outside the class' methods.

###### Initializing Class Fields

You cannot initialize class fields where they are defined. You need a default constructor if you want to do this. Initializing   a field in this way is only allowed for `static` fields which retain scope between object creation and destructions. 

###### Constructors

Answer the question of how classes and their fields get initialized. A default constructor is a constructor that is called whenever a new variable is assigned to the class. 

A constructor is just a member function you can define yourself. It should generally be public but there are exceptions.

The function name must exactly match the class name for the class to know the function is supposed to be a constructor. The constructor is a default constructor if it takes in no arguments. 

```c++
class Rectangle {
    public:
    	Rectangle() { ... }
    	...
}
```

If you do not write a default constructor, the compiler will create one for you. In this case, the compiler generated default constructor does not initialize built-in member types but will call default constructors for object member.  

We have been calling default constructors behind the scenes for example when creating an empty string or vector. 

A constructor is called implicitly when an object is declared and explicitly when `new` is used for dynamic memory allocation. `Rectangle * rp = new Rectangle()` calls default constructor but the `()` is actually unnecessary for calling the default constructor.

If we define any constructor at all, the compiler won't create one for us by default. Creating the object as you would normally would then create an error as you don't have a default constructor if you didn't define one appropriately.

###### Custom Default Constructor

```c++
class  Rectangle {
    public:
    	//initializes the values of width and height to zero by calling their constructors.
    	//this technique utilizes something called an "initializer list"
    	Rectangle() : width(0.0), height(0.0) { ... }
    	...
    private:
    	double width, height;
}
```

Defining a default constructor that does not utilize an initializer list:

```c++
class IntandString {
    public:
    IntandString() {
        i = 7;
        s = "hello";
    }
    int i;
    std::string s;
}
```

the same class utilizing an initializer list:

```c++
class IntandString {
    public:
    IntandString() : i(7), s("hello") {}
    int i;
    std::string s;
}
```

It is usually best practice to utilize an initializer list rather than the former method. Also allows `const` and `reference` variables to be defined within the class which would not be able to be initialized with the former method. Initializer lists initialize the variables before the constructor starts running. 

###### Non-Default Constructors

We can create constructors that also take parameters such as the string constructor call like so: `string s1("hello")` which creates `s1` with value `hello`. We could also create this string like this `string s2 = "hello"` which has the same result but first calls the default string constructor and then assigns the value to `hello`. 

Here is an example that utilizes C++'s default arguments which ':

```c++
class  DefaultSeven {
public:
    //Gives us three ways to call. Note default arguments in constructor
    DefaultSeven(int initial = 7, double val = 0.5) : i(initial), v(val) {}
    int get_i() {return i;}
    double get_v() {return v;}
private:
    int i;
    double v;
};

int main() {
    //creates first with two params, second has implicit second param, and 3rd uses both defaults
    DefaultSeven one(10, 20), two(2), three;
}
```

There are some rule about what you can and can't use for parameter names. You can use the same name as the variable that it will be set to with an initializer list for a parameter, however, you can't use that parameter name when calling a member function that takes in the same parameter name as the instance variable it is supposed to initialize.

The local parameter will overshadow the outer-scope one so you need to use the `this` keyword to access the object's variables. `this` is a pointer to the object's variables so we use the `->` operator to access its variables. 

You should not use `this` unless it is necessary unlike Java.

```c++
class MyThing {
    public:
    MyThing(int init) : init(init) {}
    int get_i() {return init;}
    //uses this to clarify you want to modify the private variable.
    void set_i(int init) {this->init = init;}
    private:
    int init;
};

int main() {
    MyThing s(10);
    s.set_i(20);
    cout << "s.get_i() = " << s.get_i() << endl;
    return 0;
}
```

###### Arrays of Objects

We can declare arrays of our custom class type. This calls the default constructor on every element that we create. So, to do this, the class needs a default constructor to be put in an array.

There is a way to get around implementing a default constructor. To do this, you can use list-initialization to initialize the array to avoid calling the default constructor. 

`MyThing s[10] = {{1},{2},{3},{4},{5},{6},{7},{8},{9},{10}}` allows you to create each of the 10 elements with an initial value corresponding to the array element you passed it. There is another way to do this with STL vectors: 

```c++
int main() {
    //create an empty vector with 10 elements of space
	std::vector<MyThing> s;
    s.reserve(10);
    //initialize each element with emplace_back
    for (int i = 0; i < 10; ++i)
        s.emplace_back(i);
    cout << "s[0].get_i() = " << s[0].get_i() << endl;
    return 0;
}
```

where emplace back create a new element with the argument passed to the object's constructor.

###### Destructors

We learned earlier that `new` and `delete` are used for dynamic memory allocation in C++. Constructors commonly allocate memory or open files which have to be cleaned up at the end of the class' lifespan. When creating objects, we can define a destructor that runs when the object is about to be deleted. We can use this to release any dynamically allocated memory. The destructor is always called automatically. 

When dynamically allocating arrays, we `T * fresh = new T[n]` to allocate the array and `delete[] T` to clean it up. Notice the brackets. The `delete[]` tells T to call the destructor. 

To define a destructor, we pre-pend the `~` operator to the beginning of the Class Name. For example:

```c++
//sequence.h
#ifndef SEQUENCE_H
#define SEQUENCE_H
#include <cassert>
class Sequence {
    public:
    	Sequence() : array(NULL), size(0) {}
    	Sequence(int sz) : array(new int[sz]), size(sz) {
            for (int i = 0; i < sz; i++) array[i] = i;
        }
    	//You would want to check that the array is not NULL before doing this otherwise you will get a segmentation fault by trying to delete the null pointer.
    	~Sequence() {delete[] array;}
    	int at(int i) {
            assert(i < size);
            return array[i];
        }
    private:
    	int *array;
    	int size;
}
#endif
```

###  Overloading

###### Function Overloading

Allows us to write functions with the same name but different arguments. For example

```c++
void output_type(int) {cout << "int" << endl; }
void output_type(float) {cout << "float" << endl; }

int main() {
    output_type(1);
    output_type(1.f);
    return 0;
}
```

The compiler is able to distinguish that you want the function to handle the different input arguments differently.

Allows you to create functions that handle different parameter types, different parameter numbers, and different parameter order or combinations of all of those. Default parameters also will work for overloaded functions and can be applied to the different functions differently.

This **will not work** if the functions have **different return types**. The functions may take different inputs but must return the same type. It seems that because `char` are technically integers, you can return char in place of an `int`?

###### Operator Overloading

Operators like `+` and `<<` are just functions that take arguments but are called differently. For example `a + b` is like calling `plus(a, b)` or `a.plus(b)`. Thus, operator overloading is really just function overloading. 

Operator overloading is useful for defining new meanings for operators when they act on user defined classes. It is important to make sure that the new meanings we give to the operators are intuitive.

To overload an operator, the function representing the operator is `operatorS` where `S` is the symbol for the operator you want to overload. 

For example

```c++
std::ostream & operator<<(std::ostream & os, const std::vector<int> & vec) {
    for (std::vector<int>::const_iterator it = vec.cbegin(); it != vec.cend(); ++it) {
        os << *it << ' ';
    }
    return os;
}
int main() {
    std::vector<int> vec = {1,2,3};
    std::cout << vec << std::endl; //needs vec cout
    return 0;
}
```

this works because `std::ostream` is an output stream that can be written to. It is not a constant reference because we change it in the function and return the changed reference.

The `<<` operator is evaluated from left to right. The first expression on the left returns a `std::ostream` which can then be used with the next expression to the right. Taking in the output stream, modifying it, then returning it keeps the chain going.

Suppose we have a rational class with an integer numerator and integer denominator:

```c++
Rational operator+(const Rational & left, const Rational & right);
```

overloads the addition operator, takes in two constant Rational references and returns a rational as we would expect. This overloading should be done in the Rational class so that we have access to the potentially private numerator and denominator thus, we can skip the first parameter as this is implied to be `this` as in:

```c++
Rational operator+(const Rational & right) const;
```

where the trailing `const` indicates that the `this` object's parameters arent changed. We don't have to return a pointer or reference to a Rational because the local Rational class is not deleted when the stack frame ends. Rather, the **copy constructor** of the class makes a copy of the result before the stack frame ends. 

A copy constructor looks like this:

```c++
Rational(const Rational & original);
```

and if it is not defined in your class, the compiler will create one for you. However, this copy will only be a **shallow copy** of the original. This implicit copy is a simple field by field copy but you can manually change how this works by defining a custom copy constructor.

You may want to write your own copy constructor when your class utilizes heap memory. The implicit copy constructor would copy over the other object field by field but you could save time copying if you just pointed the new object to the allocated heap memory.

A copy constructor is called when a constructor is called on an existing object, when a class object is passed by value to a function, and when a class object is returned from a function by value.

If you want to overload `<<` for a user-defined class and want to do it in the class itself, you would use:

```c++
std::ostream & operator<<(std::ostream & os, const Rational & r);
```

however, we can't make this overload `<<` within the class because the first argument has to be the `Rational` as it is implicitly plugged into the function when called as a class method.

Instead, we use the keyword `friend` to give the function an "almost-member" status which is used like so:

```c++
class Rational {
    public: //...
    friend ostream & operator<<(ostream & os, const Rational & r);
    private: //...
}
```

where the implementation of the function can be placed in the `.cpp` file. The `friend` designation tells he class that it is allowed to access private member variable without being a member of the class.

### Initialization and Assignment

We know there is a difference between the `==` and `=` operator. There is also a difference between two types of `=`.

There is the initialization`=` which works when we `int a = 4;` and we also have the assignment `=` which sets an existing variable equal to another `a = 4;`

Suppose we have the following class:

```c++
class Complex {
    public:
    	//default constructor
    	Complex() : Complex(0.0, 0.0) {std::cout << "Default" << std::endl;}
    	//Non-default constructor
    	Complex(double r, double i) : real(r), imag(i) {std::cout << "Non-default" << std::endl;}
    	//Copy constructor
    	Complex(const Complex & c) : real(c.real), imag(c.imag) {std::cout << "Copy" << std::endl;}
    	//Assignment operator
    	Complex & operator=(const Complex & rhs) {
            std::cout << "Assign" << std::endl;
            real = rhs.real;
            imag = rhs.imag;
            return *this;
        }
}

int main() {
    Complex c; //runs default constructor
    Complex c2 = {4.9, 0.5}; //initialization = calls non-default constructor
    Complex c3 = c; //= sets values with copy operator
    c3 = c2; //= outside declaration is assignment =, runs assignment operator
    if (c3.get_real() == 4.9) { //== tests equality.
        cout << "Real part of c3 is equal to 4.9" << endl;
    }
}
```

### Rule of 3

When you use a copy constructor as in `Image o_wins = x_wins;` the copy of x_wins is a shallow copy. Meaning, that pointers to memory addresses are copied rather than new memory allocated. This creates the issue of one allocation and a memory leak when the Image class allocates dynamic memory.

We want to create a **deep copy** for this class to copy the dynamically allocated memory into a new memory location.

The Rule of 3 states that if you need to create a **non-trivial destructor** such as calling a `delete` function, you need to also define a **copy constructor** and an **assignment operator** to avoid memory leaks from shallow copies. 

A Copy Constructor looks like this `ClassName(const ClassName &)` and initializes a new `ClassName` object as a copy of another. It is called by C++ when initializing a new object as another object, passing an object by value, or returning an object by value.

```c++
Image(const Image& o) : nrow(o.nrow), ncol(o.ncol) {
    //create a deep copy
    image = new char[nrow * ncol];
    for (int i = 0; i < nrow * ncol; i++)
        image[i] = o.image[i];
}
```

An Assignment Operator looks like this `operator=` and is called when one object is assigned to another. Called when one object is set equal to another but is not initialized as such. Need to first deallocate the memory allocated for the `self` object's previous data and then allocate new memory and fill that from the object you are copying from

```c++
Image & operator=(const Image & o) {
    delete[] image; //deallocate previous object's previous image memory
    
    nrow = o.nrow; //this function is not a constructor 
    ncol = o.ncol; //so we can't use initializer list syntax
    
    image = new char[nrow * ncol];
    for(int i = 0; i < nrow * ncol; i++)
        image[i] = o.image[i];
    return *this; //for chaining
}
```

Overall, we summarize this in one sentence as: when you implement a non-trivial destructor remember to implement your own copy constructor and assignment operator.