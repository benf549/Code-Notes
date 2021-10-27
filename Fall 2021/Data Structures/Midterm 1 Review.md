# Midterm 1 Review

*Benjamin Fry*

## Overview and Review

The structure of a class in java:

```java
public class Student {
    private String name; //declare access modifier, type, then variable name. Initialize in constructor.
    private String email;
    
    public Student(String name, String email) {
        ...;
    }
}
```

### Linear Search

A very simple algorithm. Loop through all the elements of a list until the desired element is found or the search space is exhausted.

```java
public linearSearch(int[] arr, int target) {
	for (int i = 0; i < arr.length; i++) {
    	if (arr[i] == target) {
        	return i;
    	}
	}
	return null;
}
```

Best case, runs in O(1) time (element is the first in the collection.) worst case, runs in O(N) time.

### Binary Search

Given an array that is sorted, we can use binary search to find our element of interest in $O(lg(N))$ time.

```java
public int binarySearch(int[] arr, int target) {
    int min = 0;
    int max = arr.length - 1;
    int mid = (int) (min + max) / 2;

    while (min <= max) {
        if (target > arr[mid]) {
            min = mid + 1;
            mid = (int) (max + min) / 2;
        } else if (target < arr[mid]) {
            max = mid - 1;
            mid = (int) (max + min) / 2;
        } else {
            return mid;
        }
    }
    return -1;
}
```

Alternatively, you could choose to use a recursive implementation:

```java
public int binarySearch(int[] arr, int target, int first, int last) {
    if (last < first) {
			return -1;
	}
	int mid = (first + last) / 2;
    if (target == arr[mid]) {
        return mid;
    } else if (target > arr[mid]) {
        return recursiveBinarySearch(arr, target, mid + 1, last);
    } else {
        return recursiveBinarySearch(arr, target, first, mid - 1);
    }
}
```

### Data Structure

We define a data structure as an encapsulation of organized mechanisms for efficiently storing, accessing, and manipulating data. 

## Inheritance and Polymorphism

### Inheritance

We signal to the compiler we want a class to inherit from another using the `extends` keyword:

```java
public class GradStudent extends Student {
	private String advisor;
    ///
}
```

When you inherit from a super-class, you have to manually call the super class's constructor within the constructor for the derived class. To do this we do the following:

```java
public GradStudent(String name, String email, String advisor) {
    super(name, email);
    this.advisor = advisor;
}
```

Unless member variables of the super class are marked as `protected` (which we would use `super.name` and `super.email` to do), derived classes will not have access to them. You will need to define getter methods, or change the privacy.

**Symmetric Relation** says we should make the more specific class the derived class and provide additional functionality only as needed.

**Multiple Inheritance** is when a class inherits from multiple parent classes and is **not** supported in Java. **Multi-Level** inheritance is allowed (inheriting from a derived class) and multiple derived classes from the same parent class are allowed. We can use interfaces to get around the lack of multiple inheritance.

### Type Substitution and Casting

**Type Substitution** is when a derived object and the parent object don't need separate functions to handle a particular process because the derived object is a parent object. For example, an array of `Student` objects would be able to hold objects of the type `Student` or of type `GradStudent`. This works because of implicit type casting. You can also manually cast a derived class to a parent class. 

Checking for type substitution:

```java
private static String greetAdvisor(Student s) {
    if (s instanceof GradStudent) {
        GradStudent gs = (GradStudent) s; // if s was declared with the addtl information for casting, this works.
    	return gs.getAdvisor();
    } else {
    	return "is an undergrad.";    
    }
}
```

in general, **upcasting** which is casting to the base class will be handled by the compiler. Think casting up towards the root of the type hierarchy. **downcasting** does not happen automatically and needs to be done explicity with `(derivedClass) obj;`

### Overriding

We can use `@Override` as metadata which tells the compiler that a method we are defining means to override another method in the base class. If you don't have a corresponding function in the base class, the compiler would throw an error. For example:

```java
public class Animal {
    public void makeSound() {
        System.out.println("Grr...");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() [
        System.out.println("Meow!");
    ]
}
```

### Overloading

```java
public void makeSound() {
    System.out.println("Grr...");
}

public void makeSound(int repeat) {
    for (int i = 0; i < repeat; i++) {
        makeSound();
    }
} 
```

allows you to define functions with the same name that have different input arguments / numbers of parameters.

### The Default Object Class

Every object in Java inherits from the `Object` class by default. This is an implicit inheritance. There are certain methods like `toString()` which are defined for the Object class that we can `@Override` to provide new implementations for. By default calling `toString()` on an object will print the name of the class @ the memory address in hex.

```java
@Override
public String toString() {
    return name + "(" + email + ")";
}
```

There are also `equals` and `hashCode` functions which we can override if needed. 

## The Abstract Data Type and the Java Interface

There are abstract base classes in java. You can indicate you want to use one of these by putting the `abstract` keyword in the class declaration and in any associated methods for which you don't provide implementations for. 

We don't really use these though. The Java `Interface` is the best way to represent an Abstract Data Type (which is used to define the essentials of what a particular data structure requires for function). An interface may contain nothing but abstract methods and does not contain a constructor or any variables. We do not need to use the `abstract` keyword as this is implicit. It does not have a `super` method so derived classes that `implement` an interface need to `@Override` the method implementations. 

A class can inherit from multiple interfaces:

```java
public class SomeClass implements InterfaceA, InterfaceB {
    ///
}

public class SomeClass extends SuperClass implements InterfaceA, InterfaceB {
    ///
}
```

A class that implements an interface is required to provide an implementation for every interface method unless it itself is `abstract`. 

We can also have interfaces which inherit from other interfaces, this is done as follows:

```java
public interface SomeInterface extends SuperInterface {
    ///
}
```

## Indexed List

### Indexed List Abstract Data Type

```java
public interface IndexedList<T> {
   /**
   * Change the value at the given index.
   *
   * @param index representing a position in this list.
   *              Pre: 0 <= index < length
   * @param value to be written at the given index.
   *              Post: this.get(index) == value
   */
    void put(int index, T value);
   /**
   * Retrieve the value stored at the given index.
   *
   * @param index representing a position in this list.
   *              Pre: 0 <= index < length
   * @return value at the given index.
   */
    T get(int index);
   /**
   * Get the declared capacity of this list.
   *
   * @return the length
   *         Inv: length() >= 0
   */
    int length();
}
```

Within the Javadoc comments we see `Pre` which indicates something that should happen when a function is called. `Post` which indicates the result of the the function after calling it. `Inv` is an invariant condition which is always true no matter what.

### Implementation of Array Indexed List

```java
public class ArrayIndexedList<T> implements IndexedList<T> {
    private T[] data;
    
    public ArrayIndexedList(int size, T defaultValue) {
        data = (T[]) new Object[size]; // cast object to generic type.
        for (int i = 0; i < size; i++) {
            data[i] = defaultValue;
        }
    }
    
    @Override
    public void put(int index, T value) {
        data[index] = value;
    }
    
    @Override
    public T get(int index) {
        return data[index];
    }
}
```

To instantiate such a list with a primitive type like integer or a character, you have to use what are known as **wrapper classes** which essentially casts int to integer:

```java
IndexedList<Integer> numbers = new ArrayIndexedList(10, 0);
IndexedList<Character> chars = new ArrayIndexedList(10, 'z');
```

## Unit Testing

We use  JUnit for unit testing. To declare a new test in the appropriate testing folder, we use the following syntax:

```java
@Test
@DisplayName("This is what the test is doing")
void testThisIsWhatTheTestIsDoing() {
    int a = 1;
    int b = 1;
    assertEquals(a, b);
}
```

IntelliJ will create a test class for you if you hit control-N in the body of an interface.

You can use

```java
private IndexedList<Integer> numbers;

@BeforeEach
void constructIndexedList() {
    numbers = new ArrayIndexedList(10, 0)
}
```

to run a defined function before every test which can help instantiate objects and save you from code duplication. 

### The Three A's of Unit Testing

Arrange everything we need to run the test such as instantiating all objects and creating all variables.

Act to set the test in motion, invoke the method to be tested with an input.

Assert the output of the method is equal to the expected outcome.

## Exception Handling

Also known as **Defensive Programming**. 

In java, when a function is capable of throwing an exception, we can indicate this with:

```java
T get(int index) throws IndexOutOfBoundsException;
```

the `throws` keyword.

To handle an exception, we use try/catch syntax:

```java
try {
    numbers.get(-1);
    fail("IndexOutOfBoundsException not thrown").
} catch (IndexOutOfBoundsException e) {
    System.out.println("Passed.");
}
```

to throw our own exception we use the following syntax"

```java
throw new IndexOutOfBoundsException("Optional Message to User.");
```

We can create our own exceptions with more specific names like so:

```java
public class IndexException extends RuntimeException {
    public IndexException() {
        super();
    }
    
    public IndexException(String message) {
        super(message);
    }
}
```

which is enough to be an exception implementation on it's own. We don't even need a constructor if we wan't to use the default constructor and have no optional message parameter. We extend `RuntimeException` because this is an unchecked exception. This means that the  compiler does not require any function that throws an unchecked exception to have a corresponding Try/Catch block to handle it. If we wanted this behavior, we could extends `Exception` which would create a checked exception. You could also extend `Throwable` to create a checked exception. 

## Java Iterator and Nested Classes

### Enhanced For Loop Syntax

In modern java, we can define an iterator which allows the user to use enhanced for loop syntax:

```java
for (int element : myIntArray) {
    System.out.println(element);
}
```

this gives us a simple way to iterate through all of the elements in a collection without having to understand how the collection is structured internally.

This is syntactic sugar for the following implementation using iterator and iterable:

```java
public Iterator<T> it = myIterableClass.iterator();
while (it.hasNext()) {
    T element = it.next();
    //Does Something With The Element.
}
```

### Iterable

A data structure that can be iterated upon needs to inherit from `Iterable` in its interface definition:

```java
public interface IndexedList<T> extends Iterable<T> {
    //
}
```

this indicates that the class is allowed to be iterated over.

### Iterator

The iterator is the thing that actually defines what it means to iterate over the iterable. Within our class, there will be the overridden iterator function:

```java
@Override
public Iterator<T> iterator() {
    return new myClassIterator<>();
}
```

Within our iterable implementation, we can define nested class to provide the iterator functionality:

### Custom Iterators

We can define a separate class that defines the iterator's functionality:

```java
public class ArrayIndexedList<T> implements IndexedList<T> {
    private T[] data;
    
    @Override
    public Iterator<T> iterator() {
        return new ArrayIndexedListIterator<>();
    }
    
    private class ArrayIndexedListIterator<T> implements Iterator<T> {
        private int cursor;

        public ArrayIndexedListIterator() {
            this cursor = 0;
        }

        @Override
        public boolean hasNext() {
            return cusor < data.length;
        }

        @Override
        public T next() {
            if (!hasNext()) {
                throw new NoSuchElementException();
            }
            return data[cursor++];
        }
	}
}
```

`hasNext` returns a boolean indicating that the cursor is not at the last element. `next` returns the element at the position of the cursor and advances it to the next element. `NoSuchElementException` is thrown when next is called despite `hasNext` returning false.

### Private Nested Class Definition

In the previous example, we have defined the iterator as a nested class within Array Indexed List.

A private nested class has access to the variables of the encapsulating class and can be instantiated in the encapsulating class. A public static nested class as we will see below has no access to the variables of the encapsulating class but can be created anywhere.

## Linked List

A data structure defined by a Node object that can point to another Node object or null. A singly linked list is useful for removing elements within the middle and resizing the collection since it is a matter of repointing nodes rather than copying every element to a new array. 

### References In Java

There are no pointers.

We can just set a variable equal to an instance of a class and this variable essentially acts as a reference to the object. This is because Java handles dereferencing for us. 

### Static Nested Class

```java
public class LinkedList<T> {
    private Node<T> head;
    
    private static class Node<E> {
        public E data;
        public Node<E> next
    }
}
```

by declaring the nested class as static, it will not have access to the instance members of the outer class, but the outer class **has access to the public members of the inner class!** This eliminates the need for getter and setter methods in the nested class.

### Linked List Operations

To insert a node at the head of the linked list, we define `insertFirst`

```java
public void addFirst(T data) {
    Node<T> temp = new Node<>();
    temp.data = data;
    temp.next = head;
    head = temp;
}
```

To insert a node at the end of the linked list, we have to iterate over the list to find the last element so we define `insertLast`

```java
public void insertLast(T data) {
    Node<T> temp = new Node<>();
    temp.data = data;
    temp.next = null;
    Node<T> cursor = head;
    while (cursor.next != null) {
        cursor = cursor.next;
    }
    cursor.next = temp;
}
```

To insert a node at a particular element of the linked list (assume the list is zero-indexed), define `insert`

```java
public void insert(int index, T data) {
    //Find the node before the index we want the new node inserted at
    Node<T> cursor = head;
    for (int i = 0; i < index - 1; i++) {
        cursor = cursor.next
    }
    Node<T> temp = new Node<>();
    temp.data = data;
    temp.next = cursor.next;
    cursor.next = temp;
}
```

To delete a node, we can just excise it from the list and the garbage collector will take care of deleting it for us. Define `delete`  to handle  this for us:

```java
public void delete(int index) {
    Node<T> cursor = head;
    for (int i = 0; i < index - 1; i++)  {
        cursor = cursor.next;
    }
    cursor.next = cursor.next.next;
}
```

### Linked List Iterator

```java
public class LinkedList<T> extends IndexedList<T> {
    ///;
    private class LinkedListIterator<T> implements Iterator<T> {
        Node<T> cursor;
        public LinkedListIterator()  {
            cursor = head;
        }
        
        @Override
        public boolean hasNext() {
            return cursor.next != null;
        }
        
        @Override
        public T next() throws NoSuchElementException {
            if (!hasNext()) {
                throw new NoSuchElementException();
            }
            T returnValue = cursor.data;
            cursor = cursor.next;
            return returnValue;
        }
    }
}
```

Remember, we need the iterator to have access to the `head` of the Linked List so for this reason, we use  a private nested class rather than a static nested class.

## RAM Model Of Computational Efficiency

In this model, the RAM is the memory of a hypothetical computer. It is arbitrarily large, and accessing the memory is free (getting a value from memory, accessing an element of an array, accessing an object instance, and finding methods or functions) do not cost us any time. 

We define simple operations that take a single step:

Assignment with the = operator

Arithmetic operations using +, -, *, /, and %

The increment and decrement operators ++ and --

Combined assignment operations +=, *= etc...

Comparison and Relational operations ==, !=, <, <= etc..

Logical operations such as !, &&, ||, etc

Jump operations such as break, continue, and return

User Input/Output operations such as value inputting, and print statements

When we have loops, these are viewed as the composition of many single operations. The number of times the loop executes can be abbreviated N when the number varies with the size of the input. Operations that take place within the body of a loop are executed N times.

### Best and Worst Case Scenarios

We define the **best case** scenario as the minimum number of steps an algorithm takes for any input size and the **worst case** scenario as the maximum number of steps an algorithm takes for any input size.

We generally focus on worst case analysis since this allows comparison of algorithmic efficiency.

Sometimes we need to use sum notation to describe loops that vary in size depending on an input. It is useful to know the sum of integers formula:
$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$
recall that we can change the index and upper bound of such a sum by adding and subtracting the value of the sum for those cases.

Generally the RAM model is overly complex so we use Asymptotic Notation

## Asymptotic Complexity

### Big O Notation

Allows us to describe the relative complexity growth rate of functions whose runtime varies depending on the size of the input.

We use the notation $T(N)$ to describe an algorithm's precise runtime while $O(N)$ describes the asymptotic runtime. To convert between the two, we drop all constants and only keep the highest order term.

$O(f(n))$ is the set  (or class) of functions that grow no faster than f(n).

In this class, $lg(N)$ is meant to mean $log_2(N)$ since generally problems in computer science deal with doubling or halving and binary numbers.

### Big  O Growth Order

$$
O(1) < O(log(n)) < O(n) < O(nlog(n)) < O(n^2) < O(n^k) < O(k^n) < O(n!)
$$

We call $O(log(n))$ functions **sub-linear**, for example binary search since size of input to search halves on each iteration.

We call $O(n)$ functions **linear**, for example linear search which takes as many iterations as there are elements in the input.

We call $O(nlog(n))$ functions **super-linear** or **linearithmic**

We call $O(N^2)$ functions **quadratic**, for example bubble sort, selection sort, insertion sort.

We call $O(N^k)$ functions **polynomial**

We call $O(k^N)$ functions **exponential**

We call $O(n!)$ functions **factorial**

### Time and Space Complexity

We generally are concerned with time complexity when we look at the runtime of a function in terms of Big-Oh notation.

We can also look at spatial complexity which refers to the amount of memory an algorithm needs to run as a function of it's input size. We want to know how space consumption grows as the size of the input grows.

#### Auxiliary Space

Is the extra/temporary space used by an algorithm during execution.

#### Input Space

Is the memory consumed to store the variables that are inputted to solve the problem.
$$
Space Complexity = Auxiliary Space + Input Space
$$
Recursive function implementations can increase the Auxiliary Space of a method over iterative ones. This is because each call to the function requires a new stack frame to be created which copies all of the input variables. If the recursive function is called N times on an input of size N, the auxiliary space will be of size $O(N)$ whereas an equivalent iterative implementation could do the same thing with $O(1)$.

For example, Binary Search can be implemented recursively or iteratively. The Auxiliary Space for the recursive implementation of binary search which copies the input array on every stack frame is $O(Nlg(N))$ where as the iterative implementation has an auxiliary space of $O(1)$ since it just requires changing a constant number of variables.

Iterative implementations are generally best, but sometimes recursive implementations are significantly easier to implement for things like tree traversals. In this case, the complexity of the iterative implementation is not outweighed by the spatial complexity of the recursive implementation. 

## Quadratic Sorts

### The Comparable Interface

To be able to sort an array of objects, they need to be able to be compared to eachother to have a notion of sortability.

To indicate that a type needs to be comparable we can tell the compiler that the type needs to extend from the comparable interface like so:

```java
public interface SortingAlgorithm<T extends Comparable<T>> {
    void sort(IndexedList<T> indexedList);
    String name();
}
```

This syntax indicates to the compiler that the type put into the indexed list in the sorting algorithm interface  must  have a notion of comparability. To make a custom defined type comparable, we extend `Comparable<T>` and `@Override` the `compareTo()` method.

#### The `compareTo()` Method

Consider `A.compareTo(B)`

This method returns an integer that is greater than zero when A is "greater than" B in some notion

This method returns an integer that is less than zero when A is  "less than" B for the same notion.

This method returns zero when A and B are equal.

We have to use this method to compare things like strings as relational operators don't work as we would expect them to.

```java
public class Student implements Comparable<Student> {
    private String email;
    ///
    @Override
    public int compareTo(Student other) {
        return this.email.compareTo(other.email);
    }
}
```

### Selection Sort

This algorithm scans the first through second to last element of a list in an outer loop. On each iteration through the outer loop, there is a `min` variable that corresponds to the smallest element found so far which is set to the index being searched for at the beginning of the loop. A second loop then scans the elements from the index being searched for to the end of the list and searches for the smallest element in this range. The smallest element is moved to the index being searched for and the element that was there is moved to where the smallest element was previously. Since everything to the left of the index being searched for is sorted, the loop continues through the elements at indices greater than this until the second to last element is found. Since the inner loop checks all elements from this element to the end of the list, the largest element ends up at the end of the list as desired.

This algorithm works from left to right so after three iterations, the 3 smallest elements are guaranteed to be in the first three indices.

**In one sentence: find next smallest, swap into final position.**

Implementation:

```java
@Override
public void selectionsort(IndexedList<T> indexedList) {
    //Start from the first element to second to last element in list
    for (int i = 0; i < indexedList.length() - 1; i++)  {
        //Set the index of the min item to be the index being searched for and update if smaller value found
        int min = i;
        for (int j = i+1; j < indexedList.length(); j++) {
            if (IndexedList.get(j).compareTo(IndexedList.get(min)) < 0) {
                min = j;
            }
        }
        //Once you have identified the index of the smallest item, if i isn't the min item, swap min to i.
        if (min != i) {
            T t = indexedList.get(i);
            indexedList.put(i, indexedList.get(min));
            indexedList.put(min, t);
        }
    }
}
```

### Insertion Sort

This sorting algorithm works by creating a sorted partition on the left and an unsorted partition to the right. The sorted partition is formed by working from the second element to the end of the list. Starting with the second element, checks against the first element which is viewed as the sorted partition since a one element list is sorted by default. It works backwards through the sorted elements until the element being inserted is less than the element being compared to. There is a minimal swaps optimization which holds the element being inserted into the sorted partition in a variable and shifts the elements of the sorted partition over by copying index j to index j+1. Once the index for the element being inserted is found, we set that index to the element being inserted.

The algorithm works from left to right, but there is no guarantee that any portion of the list will be sorted until the final step since it works one element at a time to insert it from right to left.

**In one sentence: consider each element, move as far to the left as it needs to go.**

Implementation:

```java
@Override
public void insertionsort(IndexedList<T> indexedList) {
    //Start at second index since first index trivially sorted.
    for (int i = 1; i < indexedList.length(); i++) {
        T temp = indexedList.get(i);
        int j = i - 1;
		//While j is a valid index, check if item at j is greater than temp, shift to the right (overwrites temp)
        while (j >= 0 && indexedList.get(j).compareTo(temp) > 0) {
            indexedList.put(j+1, indexedList.get(j));
        	j--;
        }
        //Once the index to put the new value is found, put it there.
        //Have to use +1 because j will be -1 if inserting at beginning of list since decrement at end of loop.
        indexedList.put(j + 1, temp);
    }
}
```

### Bubble Sort

This sort algorithm works by "bubbling up the largest element" to the end of the list. Works kinda like selection sort in that it has the effect of moving the largest element to the end of the list. Then it moves the next largest element to the second to last index. The difference between this and selection sort is that each element where `j+1 < j` is swapped until the largest element has swapped its way all the way up to the end of the list. By keeping track if any swaps were made, we can use the early stop heuristic which tells us we can stop when no swaps are made in the inner loop.

This sort does have a predictable effect. After 3 iterations of the outer loop, the 3 largest elements will be found at the end of the list. 

**In one sentence: Compares adjacent values, swaps if out of order.**

Implementation:

```java
@Override 
public void bubblesort(IndexedList<T> indexedList) {
    boolean swapped;
    //Start at end of list and work to second to last element.
    for (i = indexedList.length() - 1; i > 0; i--) {
        swapped = false;
        //Loop from first element to end of unsorted part of list
        for (int j = 0; j < i; j++) {
            //swap element at j if j+1 is less than it. Bubbles largest element up to index i.
            if (indexedList.get(j + 1).compareTo(indexedList.get(j)) < 0) {
                T temp = indexedList.get(j + 1);
                indexedList.put(j + 1, indexedList.get(j));
                indexedList.put(j, temp);
                swapped = true;
            }
        }
        //If no swaps are made, the list is sorted so end execution.
        if (!swapped) {
            return;
        }
    }
}
```

## Stacks and Amortized Analysis

A stack is a type of limited access data structure. You can only access (add/read/delete) the element at the front or back position. Access to the internals is not allowed. By placing limits on access, we can have very efficient implementations for our methods.

The stack is a LIFO (Last-In, First Out )

### The Stack ADT

```java
public interface Stack<T> {
    boolean empty();
    T top() throws EmptyException; //returns without removing. Allows peeking at top.
    void pop() throws EmptyException; //removes without returning. They could be the same function. 
    void push(T t);
}
```

### Linked List Implementation of Stack

How can we use linked lists to implement the abstract methods of the Stack ADT in $O(1)$ time?

```java
public class LinkedStack<T> implements Stack<T> {
    private Node<T> head;
    private int numElements;
    
    public LinkedStack() {
        head = null;
        numElements = 0;
    }
    
    @Override
    public void pop() throws EmptyException {
        if (empty()) {
            throw new EmptyException();
        }
        head = head.next;
        numElements--;
    }
    
    @Override
    public T top() throws EmptyException {
    	if (empty()) {
            throw new EmptyException();
        }
        return head.data;
    }
    
    @Override
    public void push(T t) {
        Node<T> newNode = Node<>();
       	newNode.data = t;
        newNode.next = head;
        
        head = newNode;
		numElements++;
    }
    
    @Override
    public void empty() {
        return numElements == 0;
    }
    
    private static Node<T> {
        T data;
        Node<T> next;
    }
}
```

We want to use the head of the linked list for this rather than the tail as otherwise we would have to loop through the entire list to implement the pop and push functions. Using the head keeps things simple because it is easy to addFront and removeFront.

### Array Implementation of Stack

```java
public class ArrayStack<T> implements Stack<T> {
    private int numElements;
    private T[] arr;
    private int capacity = 10;
    
    public ArrayStack() {
        arr = (T[]) new Object[capacity];
        numElements = 0;
    }
    
    @Override
    public void pop() throws EmptyException {
        if (empty()) {
            throw new EmptyException();
        }
		numElements--;
    }
    
    @Override
    public T top() throws EmptyException {
        if (empty()) {
            throw new EmptyException();
        }
        return arr[numElements - 1];
    }
    
    @Override
    public void push(T t) {
		arr[numElements] = t;
        numElements++;
    }
    
    @Override
    public void empty() {
        return numElements == 0;
    }
    
}
```

There is a problem with this implementation though. When we try to push more elements into the array than the `initialSize`, we can't. We need to dynamically resize the array but need a way to do this such that our implementation is still $O(1)$.

### Amortized Analysis

We can dynamically resize our array in such a way that the average call to push is done in $O(1)$ time. We confirm this with amortized analysis which essentially views the $O(N)$ resizing process as distributed across all the previous calls to push which do not require growing the array. 

To create an amortized linear time growth operation, we should double the size of the array with a new grow function when the capacity of the array stack is reached. This works because we need to copy N elements which takes O(N) time. We only do this 1 time after N push operations so we can think of this process as $\frac{O(N)}{N} = O(1)$

```java
@Override
public void push(T t) {
    arr[numElements] = t;
    numElements++;
    if (numElements == capacity) {
        grow();
    }
}

private void grow() {
    T[] newArr = new Object[capacity*2];
    capacity *= 2;
    for (i = 0; i < numElements; i++) {
        newArr[i] = arr[i];
    }
    arr = newArr;
}
```

