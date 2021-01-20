# Kernighan C Programming

*Benjamin Fry*

### Chapter 1

###### Introduction to C

Writing a hello world program:

```c
#include <stdio.h>
/* Write code in file.c. To run in bash use gcc file.c then run file.out */
main()
{
    printf("hello, world\n");
}
```

Notice that the printf line must terminate with a **semicolon**. C has functions and variables like python. The **main** function is special in that it is the function that will begin all C programs. All other programs will be called from main. The include line above tells the program to include the standard in and out library to print. When the function is defined it has **parentheses** where it takes in a list of arguments or nothing. The printf function doesn't have newlines so a bunch can be called in a row to print one line. Other than \n for newlines, there is \t for tabs, \b for backspace, and \ to escape "s. 



###### While Loop

Writing a Simple Fahrenheit, Celsius table using the below equation:
$$
^\circ{C} = \frac{5}{9}(^\circ F - 32)
$$

```c
main()
{
        /* Fahrenheit-Celcius table for Fahrenheit 0->300 */
        int fahr, celsius;
        int lower, upper, step;

        lower = 0; /* lower limit of scale */
        upper = 300; /* upper limit of scale */
        step = 20; /* step size */

        fahr = lower;
        while (fahr <= upper) {
                celsius = 5 * (fahr - 32) / 9;
                printf("%3d\t%6d\n", fahr, celsius);
                fahr = fahr + step;
        }
}
```

This program starts with a comment which is the same as block comments in CSS and javascript.  In C all variables need a **declaration** that sets them to a particular type. When they are declared, they aren't assigned a value only a type (and memory address?) The ***int*** type are 16-bit integers or whole numbers between +/- 32768. They could be set to the ***float*** type which are 32-bits and have *6 digits of precision*. 32-bit ints can be used if needed. ***char***s are single characters and thus only one byte. There are other types (long, short, double) as well. The **Assignment** statement is where the declared variables are given initial values. 

The while loop is the same syntax as javascript but if only one line can be indented without braces. Best practice to indent within braces. Rather than multiplying 5/9 by fahr-32, do the division step last because the division of integers in C will **truncate** the fractional part of 5/9 giving 0 and thus all Celsius values would have been zero.

The printf syntax is similar to other languages and uses the %d to print numbers, and %s for strings which can then be passed in for formatting in subsequent arguments.

We can change the *int* declarations to *float* declarations for more accurate conversions. Need to update the printf to use %f for floats. When acting on floats, operands convert the ints to floats as long as one of the things they act on is a float. Otherwise they perform integer arithmetic.



###### For Loop

Reimplementing the Celsius, Fahrenheit table using a for loop:

```c
#include <stdio.h>
main() {
    int fahr;
    for (fahr = 0; fahr <= 300; fahr = fahr + 20)
        printf('%3d %6.1f\n', fahr, (5.0/9.0) * (fahr - 32))
}
```

Pretty similar syntax to javascript.  No brackets needed if only one line (as with while loop.) For loops have three components in parentheses, the initialization, the evaluation performed each loop, and the increment step. 



###### Symbolic Constants

Can be used to define constants outside of functions. Generally given Uppercase names. Can be used in place of the number and used to improve readability. Just a way to define a constant in C. The #define line *is not ended with a semicolon.*

```c
#define LOWER 0 /* Lower limit of table */
#define UPPER 300 /* Upper limit of the table */
#define STEP 20 /* step size */

main() {
        int fahr;
        for(fahr=LOWER; fahr <= UPPER; fahr = fahr + STEP) {
                printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
        }
}
```



###### Character Input and Output

The standard library can read and write characters to files using something called ***Text Streams*** which are sequences in characters divided into lines. A single line from the text stream has 0 or more characters ended with \n. Two main functions for this are *getchar()* and *putchar()*. getchar() is used to get keyboard input. putchar(c) prints the integer c as a character. Putchar and printf can be used in the same program.

Application of **putchar() and getchar()**

```c
main(){
    char c;
    putchar(65);
    putchar(10);
    printf("Enter a character:\n");
    c = getchar();
    printf("the character you just typed was: %c \n", c);
}

/* Output: A \n Enter a character: \n *takes character* prints character \n */
```

**File Copying**

To read a file, use while loop to check each character for EOF indicator. When doing this we need the scanning variable to be an integer rather than a character because the EOF character returned by getchar() is very large to indicate it is not a character. The identity of the EOF character can value but it is not a valid char value. The below program can be used to copy a file to the stdout:

```c
/*This program can be used with "cat file.txt | ./a.out"*/
main() {
    int c;
    while ( (c = getchar()) != EOF )
        putchar(c);
}
```

The assignment of "c = getchar()" has to be done in parentheses because the != **takes precedence** to = and is evaluated first. The parentheses ensure that c is set before comparison.

**Character Counters**

Introduces a new operator for incrementation: *++var* adding the ++ tells the program to increment every loop. Similarly -- decrements by 1. The ++/-- can also go at the end of the variable name like in JS. Postfixing gives it a different meaning (chapter 2.)

```c
main(){
    long count;
    count = 0;
    while (getchar() != EOF)
            ++count;
    printf("%ld\n", count); /* %ld prints a long int */
    
    /* alternatively this would also work with For loop */
    for (count = 0; getchar() != EOF; ++count)
        ;
    printf("%ld\n", count)
}
```

We can use the lonely ; to terminate the for loop as a null statement with nothing going on inside of it. Alternative to longs we could use doubles which would store the numbers as floats. Long is a 64 bit integer type while double is a 64 bit float type.

According to the book, the for/while loop will do its test even if the file is empty so the count will not be incremented unless the file contains something. This leaves count as zero. While and for ensure that 0 length files are handled neatly.

**Line Counting**

Just scans characters for \n and increments count otherwise doesnt breaks on EOF.

```c
main() {
    int count, c;
    for (count = 0; (c = getchar()) != EOF; ++count ) {
        if (c != '\n')
            --count;
    }
    printf("%d", count);
}
```

A single character in ***Single Quotes*** represents the character's integer value. This is known as a character constant. Therefore, we convert the newline to 10 which getchar() will find at newlines. A while loop version of this is done in book. The if statement works liek java but like for and while we can exclude the brackets if only one line. We use == and != like in python to test equality.

Completed exercises 1.8, 1.9, 1.10 in *chap1.c*

**Word Counting**

In C there are evidently *no booleans* rather, 1 is used for True and 0 is used for False. It is best practice to use a symbolic constant to represent 1 and 0 with names. Works by starting with state variable set to OUT (False). If else block evaluated from top to bottom so if the previous character was not a space, newline, or tab and the previous state was OUT change the state to IN and increment the number of words. 

```c
#define IN 1 
#define OUT 0
void main() {
    int c, nw, state;
    state = OUT;
    nw = 0;
    
    while ((c = getchar()) != EOF) {
        if (c == ' ' || c == '\n' || c == '\t')
            state = OUT;
        else if (state == OUT) {
            state = IN;
            ++nw;
        }
    }
    printf("num words %d\n", nw);
}
```

In text they use this to also count characters and lines. All variables can be set equal to zero at one with ***nc = nw = nl = 0***  like in python. This is because equality is assigned from right to left. C uses || and && for compound logic like JavaScript.

Exercise 1-12 Completed in *chap1.c*



###### Arrays

```c
void main() {
    int c, i, nwhite, nother;
    int ndigit[10]; /* Initialize a length 10 array */
    for (i = 0; i < 10; ++i)
        ndigit[i] = 0; /* Fill the array with zeros */
    while ((c = getchar()) != EOF){
        if (c >= '0' && c <= '9') /* because 0 thru 9 are sequential in ascii characters check if between*/
            ++ndigit[c - '0']; /* since 0 is the lowest subtract that so that the array is zero indexed by ascii # */
    }
    printf("digits =");
    for (i=0; i<10; ++i)
        printf(" %d", ndigit[i]); /* Print the array */
    printf("\n");	
}
```

C arrays are 0 indexed like python. The conversion from the ascii digits to numerical indices works because all character sets are sequential. Because chars are integers corresponding to their ascii representation they can be subtracted. 



###### Functions

```c
/* Raise a number to a power with an a function */
int power(int base, int n) { /* return-type function-name(param-type param, ...) {return return-type} */
    int i, p;
    p = 1;
    for (i = 1; i <= n; ++i) {
        p = p * base;
    }
    return p;
}

int main() {
    printf("\n");
    printf("3 ^ 2 is: %d\n", power(3, 2));
    printf("\n");
	return 0;
}
```

The default return type of main is actually an int such that returning 0 indicates proper execition while any non-zero value indicates an error. gcc will warn you if *int* or *void* are not specified as the return type.

Example 1-15. completed in *chap1.c*



###### Call by Value - Arguments

Functions in c are ***call by value*** rather than ***call by reference*** so when you pass arguments to the function the arguments are copies of the original object that they get passed rather than the actual object that they're passed. The function makes a local copy of its arguments for use in the function. Python functions are call by reference. 

A function can be made call by reference using pointers as we will see later.

**Arrays are an exception** to this rule. The array that is passed into a function and is modified in the function is modified itself. A copy is not made of the array elements. 

```c
int power(int base, int n) {
    int p;
    for (p = 1; n > 0; --n)
        p = p * base;
    return p;
}
```

Because the function if call by value, when n is decremented, the variable was used to call power in the place of n will not be decremented. 



###### Character Arrays

There are no strings in C. Character arrays are used to hold lists of characters and are terminated by the null character '\0'. The following example will demonstrate these.

Ex: Prints a Character Array that holds longest line of input.

```c
#define MAXLINE 1000
int getaline(char s[], int lim) {
    int c, i;
    for (i = 0; i < lim-1 && (c=getchar()) != EOF && c != '\n'; ++i){
        s[i] = c;
    }
    if (c == '\n'){
        s[i] = c;
        ++i;
    }
    s[i] = '\0';
    return i;
}
```

The 'getaline' function reads one line of input into an array with a loop that is terminated when the index exceeds the maximum index of the array or when the end of the file is reached or when a newline is reached (only gets one line). 

If the line is the EOF, i is never incremented and therefore, getaline( ) returns 0. A single newline returns 1 and otherwise the length+1 is returned.

Essentially loops through the line and counts every character and newline at end. Puts each read character into the character array input (pass by reference) and returns the length of the line in the array (including newline). The character array is terminated by the null character '\0'. 

```c
void copy(char to[], char from[]){
    int i;
    i = 0;
    while ((to[i] = from[i]) != '\0')
        ++i;
}
```

The copy function loops through the from array and sets each index in ***to***[ ] equal to ***from***[ ] while the character the character being copied is not equal to '\0'. Despite breaking when the '\0' character appears, it is still copied into the to array.

```c
int main(){
    int len;
    int max;
    char line[MAXLINE];
    char longest[MAXLINE];
    max = 0;
    while ((len = getaline(line, MAXLINE)) > 0)
        if (len > max){
            max = len;
            copy(longest, line);
        }
    if (max > 0)
        printf("%s", longest);
    return 0;
}
```

For each iteration through While loop, set len = to the line length obtained from getaline() which returns 0 only at EOF. If len > max then sets max = to that length and copies the array **line**[ ] to **longest**[ ]. Then prints the line with the longest length by printing **longest[ ]** after reaching the EOF. 

Copy must be used because line[ ] is rewritten on each call of getaline().



###### External Variables and Scope

Variables defined within the scope of a function are known as **automatic variables** which come and go with function invocation. We can define variables similar to the global keyword in python. To do this, the variables are defined outside of the function similar to the symbolic constants discussed above. If you want to use one of these within a function, you have to mark it as coming externally as being an 'external' variable. The extern declaration makes sure the variable is not recreated as a local one.

```c
#define MAXLINE 1000
int i;
int a[MAXLINE];

void fillthearray() {
	extern int a[]; /* The extern declaration is unnecessary in this case */
	for (i = 0; i < MAXLINE; ++i) {
		a[i] = 7;
	}
}

int main() {
	int i;
	extern int a[]; /* The extern declaration is unnecessary in this case */
	fillthearray();
	for (i = 0; i < MAXLINE; ++i) {
		printf("%d", a[i]);
	}
	printf("\n");
}
```

 The **extern** keyword can be omitted if the definition of the variable comes before its declaration in functions contained within the same source file and thus can be omitted in this case. When multiple files are needed the variables and important functions for other use get collected in the *header* file. A #include statement is added at the top of files to bring its variables into the other programs' awareness. To indicate a header file, the file is ended with a *.h* suffix. 

If you want to define programs after main is defined, you have to declare them available before main. E.g. 

```c
int getline(void);
void copy(void);

int main() {
	getline();
    copy();
}

int getline(void) {
    /* code */
}

int copy(void) {
    /* code */
}
```

These examples would be written to act on global variables rather than on any arguments. We use the void keyword in the non-main function arguments which corresponds to an empty list. This is for compatibility with older c versions.

```c
int getaline(void);
void copy(void);

int main() {
	getaline();
	copy();
}

int getaline(void) {
	printf("get a line\n");
}

void copy(void) {
	printf("copy\n");
}
```

Some more nomenclature: 

A **definition** is the place in the code where the variable is created or assigned storage.

A **declaration** refers to places where the nature of the variable stated but no new storage is allocated. 