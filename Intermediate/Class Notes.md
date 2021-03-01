# Class Notes

*01/25/2021*

## Week 1

### Syllabus Review

###### Class Participation During Zoom Call: [slido](https://www.slido.com) `Password: jhuip01`

> Todo:	
>
> - [x] UGrad account by Friday
> - [x] GitHub account
>   - [x] create account
>   - [x] submit account info in form by noon Jan 27th
> - [x] command line bootcamp



###### Logistics:

Want to use the synchronous class time for interactive content while the lectures are offloaded to prerecorded, asynchronous lectures. 

Videos, slides, and exercises are posted asynchronously before class. We should do the preparation before coming to class. Class-time should be used for interactive learning such as asking questions about the asynchronous content and working on in-class exercises. 

###### Office Hours:

Dr. Hovemeyer - Tues and Thurs from 1-3pm or by Appointment

###### Course Objectives:

1. Learning to program in C and C++
2. Learning implementation to implement complex software systems
3. Working on larger projects. 
4. To become an expert programmer that can develop high quality software.
   * Short Term Laziness vs Long Term Laziness
     * Short Term bad code leads to long debugging times and ends up wasting more time that you can spend being lazy later.
5. Try to understand applicability of homework assignments 

###### Grading:

> 9% - Handwritten code understanding/reading homeworks
>
> 31% - Individual code writing assignments
>
> * Need to take these seriously as large portion of grade. **start early. Incremental progress is key.** No Code sharing or copying. 
> * Submit through Gradescope
>
> 14% - Midterm Coding Project C (team)
>
> 15% - Midterm exam
>
> 16% - Final Coding Project C++ (teams)
>
> 15% - Final Exam

In class exercises are not graded but are essential for understanding. They allow you to apply the lecture material as you learn it. Continue working on them outside of class if you don't finish and complete them all.

### Linux Basics

Linux is the OS we will use for the entire course. The Linux cli allows easy automation compared to other OS's. Reviewed Linux terminal commands. 



*01/27/2021*

### Recap Question Review

1. The first flag uses the '99 C standard, the others enable extra warnings. 

2. See Video Notes.

3. Undefined behavior is syntactically correct code that does not work in the way that you want. In other words, undefined behavior is when the program doesn't execute predictably.
   7. example: `i = i++;` post-incrementing into assignment. The increment doesn't take effect until after the statement has finished being called. 
      * This statement is problematic because the `i++`is a side effect which won't take place until reaching the semi-colon (sequence point). The assignment operator is also a side effect so we don't know whether the assignment will occur as intended. 
      * `printf("%d\n", x++);` would print the value of x. Then it would increment x.
   
4. `const` means make a variable read only. 
   
   * It is preferable to use `const `variables rather than preprocessor constants because there can be weird behavior using symbolic constants. It is personal preference though. 
   
5. Byte sizes in C aren't set by the C language. It varies by OS.
   * The data types must have at least certain sizes but the OS can provision them greater sizes. 
   * Usually modern compilers will use:
     * char - 1 byte
     * short - 2 bytes
     * int - 4 bytes
     * long - 4 (or 8 on a 64bit processor)
   
6. `7/2` would return 3 because integer division is performed if no float is passed to operands. `7.0/2.0` will produce 3.5



## Week 2

*02/01/2021*

###### `scanf` tips

```c
char c;
scanf("%c", &c); //could read a ' ' character
scanf(" %c", &c); //will skip whitespace and get first non-space char
```



*02/03/2021*

```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>

int main(void) {
    char a[] = 'Hello, world. This is some text.\n';
    int len = (int) strlen(a); //typecast output of strlen to int
    
    for (int i = 0; i<len; i++) {
        a[i] = toupper(a[i]);
    }
    printf("%s\n", a);
    return 0;
}
```

`int len = (int) strlen(a);` is a way to typecast. Takes the result returned by `strlen` and converts its type to `int` or whatever type specified.

Partial Solution to Ex2-1

```c
#include <stdio.h>

int main(void) {
	float sum, total_credits = 0;
	char grade;
	int count = 1;

	printf("Course %d: ", count);

	while (scanf(" %c", &grade) == 1) {
		float credits;
		scanf("%f", &credits); //fixme: should check return value
		//TODO: check grade
		count++;
		printf("course %f: ", &credits);
	}
	return 0;
}
```



## Week 3

*02/08/2021*

### Array Recap

You can get the size of an array of ints with `sizeof(arr)/sizeof(int)`. However, if we called the `sizeof()` an array that was passed into a function call, we would get the `sizeof()` the pointer!  This is not useful so best practice is to pass the size of the array as a separate argument to the array. 



*02/10/2021*

### Makefile, Header Guard, and Compilation Recap Questions

##### Why do we need header guards?

Prevents double declarations from confusing the compiler. A header file contains declarations. If there are multiple declarations, for the same thing, the compiler might get confused. We only want declarations to appear once in the overall source code. So, the header guard tells the compiler to ignore the declaration if it is already aware of the declaration. 

Header guards ensure that the header files are **idempotent** or that the code is only used once or not at all. 

##### What is the difference between compiling and linking?

Compilation takes `.c` files and converts them to `.o` files which are object files. 

Linking combines the object files into a single executable



##### What compiler flag is used to create object files and what extension do those files have?

We use the `gcc -c` flag to prevent `gcc` from performing the linking step. It only creates the `.o` files. 



##### What is a `target` in a Makefile?

A target is a file that can be "built". When you run `make command` the command that is specified in the Makefile is the target



##### Why use Makefiles?

Makefiles automate the compilation and linking process and ensure that only the files that have changed will be recompiled which saves compilation time in large processes. 



### Review of Binary Search Algorithm

Binary search works by dividing a sorted list in half, sampling the middle value, then if that value is less than the target recursively calls itself on the lower half of the list and if it is greater than the target, does the same with the larger half of the list. It does this until the target is found or the range becomes empty.



### Makefile Example

`rev_str` could take first and last character, then recursively swap next two characters in string. 

```c
//in revstr.h
void rev_str(char str[], int start, int end){
    return;
}

//in main.c
int main(){
    char str[] = "Hello";
    rev_str(str);
    return 0;
}
```

```c
//in recursion.h
#ifndef RECURSION_H
#define RECURSION_H

void rev_str(char str[], int start, int end);

#endif
```

```makefile
CC=gcc
CFLAGS=-g -Wall -Wextra -pedantic -std=c99

recursion: main.o recursion.o
	$(CC) -o recursion main.o recursion.o
	
main.o: main.c recursion.h
	$(CC) $(CFLAGS) -c main.c
	
recursion.o:
	$(CC) $(CFLAGS) -c recursion.c
	
clean:
	rm -f recursion *.o
```



*02/12/2021*

### Multidimensional Array and GDB Recap Questions

#### How do you declare a multidimensional array and pass it to a function?

```c
// Declare the array
float grid[4][10]; //array with 4 rows and 10 columns.

printf("%f", grid[3][4]); // prints the value stored in the 4th row and 5th column
```

When passing a multidimensional array to a function, you have to pass the size of each dimension except the first one. 

```c
void foo(float grid[][10], int rowNum){
    //do stuff
}
```

C lets you not specify the first dimension so that the length can vary in only that first dimension. The function will handle arrays of whatever length but the elements inside the array must have a consistent length. 

#### To initialize a multidimensional array with Array Initialization

Think about a 2D array as an array of 1D arrays

```
int grid[2][3] = {{1,2,3},{3,4,5}};
```



#### What is the compile flag for debugging with GDB

`gcc ... -g file.c` for any development purposes, we want to use the -g flag. Professor says that we should just always include this flag in our make file. We only wouldn't want to include this flag if we were shipping the executable for production purposes. 



#### Setting Break Points in GDB

A useful way to use breaks, is to set breakpoints at the name of the function. 

`break function_name` 

You can also break on a line number of a given source file like in:

`break main.c : 12` will break on line 12 in the file main.c

If you don't want to step through a region of code, you can set another break point at the desired location to resume control at with the same `break` syntax. You can use the `continue` keyword to allow execution to resume until the next breakpoint.



## Week 4

*02/15/20*

### Pointer Recap Questions

What is a pointer? Well a pointer value is a memory address pointer variable. Memory is a big array of bytes. The array is indexable with addresses. The value of a pointer is literally just one of the memory addresses that describes the position of something in memory. This allows us to pass the reference and value to that something around without creating extraneous variables. 



*2/17/20*

### Memory Allocation Recap Questions

We think about the stack as holding local variables. Stack variables have names and are commonly function parameters and are anything not assigned with `malloc` or `calloc`. Recall the diagram of the stack. When a function returns, the variables disappear. Stack memory is automatically allocated and deallocated. Heap memory must be manually allocated and explicitly deallocated. Java and Python are garbage collected. They both have heap memory, but the garbage collector can determine when objects like classes are no longer needed by the program. 