# Intermediate Programming Midterm Review

*Benjamin Fry - 03/09/21*

### Basics of C

Compiling a simple C program: 

`gcc -std=c99 -pedantic -Wall -Wextra program.c` which enables extra error checking and sets the C standard. 

###### Preprocessing

Content from lines like `#define` and `#include` is read from external files and substituted in the appropriate place in the file

###### Compiler

Converts each file's source code into machine code

###### Linking

Selects memory addresses and combines the project files into a single executable

###### Variables

Has a type declaration that assigns a memory address to a memory block of a type-appropriate size. By default integers are `int`, decimal numbers are `double`, single letters are `char`.

###### Operators

![image-20210127115449089](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210127115449089.png)

Pre-incrementation works by incrementing the variable before the rest of the statement executes, while post-incrementation will use the current value, execute the rest of the statement before incrementing the variable. 

`printf`, takes in a pattern string and a variables equal to the number of `%` statements and prints to standard output. 

`scanf` takes a pattern string similar to `printf`. Rather than using values in a variable, assigns the address of a variable of an appropriate type to the scanned-in variable. `scanf` returns the number of successful matches to the pattern string which will be equal to the number of `%` statements. To use you have to pass the variable name with the address of operator: `&`

###### Logical Operators and Control Statements

C uses `&&`, `||`, and `!` for and, or, and not respectively. 

The If Else statement:

```c
if (a) {
    /*do something*/
} else if (b){
    /*do something else*/
} else {
    /*do the default*/
}
```

The Switch statement:

```c
switch (integer_expression) {
    case c1: /*handle case 1*/;
    case c2: /*handle case 2 and also case 1*/;
        break;
    case c3:
    case c4: /*handle case 3 and case 4 */;
        break;
    default: /*if none of other cases */;
}
```

will execute the terms that follow the case until a break statement. Good for if you want multiple but varied things to happen based on the integer value of some variable `integer_expression`. The terms `c1, c2, c3, and c4` are the values for `integer_expression` for which you want to selectively perform actions. 

###### Loops

When looping we have access to the `break;` and `continue;` statements which will immediately terminate the loop and either continue on to the next iteration or break the loop all together.

While Loops

```c
while (boolean) {
    statement;
}
```

iterates 0 or more times depending on the truth evaluation of the boolean expression in its argument. 

Do-While Loops

```c
do {
    statement;
} while (boolean)
```

works the same as a while loop with the caveat that the contents of the while loop are executed at least once and the loop continues based on the truth evaluation of the boolean expression. 

For Loops

```c
for (initialization; boolean; incrementation) {
    statement;
}
```

composed of three statements, first sets an index variable to some value, then evaluates some boolean expression. Loop only executes if boolean evaluates to true after initialization. 

###### Arrays

An important fact about arrays in `c` is that the variable that is assigned to the array is actually just a pointer to the first element in the array. The elements of the array are one continuous block of memory of exactly the `sizeof(array_type)*array_length`. For example a character array requires one byte per character in the pre-allocated array length. 

Array Example:

```c
int arr[10];
```

allocates an array of 10 integers. Integers are about 4 bytes each so this is 40 bytes in memory. 

Arrays in C are zero-indexed so the last valid element of an array is one less than the length it was initialized with.

When an array is created, its elements are not initialized by default. You can initialize the values of an array using curly braces such as in:

```c
int arr[5] = {1, 2, 3, 4, 5}; //the 5 is actually not necessary as size is implied
```

accessing the elements of an array before initializing them leads to undefined behavior as anything could be occupying the memory location you're accessing. 

###### ASCII Table

When you create a character variable, you are setting the variable equal to an integer which is assigned by the ASCII table. When you print the integer as a character, you get the conversion, however all the integer arithmetic operations still work because the variable is just an integer. The 0th item in the ascii table corresponds to the `\0` character which is the null terminator for stings. 

Character blocks are continuous so if you know the ascii integer corresponding to 'A', you know 'Z' is found at 'A' + 25.

The functions `isalpha`, `isdigit`, `islower`, `isspace`, `tolower`, and `toupper` act on characters and can be found in the `#include <ctype.h>` file. 

###### Strings

Strings are not their own data type in c, rather a string is just a character array with the same pointer behavior as normal arrays. The last item in a string array must be `'\0'` which happens to also be 0 in the ascii table. 

```c
char day[] = "monday"; //assigns creates day string of length monday + '\0'
```

Another way is to define the string with pointers `char * str = "monday"` which does the same thing. 

Another way is to manually set the array but must remember the null character 

```c
char day[] = {'m', 'o', 'n', 'd', 'a', 'y', '\0'};
```

Strings can be indexed just like arrays which returns the character at that index. 

**The Essential thing to remember about strings is that their size must be  +1 the length of the largest word you want them to contain to accommodate the null terminator. **

If the null terminator falls before the end of the string, the string is truncated to whatever is before the null terminator. 

Some useful methods are `strlen(), sizeof(), strcmp(), strcpy(), strcat()`  which are all contained in `#include <string.h>`

###### File Input/Output

To write to text files, use `fprintf()` as follows:

```c
FILE * myfile = fopen("file.txt", "w+"); //opens file for reading and writing.
if (input == NULL){ //fopen returns null if no such file exists. 
    //handle error
}

int a = 0, b = 0;
int scanout = fscanf(myfile, "%d %d", &a, &b); //output and input similar to scanf but needs FILE pointer.
fclose(myfile); //need to close when done.
```

to use `fprintf(myfile, "hello, %s!", "world!");`

When you open a file pointer, operations like `fscanf` increment the file pointer line by line. Eventually, the file pointer will point to EOF which we can check with `feof(file)`, if the file is in an error state like reading from a write only file pointer `ferror(file)` can inform us of this, `rewind(file)` will reset the file pointer to the beginning of the file. 

The standard streams are files that are present for every c program compiled with `#include <stdio.h>` they are `stdin, stdout, and stderr` and can be written and read from just as a normal file (so use `fscanf` and `fprintf`) they do not need to be closed however, that's handled by the program.

###### Assertion Statements

Help catch bugs by checking test cases we set in the code and ensuring they return the same value throughout the program development process. The argument to an assertion is a boolean and must evaluate to true or else the program is immediately terminated with an `assertion failed` error message. 

Non-zero return statements with intelligent messages should be implemented when the USER makes an error with the program execution. Assertion statements are to catch errors made by the software developers and are less friendly. 

`assert(a == 3);`

###### Math

`#include <math.h>` gives access to useful math functions like `sqrt, pow, exp, log, log10, ceil, floor, sin, cos` and more. Weirdly, when compiling a function that includes the math module, you need to compile with the `-lm` flag to link things correctly. So to compile we would use:

`gcc -Wall -Wextra -pedantic -std=c99 -lm file.c`

The default argument type for the above functions are doubles but other types will be casted to doubles on calling the function. 

###### Functions

Function definitions need to occur before they are called. You can get around this by defining the function above everything else or in a header file and then implementing the function at the bottom of the file or in another file. To do just a function declaration, you type the function and its inputs and end single line with a semicolon.  `int func1(int a, int b);`. You would then have the implementation later in the file.

Function arguments in C are generally **pass by value** which means that a copy of the argument is made when the function is called. To get around this, you have to use pointers. Since arrays are pointers in C, they are **pass by reference**. It is useful when passing arrays to functions to also pass the length of the array so that you know how many values past the initial pointer it is safe to increment without getting undefined behavior. 

Recursion is pretty straight forward, just have the function return a call to itself or something along those lines. As always start recursive functions with base cases and branch logic out from there. Every recursive call adds a stack frame, the stack is a memory area where variables and other temporary values that exist only within function calls are stored along with the return address which gets the output of the function when it returns. Every recursive call adds to the stack frame. If the recursive calls never stop, you exceed the size of the call stack and you will get a memory error/program crash. The size of the stack is proportional to the number of calls. 

###### Command Line Arguments

The main function can take parameters as well that are passed into main when the program executes:

```c
#include <stdio.h>

int main(int argc, char * argv[]){
    //argc is the number of arguments + 1 (length of argv) so to print
    for (int i = 0; i < argc; i++){
        printf("argv[%d] = %s\n", i, argv[i]);
    }
    return 0;
}
```

where the name of the executable is always the first index of `argv` and anything passed after that when the program is run follows it. An equivalent way to express the `argv` argument is with `char argv[][]` and `char **argv` which express it with no pointers or with all pointers respectively.

###### Linking Multiple Source Files

We can use header (`.h`) files to hold constant definitions and function declarations that different files across the project will be able to use. To include this in our source (`.c`) files, we have to add `#include "functions.h"` to the top (note double quotes not angle brackets).

Once we have a header file with our function definitions, we can write those functions in a separate source file. In the `functions.c` file, we include the header file and define our functions as normal, then in the `main.c` file which contains our main function, we also include the same header file. 

Header guards are used to ensure that once a header is included in the executable the compilation process doesn't try to include it multiple times. For example if main includes `a.h` and `b.h` where `a.h` includes `b.h` inside itself, you avoid confusing the compiler with double definition. 

```c
#ifndef NAME_OF_FILE_H
#define NAME_OF_FILE_H

// do header file definition stuff

#endif
```



We could then call `gcc std=c99 -pedantic -Wall -Wextra main.c functions.c`.

We can do separate compilation to save time by not compiling files that we  have not changed and only compiling the ones that have. This is made easier with Makefiles as below. However, when we compile our `.c` files, the compiler translates them to object (`.o`)  files. The linker then takes those object files and converts them to a single executable file. We can choose only to compile a single file with `gcc -c functions.c` which would then produce `functions.o`. Assuming we have already done the same for `main.c` which is unchanged since the last compilation, we can then selectively link the object files with `gcc -o functions.o main.o`

###### Make and Makefiles

Since we can now selectively compile files, `make` keeps track of which files have changed since the last time our executable was built. The `Makefile` is a set of instructions that tell make what to do with the files that we've changed to create the executable.

```makefile
CC=gcc
CFLAGS=-std=99 -pedantic -Wall -Wextra

main: mainFile.o functions.o #relinks the output files, remakes them if needed
	$(CC) -o main mainFile.o functions.o
	
mainFile.o: mainFile.c functions.h #whenever mainfile or functions.h changes recomp main
	$(CC) $(CFLAGS) -c mainFile.c
	
functions.o: functions.c functions.h #recomp when either functiosn file changes
	$(CC) $(CFLAGS) -c functions.c
	
clean:
	rm -r *.o main
```

Once we have such a main file in our directory containing our functions, we can run `make` which just runs the main function and everything it needs to below that. You can also selectively run `main mainFile.o` to just run that compilation step but realistically idk why you'd do that. 

###### `sizeof`

Simply returns the size of its argument measured in bytes. This is useful for dynamic memory allocation. A very common use case for this is `sizeof(a)/sizeof(type_of_a_elements)` which tells you the length of an array a. 

When you pass an array to a function, the array 'decays to a pointer' which if you call  `sizeof(pointer_to_array)` would inaccurately return the size of a pointer which is usually 4 bytes. To get around this, you can wrap the array in a struct and the size of that will be correct (see below obv)



###### Multidimensional Arrays

`int a[10][10]` is a 10x10 matrix where the first bracket is the number of rows and second bracket is the number of columns. You can initialize with a loop or curly braces like so `int table[2][4] = {{1,2,3,4}, {5,6,7,8}}`

As with single dimensional arrays, multidimensional arrays are lain out as a single block of memory. This means that each row follows the previous row in memory, incrementing a pointer from the last element of the first row by 1 would point to the first element of the second row. 

When passing multidimensional arrays to functions, we can omit the first array index size but not the second. I presume this is because it is implied, we probably also want to pass with the array so we know when to stop incrementing:

```c
void sum_matrix(int list[][4], int numRows);
```

###### GDB

GDB stands for GNU debugger, it allows you to step through your code line by line, setting breakpoints and printing variable contents wherever you want. Useful for finding exactly what line of code is causing a crash or undefined behavior.

`break main` sets a break point on the main function, `n` steps forward to one line, `s` steps forward one line and into a function call if there is one on the next line, `p` prints a variable.

### More Complex Stuff

###### Pointers

A pointer is a variable that holds a memory address. The address may be on the stack or the heap. If the address is on the stack it was created in a function call and will be cleared when the function that created it returns. Pointers allow us to pass by reference between stack frames. While the stack frame that created a pointer is still alive, you can change the memory address the variable points to and more usefully, you can change the value at that memory address.

Again, pointers are variables that hold a memory address. They are typed accordingly to the value held at the memory address they point to. This could be an integer, a char, or even another memory address that itself holds something.

To declare a pointer add `*` after the type declaration as follows `int * i_ptr` which declares a pointer to an integer. This pointer is uninitialized and is equal to `NULL` by default.

To point the pointer to something, we can dereference another variable using the `&` operator as so `i_ptr = &x` where `x` is an integer variable. 

To dereference the pointer and get/set the value at the memory address to which the pointer points, we use `*p` like this: `int y = *i_ptr;` which sets a new variable y equal to the value at pointer's current memory address. To change the value at this memory location, we can use `*i_ptr = 5` to reassign the pointer to 5.

Pointer dereferencing is a common source of bugs because the `*ip` has 'unary operator precedence' which checking the table above is read right to left so operations like post-incrementation which would perform pointer arithmetic rather than incrementing the value at the address. To fix this, we just add parentheses to ensure we get what we want: `(*ip)++` increments value at `ip` while `*ip++` increments the pointer by one then dereferences.

###### Dynamic Memory Allocation

Allows us to define memory on the heap rather than the stack which is persistent regardless of when the stack frame that created it collapses. The heap also has more memory availability than the stack so it's better for large arrays. With this, we can return arrays from functions as they will persist past their stack frame.

C is not a garbage collected language so **every time we manually allocate memory, we need to free that memory before the program exits** (we are the trash collectors) otherwise we create a memory leak which is bad practice and a cardinal programming sin. 

To allocate heap memory, use the `malloc()` function which takes in a number of bytes as its argument and returns a pointer to the allocated memory. As mentioned in the `sizeof` section, we can use `sizeof(type)` to get the number of bytes of the thing that we want to allocate memory for. 

```c
int * i_ptr = malloc(sizeof(int));
if (i_ptr == NULL) {
    //allocation failed handle w/ error message
}
```

points `i_ptr` to heap memory allocated to hold exactly one integer. 

`malloc` can also be used to allocate memory for arrays, to do this we call `int * a = malloc(sizeof(int) * 10)` which creates 10 integers worth of memory and points a to the first valid memory address. This corresponds to the 0^th^ index of a as an array. In fact, a can be indexed like a normal array and a can be returned from a function.

Once we are done using a pointer to heap memory, we need to call `free(a)` and it's good practice to set `a=NULL` immediately after if you're going to keep using it. The `free` function does not have to be called in the same function that `malloc` was called. 

`ptr = realloc(ptr, new_size)`  is used to reallocate heap memory. It automatically frees the memory that `ptr` was using before the call and creates a new block of `new_size` bytes. It returns the address of the new memory block for reassignment. 

`calloc(size)` is similar to malloc but automatically initializes all bits to zero.

###### `Valgrind`

A debugging tool that helps find memory leaks and invalid memory indexing. To run, first compile the program, then run `valgrind --leak-check=full ./myFile <arg1> <arg2> ...` the first thing to look at in the output is the `error summary` line, then look at assigned/freed, invalid read/writes, etc...

###### Pointer Arithmetic

Useful operations that can be performed on pointer variables.

Assignment `ptr1 = ptr2` sets `ptr1` to point to the same memory address as `ptr2 ` dereferencing and assigning the memory location pointed to necessarily sets the other pointer's dereferenced value as well so `*ptr1 == *ptr2` returns true.

Addition/Subtraction with `+, -, +=, -=` operators can be performed on a pointer. Subtracting two pointers and adding/subtracting integers to pointers are allowed. This arithmetic is most useful when dealing with blocks of memory such as that of an array. When you add an integer to a pointer, the pointer is moved that number of elements down from its current position in the array. 

If `a` is a pointer to an integer array, then `a[3] = 20` is equivalent to writing `*(a+3) = 20`.

Subtraction of pointers returns a special type called `ptrdiff_t` which is basically a `long` integer. If you have pointers to the first and last element of an an array, you can calculate the size of the array as the difference between the last and first element. 

When you want to copy an existing array into a new pointer variable, you have to first allocate the appropriate amount of memory which for a string remember is the length of the string + 1. You can then `strcpy` the two strings. 

Another common error is for example `char str1[] = "original";` and then trying to increment `str1`. You are not allowed to do this because you would lose the original array. To get around this, you have to define another character pointer and set it equal to str1. Since this doesn't copy the array and just points to the first element you may freely manipulate the pointer since is it not the original.

###### Multidimensional Dynamically Allocated Arrays

As we saw when allocating 2D arrays earlier, they are lain out row by row as one large block in memory. If we know we want a 5x2 array, we could allocate an array of length 10.

Alternatively, we can define a multidimensional array as an array of pointers that point to smaller arrays. First, we `malloc` the desired number of rows worth of pointers, this would be a double pointer like so:

```c
int **a = malloc(sizeof(int *) * num_rows);
```

we could then loop through the rows of this array of newly allocated null pointers and allocate memory to hold each column of integers. This array actually won't be one contiguous block of memory but indexing works the same:

```c
for (int i = 0; i < num_cols; i++) {
    a[i] = malloc(sizeof(int) * num_cols);
}
a[2][1] = 10; //still works the same as normal 2D array
```

we then have to free the dynamically allocated memory as normal but have to be careful to free the memory allocated for each index since it was done separately:

```c
for (int i = 0; i < num_rows; i++) {
    free(a[i]);
}
free(a);
```

Regardless of the creation method, each row in the multidimensional array will be a one dimensional array that can be indexed and assigned like normal. 

###### `const` pointers

We can make a variable non-modifiable with the `const` keyword which acts as part of the typing of the variable (and thus must be carried into function definitions with it as well).

`const int * pointer` will make the value at the pointer address non-modifiable, but the memory address of the pointer is free to change.

`int * const pointer` makes the memory address the pointer points to non-modifiable but the value at the address is free to change. 

`const int * const pointer` makes both the address of of the pointer variable and the value at that address non-modifiable. 

###### Lifetime and Scope

The lifetime of a variable is the amount of time the variable is alive in memory, the scope is the blocks of code the variable is accessible in. Local variable lifetime begins when a function is called and ends when the function exits. Local variables are allowed out of scope only when passed as arguments to other functions.

A variable in scope can be hidden when an inner scope declares a variable with the same name such as:

```c
int i = 12;
for (int i = 0; i < 10; i++)
    printf("%d", i); //prints 0 thru 9 - original i hidden
printf("%d", i); //prints 12 - original i back in scope
```

The `static` keyword is used to keep a variable's value between calls to a function. They are automatically created and initialized to zero. They are not destroyed at the end of a block of code. For example:

```c
int addInt(int x, int y) {
    static result;
    result += x + y;
    return result
}

int main() {
    printf("add %d + %d = %d", 3, 4, addInt(3, 4)); //prints 7
    printf("add %d + %d = %d", 3, 4, addInt(3, 4)); //prints 14 because result not reset
 	return 0;
}
```

A global variable is accessible in all scopes. However, we are not allowed to use them because they make debugging difficult.

Static and Global variables are stored in a special region of memory called the data segment which is filled when the program executes (rather than being stored in stack frames).

###### The `struct` 

A struct is a bunch of related variables grouped together. Cannot contain functions, only variables.

```c
int main(){
    struct date {
        int year;
        int month;
        int day;
    };
    struct date purchase_date
}
```

The `sizeof` a struct is (at least) the sum of the size of its fields (there is a caveat that the size may have padding bytes added for many element structs with elements of different types). If you wrap a struct around an array, the size of will be able to accurately size up the array because the struct is pass by value like most other c types. Therefore the array is fully copied and does not decay to a pointer?

Because structs are pass by value, they need to be reassigned to be mutated. Alternatively, you can use pointers to manipulate the struct and its contents without having to reassign it. Using pointers to manipulate structs within functions is so common that there is a special operator in c that combines dereferencing a pointer to a struct with the attribute selection (`.`) operator. Thus, rather than writing `(*date).day` we can write `date->day` which means the exact same thing. 

`typedef` is a keyword used to avoid rewriting struct every time we want to assign a variable to be a struct. This is essentially defining our own type:

```c
typedef struct {
    float amount;
    char cc_number[16];
} cc_receipt;
```

this defines the type `cc_receipt` which we can then create without using the struct keyword like so `cc_reciept var;`

You can have `struct`s nested inside `struct`s which is summarized nicely with this example:

```c
typedef struct { //no name, immediately assigned to color attribute within parent
    struct {
        int r;
        int g;
        int b;
    } color; 
    struct  { //no name, same as above w/ position attribute
        int x;
        int y;
    } position; 
} pixel;

int main() {
    pixel p;
    p.color.r = p.color.g = p.color.b = 255; //access color attribute and sub-attrs
    p.position.x = 40; //access position attribute and sub-attrs
    p.position.y = 50;
    printf("[%d, %d. %d] at (%d, %d)\n", p.color.r, 
           p.color.g, p.color.b, p.position.x, p.position.y);
    return 0;
}
```

###### Random Number Generation

The build in `rand` function returns a value between 0 and `RAND_MAX` in a uniform distribution.

The program will always use 1 as the seed so the random numbers won't really be random by default. To get around this, you can set the seed of the RNG using `srand()` which takes an unsigned integer. It is common to `#include <time.h>` and run `srand(time(0))` which passes the time since UNIX epoch as the seed. 

The modulus operator is used to constrain the range of random numbers, the manipulations are summarized well here:

![image-20210222121905492](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210222121905492.png)

Floating point numbers can be generated as follows

```c
((rand() % 100000) / 100000.0) // which generates an inclusive range from 0.0 to 0.99999
((rand() % 100001) / 100000.0) //which generates from 0.0 to 1
```

where the granularity is determined by the number of zeros. The maximum resolution random float between zero and one is given by

```c
rand() / (double) (RAND_MAX - 1)
```

###### Binary File I/O

We can read and write files working directly with bits and bytes rather than with character strings. Any non-text file is a binary file. Storage of data this way is much more efficient than in text for example storing 255 as text requires a byte for each number while it requires only one byte to represent in binary.

Reading and writing binary files is analogous to regular file I/O:

```c
FILE *fp = fopen("data.dat", "rb"); //open for binary file reading
fread(array_to_read_into, size_of_elements, num_elements, file_pointer);
fwrite(array_to_read_from, size_of_elements, num_elements, file_pointer);
```

An example

```c
int main(){
    int SIZE = 100;
    int arr_write[SIZE];
    for (int i = 0; i < size; i++)
        arr_write[i] = i * 10;
    FILE *fp = fopen("data.dat", "wb");
    fwrite(arr_write, sizeof(arr_write[0]), SIZE, fp);
    fclose(fp);
    
    int arr_read[SIZE];
    fp = fopen("data.dat", "rb");
    int num_of_ints = fread(arr_read, sizeof(arr_read[0]), SIZE, fp);
    for (int i = 0; i < SIZE; i)
        printf("arr_read[%d] = %d\n", i, arr_read[i]);
    fclose(fp);
}
```

###### Bitwise Operations

Allow manipulation of values at the bit level. This is most meaningful for integer-based types as floats use complicated bit sequences while integers simply represent powers of 2 from 2^0^ = 1 to the maximum size of the type. The 'endianness' of the computer you are running the program on determines whether the lowest power of 2 is found at the first memory address (little-endian) or the last memory address (big-endian).

AND operator (`&`) performs logical and comparison between all bits. 

>`12 = 00001100`
>
>`25 = 00011001`
>
>`12 & 25 = 00001000 = 8` which is the value when each bit is compared and only set to 1 when they are  both 1

OR operator (`|`) performs logical or comparison across all bits

>`12 = 00001100`
>
>`25 = 00011001`
>
>`12 | 25 = 00011101 = 29` which is the logical or of each bit compared. 

Bit Shifting 

`x << n` shifts the bits of x to the left n positions. Each new bit added to the right is a zero and n bits 'fall off' the left: `25 = 00011001` and the bitwise shift of `25 << 5` introduces 5 zeros on the right like so`25 << 5 = 1100100000 = 800` (an integer is 16 or 32 bit I'm just not typing all the zeros if you shifted passed the end, the shifted bits would fall off and be lost and wouldn't wrap around)

Bit shifting to the left is equivalent to multiplying the number by 2^n^

`x >> n` shifts the bits of x to the right n positions in the same way as left shifting. This is equivalent to (floor) dividing the number by 2^n^. 

Shifting left and then shifting right will not recover the original number if any bits fall off either end. 

Here is a code snippet that prints out the binary representation of an integer as a string:

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
    tmp >>=1; // shift tmp right by 1
}
printf("%d in binary is %s\n", num, bin_str);
```

There is also the XOR operator (`^`) which performs the exclusive or operation between bits and the bit negation operator (`~`) which flips every bit in the number from 1 to 0 and vice versa.

###### Number Representation

Integers in C use the "two's complement" representation for signed integers. For a four bit integer, the highest value bit is reserved to represent the sign of the number. A 1 at the most significant digit is negative and a 0 at this position is positive. 

![image-20210310020627722](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210310020627722.png)

A useful property of this system is that if you take any number and flip all of its bits and add 1, you get the negated version of that number. For example +3 = 0011 -> 1100 -> 1100 + 1 -> 1101 = -3

Another property of this system is that overflowing the maximum positive value will overflow the number from the maximum positive number to the minimum negative number. And similarly, the smallest possible integer minus 1 gives the largest positive number.

Floats on the other hand use a complicated system to represent sign, exponent, and mantissa. Converting between int and float is not a simple bit conversion.

###### Type Casting

The type of a variable in C is determined when it is defined. If you assign a value that is not of the expected type to that variable, C will perform automatic type conversion.

When you write a decimal number in C, it is a double by default. If you want to change it to a float, you can cast it with (float) or you can write the number with a trailing f as in `3.14f`. When floats and doubles are overflown, the variable is set to `inf`

Promotion is taking a number from a smaller value to a larger one like setting a variable typed to be a float equal to an integer. The integer is automatically converted to the larger float type. Promotion raises the lower type to match the level of the higher type

Narrowing is going from a larger type to a smaller type such as setting a variable typed to int equal to a floating point number. Usually truncates the higher type's extra bits to fit into the lower type. 

Dividing two integers performs integer division by default, if you want to get float output you need to add a decimal to one of the values or cast one to a higher type. Similarly, passing floats to function parameters typed as integers will truncate the floats without warning.

No compiler errors or warnings are issued when you have a narrowing conversion even though information may be lost if the conversion is unintentional. The only time you'd get an error is if you expect the output to be one type and set it in `printf` which doesn't end up matching. 

The general type hierarchy is char < int < unsigned < long < float < double

###### Linked Lists

A data structure that stores a variable and the memory address to the next element in the list. Comparable to arrays. 

![image-20210301114106897](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210301114106897.png)

Each linked list has a starting node and a final node. The last node's pointer points to NULL and that is how it is identified as the end of the list. The head of the list is a pointer to the first node in the list.

Pointer arithmetic cannot be used to jump to the next element in the list since you have to follow the pointer chain. 

Linked lists are more dynamic than arrays because their length is not fixed. Elements can be deleted by pointing the previous node to the node that the element points to. 

Example implementation

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
```

You can then implement a print function for the list which traverses the list and prints each value until it reaches the null pointer.

A length function loops through each node and increments a counter to count number of nodes. 

An add_after function creates a new node, holds previous node's pointer, sets to new node's pointer, then points previous node's pointer to new node.

There are more operations but they're pretty much the same things. More complex ones may require arguments of pointers to pointers to nodes so that the head can be reassigned. 

### TA Review Session

###### Exam Tips

Practice solving the problems on paper. You need to have a system for tracing variables and stepping through the logic. Make sure to read the whole problem. 

Do not spend too long on multiple choice questions, check for syntax errors in written code, have a system for variable tracing, understand pointers and passing by value, understand linked lists, data type sizes and conversions (narrowing/promotion)

###### Compiler

First preprocessor processes all #include and #define statements, then compiler translates to object to code, then linker collects object files to make an executable. You can only have main function per executable. 

###### Types

Variable types: a char has 1 byte, int has 4 bytes, unsigned has 4 bytes like int but only handles positive values, longs have greater capacity than ints, floats are single precision decimals, doubles are double precision decimals, boolean have to be included with standard bool, all pointers are 8 bytes.

###### Short Circuiting

Remember that the C compiler is lazy. When you use an OR statement, if the first test (left most test) evaluates to true, the second test wont be run, the professors like to try to trick students with this. Similarly, if the first statement in an AND statement is false, the second term is never evaluated because the truth statement is known. 

###### ASCII Table

![Ascii Table](http://www.asciitable.com/index/asciifull.gif)

Behind the scenes, characters are just small integers.  

If you want to convert characters to numerical offsets from the beginning of their block, you can take char - 'A' (which is the character you're looking at minus the character that defines the beginning of the group). This works because similar characters are grouped together. This lets you index the characters as if they were an array. 

###### C-Strings

Do not forget that strings require a null terminator to end them. This is implicit when you define it with "" and you need to allocate an extra character to hold it. 

Strings cannot be copied by setting a pointer equal to another string. Rather, loop through every value or use strcpy.

`strlen, sizeof, strcpy, strcat, and strcmp` are all in `#include <string.h>`

###### 2-D Arrays

Malloc a a row of pointers, then fill those pointers with address of first element of each column. If you do it like this, you have to free in the opposite order that you create them to ensure you don't lose the pointers to the column rows. 

```c
int ** grid = (int **) malloc(sizeof(int *) * NUM_ROWS);
for (int j = 0; j < NUM_COLS; j++) {
    grid[j] = (int *)malloc(sizeof(int) * c);
}
```

More standardly, you create them with `int grid [3][2]`

Indexing a 2D array is done with `grid[i][j]` an alternative way to do this is `(*(grid + i))[j]` which increments to desired row, then dereferences to get pointer to the corresponding column array. You can really commit to this by also doing this: `*((*(grid + i)) + j)` which increments to desired tow, then dereferences to get pointer to corresponding column array and increments to desired column and is then dereferenced to get the value there. 

You could also make a 2D array by making a 2D array that is ROWs times COLs in length, This then takes the form of one large block in memory and you have to be more creative with indexing. You could do this by indexing the `onedim[(N_COLS * j) + j]` 

###### Lifetime/Scope

Local variables live in the stack and are created and destroyed with stack frames. 

Static and Global variables live in a region of memory known as the data segment which is allocated when the program begins and destroyed upon its completion. 

Dynamically Allocated Memory lives in the heap where the user is responsible for allocating and freeing memory. 

###### Dynamic Memory Allocation

`int * arr = (int *) malloc(sizeof(int) * n);`

`int * arr = (int *) calloc(n, sizeof(int));`

`realloc` adjusts dynamically allocated memory's size. If needed, copies data from previously allocated memory and returns a pointer to the new first address of the memory block. 

###### Common Things On Exam

These things are very common for code writing questions:

> 1. Make a deep copy of an array of structs:
>
> This entails dynamically allocating pointers within the structs and copying elements within the struct itself. 
>
> 2. Allocation and Deallocation of Memory for a 2D array
>
> Just application of malloc and free, ensure done in proper order to free everything.
>
> 3. Identification of where memory leaks come from
>
> Just practice code reading look for absence of `free` statements
>
> 4. Making a dynamically-resizable array
>
> When the array reaches capacity, `realloc`

###### Pointer Arithmetic

Indexing an array `arr[i]` is equivalent to `*(arr + i)`

Doing this may lose your original pointer to the array. Use a dummy variable to increment.

###### Structs

They are passed by value

There are two ways to define them:

This first way is doing it as a struct. This is a pain though because you have to use the word struct before the name you gave the struct before.

```c
struct person {
    char * name;
    int age;
    bool isAwesome;
};

int main() {
    struct person ben;
    ben.name = "Ben";
    ben.age = 20;
    ben.isAwesome = false;
    
    return 0;
}
```

Alternatively, you can use typedef to define the struct as a type. Then you only have to use the name of the struct to create it. Think of this as creating an alias for the struct which you define after the curly brackets. You can probably still create a struct with the struct _person statement. 

```c
typedef struct _person {
    char * name;
    int age;
    bool isAwesome;
} Person;

int main() {
    Person ben;
    ben.name = "benjamin";
    ben.age = 20;
    ben.isAwesome = true;
}
```

It is very common to use pointers to structs defined elsewhere when passing them to functions so that the struct is actually manipulated rather than pointlessly doing it on a pass by value copy. The `->` operator takes care of the dereferencing.

Any pointer within the struct has to have memory allocated in addition to the memory allocated for the struct itself because the struct itself only has memory allocated for the pointer itself 8 bytes.

```c
struct person {
    char * name;
    int age;
    bool isAwesome;
};

int main() {
    struct person * p = malloc(sizeof(struct person)); //def struct mem
    p->age = 25;
    p->name = malloc(sizeof(char) * MAX_NAME_SIZE); //allocates name mem
    p->isAwesome = true;
    
    free(p->name); //free allocated array within struct first
    free(p) //then free struct memory
}
```

###### Promotion, Narrowing, and Casting

char < int < unsigned < long < float < double

In operations, generally the lower precedence operator is promoted to the higher precedence operator. 

Casting allows manual type changes.

###### Linked Lists

```c
typedef struct _node {
    char data;
    struct _node *next;
} Node;
```

A linked is just a bunch of nodes that point to other nodes or NULL. The beginning of the list is held by the head variable which holds the pointer to the first node in the list. 