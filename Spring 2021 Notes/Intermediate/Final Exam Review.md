# C++ Final Exam

##### Benjamin Fry

### Transitioning To C++ From C

`int`, `char`, `float`, `double`,  `pointer`, and `bool ` are default types. More types can be  `include`-ed once imported from STL. Operators, control structures, functions, pass by address and value all work the same as in C. 

To compile a C++ file we use `g++ std=c++11 -pedantic -Wall -Wextra -c file.cpp` to generate `file.o` which we then link using `g++ file.o -o file` to generate the `file` executable.

To print  to standard out, we do the following:

```c++
#include <iostream>
using std::cout;
using std::endl;
int main()  {
	cout << "printing"  << endl;
	return 0
}
```

###### Namespaces

When you gave two things the same name in C you could get errors but might also get undefined behavior. In C++, namespaces are used  to  ensure that items with the same name can get along without error.

The `using` keyword sets the namespace you specify as the default way to handle that name. For example `using std::cout` tells us to look in the STL for `cout` rather than anywhere else. If you had another `cout` function, you would need to use `other_namespace::cout`  wherever you wanted to use that alternative implementation.

###### Text IO

As we mentioned `std::cout`  is used to write to console and `std::endl` terminates lines. The `<<` operator is the insert operator and allows chaining of many inserts without going to a new line until `endl`. 

We can actually import any c library by using `#include <cstdio>` (attach prefix `c`) and you will have access to `printf`.

To collection input, we use `std::cin` with the extraction operator `>>` which when combined, reads standard input one word at a time where a word is any text character separated by white space.

```c++
while(cin >> word) {
    cout << word << endl;
}
```

###### Strings

In C++, strings are objects. To use them, we `#include <string>` and use `std::string` to access aspects of the string. 

```c++
string s1 = "world"; //same as C
string s2("hello"); //calls the string constructor
string s3(3, "a"); //replicates "a" 3 times
string s4; //empty string
string s5(s2); //copies s2 into s5.```
```

Strings in C++ are dynamically allocated on the heap by default. Thus, they can be arbitrarily long. We have the following methods available as well:

`s.size()` prints the number of characters in the string. returns an **unsigned int** called `size_t`

`s.capacity()` returns the number of bytes allocated for the string

`s.substr(offset, howmany)` gives a substring starting at offset for `howmany` characters

`s.c_str()` returns a c-style array of characters. You can then use C library functions like `strlen` on this as a normal character array.

`s.at(5)` returns the 6^th^ element of the string, but unlike `s[5]` **does a bounds check to ensure that the address is not out of bounds**! This will help avoid undefined behavior and thus should be the default for indexing. 

### STL - Objects

This is a built-in library which contains useful data structures and algorithms in C++.

Allows us to define templates which allow writing objects and functions that can handle input of any type. They are used as follows:

```C++
template<typename T>
struct Node {
    T payload; //T is used as a type placeholder
    Node *next;
}

template<typename T>
void print_list(Node<T> * head) {
    Node<T> * cur = head;
    while (cur != NULL) {// NULL is the null pointer in C++
        cout << cur->payload << " ";
        cur = cur->next;
    }
    cout << endl;
}
```

Once  we've defined a struct with a generic type we can then instantiate it like so:

```C++
    Node<float> f3 = {95.1f, NULL};
    Node<float> f2 = {48.7f, &f3}; //& works as in C to get address
    Node<float> f1 = {24.3f, &f2};
    print_list(&f1);
    
    Node<int> i2 = {239, NULL};
    Node<int> i1 = {114, &i2};
    print_list(&i1);
```

###### Vectors

A vector is a built-in type in STL. It takes a generic type and acts like a C array, but the main difference is that arrays are fixed length while vectors automatically allocate and deallocate memory as elements are pushed and removed. Similar to string indexing, we can use the `.at()` method to avoid indexing out of bounds. 

To declare a vector you need to supply the type for the template - `std::vector<std::string> names` creates a vector of strings. 

To add elements to the end of a vector we use the `.push_back(data_type)` function.

We also have access to `.size()` which gives the length of the vector, `.front()` which  gives the first element of the vector, and `.back()` which gives the last element of the vector. 

We can use **iterators** to loop through the elements of a vector rather than for loop with numerical indexing as these handle length changes better. To do this:

```c++
for(std::vector<std::string>::iterator it = names.begin(); it != names.end(); ++it) {
    std::cout << *it << std::endl;
}
```

where an iterator `it` pretty much behaves like a pointer but also allow decrementation unlike C pointers. 



Other built-in data structures include:

`set` - mathematical set where elements may only appear once

`list` - a linked list

`map` - associative list or dictionary

`stack` - last-in first out data structure (LIFO)

`deque` - double-ended queue, flexible combo of LIFO/FIFO

###### Maps

Maps are similar to python dictionaries. They are collections of key-value pairs where the value is any arbitrary type and the key is any type that can be used in binary comparison such as numeric types, `std::string` which is sorted alphabetically, and any custom class that has the `<` operator overloaded. This is because, maps are always sorted by key. Thus, when you iterate through them, it will print in ascending order.

Map keys are one to one. One key is linked to exactly one value. 

To define a map, define the template types: `std::map<int, std::string> mymap`. 

We can use `.size()` method to get the number of keys in the map.  To check if a given key is found in a map, we can use the `.find()` function like so:

```c++
if (mymap.find(10) != mymap.end()) {
    std::cout << "found it" << std::endl;
} else {
    std::cout << "didnt find it" << std::endl;
}
```

where the `.end()` operator is the iterator one past the end of the map. We can also use iterators when we need to loop through all the elements and get access to both the keys and values:

```c++
for (map<int, string>::iterator it = mymap.begin(); it != mymap.end(); ++it) {
    std::cout << it->first << ": " << it->second << std::endl;
}
```

we can dereference the `it` iterator for `first`  and `second` because each element of a map is a `pair` which is its own object that has a `first` and `second` element.

###### Pairs and Tuples

Pairs are used as elements in maps. We can also take advantage of them when we need to return two values from a function. 

```c++
pair<int, int> divmod(int a, int b) {
    return std::make_pair(a/b, a%b);
}
int main() {
    std::pair<int, int> = divmod(10, 5);
    std::cout << "first: " << test->first << std::endl; //dereference to access elmnts
    std::cout << "second: " << test->second << std::endl;
}
```

We can also compare pairs using `<` and other operators. Compares the first elements of the two and then the second element. For example `make_pair(2,3) < make_pair(3,2)`

There are also tuples which can return as many elements as you want. You have to `#include tuple` and use a similar syntax as for maps.

```c++
tuple<int, int, float> divmod(int a, int b) {
    return make_tuple(a/b, a%b, (float) a/b);
}
```

rather than having to use the `tuple->first` syntax to get each element of the tuple, you can use the `get<N>(tuple_name)` function which returns the `N`th element of the tuple.

###### The *typedef* Keyword

We can use `typedef` to avoid having to keep writing out very long prefixes such as when you need to repeatedly call iterators:

```c++
typedef map<int, std::string> TMap;
typedef TMap::iterator TMapItr;

typedef vector<int>::iterator TItr;
void prefix_sum(TItr begin, TItr end) {//.begin() and .end() iterators
    int sum = 0;
    for (TItr it = begin; it != end; ++it) {
        *it += sum;
        sum += *it;
    }
}
```

where `prefix_sum` converts the vector to a cumulative sum vector.

###### Types of Iterators

We also have access to iterators which cannot change the elements of the object we are looping through as well as iterators that work backwards through the elements of the object.

A `const_iterator` works exactly the same but does not allow modifications to the elements of the object the iterator operates on. Reassignment of `*it` is forbidden. The iterator is started with `.cbegin()` and ended with `.cend()`

`reverse_iterator`s work by starting at the end of the object and working to the beginning. The iterator is started with `.rbegin()` and ended with `.rend()`

`const_reverse_iterator`s do both. They are started with`.crbegin()` and end with `.crend()`.

###  STL - Algorithms

 To use the built-in STL algorithms, you can `#include algorithm`. A common algorithm to import is the `sort`.

```c++
#include algorithm
int main() {
    vector<float> grades;
    algorithm::sort(grades.begin(), grades.end());
    std::cout << "Median Grade was " << grades.at(grades.size() / 2) << std::endl;
}
```

Another, common algorithm is the `find` algorithm which searches a vector for an element:

```c++
int arr[] = {1,  20, -2, 4};
int * p;
p = std::find(arr, arr+4, 30); //arrays dont have .begin and .end
if (p != arr + 4) {
    //30 was found
} else {
    //30 was not found
}
```

Another common algorithm is the `count` algorithm which counts the frequency of a given element in an array:

```c++
int arr[] = {10, 20, 30, 30, 20, 10, 10, 20};
int mycount = std::count (arr, arr + 8, 10);
cout << "10 appears " << mycount << " times in arr.\n";
//To use with a vector
std::vector<int> vec (arr, arr + 8);
mycount = std::count (vec.begin(), vec.end(), 20);
cout << "20 appears " << mycount << " times in vec.\n";
```

Another one is `is_permutation`  which tells you if  two vectors are permutations of the same set.

```c++
int main() {
    array<int, 5> foo = {1, 2, 3, 4, 5};
    array<int, 5> bar = {3, 1, 4, 5, 2};
    if (std::is_permutation (foo.begin(), foo.end(), bar.begin()) )
        cout << "foo and bar contain the same elements." << \n;
    return 0;
}
```

### File I/O

We can also use the `#include iostream` library to do File IO. An `fstream` object is the parent class of `ofstream` and `ifstream` which are used to output to and read from a file respectively. We do so using the extraction and insertion operators respectively. 

To write to a file:

```c++
#include <iostream>
#inclide <fstream>

int main(){
    std::ofstream ofile("hello.txt"); //creates hello.txt in ofile for writing.
    ofile << "hello!" << std::endl;
}
```

To read from a file:

```c++
std::ifstream ifile("hello.txt");
std::string word;
while(ifile >> word) {
    std::cout << word << std::endl;
}
```

To open a file for both reading and writing:

```c++
const std::ios::openmode mode = std::ios_base::in | std::std::ios_base::out
    	| std::stream::ios_base::app;
std::fstream fs;
fs.open("hello.txt", mode);
fs << "hello CS 220" << std::endl;
fs.clear(); //clear error state
fs.seekg(0); //reset file stream to beginning of file
```

the function `fs.clear` above clears all the error flags so that further operations can be done without exiting the program. You would want to use this in an if statement that is checking for error states, alert the user, then clear to try to recover the program. 

We can use `stringstream`s  to read or write to a temporary 'file' which can then be printed or written once it is processed to our liking. We can treat `stringstream` objects just like a string but we can use read functions on them. If you want one only for reading from you can use `istringstream` and if you want one only for writing you can use `ostringstream`. 

`stringstream` objects can be converted to strings with the `.str()` function. 

When looking at these stream objects, the base class for all is the `ios`. `istream` and `ostream` inherit from this. `ifstream` inherits from `istream` and `ofstream` inherits from `ostream`. `iostream` inherits from both. The `>>` is defined for all input streams and the `<<` operator is defined for all output streams. Since `fstream` and `stringstream` both inherit from `iostream` both operators are defined.

### References

C++ has special objects called references which work similarly to pointers. A reference is a variable that acts as an alias for an existing variable or memory location. This allows two names to exist which simultaneously refer to the same memory location. References are safer than pointers as they can never be `NULL` as they must be defined immediately once declared. Once the alias is set to a variable, it can't be set to be an alias for another variable later.

To declare a reference to an integer, we use the `&` operator in the declaration. Such as

```C++
int a = 5;
int & b = a; //sets b to be an alias for a
int * c = &a; //sets c to the memory address of a
```

The true value of the reference is when we are using them as function parameters.

```c++
void swap(int &a, int &b) {
    int tmp = a;
    a = b;
    b = tmp;
}
```

which allows us to actually change the value of `a` and `b` in the place where they were passed to the `swap` function. 

The use of references is preferred to pointers because they are safe. A confusing part about using references is that you won't know whether a variable is a reference unless you can check the function implementation. 

A reference can also be returned like a pointer. This is especially useful if you want to return an object as you passed it into the function without making a copy and returning that. 

You can make a reference `const` which will prevent changing the that variable through the reference while using it in the function despite the original variable not being `const`. When passing a `const` reference to a function, you can save memory especially if the reference object is very large as you don't have to make a copy.

### Dynamic Memory Allocation in C++

`new` is the C++ equivalent of `malloc` and `delete` is the C++ equivalent of `free`. The `new` keyword calls the appropriate constructor if the object being created is a class. The `delete` keyword will trigger the destructor. Neither function requires parentheses. 

`new TYPE[N]` is a separate keyword which allows you to allocate a block of memory of N objects of the TYPE class. If we were to do `T * fresh = new T[n]` we would then free this memory with `delete[] fresh`.

### Classes

###### Defining a Class with Methods

Classes are like C structs but can have member functions within them. The general class syntax is as follows:

```c++
class Rectangle {
    public:
    	double width;
    	double height;
    
    	void print() const { //trailing const indicates won't modify object fields
            std::cout << "width=" << width << ", height=" << height << std::endl;
        }
    	void area() const {
            return width * height;
        }
}; //don't forget trailing semicolon
int main() {
    Rectangle r = {30.0, 40.0} //defined without a constructor.
}
```

It is best practice to put the implementation of a class in a `.h` file which can be imported as needed. Functions can be implemented in the header but usually only if it can be done in a one-liner.

We can then implement the member functions in the `classname.cpp` file in which we need to specify the namespace for all of our implementations with `Classname::functions(){}`

An example header file:

```c++
//rectangle.h
#ifndef RECTANGLE_H //header guard
#define RECTANGLE_H

class Rectangle {
    ...
    double getHeight() const {
        return height;
    }
    double area() const {
        //short function definition;
        return width * height;
    }
    ...
};
#endif

//rectangle.cpp
double Rectangle::getHeight() const { //specifies the namespace to define method
    return height;
}
```

###### Private vs Public Members

Everything in a C++ class is `private` by default unless marked otherwise. It is best practice to set the member fields as being private so only functions we explicitly allow can alter them. A `public` member function or field can be accessed freely by any code with access to the class definition (eg. imports the `.h` file). A `private` field or method can only be accessed by other member functions and variables in the object itself. Nothing outside the class definition can access these variables.

###### Constructors

You cannot initialize class fields where they are defined. Rather you use a **constructor** method which can do this with default variables or with passed in variables. Initializing a field where it is defined is only allowed for `static` variables which if you recall from C retain their value across scopes including object creation and destruction.

To define a constructor, simply define function with the same name as the class it is in. A function that does not require any arguments (can be empty parentheses or had default parameters) is a default constructor. If a default constructor is not specified, the compiler will create one for you but it will not set member types to any values. It will simply call their default constructors if applicable.

The `new` keyword calls the constructor for an object when no arguments are supplied or when they are used in an array or vector of objects.

When we define a constructor (even a non-default constructor), the compiler does not define a default constructor for us. Thus, an error will be thrown if you need a default constructor and didn't define one.

```c++
class Rectangle {
  public:
    Rectangle(): width(0.0), height(0.0) { ... }
  private:
    double width, height;
};
```

the above code block defines a default constructor which uses **initializer-list** syntax to set `width` and `height` to `0.0`. The initializer list syntax allows the constructor to define `const` and `reference` variables that would otherwise not be able to be defined with equality operators within the constructor function body. More complicated initializations can be handled in the function body though.

Non-Default Constructors are constructors that can take parameters. We can do this with (or without) default parameters which can actually be used in any function in C++.

```c++
class DefaultSeven {
public:
    DefaultSeven(int initial = 7; double val = 0.5): i(initial), v(val) {}
private:
    int i;
    double v;
};
int main() {
    DefaultSeven one(10, 20), two(5), three; //Each uses different parameters
}
```

variable names in C++ classes are scoped. When a member function has a parameter with the same name as a field in the class, the local variable will take priority over the class-scope one. In this instance, you can use `this->field_name` to get access to the class field. It is generally best to just avoid ever having to use the `this` keyword though. `this` is a pointer to the object's variables. 

###### Arrays of Objects

We can declare arrays of our custom types. This will call the default constructor on every element that we create unless you explicitly specify parameters for each element with list-initialization. Such as with `mything s[10] = {{1},{2},{3},{4},{5},{6},{7},{8},{9},{10}}`.

An alternative to this is to use a vector with the `reserve()` and `emplace_back()` function:

```c++
std::vector<my_thing> s;
s.reserve(10); //creates an empty vector with 10 my_thing worth of space
for (int i = 0; i < 10; i++) {
    s.emplace_back(i);//initializes a new my_thing with parameter i
}
```

where the argument of `emplace_back` is the parameter to initialize each `my_thing` with.

###### Destructors

When we dynamically allocate memory in a constructor, we can use a **destructor** to deallocate that memory before the object is destroyed upon going out of scope or program completion. 

We need to remember to use `delete[]` with the trailing braces to indicate that you want to call the destructor on each of the elements within the array.

To define a destructor we just use the name of the class with a `~` prefix, for example:

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

###### Copy Constructor

A copy constructor takes in an object and defines how to make a copy of it. By default the compiler will create a shallow copy where it will simply do a field by field copy including potentially `delete`-ed memory addresses. Thus, you probably need to explicitly define a copy constructor when your class relies on dynamically allocated memory. 

```C++
Rational(const Rational& original) {...}
```

### Operator and Function Overloading

###### Function Overloading

We can write functions that have the same name but take different arguments. Then when you call that function, the compiler will check which parameters you supplied and perform the appropriate task. 

```c++
void output_type(int) {cout << "int" << endl;}
void output_type(float) {cout << "float" << endl;}

int main() {
    output_type(1);
    output_type(1.0f);
}
```

You can also supply default parameters to functions to handle even more input variations. This requires that the functions with the same name have **different return types**. (exception might be char vs int since a char can be cast to an int?)

###### Operator Overloading

The operators `+` and `<<` are just functions that take arguments but are called without parentheses. Operator overloading boils down to function overloading. The new definition you give an operator should be intuitive.

To overload an operator, generally check the operator's documentation to see its inputs and return type and then define a new function called `operatorS` where `S` is the symbol for the operator you want to overload. 

```c++
std::ostream& operator<<(std::ostream& os, const std::vector<int>& vec) {
    for (std::vector<int>::const_iterator it = vec.cbegin(); it != vec.cend(); ++it) {
        os << *it << ' ';
    }
}
int main() {
    std::vector<int> vec = {1,2,3}
    std::cout << vec << std::endl;
}
```

Generally, the inputs should be `const references` unless you are changing and returning them. 

When you overload an operator within a class, you don't need to define two parameters as inputs as the function will have access to the member fields. For example if you have a rational class:

```C++
Rational Rational::operator+(const Rational & right) const {
    ...
}
```

you could then access `numerator` and `denominator` of the current object and add those of the `right` object. You would then return a new Rational.

The trailing `const` indicates that the `this` object's parameters aren't changed by the actions of the function. We don't have to create a reference to a new Rational to return in this case because the **copy constructor** will be called on the returned object once the stack frame dies and a new equivalent object will be created where the function is called. 

The `friend` keyword is used when you want to overload a function within a class definition file, but the first argument of the overloaded function is not a member of the class which would normally be passed in implicitly:

```c++
friend ostream & operator<<(ostream& os, const Rational & r);
```

this gives the function member-function-like status where the function can have access to the private fields of the class objects passed in as parameters.

### Initialization and Assignment Operators

There is a difference between types of `=` by the context in which we use it. 

Initialization is used when we define the variable and assign it at the same time `int a = 1` where `=` is acting in its initialization context. 

Assignment is used when we set one variable equal to another variable. 

```c++
class Complex{
public:
    Complex() : real(0.0), imag(0.0) {} //Default constructor
    Complex(double r, double i) : real(r), imag(i) {}//Non-default constructor
    Complex(const Complex & c) : real(c.real), imag(c.imag) {}//Copy constructor
    Complex & operator=(const Complex& rhs) { //Assignment Operator
        real = rhs.real;
        imag = rhs.imag;
        return *this;
    }
private:
    double real, imag
};
int main() {
    Complex c; //calls default constructor
    Complex c2 = {4.9, 0.5}; //calls non-default constructor
    Complex c3 = c; //calls copy constructor because initializing with =
    c3 = c2; //calls assignment operator because both already exist
}
```

### The Rule of 3

Whenever you need to create a **non-trivial destructor** such as calling a `delete` function, you need to also define a **copy constructor** and an **assignment operator** to avoid creating memory leaks from the creation of shallow copies that copy old memory addresses. 

To define a copy constructor that makes a deep copy, it may take the form of something like this:

```c++
Image(const Image& o) : nrow(o.nrow), ncol(o.ncol) {
    image = new char[nrow * ncol];
    for (int i=0; i < nrow*ncol; i++)
        image[i] = o.image[i];
}
```

To define an assignment operator, it might look like this:

```c++
Image& operator=(const Image& o) {
    delete[] image; //delete whatever was previously dyn. alloc in the object
    nrow = o.nrow;  //copy over all the elements from other object
    ncol = o.ncol;
    image = new char[nrow*ncol]; //allocate new memory and fill with other object's info
    for(int i=0; i<nrow*ncol; i++) {
        image[i] = o.image[i];
    }
    return *this; //allows chaining?
}
```

### Templates

###### Template Functions

We can use templates to create functions that can handle many types at once.

```c++
template<typename T>
void fun(const T& input) {...}
```

where the compiler will create the appropriate function when it is called. It is best to use template functions  when the logic to handle the different types is pretty much the same between functions. Otherwise, you should use function overloading to define different ways to handle each parameter type.

`template<typename T>` and `template<class T>` are interchangeable.

###### Template Classes

Suppose you want to define a class that can handle different field types:

```c++
template<typename T>
class Node {
public:
    Node(T pay, Node<T> *nxt) : payload(pay), next(nxt) {}
    void print() const {
        const Node<T> *cur = this;
        while (cur != NULL) {
            std::cout << cur->payload << ' ';
            cur = cur->next;
        }
    }
private:
    T payload;
    Node<T> * next;
}
```

**you cant define a template class in a `.h` file** because the compiler will only create template functions after we call the function with a parameter and the compiler gets confused when we define the class in a `.h` file and implement it in a separate `.cpp` file. To resolve this issue, we put the entire function implementation in the `.h` file OR implement the function methods in a different file type like a `.inc` or `.inl` file. We can then add a `#include "node.inc"` statement at the top of the file we need it in, or put the include statement at the **bottom of the header file** we have the function definitions in to avoid having to remember this. 

### Class Inheritance

Inheritance is an "is-a" relationship where composition is a "has-a" relationship:

```c++
class BaseClass {
    //Definitions for Base Class
};
class DerivedClass : public BaseClass {
	//Definitions for Derived Class  
};
```

in the above example `DerivedClass` inherits from `BaseClass` through `public` inheritance. This gives `DerivedClass` access to the fields and member functions of the `BaseClass` which is generally what you want if you are using inheritance. The default inheritance type is `private` and you also have `protected` as an option. 

###### Access Modifiers

`public`, `protected`, and `private`.

`protected` fields and functions can only be accessed from member functions of their class or member functions of derived classes. `public` and `protected` members marked public or protected can be accessed from member functions defined in the derived classes. `private` members cannot be accessed from member functions defined in the derived class.  

Constructors and assignment operators are not inherited from base class to derived class. Derived classes cannot delete the things that they inherit and cannot pick and choose what things they inherit. 

Derived classes can overload inherited member functions with altered functionality.

```c++
class Account { //Base Class
    public:
    	Account() : balance(0.0) { }
    	Account(double initial) : balance(initial) { }
    	void credit(double amt) 	{ balance += amt; }
    	void debit(double amt) 		{ balance -= amt; }
    	double get_balance() const	{ return balance; }
    private:
    	double balance;
};
class CheckingAccount : public Account { //Derived Class
    public:
    //derived class does not inherit the base class constructor, you need to call the base class constructor to initialize the inherited data fields
    	CheckingAccount(double initial, double atm) : 
    		Account(initial), total_fees(0.0), atm_fee(atm) { }
    
    	void cash_withdrawl(double amt) {
            total_fees += atm_fee;
            debit(amt + atm_fee);
        }
    	double get_total_fees() const { return total_feses; }
    private:
    	double total_fees;
    	double atm_fee;
};
```

the base class constructor must be the first call in the derived class' constructor's initializer list. 

The destructor for the base class is called after a destructor for the derived class is called. This results in a chain of destructor calls when using multi-level inheritance.

While constructors are called from base class to derived class, destructors are called from derived class to base class. 

### Polymorphism

We can use functions that are defined to take in a base class as its parameter with a derived class as its argument. Because a `CheckingAccount` is still an `Account`, we can pass a `CheckingAccount` to a function defined to work with an `Account`. 

The problem with this is that if you have overloaded any of the functions in the derived class, if the function that `CheckingAccount` has been passed to in place of `Account` will not know to call the derived class' implementations of those functions. Think of this as the program casting the derived class to the base class in this case and only being aware of the base class' function implementations. 

We can get around this problem with **dynamic binding** which is the key to polymorphism like this. This makes use of the `virtual` keyword which we just prepend to the member function we want to use differently when passed as a base class argument. The virtual keyword tells the compiler to look if we have replaced the base class implementation in the derived class.

```C++
class Account {
public:
    ...
    virtual std::string type() const { return "Account"; }
    ...
};
class CheckingAccount {
public:
    ...
    std::string type() const { return "CheckingAccount"; }
	...
};
```

the derived class does not also need the virtual keyword.

We can now pass `CheckingAccount` to a function such as:

```c++
void print_account_type(const Account& acct) {
    std::cout << acct.type() << std::endl;
}
```

and the correct type is returned. However, this only works because the **account argument is passed by reference**. If we passed the account argument by value, the copy constructor would have cast the input to a new temporary `Account` variable and we would not get the desired result. 

###### More on Dynamic Dispatch

How does the `virtual` keyword work? When you use the `virtual` keyword, a virtual table is created which holds type information about the object and the address of the member function that should be called. The virtual table is created in the base class and allows the overriding of functions by derived classes because it keeps track  of the class type that created it. 

When using this, you may have trouble finding mismatched parameters. The `virtual` keyword requires that everything about the two functions being overridden are the same but you won't get a compiler error unless you add the `override` keyword to indicate to the compiler what you're trying to do. Only then will the compiler inform you about something like mismatched trailing `const`s and easy mistakes like this.  

###### Function Hiding

When functions have the same name but different parameters without using the `virtual` keyword between the base class and derived classes, if you call the function on an instance of the derived class, you will get the derived class version. If you call that function on an instance of the base class, you will get the base class version. 

When you add the `virtual` keyword, you need to have exactly the same parameters, return type, and declarations otherwise the compiler hides the base class function from being accessed through the derived class. 

```c++
class Base {
    public:
    virtual void func(int i, int j) const {std::cout << "Base " << i << " " << j << std::endl; }
};

class Derived : public Base {
    public:
    void func(char c) const {std::cout << "Derived " << c << std::endl; }
    void func(int i, int j) const override {std::cout << "Derived " << i << " " << j << std::endl; }
};

int main() {
    Derived d;
    d.fun(76, 77); //calls two-parameter derived class implementation
    d.Base::fun(76, 77); //explicitly calls base class implementation
    ((Base &) d).fun(76, 77); //passes as reference thru base class to call derived impl.
    ((Base) d).fun(76, 77); //copies to base class to call base implementation
    return 0;
}
```

### Abstract Classes

Abstract classes are classes that are composed only of `virtual` functions:

```c++
class Shape {
    public:
    	virtual double size() const = 0; //the =0 makes it a pure function
    	...
};
class Shape2D : public Shape {};

class Circle : public Shape2D {
    public:
    	Circle(double r) : Shape2D(), r(r) {}
    	double size() const { return 3.14*r*r; } //need to define the size function definied in shape
    private:
    	double r;
};
```

Implementing an abstract class deliberately leaves the implementations of all functions to derived classes. The `= 0` is like setting the address of the function to the null pointer. 

You cannot create an object that is an abstract class itself. It has to be created from a class that inherits from the abstract class and has its functions defined. 

In the example above, `Circle` can only be instantiated because it has a defined `.size()` function. 

Another way to make a class abstract is to make the constructor `protected`:

```c++
class Piece {
    public:
    	...
    protected:
    	Piece(bool is_white) : is_white(is_white) {}
    	...
    private:
    	bool is_white;
};

class Queen: public Piece {
    ...
    Queen( bool is_white ) : Piece(is_white) {}
    ...
};
```

while we can have pointers and references to abstract classes, we can not directly instantiate them. A class that inherits from an abstract class will also itself be abstract if it does not override all of the virtual functions. 

###### Virtual Destructors

Since destructors behave just like functions, if you were to pass a derived class by reference to a function that causes its destruction, the base class destructor would be called in place of the derived class destructor. To get around this, we can use the `virtual` keyword to allow the derived class destructor to override the base class destructor:

```c++
class Base {
    public:
    	Base() : base_memory(new char[1000]) {}
    	virtual ~Base() {delete[] base_memory; }
    private:
    	char *base_memory;
};
class Derived : public Base {
    public:
    	Derived() : Base(), derived_memory(new char[1000]) {}
    	virtual ~Derived() { delete[] derived_memory; }
    private:
    	char *derived_memory;
};
```

for any class that relies on a destructor working properly and implements a virtual member function's definition **should also have a virtual destructor**.

### Object Oriented Design

If you can say A is a B, then A is the derived class of the parent class B and in other words, A inherits from B. If you can say A has B as a component but A is not necessarily a type of B, then A and B have a composition/aggregation relationship. 

Examples of is-a relationships: every cat is a mammal, every desk is furniture,  every mammal is an animal. Examples of has-a  relationships: every clinic has mammals, every clinic has employees (aggregation), every desk has (one) chair (composition), every clinic has furniture (not every employee has a clinic?) 

###### UML - Unified Modeling Language

![image-20210423123533459](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210423123533459.png)

Where we have arrows signifying inheritance and diamond-tipped lines symbolizing composition relationships.

### Enumeration

###### Un-Scoped Enumeration

An enumeration is a distinct type whose value is restricted to a range of (numerical) values. Lets us use variables in place of numbers for error code handling and similar things that require numbers to delineate differences but the actual identity of the numbers isn't super important. 

Enumerators are the explicitly named constants, the values of which are determined by the compiler.

```c++
enum Color {red, green, blue}; //an unscoped enum
Color r = red;
switch (r) //we can switch because the enum assigns an integer 'key' to each variable
{
    case red: std::cout << "red\n"; break;
    case green: std::cout << "green\n"; break;
    case blue: std::cout << "blue\n"; break;
}
```

​                                                                                                                                                            by default, the compiler will start with zero and add one until it reaches a code-defined value from which it will continue counting from:

```c++
enum Foo {a, b, c=10, d, e=1, f, g=f+c}; //a=0, b=1, c=10, d=11, e=1, f=2, g=12
```

the values that you assign can then be cast to their underlying type such as:

```c++
enum color {red, yellow, green=20, blue};
color col = red;
int n = blue; //n is 21
```

but you can manually set the underlying integer type to convert the values to like so:

```c++
enum color:char {red, yellow, green=20, blue};
```

###### Scoped Enumeration

To declare a scoped enumeration you can use the keywords `struct` and `class` interchangeably:

```c++
enum class Color {red, green=20, blue};
Color r  = Color::red;
int n = Color::blue; //This throws a compiler error bc of implicit conversion.
int m = (int) Color::blue; //Explicit cast to int is allowed.
int l = static_cast<int>(Color::blue); //also allowed.
```

by using a scoped enumeration, you forbid implicitly casting to the underlying numeric type. This ensures you always are working with elements of the enumeration and aren't passing integers around which could potentially get modified as you work. You can still perform explicit casts if you need to.

###### Un-Scoped vs Scoped

Un-scoped enumerations are less safe than using scoped enumerations. If you want the enumerations to retain their ability to behave in comparison tests, you need to use un-scoped enumerations because scoped enumerations will throw a compiler error because comparison tests would implicitly cast to integers.

###### When to Use

Enumerations are great for things like error codes where the number doesn't matter but each number needs to be handled differently:

```c++
enum class ReturnCode = {..., RECEIVED_TWICE=97, NOT_RECEIVED=98, ...};
ReturnCode return_code = some_process();
switch (return_code)
{
    case ReturnCode::RECEIVED_TWICE: 	handle_received_twice();	break;
    case ReturnCode::NOT_REVEIVED:		handle_not_received(); 		break;
}
```

using the enumeration is more readable than referring to error codes as integers.

### Exceptions

There are special ways to return errors in C++. We use exceptions to indicate **fatal errors** have occurred where there is no reasonable way to continue executing the program from the point of the error. It may be possible to continue from a previous execution point but not from the point of error. 

![image-20210423131252080](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210423131252080.png)

We use `try/catch` blocks to handle exceptions as they arise:

```c++
#include <new> //bad_alloc is defined in new
int main() {
    size_t mem=1;
    char * lots_of_mem;
    try {
        while(true) {
            lots_of_mem = new char[mem];
            delete[] lots_of_mem;
            mem *= 2;
        }
    } catch (const std::bad_alloc & ex) {
        sed::cout << "Got a bad alloc!" << std::endl; << ex.what() << std::endl;
    }
    std::cout << "Eventually, runs out of memory..." << std::endl;
    return 0;
}
```

We can also do this for array indexing:

```c++
int main() {
    std::vector<int> vec = {1,2,3};
    try{
        std::cout << vec.at(3) << std::endl;
    } catch (const std::out_of_range& e)  {
        std::cout << "Exception: " << std::endl << e.what() << std::endl;
    }
    return 0;
}
```

The `try` block is the part of the code that could potentially throw the exception. The `catch` block specifies what to do in the event of that particular exception being thrown. 

The point where the exception is thrown is known as the **throw point**. Where the exception is thrown, we don't proceed to the next statement. We begin the unwinding process immediately which moves up through scopes until it encounters an appropriate `catch` block to handle the specific type error or a parent class of that error or it reaches the `main` function's stack frame at which point the program crashes.

When using arrays, we should only use `.at()` to do index checking and return an out of range error. 

`throw exception_name` allows us to throw exceptions when we want to.

###### Customized Exceptions

We can have multiple catch blocks for different exceptions and we can also define our own exceptions which inherit from an exception parent class:

```c++
class BadCardError : std::runtime_error {
    public: BadCardError(Card c): std::runtime_error("bad card"), card (c) {}
    private: Card card;
}
```

### Custom Iterators

Any time we want to loop through all the elements in some kind of container class, we could define an iterator. The code for looping through a linked list is pretty different than looping through a vector. Iterators provide a common logic system for us to handle looping between containers without having to actually handle the logic of how to loop.

There are 4 types of iterators: `iterator`, `reverse_iterator`, `const_iterator`, `const_reverse_iterator`. A plain iterator traverses elements in a container from beginning to end. A reverse iterator traverses elements from end to beginning. A constant iterator promises not to modify individual elements as it progresses through them. 

To define our own iterator, we can use a pointer for objects that have their data lain out in one consecutive memory block but this won't work for something like a linked list. 

We may want to write our custom iterator as a nested class which is defined inside the container class. This gives the iterator access to the `private` fields and functions of the class. 

An iterator takes the general form:

```c++
MyType c;
for (MyType::iterator it = c.begin(); it != c.end(); ++it) {
    std::cout << *it << std::endl;
}
```

so to get our iterator working, we need to define:

1. The `!=` operator
2. The dereferencing operator `*`
3. The preincrement operator `++`

we may also want

4. equality testing with `==`
5. the arrow operator `->`

and will also need to define:

7. the `.begin()` which returns the iterator to the first element in the collection
8. and `.end()` which returns the iterator to one-past the last element element in the collection.

A `const` operator will need a different `operator*` implementation than a normal operator. A `reverse` iterator will need a different `operator++` implementation.

###  TA Session Review

The exam will mainly focus on C++. There will be concepts from C included still but the majority will be on C++. 

##### References and Pointers

Pointers are variables that hold memory addresses of another variable.

A reference is a variable that is an alias for another variable. 

| Pointers                                                     | References                                               |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| Can be reassigned                                            | Cannot be reassigned                                     |
| Can be set to NULL                                           | Cannot be set to NULL                                    |
| Can be declared without initialization                       | Must be initialized immediately. Must alias something    |
| Can have pointers to pointers with different levels of indirection. | Can not have a reference to another reference            |
| Pointer arithmetic allows adding to increment memory addresses through vectors. | There is no equivalent for references.                   |
| Must be dereferenced with `*` or `->` to access value        | Automatically dereferenced                               |
| Have own memory address                                      | Shares same memory address as variable being referenced. |

Swap function equivalents:

```c++
void swapPointers(int* a, int* b){
    int temp = *a;
    *a = *b;
    *b = temp;
}
void swapRefs(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}
```

and both functions will be equivalent and have the same effect of swapping the values held in each variable. 

##### Dynamic Memory Allocation

`new` and `delete` are used in C++. The number of `new` has to match the number of `delete`. You shouldn't mix with `malloc` and `free`. The `new` function calls the object's constructor unlike `malloc` and the `delete` function calls the object's destructor unlike `free`.

```c++
int * a = new int[12]; //create new 12 member array of integers
Box * b = new Box(5, 5, 7); //create new object
delete[] a; //free memory for every item of array
delete b; // delete the object.
```

To create an array of arrays:

```c++
int n = 10;
int **myArray = new int*[n];

for (int i = 0; i < n; i++){
    myArray[i] = new int[n];
}

for (int i = 0; i < n; i++){
    delete[] myArray[i];
}
delete[] myArray; //after deleting array at each element delete array itself.
```

##### Standard Template Library

Provides template classes that implement many data structures and algorithms to avoid writing repetitive code.

Rather than silently failing and creating undefined behavior, all STL containers can throw exceptions to alert you to errors. 

###### Vectors

Dynamically allocated arrays. Empty spots are initialized to some value. You can use `[]` to index without bound checking but this could `seg fault` if you index unallocated memory or use `.at()`  method to access elements with bound checking which will throw an exception when an out of bounds element is passed. `.push_back()` adds an element to the end of the vector. `.insert()` adds an element at a  specified position. 

When you create a vector, you have to specify the type the vector will hold when it is defined. A vector can be created with default size and value as in `vector<int> vec (5, 10)` which initializes the first five indices with `10` and we can even use iterators as in `vecot<int> vec(begin, end)` where begin and end are the `std::vector<int>::iterator begin  = ovec.begin()`, and we can also use bracket notation similar to arrays like `std::vector<int> v6{1, 2, 3, 4, 5, 6}`

###### Maps

Are associative arrays. They have a single key which refers to a single value. Keys cannot be duplicate but different keys may hold the same values. To create a map we use `std::map<type, std::vector<type>>` which would create a map of keys to vectors of a certain type. 

The elements of a map are sorted numerically by their key. They can be accessed with `.at()` or `[]` syntax. If a key indexed at `[]`  does not exist, the map will insert the key and construct a default value for you. If you use the `.at()` function to index the map with a key that doesn't exist, an exception will be thrown.

Insert new values into a map using `map[key] = value;` or `.insert(pair<type type>(key, value))` if you so desire.

The `.find(key)` method can be used to find if a key is in the map or not.

###### Strings

Behind the scenes, strings are vectors of chars so you can use the same methods that you would use on a vector including indexing and inserting. You can concatenate strings using the `+` and `+=` operators.

You can compare strings lexicographically with the `<`, `<=`, `>`, `>=`,  and `==` operators.

###### Iterators

Used to point to elements inside containers, often used to loop through (iterate over) the contents of a container. Can be thought of as pointers designed specifically for containers. For `const` containers, you have to use a `const_iterator`

`.begin()` and `.cbegin()` are methods that returns an iterator to the first element. `.end()` and `.cend()` return an iterator to the theoretical element that follows the last element in the container.

```c++
//Special for loop that loops over every element in the vector.
//Using the & makes each element a reference and allows mutation of the elements.
std::vector<int> vec(5); //initialize 5 elements as zero
for (int& i : vec) {
    i++;
}

std::vector<int> vec(5);
std::map<std::string, int> m;
m["john"] = 1;
for (int& i:vec) {
    std::cout << i << std::endl;
}
for (std::pair<const std::string, int>& p :m) {
    std::cout << p.first << p.second << std::endl;
}
```

###### Other Useful Functions

`.empty()` returns whether or not the container is empty, `.clear()` clears the data but does not free the memory, `.size()` returns the current number of elements, `.capacity()` gives the total capacity of a container (only applies to vectors), `.resize()` changes the size of the container (only applies to vectors and lists)

##### Important Keywords

###### Access Modifiers

`public` Any codes with access to the object has access to something marked as public.

`protected` can only be accessed from within the class and its derived classes

`private` can only be accessed from within the class.

Generally, you want instance variables (fields) to be `private` with `public` getter and setter functions. `public` methods are those an outside user can interact with. Helper methods for use in the class should be `private`

###### Constants

The `const` keyword can be a source of confusion. A `const` variable means the variable cannot be modified. A `const` member function means the function is not allowed to modify the object on which it is called. `const` functions can also only call other `const` functions to ensure the object cannot be changed externally.

`const int myFunc(const & int) const;`:

The first `const` means the function returns a constant integer which cannot be changed once assigned.

The second `const` reference means that you can't change the value of the integer reference that was passed in. 

The third `const` means that this function is not allowed to modify any variables in the class. 

###### Static Variables

A `static` variable gets allocated for the entire lifetime of a program. Think of these as global variables. They retain their values between function calls. 

`static int count = 0` sets count equal to zero initially. This line is not called on subsequent execution of the function that contains it and the value of count is retained once it is modified.

A function containing a `static` variable within a class does not need to have its class instantiated to be called. Suppose `myStaticFunction` resides within `MyClass`. We can call the function to perform the static function without creating the `MyClass` object using the appropriate namespace like so: `MyClass::myStaticFunction()`

###### Friend Functions

Allows us to specify outside functions which can have access to our class's private parameters. Commonly needed when a function requires that a non-class object be passed in before the instance of the object that you are defining the function for such as when overloading the `<<` operator:

```c++
friend ostream& operator<<(ostream&, const Thing&);
```

You can also make other classes `friend`s which would give them access to this class' private variables which could be useful. Generally, you'd probably want to use inheritance to allow this rather than friending.

###### The This Keyword

`this` is a pointer to the current object, all objects automatically have one and it is an implicit parameter to all member functions. You can use `*this` to get the current object which you may need to return to return a reference. You can use `this->variable` to access a member variable of the current object. This helps to be explicit when delineating from member variables and local variables. 

##### Classes and Objects

A class is a user defined type with a set of variables and functions. An object is a specific instance of a class. Class function prototypes/definitions go in header files while their implementations go in `cpp` files.

When writing function implementations outside the scope of the header file, you need to add the `::` (scope resolution operator) to specify what you're talking about. `int ClassName::member_function()`

Members of a `struct` are public by default while members of a class are `private` by default. C structs cannot have functions (interestingly, they can have function pointers though which is out of scope of this course.)

###### Types of Constructors

A constructor is a special  member function that initializes an object. It is automatically called when an object is created. It has the same name as the class and can take in parameters. It has no return value. You can overload constructors to give multiple ways to create a new object. They are mainly used to initialize member variables and create deep copies of other existing objects.

A default constructor is a constructor that takes no arguments. If a constructor is not specified, the compiler generates one for us. Takes the form `MyClass::MyClass(){...}`

A parameterized constructor is a constructor with arguments. Takes the form `MyClass::MyClass(int x, int y) {...}`

A copy constructor initializes an object using another object of the same class. Takes the form  `MyClass::MyClass(const MyClass  &old_obj) {...}`. A copy constructor is invoked when you do the following: `Point p2 = p1;` or `Point p2(p1)`. Not that it is **not the assignment** operator when you use the `=` in the same line as the variable declaration. Used whenever a completely new object is created.

The assignment operator is used to set an existing object equal to another already initialized object. 

Both the assignment operator and the copy constructor perform shallow copies by default and should be overloaded manually to be defined for a deep copy when using dynamically allocated memory.

We use **initializer list syntax** to set the values of variables which is more efficient than setting said values within the body of the constructor. When variables are declared in the body, the default constructor is called first and then the `=` assignment operator is applied which does twice the work. Initializer list syntax is required for setting `const` data members, setting `reference` object members because you cant have null references, and object fields without a default constructor.

###### Destructors

A destructor always has the same name as the class with a ~ prefix. Destructors are special member functions that destroy the object when its stack frame collapses or it is `delete`-ed

There is only ever one destructor. It has no return value and takes no parameters.

The compiler-generated default constructor is usually fine unless you've dynamically allocated memory in the class.

##### Inheritance and Polymorphism

###### Inheritance

C++ allows a class to inherit from another. Establishes the is-a relationship between derived and base class. Derived classes inherit everything from their parent class except for constructors and destructors. While private elements are inherited, they are not directly accessible by the derived class. 

Constructors are called starting with the base class' constructor and destructors are called in reverse order. 

The first initializer list in a derived class constructor has to be setting the base class.

###### Polymorphism

We use polymorphism to mean calling different implementations of a function based on the type of object that you are calling it on.

**Overloading** a function is when you  have the same name with a different parameter list. The compiler automatically picks the correct version of the function based on the parameters you supplied.

Operator overloading is common in C++. Overloading comparison operators is important for allowing an object to be sortable and thus allows you to use it as a map key and the `.sort` function. 

**Overriding**  a function is when you have the same name and  the same parameter list and optionally use the `override` keyword to indicate this is what you intend to do. Tells the compiler you expect a function to be overridden when using the `virtual` keyword in the base class. 

The `virtual` keyword is a member function declared within a base  class and overridden by a  derived class. This is critical for inheritance and polymorphism. It ensures that the correct function is called for an object regardless of the reference or pointer used to call the function. (especially important when you have a function or cast to the base class and wish to call a function which could have different implementations across derived classes.) Virtual functions cannot be static or friend of another class. 

Unless they are a pure virtual function, it is not required for the  derived class to override the base class' implementation. Sometimes you want the base implementation and to only specify where necessary.

######  Pure Virtual Functions and Abstract Classes

A pure virtual function  is a virtual function that is declared without an implementation which is denoted with `= 0` as in

```c++
virtual void myFunction() = 0;
```

any such pure virtual function must be overridden in the derived classes.

A class is an **abstract class** if it has at least one pure virtual function. As a result it will be impossible to create an object from as the pure virtual function is never defined intentionally. Abstract classes act as blueprints for derived classes with a common base.

###### Virtual Destructors

We need to implement virtual destructors  to ensure the correct destructor is called. If we create an object of a derived  class by using a pointer to the base class this becomes important. We need to make the compiler aware that when we call `delete` we want it to check if there is a more specific destructor it should be using:

`Base * myObject  = new Derived();`

If the destructor is not marked as virtual and you use a pointer like this, you will get undefined behavior. 

To mark a destructor as virtual, just prepend the `virtual` keyword before the `~`

##### Templates

Allow us to do generic programming and minimize rewriting code to handle type differences.

`template<typename T>` or equivalently `template<class T>`. Either way, this declaration goes on the line right before any generic function implementation.

If you are defining a generic class, the actual body of the function needs to be included in an `.inc` file which gets imported at the bottom of your header file. 

You can use different letters for different generics as in:

```c++
template<typename T, typename U>
U add(T x, U y) {
    return x+y;
}

int main(){
    int x = 5;
    double y  = 7.5;
    std::cout << add(x, y) << std::endl;
}
```

##### Streams

Streams are string buffers that let you read or write characters to or from files or other strings. `std::cout` and `std::cin` are both `iostreams`.

`stringstreams` can be used to generate string objects:

```c++
#include <sstream>
#include <iostream>

int main() {
    std::stringstream s;
    int x = 1;
    int y = 2;
    s << x << " and "  << y;
    std::string result = s.str();
    std::cout << result << std::endl;
    return 0;
}
```

##### Exceptions

Let us know when something goes wrong and gives us the opportunity to handle these cases gracefully.

We wrap potentially risky code in a `try/catch` block to deal with exceptions. We should not do this too much as over-try-catching is a sign of bad code. We can catch something of general type `std::exception` or we can use a specific extension. Calling `.what()` on the exception will give you more information about it.

We can throw our own exceptions with  `throw exceptionName("error text here");`

##### Default Parameter Values

We can supply default values for parameters.  Required parameters should be listed first and then parameters that have default values. 

##### Defining a Custom Iterator

```c++
class ContainerClass {
  int size = 0;
  //Example assumes the container has data stored in sequential memory and head is the pointer to the first element.
  class Iterator {
    private:
      MyNode<T>* ptr;
    public:
      Iterator(MyNode<T>* initial) : ptr(initial){}
      Iterator& operator++() {ptr++;  return *this;}
      bool operator!=(const iterator &o) const {return ptr != o.ptr;}
      T& operator*() {return ptr->data; }
  };
  
    Iterator begin() {return Iterator(head); }    
    Iterator end() {return Iterator(head + size); }//one past last element
};
```

