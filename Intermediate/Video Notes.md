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

preincrementing has higher precedence than postincrementing. 

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