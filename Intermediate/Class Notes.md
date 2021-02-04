# Class Notes

*01/25/2021*

## Week 1

### Syllabus Review

###### Class Participation During Zoom Call: [slido.com]() `Password: jhuip01`

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

