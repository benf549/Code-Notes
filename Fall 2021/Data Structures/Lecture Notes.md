# Lecture Notes

*Benjamin Fry*

## Unit 1

### Object Oriented Programming In Java

*08/30/21*

###### Homework

Every homework comes with its associated rubric which is the exact thing the TAs will use to grade us. Read this while working on the assignment. The assignments are found on the [homepage](https://cs226fa21.github.io/index.html), the gradescope submission results will also let us know whether we have met the desired criteria.

###### Class Notes

Every class will have class notes posted on the course homepage prior to the class. The classes generally will consist of programming problems. The associated solutions will be posted at 5pm the day of the class. The notes are a combination of worksheets, slides, etc.. pressing `p` on the course homepage will allow you to draw on the course note. 1, 2, 3, 4, 5, ' ' switch between markup tools.

We are highly encouraged to work on the exercises given the opportunity.  

###### Midterms

Will be in person and we will be required to attend our section's midterm.

##### Programming in Java with IntelliJ

**Student.java**

```java
//packages group related objects
package starter;

//class
public class Student {
 	//core pieces of information - attributes/fields/member variables.
    private String name;
    private String email;
    
    //constructor - name must be exactly the name of the class with no return type. gives inital values to attributes
    public Student(String name, String email) {
        this.name = name;
        this.email = email;
    }
    
    public String getName() {
        return name;
    }
    
    public String getEmail() {
        return email;
    }
}
```

**Main.java**

```java
package starter;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Data Structures");
        //intantiate an object.
        Student student1 = new Student("Ali", "ali@email.com");
    }
}
```

It is good practice to make member variables in java objects private and define getters and setters as needed. Intellij has getter boilerplate generation built in. You can suppress java warnings using `@SuppressWarnings("all")`. 

/** auto-creates documentation in intellij

**Abstraction** is utilized in the above example by only collecting attributes that are needed to perform the tasks at hand. For example, the Student class only uses name and email despite there being many other ways to define a student.kk

**Encapsulation** is utilized in the above example by putting the data and the operations that act on that data into one unit of code which in this case is the Student class. 

**Data Types** tell you and the compiler what types of objects/information can be stored in the variable of interest. Ex: int, double, String... Data types also define what operations are available for use. In the above example, Student is a datatype that is programmer defined. 

```java
package starter;

public class Roster {
    private Student[] students;
    private int numStudent;
    
    public Roster(int size) {
        //define an array of students with size elements.
        students = new Student[size];
    }
    
    public void add(Student student) {
        //stub
    }
    
    public void remove(Student student) {
        //stub
    }
    
    //Assumption - student emails are unique
    public Student find(String email) {
        for (int i = 0; i < numStudent; i++) {
            if (students[i].getEmail().equals(email)) {
                return students[i];
            }
        }
        return null; //not-found
    }
}
```

A stub is the boilerplate code written such that the compiler won't complain, but lacks implementation. 

The find method defined above is an example of a sequential search algorithm, this just loops through all elements in order to find something.

`.equals()` is a function for string data types in java. It allows you to check that strings are equals. You should only use comparison operators with primitives. Any other type requires `.equals()`, you may need to define this method for your class. By default, `.equals` is defined to check if two objects share the same memory location. If you want to overload this, intelliJ can automatically do this. The details are not important at the moment.

###### Sequential/Linear Search

An example of an algorithm. An algorithm is a set of rules or to be followed to perform a task. In CS, every step in an algorithm must be explicit (not subjective) and the process must be able to be carried out in a finite amount of time. We can describe the running time of an algorithm to compare different algorithms for accomplishing the same task. 

The best case scenario for linear search is the student of interest is the first one checked, the for loop executes one time and the program returns. The worse case scenario is that the student of interest is the last one in the array. The number of iterations linearly scales with the number of elements.

###### Binary Search                                 

Only applicable if the students in the array are sorted. This search algorithm is much faster in the worst case scenario. First, we pick the "middle" object of the array, if the object we are searching for is "less" than this object, we split the array and search the [beginning, middle-1], if "greater" than this object, we split the array and search [middle+1, end]. At each step, check if the middle of choice is equal to the thing we are searching for

```java
private Student find(String email, int first, int last) {
        //Base Case - handle empty array region.
        if (last < first) {
            return null;
        }

        int mid = (first + last) / 2; //implicit conversion to int

        String studentEmail = students[mid].getEmail();

        /* comparison == 0, email == studentEmail
         * comparison > 0, email > studentEmail
         * comparison < 0, email < studentEmail */
        int comparison = email.compareTo(studentEmail);
        if (comparison == 0) {
            return students[mid];
        } else if (comparison > 0) {
            //search the second half of the array, update first and last idcs.
            return find(email, mid+1, last);
        } else {
            return find(email, first, mid-1);
        }
    }
```

| Step | Search Space | Pattern |
| ---- | ------------ | ------- |
| 0    | n            | n/$2^0$ |
| 1    | n/2          | n/$2^1$ |
| 2    | n/4          | n/$2^2$ |
| ...  | ...          | ...     |
| x    | 1            | n/$2^x$ |

The process continues halving the size of the array until there is one element left. The pattern is divided by increasing power of 2 for each step, thus we can solve for number of steps $x$ by using the logarithm base-two $x = log_2(n)$ while linear search will take $x = n$ in the worst case.

###### Data Structure

A data structure is defined as an encapsulation of organized mechanisms for efficiently storing, accessing, and manipulating data. The Roster object we created above is thus, an example of a data structure. Roster is a very specific data structure to a particular problem. 

###### Inheritance in Java

```java
public class GradStudent extends Student {
    private String advisor;

    public GradStudent(String name, String email) {
        super(name, email); //calls the parent obj's constructor.
    }

    public String getAdvisor() {
        return advisor;
    }

    public void setAdvisor(String advisor) {
        this.advisor = advisor;
    }
} //Grad student inherits from the student object.
```

When grad student inherits the name and email strings from the student it may not have access to these variables directly since they are designated private.

You can use `super.name` and `super.email` to access member variables if they are marked as protected, but NOT if they are private. You should use the getter methods to get the variables if you need to keep them as private. You can also use `this.getName()` and `this.getEmail()` which will first use getter methods defined for the derived class, if they are not found the compiler will then search for the methods in the superclass. 

To explicitly define the getName method in the derived class while avoiding code duplication:

```java
public String getName() {
    return super.getName() + ", the Grad student!";
}
```

The concept of **Symmetric Relation** states that we should make the more specific class the derived class which can extend the functionality of the more general base student class. We try to model the solution after the real world.

**Multiple Inheritance** is when a class inherits from more than one parent class, Java **DOES NOT SUPPORT THIS**. Multi-level inheritance is allowed but not multiple inheritance. Multiple derived classes from one parent class on the other hand are of course allowed. 

**Type Substitution** is when `Student` and `GradStudent` are not linked through inheritance, you have to duplicate every data structure to store students and grad students separately. If there is an inheritance relationship, you only need one data structure which can handle the base class shared by both. For example

```java
public class Roster {
	private final Student[] students;
}
```

the roster class has the `Student[]` which can handle both `Student` and `GradStudent` objects. The reason the `GradStudent` object can be stored in a `Student` array is because of **Type Substitution**: A given type variable may be assigned a value of any subtype, and a method with a parameter of a given type may be invoked with with an argument of any subtype of that type.

**Casting of Types** The advantage of building type hierarchies lies in the power of type substitution. 

```java
Student jane = new GradStudent("Jane Doe", "jane@email.com");
GradStudent matt = new GradStudent("Matt Doe", "matt@email.com");

matt.getAdvisor(); //works fine
jane.getAdvisor(); //breaks because jane is a Student not a GradStudent.

private static String greetAdvisor(Student s) {
    GradStudent gs = (GradStudent) s; //Cast object of Student to GradStudent, this only works if the Student was instantiated as a GradStudent. We can guard agains this with the following:
    if (s instanceof GradStudent) {
        GradStudent gs = (GradStudent) s;
        return return "Hi, " + gs.getAdvisor();
    } else {
        return "This student has no advisor!";
    }
}
```

Upcasting (casting to the general base class) is automatically done by the compiler, downcasting does not happen automatically (ex automatically calling `getAdvisor()` only when the object is of a base class where that method is defined.)

Sometime the apparent and actual data type of an object can differ. `Student jane = GradStudent(...);` is a case where the apparent datatype is a `Student` and the actual datatype is a `GradStudent` which still retains any extra member variables/methods that are defined only for graduate students.

While you can instantiate a variable declared as a base class as a derived class, you cannot instantiate a variable declared as the derived class as the base class since information would be missing.

###### Overriding

```java
public class Animal {
    public void makeSound() {
        System.out.println("Grr...");
    }
}

public class Cat extends Animal {
    //The overrride keyword makes sure that you are overriding a function from the base class. If you had a typo in the makeSound function in cat class, the compiler will throw an error. This is an example of metadata that helps you avoid making mistakes. 
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof");
    }
}
```

###### Overloading

Overloading is when you have multiple functions with different numbers of parameters. This could be done across the class or within objects. 

```java
public class Animal {
    public void makeSound() {
        System.out.println("Grr...");
    }
    //An example of overloading
    public void makeSound(int repeat) {
        for (int i = 0; i < repeat; i++) {
            makeSound();
        }
    }
}
```

###### Semantics in OOP

Inheritance should be used to model *is-a* relationships. In these relationships, the derived class IS an instance of the base class. 

The has-a relationship is modeled by composition between classes. There are many cases where one entity is made up of another of other entities. For example, a car is an engine, tires, seats, windows, etc...

For example a `GradStudent` is a `Student` while a `Roster` has many `Student`s

###### The Object Class

In Java, every class is descended from the `Object` class. This is an implicit inheritance (happens automatically). Since the Object class contains a `toString()` method, we can call `toString()` on any programmer defined type and get its string representation. 

```java
Student john = new Student("John Doe", "jdoe@email.org");
System.out.println(john); //calls john.toString() automatically
//Student@1ee0005
```

This returns a string consisting of the object name appended to the unsigned hexadecimal representation of an object's hash code corresponding to the object's memory location. 

We can override the default `toString()` method to return a different string representation:

```java
public class Student {
    ...
    @Override
    public String toString() {
    	return name + " (" + email + ")";   
    }
}
```

 Doing this utilizes runtime polymorphism.

IntelliJ can automatically generate `toString` methods for you too (check the documentation for a tutorial).

The Object class also has several other methods including `equals` and `hashCode` which we will learn to override later.

### Abstract Data Type & Java Interface

Recall the `Roster` class from the previous chapters:

```java
public class Roster {
  private Student[] students;
  private int numStudents;

  public Roster(int size) {
    students = new Student[size];
    numStudents = 0;
  }

  public void add(Student s) {
    // stub
  }

  public void remove(Student s) {
    // stub
  }

  public Student find(String email) {
    return null; //stub
  }
}
```

If the `find` method is more important for speed than `add` or `remove`, we can implement `find` to utilize binary search while `add` and `remove` keep the underlying array sorted. Since the sort process is rarely called, find is very efficient.

If the `add` and `remove` functions are called frequently with large numbers of students, we may not want to be sorting the array every time they are called. Then we just implement `find` to utilize linear search rather than binary search. 

We could define `JhuRoster` and `MoocRoster` as different implementations of the `Roster` class where `JhuRoster` utilizes the binary search find algorithm as our courses rarely change students and the `MoocRoster` utilizes the linear search find algorithm as the list of students in such a course may change very frequently. 

We could have a roster extend from from the other but there may be methods for the base class that are not utilized in the derived class. It doesn't make sense to have to override almost every function as code reuse isn't really an advantage of this design decision. We could create the `JhuRoster` and `MoocRoster` as entirely different data types, but this may lead to code duplication if we add functionality that should be shared between the two rosters. We also wouldn't be able to store the different types of rosters in a shared array. Finally we could use a `Roster` class where both `MoocRoster` and `JhuRoster` extend it but what would we use as the default implementations for our methods? We could use an **Abstract Base Class**.

```java
//Note abstract keyword in both the class definition and method implementations.
public abstract class Roster {
    protected Student[] students;
    protected int numStudents;
    
    //Defines a constructor that any derived class can use.
    public Roster(int size) {
        students = new Student[size];
        numStudents = 0;
    }
    
    //ABC does not implement functions, but defines them. Any derived class must implement.
    public abstract void add(Student s);
    
    public abstract void remove(Student s);
    
    public abstract Student find(String email);
}
```

You are not allowed as a developer to instantiate a `Roster` object directly. This is because you cannot call methods which do not have an implementation. If you want to instantiate a Roster, you have to instantiate with one of the subtypes which do have methods defined. 

###### Abstract Data Type

A data type is a type (collection of values) together with a collection of operations to manipulate the type. A data structure encapsulates organized mechanisms for efficiently storing, accessing, & manipulating data. An Abstract Data Type (ADT) is a description (representation) or some type of data and the operations that are allowed on that data while abstracting (ignoring) the implementation details of the operations.

ADT provides the minimal expected interface and set of behaviors without regard for how they will be implemented. A data structure is an implementation of an ADT. 

ADTs are used by theoreticians to design data structures, analyze algorithms, programming languages, and software engineering. They are often described in terms of algebraic specifications with axioms that formalize the operations and their expected behaviors. Most programming languages do not directly support formally specified ADTs, but abstract class constructs come close. `Roster` can be an ADT which lays out the fact that a 'roster' is defined by its ability to `add`, `remove`, and `find` students. These operations are specified but not implemented where implementations are left up to the data structures. 

###### Java Interfaces

Java has a construct called an **Interface** that is closely related to an abstract class. An Interface is an abstract class containing nothing but abstract methods. An Interface is another level of abstraction that is even more abstract than an ABC. 

```java
public abstract class Roster {
    public abstract void add(Student s);
    public abstract void remove(Student s);
    public abstract Student find(String email);
}

//An interface does basically the same thing but is more succinct.
//Multiple inheritance is allowed only if both parents are interfaces.
//Never use constants, default methods, static methods, and nested types which are technically allowed in java interfaces, but not in this class. 
public interface Roster {
    void add(Student s);
    void remove(Student s);
    Student find(String email);
}
```

We will use `interface`s to represent ADTs. 

```java
//An interface is implements while a base class extends
public class MoocRoster implements Roster{
    private Student[] students;
    private int numStudents;
    
    public MoocRoster(int size) {
        students = new Student[size];
        numStudents = 0;
    }
    
    @Override
    public void add(Student s) {
        //...
    }
    
    @Override
    public void remove(Student s) {
        //...
    }
    
    @Override
    public Student find(String email) {
        //...
    }
}
```

The roster needs to define its fields since the interface only defines methods and does not have a `super` methods. 

```java
//closest thing java has to multiple inheritance.
public class SomeClass implements InterfaceA, InterfaceB {
    //...
}

//A class can extend another class and implement one or more interfaces at the same time.
public class SomeClass extends OtherClass implements InterfaceA, InterfaceB {
    //...
}
```

When a class implements an interface, it must implement all its methods unless it is an abstract class where it can defer implementation to subclasses. 

```java
public interface SomeInterface extends OtherInterface {
    //...
}
```

allows us to define `SomeInterface` as a subtype of `OtherInterface` where it extends the other interface.

![image-20210910133441563](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210910133441563.png)

###### IndexedList ADT

The first ADT we will declare in this course. The `IndexedList`.

```java
package starter;

/**
 * IndexedList ADT.
 */
public interface IndexedList {
   /**
   * Change the value at the given index.
   *
   * @param index representing a position in this list.
   *              Pre: 0 <= index < length
   * @param value to be written at the given index.
   *              Post: this.get(index) == value
   */
   void put(int index, int value);
    
   /**
   * Retrieve the value stored at the given index.
   *
   * @param index representing a position in this list.
   *              Pre: 0 <= index < length
   * @return value at the given index.
   */
   int get(int index);
    
   /**
   * Get the declared capacity of this list.
   *
   * @return the length
   *         Inv: length() >= 0
   */
   int length();
}
```

This is an abstraction of a list which is a sequential set of elements to which you can add (get) data with an index (nonnegative integer repr. data in the sequence). This is not completed until it is thoroughly commented. 

`Pre` is short for pre-condition. All the conditions that are supposed to be met when you call the function. In the `put()` function, the `Pre: 0 <= index < length` tells the user that you must use a 'good' index that follows the rule specified or else they may get an error/undefined behavior.

`Post` is short for post-condition. This tells the user what the result of calling a function will do. In `put()`, the `Post: this.get(index) == value `condition indicates that the value at a given index will be set to value.

`Inv` is short for invariant. This tells the user that throughout the lifetime of the object, this statement will always hold. `Inv: length() >= 0` tells the user that length will always be greater than or equal to 0.

When input checking is trivial, we can do a quick check and throw an exception. 

### Java Generics and Unit Testing

###### Generics

```java
package starter;

/**
 * An implementation of IndexedList that takes a default value
 * to plaster over the entire data structure.
 */
public class ArrayIndexedList implements IndexedList {
  private int[] data;

  /**
   * Construct an ArrayIndexedList with given size and default value.
   *
   * @param size         the capacity of this list.
   * @param defaultValue an integer to plaster over the entire list.
   */
  public ArrayIndexedList(int size, int defaultValue) {
  	data = new int[size];
    for (int i = 0; i < size; i++) {
        data[i] = defaultValue;
    } 
  }

  @Override
  public void put(int index, int value) {
    data[index] = value;
  }

  @Override
  public int get(int index) {
    return data[index];
  }

  @Override
  public int length() {
  	return data.length;
  }
}
```

but this data structure is only able to store integers. We want to use type generics. You used to have to use `Object` as the base class for a generic class and manually downcast every subtype but this is annoying. 

```java
package starter;

/**
 * IndexedList ADT.
 * @param <T> generic element type.
 */
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

public class ArrayIndexedList<T> implements IndexedList<T> {
  private T[] data;

  /**
   * Construct an ArrayIndexedList with given size and default value.
   *
   * @param size         the capacity of this list.
   * @param defaultValue a value of Type T to plaster over the entire list.
   */
  public ArrayIndexedList(int size, T defaultValue) {
  	//Intellij yells at you for this. You can't directly instantiate a generic arrary.
    //data = new T[size];
    data = (T[]) new Object[size]; //this is just a stupid idiosyncracy of java to ensure back. compat. with old java.
    //data = (T[]) Array.newInstance(Object.class, size);
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

In java, you can't use primitive types when using generics. To get around this, you have to define a wrapper class to force the primitive type to allow integer.

```java
IndexedList<Integer> numbers = new ArrayIndexedList<>(10, 0);
numbers.put(0, 23)
```

Under the hood, this essentially casts the int to Integer, but in this context we call it **boxing.** There is more information [here](https://beginnersbook.com/2017/09/wrapper-class-in-java/).

```java
IndexedList<Character> chars = new ArrayIndexedList<>(10, 'c');
chars.put(0, 'c');
```

###### Test-Driven Development

We will use TDD in this class woo-hoo...

The `JUnit` package will help us write tests in this class. Inside the `/src/test/` folder, there is a similar layout to the content of the `/src/main/` code that holds the main code form the repo. 

Within `/src/test/` we create a new class that has `Test` in the name somewhere. We use `JUnit5` which contains a number of files that get compiled into the main `.jar` file. These `junit` files get included in the `/lib/` folder. 

```java
package starter;

import org.junit.jupiter.api.Test;

public class IndexedListTest {
    //annotation to tell intellij you are specifying a test whihc can be run from the testing gui
    @Test
    void myTest1() {
        
    }
    
    @Test
    void myTest2() {
        
    }
}
```

In JUnit, a test only fails if the execution fails with an exception. If nothing is specified, the test will pass. We want our test names to be as descriptive as possible. Each test should focus on a particular component of the class. Each test should correspond to a given function in the class being tested. We also probably want to test functions multiple times in multiple different ways to try to break our code in as many ways as possible. 

When naming the test class use the name of the class being tested followed by Test. Intellij will actually create a test class for you by `cmd-N` somewhere within the body of the interface.  We want to write our tests for the interface rather than the implementation of the test unless the implementation does something that the interface doesn't. 

```java
class IndexedListTest {
    @Test
    @DisplayName("length() returns the size which IndexedList was constructed with")
    void testLengthAfterConstruction() {
        //make and IndexedList
        IndexedList<Integer> numbers;
        //give it a size
        numbers = new ArrayIndexedList<>(4, 0);
        //test lenth returns the correct size.
        assertEquals(4, numbers.length());
    }
    
    @Test
    void testLengthDoesNotChangeWhenPutCalled() {
        IndexedList<Integer> numbers;
        numbers = new ArrayIndexedList<>(4, 0);
        numbers.put(2, 12);
        assertEquals(4, numbers.length());
    }
}
```

You can use breakpoints to run the program in debug mode in the tests which will allow us to inspect the test code to see where it is failing. When debugging, if you step through the code after your breakpoints to the implementation that is causing an issue, you can click on the implementation in the code with your mouse and it will take you to debugging within the function where you can inspect where the error is!

For this class, `DisplayName`s are optional but we probably should use them as a best practice.

```java
@Test
@DisplayName("get() returns the default value after IndexedList is instantiated")
void testGetAfterConstruction() {
    IndexedList<Integer> numbers = new ArrayIndexedList<>(4, 0);
    for (int i = 0; i < 4; i++) {
        assertEquals(0, numbers.get(i));
    }
}

@Test
@DisplayName("put() changes the default value after IndexedList is instantiated.")
void testPutChangesValueAfterConstruction() {
    IndexedList<Integer> numbers = new ArrayIndexedList<>(4, 0);
    numbers.put(0, 2);
    assertEquals(2, numbers.get(0));
}

@Test
@DisplayName("put() overwrites the existing value at given index to provided value.")
void testPutUpdatesValueAtGivenIndex() {
    IndexedList<Integer> numbers = new ArrayIndexedList<>(4, 0);
    //TODO
}
```

Notice that all of these programs require the same object instantiation process. JUnit allows us to create a `setup` method that allows us to avoid the code duplication. 

```java
private IndexedList<Integer> numbers;

@BeforeEach
void constructIndexedList() {
    numbers = new ArrayIndexedList<>(4, 0);
}

@Test
@DisplayName("get() returns the default value after IndexedList is instantiated")
void testGetAfterConstruction() {
    for (int i = 0; i < 4; i++) {
        assertEquals(0, numbers.get(i));
    }
}

@Test
@DisplayName("put() changes the default value after IndexedList is instantiated.")
void testPutChangesValueAfterConstruction() {
    numbers.put(0, 2);
    assertEquals(2, numbers.get(0));
}

@Test
@DisplayName("put() overwrites the existing value at given index to provided value.")
void testPutUpdatesValueAtGivenIndex() {
    //TODO
}
```

This allows the tests to not repeat code that isn't directly pertaining to the test you are testing. We need to give  all the other functions access to numbers to allow the `@BeforeEach` decorator to work properly. To do this, we mode the declaration to outside the setup method.

**3 A's of Unit Testing**

**Arrange**: everything we need to run the test. For example, instantiate an object with some parameters.

**Act**: to set the test in motion. Invoke the method to be tested with some input.

**Assert**: the output of the method under test checks against the expected outcome.

Test first development is when we write the tests first, then provide the implementations. Test driven development is when we write a test, then provide the minimal implementation to pass the test. We then write another test to and repeat.

### Exceptions (Defensive Programming)

When defining our ADT as an interface, we used the `pre` and `post` decorators to tell the users what the values of variables should be. We can throw exceptions to ensure when these rules are violated, we gracefully quit the program and alert the users. 

For the `get(int index)` method in the IndexedList ADT:

```java
/**
* Retrieve the value stored at index
*
* @param index representing a position in the indexed list
* @return value at a given index
* @throws IndexOutOfBoundsException
*/
T get(int index) throws IndexOutOfBoundsException;
```

which we can then test in our unit testing with:

```java
@Test
@DisplayName("get() throws exception when index < 0")
void testGetThrowsExceptionWhenIndexBelowRange() {
    try {
        numbers.get(-1);
        System.out.println("Bad!!");
        //this is how we tell JUnit our test didn't pass.
        fail("IndexOutOfBoundsException not thrown :(");
    } catch (IndexOutOfBoundsException ex) {
        System.out.println("Good!");
    }
}

@Test
@DisplayName("get() throws exception when index > size.")
void testGetThrowsExceptionWhenIndexAboveRange() {
    try {
        numbers.get(size + 1);
        System.out.println("Bad!!");
        fail("IndexOutOfBoundsException not thrown.");
    } catch (IndexOutOfBoundsException ex) {
        System.out.println("Good!");
    }
}
```

we then need to add the exception raising to our implementations of the interface:

```java
public T get(int index) throws IndexOutOfBoundsException {
    if (index < 0 || index >= data.length) {
        throw new IndexOutOfBoundsException();
    }
    return data[index]; //technically, our above exception isn't necessary.
}
```

this should allow the error throwing test to pass. Throwing an exception 

###### Custom Exceptions

It is best practice to throw your own custom exceptions with very specific names.

```java
package starter;

public class IndexException extends RuntimeException {
	public IndexException() {
        super();
    }
    
    public IndexException(String message) {
        super(message);
    }
}
```

This on its own (without constructors defined) is enough to be an exception implementation. If we want to pass a message to it we need to define a constructor for both a message and no message.

If you are throwing an exception, always add the `throws Exception` decorator to the function name.

`RuntimeException` is used when you want the exception to be unchecked. `Exception` on the other hand would be checked (see below).

Because exceptions are classes. We can define a type hierarchy which allows us to create exceptions that get more specific and are related to other exceptions defined for the program. All exception types inherit from throwable. Exceptions are a type of throwable. RunTimeException are unchecked while Exceptions are checked. You can directly extend throwable if you want.

By defining a type hierarchy, we can `catch` with type substitution. This allows us to catch exceptions more generally. We catch the children before we catch the parent exception to ensure we handle the more specific exceptions more specifically. Catching the parent class first will skip the derived exceptions.

###### Checked and Unchecked Exceptions

These are the two types of exceptions in Java. This is idiosyncratic to Java. Both types of exceptions will halt execution. 

The difference is the way the compiler handles them. A checked exception is an exception where the compiler will not let you call it directly. The compiler requires you to have a Try/Catch block that handles that exception wherever it is thrown. 

For example if you have the function:

```java
public void doSomething() {
    doThisFirst();
}
```

if `doThisFirst` throws or can throw a checked exception, the compiler will complain that the checked exception is not handled. To fix this, we have to wrap in a Try/Catch block:

```java
public void doSomething() {
    try {
        doThisFirst();
    } catch (SomeCheckedException e) {
        //deal with this.
    }
}
```

if you don't want to handle the potential exception in `doSomething` you can change the function declaration to:

```java
public void doSomething() throws SomeCheckedException {
    doThisFirst()
}
```

but the function that calls `doSomething()` will have to have the Try/Catch block.

Unchecked exceptions do not require a Try/Catch block to surround function implementations. Unchecked exceptions give programmers the flexibility to not handle certain errors that rarely happen. For example, we don't want to have to have a Try/Catch block every time we use division because of the possibility of the division throwing a `ZeroDivisionException`. 

We extend `Throwable` or `Exception` to have a checked exception while `RuntimeException` is used to create unchecked exceptions. 

### Java Iterator and Inner Class

When we typically write arrays, we do this:

```java
for (int i = 0; i < myArray.length; i++) {
    System.out.println(myArray[i]);
}
```

but there is an alternative way to write a loop called an *enhanced* for loop:

```java
for (int element : myArray) {
    System.out.println(element);
}
```

this is a simpler way to iterate through all the elements in a **collection**. We can implement this for other data structures in addition to arrays using `iterators`. Not all data structures are positional (ex: Sets do not have order inherently). This gives us a way of traversing the elements of a data structure.

###### Iterable and Iterators

To create a data structure that can be iterated upon, we can use the following declaration in the interface:

```java
public interface IndexedList<T> extends Iterable<T> {
    
}
```

adding the extension has some additional operations we have to provide implementations for in our implementation class:

```java
public Iterator<T> iterator() {
    //Arrays.stream(data).iterator(); //returns a sequence of data with an iterator. We will never do this.
    
}
```

```java
void testIteratorWithForEachLoop() {
    int counter = 0;
    for (int number : numbers) {
        assertEquals(defaultValue, number);
        counter++;
    }
    assertEquals(size, counter);
}
```

###### Custom Iterators

Iterators are classes. To implement our ArrayIndexedList as an iterable, we need to define a separate class that defines the iterator function:

```java
public class ArrayIndexedListIterator<T> implements Iterator<T> {
    // new class that implements the iterator interface. This plugs into an iterable.
    private T[] data;
    private int cursor;
    
    public ArrayIndexedListIterator(T[] data) {
        this.data = data;
        this.cursor = 0;
    }
    
    @Override
	public boolean hasNext() {
        return cursor < data.length;
    }
    
    @Override
    public T next() {
        if (!hasNext()) {
            throw new NoSuchElementException();
        }
        return data[cursor++];
    }
}
```

to understand what these functions are doing we have to realize that the enhanced for loop is syntactic sugar for this:

```java
Iterator<T> it = myCollection.iterator();
while (it.hasNext()) {
    MyType element = it.next();
    //do something with the element.
}
```

from this we see that the `next()` function returns the next element in the collection and `hasNext` tells you whether there is an element that hasn't yet been iterated over.

To do the implementation above, we store the data in a variable called data and use cursor to keep track of the current element. This is the index position of the current element. 

`hasNext` is true if the cursor is not at the last element and `next` returns the element pointed at by the cursor and advances it to the next element. If the client calls `next` when the iteration is over we throw `NoSuchElementException`.

To implement the iterator, we add the following to the ArrayIndexedList class:

```java
public class ArrayIndexedList<T> implements IndexedList<T> {
    @Override
    public Iterator<T> iterator() {
        return new ArrayIndexedListIterator<>(this.data);
    }
}
```

###### Inner Classes

It is common practice to define the iterator class within the class it is being defined for. This subclass becomes an inner class:

```java
public class ArrayIndexedList<T> implements IndexedList<T> {
  private final T[] data;

  // No changes were made to other operations. 

  @Override
  public Iterator<T> iterator() {
    return new ArrayIndexedListIterator();
  }

  private class ArrayIndexedListIterator implements Iterator<T> {
    private int cursor = 0;

    @Override
    public boolean hasNext() {
      return cursor < data.length;
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

doing the iterator definition like this helps with encapsulation, logically groups classes that depend on eachother for function, and leads to more readable and maintainable code. 

**We are required to use an inner class for iterator definitions in this class.**

### Linked Lists

Recall than an array is an object of a particular size. We need a bigger array to extend the size. We know where the array exists in memory and the size of each element. This allows us to move sequentially in memory to find an element with random access (direct access). To delete an element from the front or middle of an array we need to resize the array and move all the elements which is inefficient.

A linked list is a collection of objects that are themselves composed of data and a reference to another object. The first node is the head node and the final node points to `null`. It is easy to insert and remove nodes which is an advantage over arrays. 

###### References in Java

References in java are handled weirdly compared to C++ and C. A Java variable of the type Object stores a reference to an object. This is essentially a pointer giving the address of that object in memory. When an object variable is used in Java, it automatically follows (dereferences?) the pointer in memory to find the actual object. This is done behind the scenes instead of explicitly.

```java
//basic implementation of a linked list element.
public class Node<E> {
    private E data;
    private Node<E> next;
}
```

The declaration line does not create an object in memory. `next` is a variable that can hold a Node object. What gets stored in `next` is not the object but the memory address that corresponds to an object. Dereferencing happens automatically in Java. Java doesn't let you work with memory directly so this is how we have to deal with this, but we don't have to worry about memory leaks. Java is a garbage collected language which cleans up memory that goes out of scope. Technically `data` also points to an object of the generic type E.

```java
public class LinkedList<T> {
    private Node<T> head; //this is also a reference variable.
}
```

The linked list is terminated by `null` which is a memory address pointing to nothing and can be set to any type.

###### Static Nested Classes vs Inner Classes

This is another Java idiosyncracy.

To implement our linked list, we can use an inner type to nest the Node class within the linked list to encapsulate the data:

```java
public class LinkedList<T> {
    private Node<T> head;
    
    public LinkedList() {
        head = null;
        numElements = 0;
    }
    
    public void addFirst(T t) {
        Node<T> node = new Node<>(T);
        node.next = head;
        head = node;
        numElements++;
    }
    
    //no access to variables. Allows instantiation by linked list.
    private static class Node<T> {
        T data;
        Node next;
    }
    //access to the linked list variables and methods. Needs access to head.
    private class LinkedListIterator implements iterator<T> {
        //stuff
    }
}
```

A non-static nested class is known as an **inner class**. This means the class will have access to the variables from the outer class while the outer class will not have access to the variables in the nested class. A static nested class such as the one we are defining for linked list  does not have access to the elements outside but the outside does have access to the elements inside.

###### More Linked List Operations

```java
public T get(int index) {
    Node<T> cursor = head;
    for (int counter = 0; counter < index; counter++) {
        cursor = cursor.next;
    }
    return cursor.data;
}

public void addFirst(T t) {
    Node<T> newNode = new Node<>(t);
    newNode.next = head;
    head = newNode;
}

public void addLast(T t) {
    if (head == null) {
        addFirst(t);
    } else {
        Node<T> cursor = head;
        while (cursor.next != null) {
            cursor = cursor.next;
        }
        cursor.next = new Node<>();
        cursor.next.data = t;
        cursor.next.next = null;
    }
}

public void insert(int index, T t) {
    Node<T> cursor = head;
    for (int counter = 0; counter < index - 1; counter++) {
        cursor = cursor.next;
    }
    Node<T> node = new Node<>(t);
    node.next = cursor.next;
    cursor.next = node;
    numElements++;
}

public void delete(int index) {
    Node<T> beforeTarget = head;
    for (int counter = 0; counter < index - 1; counter++) {
        beforeTarget = beforeTarget.next;
    }
    //extract the node by removing pointer to next node.
    beforeTarget.next = beforeTarget.next.next;
}
```

To implement the linked list iterator, we need to loop over every element step by step. We always need a cursor to implement these more or less:

```java
private class LinkedListIterator implements Iterator<T> {
	Node<T> cursor;
    public LinkedLIstIterator() {
        cursor = head;
    }
    
    @Override
    public T next() {
        if (!hasNext()) {
            throw new NoSuchElementException();
        }
		T data = cursor.data;
        cursor = cursor.next;
        reutrn data;
    }
    
    @Override
    public boolean hasNext() {
        return cursor.next != null;
    }
}
```

### RAM Model

We want to be able to discuss the efficiency of our algorithms. The RAM model of computation gives us a way to begin doing this. In this context, the RAM is the memory of a hypothetical computer. In this model, we make some assumptions about our hypothetical computer:

We assume the RAM is arbitrarily large, that accessing the memory is free (it variable declaration, getting a value from memory, accessing an element of an array, accessing an object instance, and finding a method or function) does not cost us any time. We do not care where the RAM actually is whether it is a register, stack, heap, disk, or server.

We define simple operations which take one step: The assignment statement (=), arithmetic operations (+, -, *, /, %), the increment and decrement operators (++, --), combined assignment (+=, *=, etc...), comparison and relational operations (==, !=, <, <=, etc), logical operations (!, &&, ||), jump operations (return, break, and continue), branch operations (if, case), and user input and program output (print statements).

Loops on the other hand are the composition of many single-step operations. 

Even though we said calling a function is free, the function's runtime is affected by the function/method's time steps. We measure runtime by counting the number of steps it takes to execute a function under the RAM model.

For example:

```java
int count = 0; //one operation
for (int i = 0; i < 10; i++) { // 1 initial assignment, 11 < checks, 10 increments
    for (int j = 0; j < 5; j++) { //1 initial assignment, 6 < checks, 5 increments (every time above loop runs)
        count++; // 1 operation
    }
}
System.out.println(count); //1 operation
```

When a function's execution is dependent on an input of arbitrary size we abbreviate that size with N.

```java
public class Arrays {
    public static <T> void print(T[] arr) { //takes in an array of size N
        for (int i = 0; i < arr.length; i++) { // (1 + N+1 + N)
            System.out.println(arr[i]); //N * 1 .. note arr[i] and arr.length are free
        }
    }
}
```

thus, the total runtime of the above function would be $T(N) = 3N+2$

```java
public int myStrangeSum (int num) {
  int sum = 0; // 1
  int count = 2 * num; // 2
  for (int i = 0; i < count; i += 4) { //1 + (2*N / 4) + 1 + N/2
      sum += i; //1 * N/2 ... the loop runs 2*num / 4 times.
  }
  return sum;
}
```

so the total runtime of the above function is $T(N) = \frac{3N}{2} + 6$

###### Best and Worst Case Scenarios

Considering the following program

```java
public int indexOf(String str, char target) {
    for (int i = 0; i < str.length; i++) { //1 + N+1 + N || 1 + 1
        if (str.charAt(i) == target) { // N * (1 + 1) || 1 + 1
            return i; //0 || 1
        }
    }
    return NOT_FOUND; //1 || 0
}
//Worst case = 1 + N+1 + N*2 + N + N = 4N+3
//Best case (str.charAt(0) == target) = 1 + 1 + 1 + 1 + 1= 5 
```

the runtime of `indexOf` depends on where the `target` value is situated in the input String `str` - if it's in it at all.

Therefore there are two extreme cases,

the **best case scenario** is the minimum number of steps the algorithm takes for any input size.

the **worst case scenario** is the maximum number of steps an algorithm takes for any input size.

We generally ignore the best case and talk about efficiency in terms of the worst case scenario. The **average-case runtime** if the function defined by an average number of steps taken on any instance of size N. Usually considered when we have some kind of random process that occurs where we can draw conclusions based on the anticipated frequencies of the different inputs. This gets complicated so we will focus on **worst case runtime.** We can assume this is the runtime we're being asked for when prompted.

Consider the following:

```java
int sum = 0; // 1
String s = keyboard.nextLine(); // 1
String v = "aeiou"; //1
for (int i = 0; i < v.length(); i++) { //1 + 6 + 5
    if (s.indexOf(v.charAt(i)) >= 0) { // 5 * (1 + (4N+3) + 1) assume worst case-runtime for linear search of 4N+3
        sum++; // 1 (may be executed 0 to 5 times).
    }
}
```

we require detailed knowledge of every method we call's worst-case runtime to estimate it for a function that uses them.

Consider the following:

```java
public int myStrangeSum(int num) {
    int sum = 0; //1
    int numnum = 3 * num; //2
    for (int i = 0; i < numnum; i++) { //1 + 3*N+1 + 3*N
        for (int j = 0; j < 5; j++) { //3*N * ( 1 + 6 + 5)
            for (int k = i; k > 1; k--) { // 3*N * 5 * (X)
                sum++; //1*X*3N*5
            }
        }
    }
    return sum; //1
}
```

We don't know how long it takes to evaluate `X` by looking at it. We can set up a table of values from 0 to 3N-1 and look at the arithmetic sum that results:

doing that results in the complexity:
$$
T(N) = \frac {135N^2 - 9N + 28} {2}
$$
This is extremely tedious and not necessary. This is why we introduce the concept of **Big O** notation in the next section.

### Asymptotic Growth Rate

###### Big O Notation

Allows us to describe the relative growth rate of functions. We don't need to calculate precisely the number of operations each step takes. This is an approximation based on asymptotic analysis from a branch of mathematics.

$T(N)$ indicates an algorithm's precise runtime while $O(N^2)$ indicates the asymptotic runtime. To convert between the two, we drop all constants and only keep the highest order term. 

```java
public void countUp(int num) {
    for (int i = 1; i <= num; i++) {
        System.out.println(i);
    }
}

public void countUp(int num) {
    int count = 1;
    for (int i = 0; i < num * 2; i+=2) {
        System.out.println(i);
    }
}

public void countUp(int num) {
    int count = 1;
    int upper = num * 2;
    for (int i = 1; i <= upper; i+=2) {
        System.out.println(count++);
    }
}
```

all three of the above functions count in linear time. They do so differently with different precise runtimes (constants), but the main point here is that they do the same thing. We just take the first order term so we call them all $O(N)$

We make the assumption that the data is constantly increasing in size which is generally a true assumption for algorithms.

Give the Big O notation for the following precise runtimes:

$T(n) = 5 + 0.001n^2 + 0.025n$ has an asymptotic time complexity of $O(n^2)$

$T(n) = 3 log(n^2) + (log(n))^2 + (n+1)^2 * log(4n)$ this has an asymptotic time complexity of $O(n^2 log(n))$ recall the rules of logarithms to simplify this down to a polynomial $n^2log(n) + 2n^2 + 2nlog(n) + 4n + log^2(n) + 8 log(n) + 2$

We need to be able to look at an implementation and reason about its performance:

```java
public boolean contains(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) { //N operations
        if (arr[i] == target) {
            return true;
        }
    }
    return false;
}
```

has a asymptotic complexity of $O(N)$ because the loop runs $N$ times with some constant operations within.

```java
public boolean contains(int[] a, int[] b, int target) {
    for (int i = 0; i < a.length; i++) { //N operations
        if (a[i] == target) {
            return true;
        }
    }
    
    for (int i = 0; i < b.length; i++) { //N operations
        if (b[i] == target) {
            return true;
        }
    }
    return false;
}
```

has complexity $O(n)$ because there are two loops with the same complexity which we drop the 2*N constant from.

```java
public boolean hasCommonElement(int[] a, int[] b) {
    for (int i = 0; i < a.length; i++) {
        for (int j = 0; i < b.length; j++) {
            if (a[i] == b[j]) {
                return true;
            }
        }
    }
    return false;
}
```

has a complexity of $O(N^2)$ because the second loop takes N operations and is called N times.

```java
public boolean hasDuplicates(int[] a) {
    for (int i = 0; i < a.length; i++) {
        for (int j = i + 1; j < a.length; j++) {
            if (a[i] == a[j]) {
                return true;
            }
        }
    }
    return false;
}
```

The outer loop executes N times. While the inner loop executes (n-1) + (n-2) + (n -3) + ... + 1 + 0 times which if we apply gauss's formula for the sum of the first N-1 integers, $N-1(N) / 2$  which gives us the runtime O(N)

```java
public int myStrangeSum(int num) {
    int sum = 0;
    for (int i = 1; i < num; i *= 2) { // N/2/2/2... loops which is log(n)
        sum += i;
    }
    return sum;
}
```

First loop is 1 step, second loop is 2 steps, third loop is 4 steps. How many steps are taken from the start to the end? There are $log_2(n)$ steps required to halve n until it equals 1. In most cases in computer science, we are dealing with log base 2, which we denote $lg$

```java
public int indexOf(String str, char target) {
    for (int i = 0; i < str.length; i++) { //Loop N times
        if (str.charAt(i) == target) {
            return i; 
        }
    }
    return NOT_FOUND; 
}
```

in the worst case, this takes N loops, In the best case this takes 1 loop and a couple constant operations. This is indicated by $O(1)$ which is the constant time order.

Now consider the following operations: 

inserting into the front of an array or linked list: For a linked list, we can do this in O(1). For a regular array, this would take O(N).

inserting into the middle of an array or linked list: For middle insert, for a regular array, this would be O(N/2)=O(N). 

inserting at the back of an array or linked list: For a regular array, this would be O(1).

deleting an item from the array (front middle or back): To delete front would need O(N) because we'd have to shift everything to the left. If we don't care about the order of the array, we could take an element from the end of the array and replace any index with this element. Generally the order is important though so we wouldn't do this.

accessing an item in the array and reading its value at a random index: Should be O(1) because accessing is generally constant time.  

###### Big O Growth Order

$$
O(1) < O(log(n)) < O(n) < O(nlog(n)) < O(N^2) < O(N^k) < O(c^n) < O(n!)
$$

When we have an $O(1)$ operation, runtime is independent of input size, but this does not mean it only takes one step. When we have an $O(lg(N))$ function, we call this a **sub-linear** function. Runtime grows slower than the size of the problem (binary search). $O(N)$ has a run time proportional to the input size (linear search). $O(nlog(n))$ **super-linear functions** also called **linearithmic** functions. (merge sort and heap sort). $O(N^2)$ are quadratic functions where runtime is proportional to the square of input size (bubble sort, insertion sort, selection sort). $O(n^k)$ are polynomial functions where the k is a constant greater than or equal to 1 (enumerating the subsets of k nodes in n nodes). $O(k^n)$ are exponential functions which enumerate all subsets of n items. $O(n!)$ are factorial functions (generating all possible permutations or orderings of n items).

### Asymptotic Analysis

This chapter covers the mathematical nuance of the asymptotic notation (mathematically proving these). We don't need to take notes on this chapter because it's generally outside the scope of the course.

###### Asymptotic Complexity

Use asymptotic notation to describe the computational complexity - how many resources are used by the program. 

**Time complexity** is the asymptotic analysis that we have used in this course up to this point. 

**Space complexity** measures the amount of memory an algorithm needs to run as a function of its input size. Want to know how space consumption grows as the size of the input increases. There are two measures of space complexity:

**Auxiliary space** which is the extra space or temporary space used by an algorithm during execution. We define Space complexity in this class as
$$
Space \ Complexity = Auxiliary \ Space + Input \ Space
$$
The **input space** is the memory consumed to store the values that are inputted to solve the problem.

Sometimes the two components are both talked about independently as Space Complexity in different resources. 

| **Algorithm** | **Time Complexity** | **Space Complexity** | **Input Space** | **Auxiliary Space** |
| ------------- | ------------------- | -------------------- | --------------- | ------------------- |
| Linear Search | O(N)                | O(N)                 | O(N)            | O(1)                |
| Binary Search | O(lg(N))            |                      |                 |                     |

for linear search, the input space is $O(N)$ since we need an array of length N to store the numbers to search. The Auxiliary Space is $O(1)$ because there are a constant number of variables defined to hold the indices to search the input which do not depend on the input size. 

for binary search we also require an input space of $O(N)$ because we also need to hold the numbers in an array. When the Auxiliary Space is defined for an iterative implementation of binary search, it occurs in $O(1)$ variables since there are a constant number of variables defined for each loop. If the implementation is done recursively, the number of recursive function calls varies with the input size. This is an $O(lg(N))$ process because the number of recursive calls needed to complete the search is halved at each step. A version of the binary search algorithm can have $O(NlgN)$ input space if you need to copy the input array on each loop. Since the iterative implementation is more efficient, this is generally best, but recursive implementations are generally easier to implement especially for things like traversing trees. 

```java
public static void countup(int n) {
    for (int i = 1; i <= n; i++) {
        System.out.println(i);
    }
}
```

```java
public static void countup(int n) {
    if (n > 1) {
        countup(n-1);
    }
    System.out.println(n);
}
```

| `countup`             | **Time Complexity** | **Space Complexity** | **Input Space** | **Auxiliary Space** |
| --------------------- | ------------------- | -------------------- | --------------- | ------------------- |
| first implementation  | O(N)                | O(1)                 | O(1)            | O(1)                |
| second implementation | O(N)                | O(N)                 | O(1)            | O(N)                |

```java
public class Arrays {
  public static <T> void reverse(T[] arr) {
    T temp;
    for (int i = 0, j = arr.length - 1; i < j; i++, j--) {
      temp = arr[i];
      arr[i] = arr[j];
      arr[j] = temp;
    }
  }
}
```

```java
public class Arrays {
  public static <T> void reverse(T[] arr) {
    int n = arr.length;
    T[] tmp = (T[]) new Object[n];

    for (int i = 0; i < n; i++) {
      tmp[i] = arr[n - i - 1];
    }

    for (int i = 0; i < n; i++) {
      arr[i] = tmp[i];
    }
  }
}
```

| `reverse`             | **Time Complexity** | **Space Complexity** | **Input Space** | **Auxiliary Space** |
| --------------------- | ------------------- | -------------------- | --------------- | ------------------- |
| first implementation  | O(N)                | O(N)                 | O(N)            | O(1)                |
| second implementation | O(N)                | O(N)                 | O(N)            | O(N)                |

### Quadratic Sorts

Here we discuss three quadratic complexity sorting algorithms: **Selection Sort**, **Insertion Sort**, and **Bubble Sort**. 

We have the sorting algorithm interface:

```java
public interface SortingAlgorithm<T extends Comparable<T>> {
	//Sorts a collection
    void sort(IndexedList<T> indexedList);
    
    //Name of algorithm
    String name();
}
```

###### The Comparable Interface

the line `<T extends Comparable<T>>` indicates to the implementation that the type that we put into the indexed list must be comparable between objects. Comparable is an interface that allows us to use the `compareTo(T obj)` function. A negative integer is returned by this function if the object passed into the function is greater than the object we call it on as in `5.compareTo(4)` returns a negative value. A positive integer is returned if the object passed in is less than the object called on, and zero is returned if the two are equal. 

The comparable interface allows us to define what it means for objects to be greater than, less than, or equal to another. 

```java
public class Student {
    private String name;
    private String email;
    
    public Student(String name, String email) {
        this.name = name;
        this.email = email;
    }
    
    public String getName() {
        return name;
    }
    
    public String getEmail() {
        return email;
    }
    
}
```

by default instances of Student are not comparable.

```java
public static void main(String[] args) {
    SortingAlgorithm<Student> mySort = new SelectionSort<>();
    IndexedList<Student> roster = new ArrayIndexedList<>(75, null);
    mySort.sort(roster);
}
```

to allow Student to be comparable, we update it as so:

```java
public class Student implements Comparable<Student> {
    ...
    //sort by email.
    @Override
    public int compareTo(Student other) {
        return this.email.compareTo(other.email);
    }
}
```

So, let's look at the code for the different sorting algorithms. 

###### Selection Sort

Works by scanning the list for the smallest element and swapping this element for the first element, it then scans the n-1 elements of the list for the next smallest element and swaps this element with the second element, it then continues until there are only two elements left in the list where it swaps them if necessary and completes. Selection sort because it selects the smallest or largest element and then puts the element in the correct position. 

```pseudocode
for i gets the values from 0 to length-2
	min = i
	for j gets the values from i+1 to length-1
        if val[j] < val[min]
            min = j
	swap val[min] and val[i]
```

The time complexity is $O(N^2)$ the input space is of $O(N)$ and the auxiliary space is $O(1)$ for a total space complexity of $O(N)$

this is a comparison-based sorting algorithm. It does a comparison and then swaps elements. To reason about the complexity, we can count the number of swaps and comparisons. We require $O(N^2)$ comparisons and $O(N)$ swaps.

###### Insertion Sort

In insertion sort, we divide the list into two parts, a sorted part and an unsorted part. We start by inserting the first element into the sorted portion. We then look at the first element in the unsorted part and insert it into the sorted part by ensuring that it remains sorted. We then look at the next element and compare it to all of the elements in the sorted part making sure it remains sorted, we then repeat until all elements are in the sorted part and the unsorted part is empty.

```pseudocode
for i gets values from 1 to length-1
	j gets i
	while j > 0 and val[j] > val[j-1]
		swap val[j] and val[i]
		decrement j by 1
	//all elements to the left of index i are sorted when while loop exits.
```

Time complexity is $O(N^2)$ and space complexity is $O(N)$

###### Bubble Sort

Bubble sort goes over all the elements by two and swaps them until the largest element "bubbles up" to the end of the array. 

```pseudocode
for i gets the value from last index to 1
	for j gets the values from 0 to i-1
		if val[j] > val[j+1]
			swap val[j] & val[j+1]
```

A round that has no swaps can indicate that the array is already sorted which can save some time in good cases. This is known as the **early stop heuristic.** This saves a lot of time when there are very many numbers that are just a little bit out of order.

Time complexity is $O(N^2)$ and space complexity is $O(N)$

### The Stack Data Structure

###### Limited Access Data Structures

An array is a **random access data structure** where any element can be accessed directly and in constant time. Random access is required for some algorithms like Binary Sort.

A linked-list is a **sequential-access data structure** where each element can be accessed only by traversing the entire list.

A **stack** and a **queue** are examples of **limited-access data structures** where you can only access the element in the front or back position (or both) and access to other parts is forbidden. By limiting access, we can get very efficient implementations. 

###### Stack Abstract Data Type

The stack ADT has two main operations

**Push** which adds an element to the data structure and **pop** which removes the most recently added element that was not yet removed.

The order in which the elements gives the nomenclature **LIFO** which stands for last-in first-out to describe a stack. Think of a tall stack of books. Add to top or remove from top.

Every time we run a program, we utilize a stack of calls which ensure that the last thing gets executed first. Also used in an undo function in a text editor.

```java
public interface Stack<T> {
    boolean empty();
    T top() throws EmptyException;
    void pop() throws EmptyException;
    void push(T t);
}
```

we have `pop()` which removes without returning the element. `top()` returns the element without removing it.

`EmptyException` is a runtime exception so we are not forced to handle it.

###### Singly-Linked List Implementation of Stack

Singly linked-list implementation of a stack. We want to use the head to represent the top of the stack. We can implement the `push` method as the `addFirst` or prepend operation. `top` can return the `head.data`. `pop` can excise the head by setting `head = head.next`. These are all constant time operations. 

Practice implementing the `LinkedStack` for the midterm. 

###### Array Implementation of Stack

We could also implement a stack using an array to hold the data. We could implement the `empty()` function by checking if `numElements` of the array is zero. We could implement `top` we could return the element at the end of the array by indexing with `numElements-1`. `pop` could be implemented by setting the last element equal to the default value. `push` could be implemented by decrementing the value of `numElements` even if we don't overwrite the value of the element that was at the top to null.

Practice implementing the `ArrayStack` for the midterm.

Remember that to create an array that can hold any type, we need to use the following line:

```java
data = (T[]) new Object[capacity];
```

###### Resizing a Stack

When the number of elements is equal to the size of the stack, we can re-instantiate the array with doubled capacity.

We can start the implementation of  the ArrayStack with a constant size and define a `grow` function that doubles the capacity of the array after the object is filled

```java
private void grow() {
    temp = (T[]) new Object[capacity*2];
    for (int i = 0; i < numElements; i++) {
        temp[i] = data[i];
    }
    data = temp; //point data to the temp array
    capacity *= 2;
}
```

This implementation is a linear time operations. 

```java
public void push(T value) {
    if (numElements == capacity) {
        grow();
    }
    data[numElements++] = value;
}
```

Push is a linear time operation in the worst case (the array needs to grow), but otherwise it is $O(1)$. We want an $O(1)$ implementation like we had for the linked list. 

We want our grow operation to do a multiplicative size increase to ensure we get an amortized analysis of $O(N)$. If we used a fixed size incrementation, we would need to run the grow method much more frequently and would lose out on the time savings when inserting very large numbers of elements:

### Amortized Analysis

**Amortized Constant Time** describes the operation of the `push` function. We require $O(N)$ time to grow the array. This is the cost **per operation** for a sequence of n operations. If somewhere in the execution there is an $O(N)$ process that needs to occur, this additional time complexity can be thought of as spread across the other $O(1)$ operations. 

If we run an operation n times where each run takes one RAM step, followed by an operation that takes n steps, the amortized cost of this operation is 
$$
\frac {n + n}{n + 1} < \frac{2n}{n} = 2 \in O(1)
$$
calling such a process n+1 times, calls n $O(1)$ operations plus one $O(n)$ operation. Dividing 2 $O(n)$ processes over n processes gives us an overall protocol average operation cost of 2 which is in $O(1)$

This is especially useful for data structures. The more complicated they get, the more often you need to do this kind of analysis. If you have a tree or something that needs to be rebalanced every once in a while, we don't want the worst case because that would misrepresent the average time it takes to run a process.

## Unit 2

### The Queue Data Structure

There are two main operations, `enqueue` and `dequeue` which makes it a FIFO data structure: first in, first out.

This is analogous to a line of people. Get there first, get served first. Another example is a job queue for a single threaded server.

The Queue ADT:

```java
public interface Queue<T> {
    void enqueue(T value);
    //Removes the element at the front of this queue.
    void dequeue() throws EmptyException;
    //Peeks at the front of the queue without removing it.
    T front() throws EmptyException; 
}
```

We could implement this with a linked list or an array as with the stack.

###### Singly Linked List Implementation of Queue

Can represent the Queue ADT efficiently as long as it has a `tail` pointer which points to the last element of the list. I'm not 100% sure about the implementation below but when studying for the next midterm look at the solution provided and compare.

```java
public class LinkedQueue<T> implements Queue<T> {
    private Node<T> head;
    private Node<T> tail;
    
    public LinkedQueue() {
        head = null;
        tail = head;
    }
    
    @Override
    void enqueue(T t) {
        if (head == null) {
            head = new Node<T>();
            head.next = null;
            head.data = t;
        } else {
            tail.next = new Node<T>();
            tail.next.next = null;
            tail.next.data = t;
            tail = tail.next;
        }
    }
    
    @Override
    void dequeue() {
        head = head == null ? null : head.next;
    }
    
    @Override
    T front() {
        return head.data;
    }
}
```

We want to use the head to represent the beginning of the list because we can `enqueue` easily at the end of the list and `dequeue` easily at the head of the list. We cannot `dequeue` from the tail of the list because we would need to search through the entire list to find the element before the tail to point it to null.

###### Array Implementation of Queue

This is a more complicated implementation. We create a variable to hold the "back" of the array which points to the first open element. We pretend the array is circular in that the back of the array can be incremented to wrap back around to the front of the array. We need to dynamically grow this array when back is equal to front.

```java
public class ArrayQueue<T> implements Queue<T> {
    private int front;
    private int back;
    private int[] data;
    private int numElements;
    private int capacity;
    
    public ArrayQueue() {
        front = 0;
        back = 0;
        numElements = 0;
        capacity = 1;
        data = new int[capacity];
    }
    
    @Override
    public void enqueue(T t) {
        data[back] = t;
        back = ++back % capacity;
        numElements++;
        if (numElements == capacity) {
            grow();
        }
    }
    
    @Override
    public void dequeue() {
        if (empty()) {
            throw new EmptyException();
        }
        front = ++front % capacity;
        numElements--;
    }
    
    @Override
    public T front() {
        if (empty()) {
            throw new EmptyException();
        }
        return data[front];
    }
    
    private void grow() {
        newArr = new Int[capacity * 2];
        for (int i = 0; i < capacity; i++) {
            newArr[i] = data[front];
            front = ++front % capacity;
        }
        data = newArr;
        front = 0;
        back = capacity;
        capacity *= 2;
    }
    
    private void shrink() {
        //you could also implement this to shrink when numElements < capacity/2
    }
    
    private boolean empty() {
        return numElements == 0;
    }
}
```

###### More Limited Access Data Structures

A Steque ADT is a data structure that supports push, pop, and enqueue (adding to the bottom of the steque). This allows you to add at both ends but only remove from one end. A Quack ADT is a data structure that has push and pop as well as dequeue meaning you can add only to the top but can remove from the top or the bottom. A Deque is a data structure that allows insertion or removal at either end in O(1). A deque allows you to implement any of the previously mentioned data types by just choosing which end will be the front and which ways you choose to add and remove elements relative to the front. 

Practice implementing the Deque as practice for the next midterm.

### Positional List

###### Doubly Linked List

A linked list with nodes that track both their next node and previous nodes.

```java
public class DoublyLinkedList<T> {
    private Node<T> head;
    private Node<T> tail;
    private int numElements;
    
    //Because we are exposing the Node Class to the client, we need to declare as public to allow client to access.
    //We dont really want to do this though because the client can mess with the internals of the list.
    private static class Node<E> implements Position<E> {
        E data;
        Node<E> next;
        Node<E> prev;
        DoublyLinkedList<E> owner; //unique identifier for a given DLL class (memory location at "this")
        
        Node(E data, DoublyLinkedList<E> owner) {
            this.data = data;
            this.next = null;
            this.prev = null;
            this.owner = owner;
        }

        @Override
        E get() {
            return data;
        }
    }
    
    public DoublyLinkedList() {
        head = null;
        tail = null;
        numElements = 0;
    }
    
    public Position<T> addFirst(T t) {
        if (head == null) {
            head = new Node(t, this);
            head.next = null;
            head.prev = null;
            tail = head;
        } else {
            newNode = new Node(t, this);
            newNode.next = head;
            head.prev = newNode;
            newNode.prev = null;
            head = newNode;
        }
        numElements++;
        return head;
    }
   
    public Position<T> addLast(T t) {
        if (tail == null) {
            tail = new Node(t, this);
            tail.next = null;
            tail.prev = null;
            head = tail;
        } else {
            newNode = new Node(t, this);
            newNode.next = null;
            tail.next = newNode;
            newNode.prev = tail;
            tail = newNode;
        }
        numElements++;
        return tail;
    }
    
    public Position<T> get(int idx) {
        Node<T> cursor = tail;
 		for (int j = numElements - 1; j > idx; j--) {
            cursor = cursor.prev;
        }
        return cursor;
    }
    
    private Node<T> convert(Position<T> position) throws PositionException{
        //Need to handle condition where position is a different implementation of Position that cannot be cast to a Node.
        //handle case where position is also null.      
        try {
            Node<T> node = (Node<T>) position;
            if (node.owner != this) {
                //You could also pass a Position that belongs to another implementation of a DLL. In this case, the thing that is passed in is correctly a node, but this thing is not a node that belongs to this DLL. To handle this, we can create a pointer to the parent class that gets stored in the Node class.
                throw new PositionException();
            }
        } catch (NullPointerException | ClassCastException e) {
            throw new PositionException();
        }
        
        return node;
    }
        
    public void delete(Position<T> target) {
        Node<T> target = convert(target);
		//TODO: handle empty list edge cases.
        target.prev.next = target.next;
        target.next.prev = target.prev;
        
        numElements--;
    }
    
    public Position<T> insertAfter(Position<T> target, T data) {
        Node<T> node = new Node<T>(data, this);
        Node<T> target = convert(target);
        node.next = target.next;
        target.next.prev = node;
        target.next = node;
        node.prev = target;
        return node;
    }
    
    public Position<T> insertBefore(Node<T> target, T data) {
        Node<T> node = new Node<T>(data, this);
        Node<T> target = convert(target);
        target.prev.next = node;
        node.prev = target.prev;
        node.next = target;
        target.prev = node;
        return node;
    }
}
```

we are able to traverse the list in any direction. **All of the implementations above have unhandled edge cases.**

How can we get a pointer to a node in the list though? We want to find a way to expose the nodes to a client.

We can also return a pointer to each node we create after each item is inserted so the user can pass the returned node along the way. 

We don't want the client to mess with the data structure, but we don't want to expose the node by changing it to public. 

```java
public interface Position<T> {
    //don't need a function at all. just want a way to keep the node hidden from the client.
    //implementing the node as an implementation of position, means the client can only instantiate a position.
    
    //Returns the data at a position but said data does not modify value at the node.
    T get();
}
```

By creating a node as an implementation of position, the client no longer has access to our next and previous pointers so they cant mess with the internals of the data structure. We have to change our functions to downcast a position to a Node since downcasting is not automatic (upcasting from a Node to a Position would be such as when we return a Node, the user can store this in a Position variable).

###### List ADT

This is a more general implementation of a list than indexed list. Using this we can implement any of the restricted access data structures we talked about previously but we have even more functionality since we can access data at any index of the list.

```java
public interface List<T> extends Iterable<T> {
    int length();
    boolean empty();
    Position<T> insertFront(T data);
    Position<T> insertBack(T data);
    Position<T> insertAfter(Position<T> p, T data) throws PositionException;
    Position<T> insertBefore(Position<T> p, T data) throws PositionException;
    void remove(Position <T> p) throws PositionException;
    void removeFront() throws EmptyException;
    void removeBack() throws EmptyException;
    Position<T> front() throws EmptyException;
    Position<T> back() throws EmptyException;
    boolean first(Position<T> p) throws EmptyException; //if position p is the first element in the list
    boolean last(Position<T> p) throws EmptyException;
    Position<T> next(Position<T> p) throws PositionException; //the next element in the list after p
    Position<T> previous(Position<T> p) throws PositionException;
    Iterator<T> forward();
    Iterator<T> backward();
}
```

in order to implement these operations efficiently, you NEED to implement the list interface using a Doubly Linked list. An array or singly linked list implementation will not be able to perform all of these operations in constant time. 

For example, remove cannot be done with an array efficiently because the array will need to shift every thing over. The singly linked list cannot get access to the previous element without iterating from the head so it also cannot be done in O(1) time. 

There is an exercise to implement the `LinkedList` which is an implementation of the List ADT as a doubly linked list. To do this, we will also have to handle all the null pointer exception edge cases from the DLL implementation from before. 

To minimize the number of edge cases we have to handle in the DLL implementation, we can use the **sentinel nodes** strategy. Sentinel nodes are "dummy nodes" that the client never has access to, but we create so that we never have a case where head and tail are null or when they point to the same thing: 

![image-20211017234203134](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211017234203134.png)

The true elements of the list will always be between the head and tail dummy nodes. 

```java
public DoublyLinkedList() {
    head = new Node(null, this);
    tail = new Node(null, this);
}
```

if we do this our addFirst implementation can't use `head` directly anymore, we have to implement `head.next` which isn't too hard. This implementation is much less prone to error!

### The Set Data Structure

```java
//The iteration order is undefined, client should not expect a particular element order.
public interface Set<T> extends Iterable<T> {
    void insert(T t); // set doesnt change if t is already in the set.
 	void remove(T t); // removes t from set
    boolean has(T t); // whether element is in the set.
    int size(); // utility method to know the number of elements in the set.
}
```

a set is a collection of unique objects with no notion of order. We can also define an ordered set that has Comparable elements. In this implementation, we haven't defined any error throwing, the implementation will just ignore bad elements. 

###### Linked Implementation of Set

Singly linked implementation of a set:

`has` can be implemented by performing linear search over the nodes and checking for the element in O(N) time. We cant do binary search even if the set is sorted because we can't jump around in position, linked lists are sequential access data sets.

`insert` can be implemented by running addFirst only if `has` returns false. O(N)

`remove` have to find the element to remove it which can be done in constant time by finding node before the one we want to remove but still O(N)

`size` can be done in O(1) if we have an integer to track `numElements`.

There are some ideas we can implement to make these operation more efficient in practice.

Implementing these operations for the `LinkedSet` is left as an exercise for preparation for the next midterm.

**Improving the performance of the linked set**

The Move To Front Heuristic moves the target of a search to the head of a list so that it is found faster next time. Items that are searched for more frequently are more quickly found. Speeds up the linear search. This operates under the assumption that some subset of the total number of values is being searched more frequently than the total number of objects in the set. To do this, we `remove(n)`, `prepend(n)`, and return the head. We need to do these operations in linear time so that the heuristic will actually improve the time taken to run the algorithm. We could do remove in linear time by tracking the previous node.

###### Array Implementation of Set

`has` runs linear search on the array and finds if the element is in the set in O(N). If the type in the set, we could keep the set ordered and implement binary search, but we don't necessarily know that the data is ordered so we can't do this.

`insert` appends the element to the end of the array and grows array if necessary needs to run `has` so runs in amortized O(N)

`remove` runs has to check if item in the list, if it is, we can swap the last element in the array with this element and decrement `numElements`

`size` just returns `numElements` in O(N)

implementation is left as an exercise.

Can we use a heuristic here? We can't implement the move to front heuristic in O(1) time since we cant efficiently move element order in an array without copying the elements after the moved elements through the rest of the list. We would lose the order of the previously searched for elements if we implemented a swap heuristic. This cannot be done in O(1) since copying the elements has a worst case efficiency of O(N). It is also possible to implement move to front heuristic with a circular array but it gets pretty complicated and is prone to error.

There is actually a heuristic that we can use to help speed up the searches over many searches. We can do this by saying that any time we access an element, swapping it with its element to the left. This is transpose sequential search. This won't be as fast as move to front heuristic since we have to wait for the element to percolate to the front of the list.

###### Set Iterator

To implement the set iterator, it makes the most sense to iterate from head to tail in a linked set and from index 0 to numElements-1 in an array set.

###### Fail-Fast Iterators

We really don't want to allow users to modify a data structure while iterating over it. This can corrupt the iteration because say we were at a node in a linked list in our iteration and removed its next node. The iterator would move to the next node but this node is deleted so we might get undefined behavior leading to incomplete or incorrect iteration. 

We need to specify a way for our data structures to detect modification when being iterated over and throw errors to prevent the user from doing this. Java throws `ConcurrentModificationException` to alert the user of this. This is very useful for implementing multithreaded programming where modification in one thread may occur while another thread is iterating over the data structure.  

We never have to actually implement this because it's an issue of the client to alter the data structure while iterating over it, but we also will see how to fix this if we ever need to. Iterators also have remove methods in java and these are what should be asked to reorder the data structure not the object being iterated over. 

To implement this, we need a way of telling the iterator that the data structure has been modified since iteration started. We could have a boolean `modified` that is set to true by all of our mutation methods. We could also create a counter that measures the number of modifications of the data structure. The iterator can check the number of modifications at the beginning of iteration and then make sure this value stays constant throughout iteration. 

###### Ordered Set

```java
public interface OrderedSet<T extends Comparable<T>> extends Set<T> {
    
}
```

Linked List implementation

`has` cannot be implemented for binary search in a linked list implementation despite the sorted data so we need to use linear search, `insert` can be done with insertAfter, `remove` and size are the same as before

Array Set Implementation

We can finally do binary search for our has implementation `has` is then O(lg N), but our remove and insert operations require shifting the other elements of the array so these operations are still O(N), and size is still O(1).

###### Set Theoretical Operations

The union of two sets is the set of both elements of A and B

the intersection of two sets is the elements in both A and B

the set difference is the set of elements in A that are not in B: A-B

implementing these operations efficiently for objects of the Set class is a useful programming exercise and can be difficult. This is hard so it's not necessarily something we will cover in the class.

### Binary Search Tree ADT

A tree is composed of **nodes**. The first node from which the tree originates is called the **root node**. A binary search tree is a branched data structure (a generalization of a linked list). Every node except for the rode node has a **parent** and zero or more **children**. Nodes that do not have children are called **leaves**. **descendents** are all the nodes that are children or children of those children. **ancestors** are the opposite, the parents and parents of parents. **siblings** are nodes that share a parent.

###### Binary Tree

A binary tree has at most two children (two = binary). A binary tree is an inherently recursive structure! Each child from the root is itself a binary tree. Every tree is a node that has a right and left subtree.

###### Binary Search Tree

Has an ordering property. The nodes of the tree follow an ordering criteria. Every value to the left of a node is less than the node, every value to the right is larger than the node.

```java
public class BstOrderedSet<T extends Comparable<T>> implements OrderedSet<T> {
    private Node<T> root;
    
    private static class Node<E> {
        E data;
        Node<E> left;
        Node<E> right;
        
        Node(E data) {
            this.data = data;
        }
    }
}
```

A non-linear linked structure when compared to linked list which is a linear linked structure. 

Looks a lot like the node class in the doubly-linked list but the implementation and conservation of order is what distinguishes the two.

To insert a node, the search process is repeated and if the target is found, we return or throw an exception to alert user of duplicate value. Otherwise, we find the leaf that we can add the target value to. Once we have traversed the tree, we just create a new node at the right or left of the node.

Removal is more involved. Consider 3 scenarios. The simplest case is when we want to remove a leaf. To do this, we can find the previous node, then point the pointer to this node to null. A more complex case is when we want to remove a node inside the tree with only one child. To fix this, we can promote the child. Just connect the parent to the child The most complex case is when the node to be removed has two children. To do this, find the **in-order successor* which is the child node that comes directly after (or before) the target node for deletion in a sorted list of values. We then promote this value to the position of the node to be deleted and point it to the deleted node's children. This means finding the largest value in the left subtree or the smallest value in the right subtree and swapping this with the target. Once we have swapped the target with the successor, we remove it again and the process repeats until we have a simpler case as defined above.

You could simplify the removal processes by having the node track their parent, but we don't do this.

```java
public class BstOrderedSet<T extends Comparable<T>> implements OrderedSet<T> {
	Node<E> root;
    private int numElements;
    
    public BstOrderedSet() {
        root = null;
        numElements = 0;
    }
    
    //iterative implementation
    @Override
    public void insert(T t) {
        Node<T> curr = root;
        while (curr != null) {
            int cmpt = root.data.compareTo(t);
            if (cmpt == 0) {
                return; //we have duplicate so dont do anything
            } else if (cmpt > 0) {
                //explore the left subtree
                if (curr.left != null) {
                    curr = curr.left;                    
                } else {
                    curr.left = new Node<T>(t);
                }
            } else {
                //explore the right subtree.
                if (curr.right != null) {
                    curr = curr.right;
                } else {
                    curr.right == new Node<T>(t);
                }
            }
        }
        //I know i dont have t in the tree, so insert here.
        return; 
    }
    
    //recursive implementaion
    @Override
    public void insert(T t) {
        root = insert(root, t);
    }
    
    private Node<T> insert(Node<T> curr, T t) {
 		//base case    
        if (curr == null) {
            return new Node<>(t);
        }
        
        int cmpt = root.data.compareTo(t);
		if (cmpt > 0) {
            //explore left subtree
            curr.left = insert(curr.left, t);
        } else if (cmpt < 0) {
            //explore right subtree
        	curr.right = insert(curr.right, t);
        }
        //we have duplicate, so exit.
        return curr;
    }
	    
    @Override
    public void remove(T t) {
        
    }
    
    //Iterative Implementation
    private Node<T> find(T t) {
        Node<T> curr = root;
        while (curr != null) {
            int cmpt = root.data.compareTo(t);
            if (cmpt == 0) {
                return curr;
            } else if (cmpt > 0) {
                //explore the left subtree
                curr = curr.left;
            } else {
                //explore the right subtree.
                curr = curr.right;
            }
        }
        return null; //NOT_FOUND
    }
    
    //Recursive implementation, takes root in on first call.
    private Node<T> find(Node<T> curr, T t) {
        if (curr == null) {
            return null; // Not_found base case.
        } 
        int cmpt = root.data.compareTo(t);
        if (cmpt == 0) {
            return curr;
        } else if (cmpt > 0) {
            return find(curr.left, t);
        } else {
            return find(curr.right, t);
        }
    }
    
    @Override
    public void has(T t) {
        Node<T> target = find(t);
        return target != null;
    }
    
    @Override
    public int size() {
        return numElements;
    }

}
```

The binary search tree is only more efficient than linear search when the tree is balanced. If the data is inserted from smallest to largest, we just create a linked list which is not a balanced tree and searching is just linear search. We will talk about balancing the tree later.

**Implement the remove method as practice to make sure you understand what's going on!**

### Trees and Tree Traversal

How should we implement the iterator to iterate all the elements in the BST. We have a few different traversal strategies for doing this:

###### Level-Order Traversal

This says go over the tree level-by level. Start at root and print every node to the left and right, then go to those nodes, and return all of their direct children. Then continue until there are no more children.

###### In-Order Traversal

This prints the elements of the list in order. We start at the root, first visit everything to the left first, then print the root, then print the right. We can do this recursively for each subtree from the root. Once we find the leftmost element we print it then go to its parent and print that, then print the nodes on the right of the parent considering each node a subtree. The strategy is Left, Root, Right.

```java
inOrder(node) {
    if (node.left != null) {
    	return;
    }
    inOrder(node.left);
    print(node);
    inOrder(node.right);
}

//Iterators need to be implemented iteratively.
//O(1) time, but O(N) space in worst case (unbalanced tree). There is a way to implement this in O(1) space, but you need to augment the tree by adding backwards linked pointers to the nodes.
inOrder_iterative(Node<T> node) {
    //Need an auxillary space data structure to do this.
    //Use a stack to recreate the call stack of the recursive implementation
    Stack<Node<T>> stack = new Stack<>;
    while (stack.empty() == false) {
    	pushAsLongAsLeft(stack, node); //As long as there is a left node, add node to stack until left is null.
        Node<T> toPrint = stack.pop();
        print(toPrint);
        node = toPrint.right; //might need to check if right exists
    }
}
```

###### Pre-Order Traversal

This says, do the root first, then print the left, then print the right. This prints the subtree to the left of the root, then the subtree to the right of the root. It recursively visits the left subtree and prints each subtree to the left first until there are no nodes left on the left, then prints the subtree to the right. Prints the root before the subtrees. The strategy is Root, Left, Right. Good order for making a copy of the tree.

```java
inOrder(node) {
    print(node);
    if (node.left != null) {inOrder(node.left)}
    if (node.right != null) {inOrder(node.right)}
}
```

###### Post-Order Traversal

This says start at the root, then visit everything to its left first, recursively visit everything to the left of that subtree until there are no nodes to the left. Then visit the nodes to the right of the left most element. We then print the rightmost element of the leftmost element and return to the parent of that element and print that since we have already printed the elements to its left and right. We recursively move up the tree printing the parent after its left and right elements are visited. The strategy is Left, Right, Root.

```java
inOrder(node) {
    if (node.right != null) {inOrder(node.right)}
    print(node);
    if (node.left != null) {inOrder(node.left)}
}
```

##### More Tree Terminology

###### Path

a sequence of nodes in a tree such that n1 is the parent of n2 which is the parent of n3 and so on down to n(k-1) which is the parent n_k. It is the edges between nodes from the first node to the last node.

###### Length

The length of a path is k-1 where k is the number of nodes on the path. This is the number of edges between the nodes.

###### Height

The height of a node is the **length of the longest path** from a node to a leaf. The height of a root defines the height of the tree. The height of the BST is indicative of its performance. We can define height recursively:

```java
public int height(n) {
    if isLeaf(n) {
        return 0;
    } else {
        return 1 + max(n.left, n.right);
    }
}
```

###### Depth

The depth of a node is the opposite of the height. We also consider this the same as the level of the node. The height of the tree is the depth of its deepest node.

```java
public int depth(n) {
    if isRoot(n) {
        return 0;
    } else {
        return 1 + depth(parent(n));
    }
}
```

We can use these terminology to describe unbalanced binary trees. The upper bound on height is a sorted linked list with all elements to the right of the smallest element or all elements to the left of the largest element.

###### A Perfect Binary Tree

Other than the leaves, every node has exactly two children and all the leaves have the same depth or same level.

In a perfect tree, the number of nodes is $2^d$ where d is the depth of the node.

The height of a perfect binary tree is $O(lg(n))$ where n is the number of nodes. To count the number of nodes in a perfect binary tree, we can use the following formula:
$$
n = 2^0 + 2^1 + ... + 2^d = 2^{d+1} -1
$$
where d is the depth of the deepest node. If you can find d, you can find the height. We can thus, solve for d from the number of nodes:
$$
d = ln(n+1) -1
$$
So, the height of a perfect binary tree is $O(lg(n))$

###### BST Analysis

The BST provides a reasonably fast implementation of the OrderedSet ADT. The insert, remove, and has operations start at the root and follow a path down to, in the worst case, the leaf at the lowest level. The time complexity of each operation is therefore, $O(h)$ where h is the height of the tree. 

The worst case scenario is an n-node tree that is a linked list with the smallest value at the root and largest value as a leaf to the right. Or the largest value as the root and the smallest value as a leaf to the left.

The best case scenario for insert, remove, and has operations is performed in a situation when the BST is a perfect binary tree. The height of an n-node binary tree is $O(lg(n))$ so, the core operations of the OrderedSet ADT will take $O(lg(n))$ time to run on a collection of n elements. Making the tree as shallow as possible is the best-case scenario.

###### Tree ADT

A general or unrestricted Tree is one where each node has an unlimited number of children nodes. 

```java
public interface Tree<T> extends Iterable<T> {
    int size();
    boolean empty();
    Position<T> insertRoot(T t) throws InsertionException;
    boolean root(Position<T> p) throws PositionException;
    Position<T> root() throws EmptyException;
    Position<T> insertChild(Position<T> p, T t) throws PositionException;
    boolean leaf(Position<T> p) throws PositionException;
    Position<T> parent(Position<T> p) throws PositionException;
    T remove(Position<T> p) throws PositionException, RemovalException;
    Iterator<T> iterator();
    Iterable<Position<T>> children(Position<T> p) throws PositionException'
}
```

### Maps and Balanced Binary Search Trees

A map is a collection of key-value pairs. Keys must be **unique** and **immutable**. Maps are also known as dictionaries or associative arrays or symbol tables in other contexts. Sometimes maps and dictionaries are distinguished by dictionaries being allowed to have duplicate keys. The core operations of a map are insertion, removal, and update of the key-value pairs, as well as lookup of a value associated with a particular key.

Maps provide a fast "key lookup" data structure that offers a flexible means of index into its elements. 

Maps are very similar to sets. The keys are unique and can essentially be implemented as a set with extra lookup functionality.

```java
// K is the type for keys,
// V is the type for values.
public interface Map<K, V> extends Iterable<K> {
    //Insert a new key-value pair. Exception if k is null or already mapped.
    void insert(K k, V v) throws IllegalArgumentException;
    //removes the key-value pair from the map and returns the value associated with the key
    V remove(K k) throws IllegalArgumentException;
    //Update value at a key, exception if k is null or unmapped.
    void put(K k, V v) throws IllegalArgumentException;
    //return the value at a key, throw exception if null key or unmapped key
    V get(K k) throws IllegalArgumentException;
    boolean has(K k); //check the existence of a key.
    int size(); //number of mappings.
}
```

This chapter's starter code contains an inefficient implementation of the map with an array similar to that of a set. We should look at it and reason about the asymptotic complexity of the implementations as practice for the midterm. 

This example implementation also uses the built-in java lists for 

###### Balanced Binary Search Trees (BBST)

Want a binary search tree that is self-balancing to keep the operations efficient. 

Recall before we defined a binary tree as a tree where every node has two children. A binary search tree extended this idea by keeping the nodes sorted with an ordering property where a node to the left of the root is less than the root and a node to the right is greater than the root. Here, we define a new (BBST) with a balance property that says that the heights of a nodes left and right subtrees are either equal or differ by at most 1. If a binary search tree is balanced, it has logarithmic height.

How do we programmatically quantify balancing? We add a balance factor to each node in the tree which tracks the height of the left subtree minus the height of the right subtree. 

```java
bf(node) = height(node.left) - height(node.right);

public int height(node) {
	if (node == null) {
        return -1;
    } else if (isLeaf(node)) {
        return 0;
    } else{
        return 1 + max(height(node.left), height(node.right));
    }
}
```

A BST is then balanced if for every node, the balance factor is 1, 0 or -1. 

Do the examples in the chapter for midterm practice

### AVL Trees

Named after its creators. Provides a way to correct a BST to ensure it remains balanced. This ensures that any operation performed on these trees is optimally $O(lg(n))$. 

These operations need to be efficient as there is no point in keeping the tree balanced if the operations make maintaining the tree less efficient than $O(lg(n))$.

There are 4 patterns that can create an unbalanced BST.

###### Structural Rotation

Given 3 values, there are 3! ways to insert these values in to the tree and thus, that many ways to build valid trees with them. Which value serves as the root changes the balance of the tree. 

Any unbalanced BST, can be modified into a balanced BST. 

Both removal and insertion can cause incorrect balancing.  

###### Single Right Rotation

Notice that of the ways we can create a balanced BST from 3 nodes, a **right rotation** can be defined as the operation in which the node in the middle gets promoted to the root and the node that was previously the root gets demoted to the right child of the middle node. This is the correction that needs to be applied when **the problem is in the left subtree of the left child** from the perspective of the unbalanced parent node. 

Example 3 in the nodes for right rotation shows an example where the unbalanced parent node is the great grandparent of the node that caused the imbalance. To correct this, we have to move 7 up, make 14 its right child, and make 11 the left child of 14. 

![image-20211101133250757](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211101133250757.png)

How can we implement a single right rotation generically?

![image-20211101134620039](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211101134620039.png)

```java
Node<T> rightRotation(node<T> root) {
    Node<T> leftChild = root.left;
    root.left = leftChild.right;
    leftChild.right = root;
    root = leftChild;
    return root;
}
```

###### Single Left Rotation

The opposite problem as that resolved with single right rotation. This is when the issue arises in the **right subtree of the right child**.

![image-20211101141718852](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211101141718852.png)

###### Right-Left Rotation

When the problem with our tree is in the **Right Child's left subtree**, we need to apply a right rotation, followed by a left rotation:

![image-20211101141901334](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211101141901334.png)

###### Left-Right Rotation

Resolves the same but opposite problem to the previous rotation. This is needed when the problem is in the **Left Child's Right Subtree**

![image-20211101141953987](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211101141953987.png)

###### Detecting These Rotations Programmatically

By looking at our balance factors, we can tell if the subtree is left or right heavy. A positive balance factor is left heavy while a negative balance factor is right heavy.

| Imbalanced Node                        | Child's Balance Factor is `-1` (right heavy) | Child's Balance Factor is 1 (left heavy) |
| -------------------------------------- | -------------------------------------------- | ---------------------------------------- |
| **Balance Factor is -2 (right heavy)** | Left Rotation                                | Right-Left Rotation                      |
| **Balance Factor is +2 (left heavy)**  | Left-Right Rotation                          | Right Rotation                           |

It is not possible to need to apply more than one rotation upon insertion. However, it is possible to need to apply rotation up to lg(n) times up to the root upon removal.

Try the structural rotation exercise before implementing the homework assignment. 

### Priority Queue

Recall that a queue works on a first in first out basis. A priority queue works by taking elements of higher priority over an element that may be first in the queue if it is of lower priority. Think an IT desk ticketing system or distributing limited computer resources.

We typically implement this with priority defined by the natural ordering of the elements. If the two elements have the same priority, they are dequeued on a first-come-first-serve basis. For example, if we have a priority queue of integers, we dequeue by lowest value.

To motivate the functionality of the priority queue we have the following example:

###### `Submission` Class, Comparator vs Comparable

Represents a homework submission made by a student. Among its attributes are:

```java
private int positionInQueue;
private String student;
private int numPriorSubmission;
```

Process submissions in the order they are received. Thus, submissions are comparable to one another, based on the order they were received. 

```java
@Override
public int compareTo(Submission other) {
    return this.positionInQueue - other.positionInQueue;
}
```

 `Collections.sort(submissions)` can be used to sort submissions using the definition of `compareTo`

Java takes the `compareTo` function to be the natural ordering of the elements. We can also call `Collections.sort(submissions, new LessSubmissionHigherPriority)` with a second argument which is an instance of a `Comparator`. A comparator implements the `compare` function whereas a `comparable` implements the `compareTo` function.

```java
private static class LessSubmissionHigherPriority implements Comparator<Submission> {
    @Override
    public int compare(Submission s1, Submission s2) {
        return s1.getNumPriorSubmission() - s2.getNumPriorSubmission();
    }
}
```

both `compare` and `compareTo` return the same type of integer where a > b indicates that a comes after b.

Know the difference between comparator and comparable for the homework and exams. There are several explanations in the lecture notes to review before the midterm. 

In our `priorityQueue`, we define two constructors. The first constructor uses the natural order of its parameters while the second constructor uses a comparator to overwrite the natural ordering of the elements.

###### Priority Queue Implementation

Regardless of the implementation, if we keep the array sorted, we can find the first element in $O(1)$ since it will just be the first element.

To implement the priority queue with an array, we keep the best element at the end of the element and just remove it by decrementing numElements assuming we sort the array so that the best elements are at the end of the array. Insertion is $O(N)$, we need to find the element to insert after and copy the elements.

To implement the priority queue with a linked list, we can keep the best element at the head and the next best attached to the head. We just removeHead to remove the element. If we want to insert into the sorted linked list, we can't do better than $O(N)$ since we still have to find the element in the linked list and cant binary search on a linked list. 

The best priority queue implementation, thus uses a tree data structure which can find the elements in O(lg(N)) time with insertion and removal in O(1) time.

###### Binary Heap

The aforementioned data structure we will use to implement a tree-based priority queue. This is also sometimes just referred to as a heap. The structure of a heap is a **complete** binary tree which limits its height to $O(lg(N))$ and the order of the heap means that each element stored at each node has a higher priority than its children. The ordering implies that the best element is always the node at the root.

But what is a complete binary tree? This is what differentiates the heap from a BST. A BST only has to have the structure of a binary tree. A  **complete** binary tree is one where the tree is "full" on all levels except possibly the last level which must have all of its nodes on the left side.

![image-20211103173519126](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211103173519126.png)

This is a slightly looser condition than the perfect binary tree where all leaves had to be on the same level. You can check if a tree is a complete binary tree by ignoring the lowest layer of leaves. If the remaining nodes form a perfect binary tree, then the tree is complete. 

The ordering of the BST is such that the left node is less than its parent and the right node is greater than its parent. The ordering of the heap implies that the priority of its children are no better than itself.

###### Heap Order Property

The binary heap must be ordered in one of two ways. Either **min-heap** in which the value of each node is less than or equal to the value of its children with the minimum value  element at the root or **max-heap** in which  the value of each node is greater than or equal to the value of its children with the maximum-value element at the root. 

A complete binary tree can be very creatively stored in an array which massively simplifies its implementation. To do this,  we store the elements in level-order in the array. For convenience we ignore the index-zero the array. Considering the $K^{th}$ element  of  an  array, the left child is found at the index $2*K$ and  the right child is found at the $2K+1$ index. The parent of the $K^{th}$ element is found at the $k/2$ index.

###### Binary Heap Implementation

To implement the `best` function, we just return the value at the root.  To implement the `insert` function, we have to insert at the next leaf slot from the left. To add an element, We just add the new element to the end of the array. Then we need to fix the ordering of the heap. To do this, we swap the child with its parent until, its children and parent fit the ordering criteria (depends on if min or max heap implementation). Since the value swims up, the worst case is that the value starts as a leaf and swims all the way up to become the root. The height of the tree is $O(ln(n))$ so in the worst case, insertion is logarithmic. `remove` is always done at the root, we can do this, by replacing the target value with the last element of the array and decrementing the number of elements of the array. Now that we have a value at the root which may violate the ordering property, we need to let this value sink down until the ordering is restored. The worst case you start at the root and travel down to a leaf. This has a worst case time complexity of $O(lg(n))$ which is still better than an array or linked list implementation. When we swap the value at the root, we swap the root with the better of the two children, so that the ordering is preserved. 

This is an extremely clever data structure :)

### Treap

Say we have a sequence of numbers that is inserted into a BST, if we randomly shuffle these numbers, we can get trees that better approximate the logarithmic height of the random height. Linear order is very unlikely to occur from random shuffling. If we knew all the keys to insert into a BST, just 1 shuffle with give a BST that is probabilistically within the bounds of $O(lg(N))$. In a Treap, we don't know the values ahead of time, but we can assign random priorities to the values as we insert them which we can use to structurally rotate the tree and obtain balanced trees within $O(lg(N))$.  

###### Insertion

To insert an element into a treap, we can generate priorities in  the range of 0 to 1.  If we keep a max-heap (higher priority is higher in the heap). When inserting, we want the nodes with higher priority closer to the root of the tree. We could swap the elements, but this would violate binary search tree ordering. To fix this, we can rotate the tree as in the AVL tree. We only need to handle rotation left and rotation right.

There are two properties we need to maintain: The binary search tree aspect of  the data structure requires that the order of the values of the nodes follow that of a BST. This means that the value of the left child is less than the parent and the value of the right child is greater than the parent. The heap aspect of the treap requires that the order in which the values are arranged in the treap is sorted by priority. This means that the priority of  any children nodes  must be less than that  of the parent, otherwise we need  to apply structural rotation. A treap  must  both be structured  as a BST and the order is sorted by the priorities.

![image-20211105020109271](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211105020109271.png)

where the BST is sorted by the letters or values at the nodes and the priority is indicated by the  associated integers. The largest integer is at the root and the order is alphabetically sorted.

### Hash Tables

Binary trees gave us a way to do the core operations of a set or a map in logarithmic time. Is there a way to do this in constant time? Yes (amortized constant time) with a hash table. 

The core of a hash table is that given a key, we have some function that converts that key to an index in the hash table. We map a key to a 'unique' index. To insert, we just get the index and insert at that insertion which can be done in constant time. If the function that maps a key to an index is constant time, the insert, update, and search functions are all constant time. 

This function is called a **hash function** and the process is called hashing. The first step of a hash function is to generate a numerical representation for the key. This is called a generating a **hash code**. We can really easily do this in a computer since everything is represented as numbers or memory addresses. The next step is to convert the hash code to a smaller range as the hash codes are likely bounded by the size of integers on the computer. We need to move the hash code to a smaller range from 0 to M. This process is called **compression**.

A good hash function is:

* <u>Uniform</u>: which means it maps keys to array indices as evenly as possible. Ideally you have an equal likelihood of generating each index value. A non-uniform hash function is called biased.
* <u>Deterministic</u>: which means a given key is always mapped to the same index so we can look it up after insertion. If this doesn't happen, this whole process doesn't really work as we wouldn't be able to find that index again.
* <u>Cheap:</u> which means that the operation is simple and fast to compute. Just because the hash function is constant time, doesn't mean that it happens quickly. The process could take a crazy amount of time independently of the size of the input and still bee constant time. We need the hash function to work quickly.

The faster the has function is, the more performant the whole data structure is.

We typically break the two responsibilities of hashing into two. There is an element which generates its own hash code which is the type that gets inserted into the data structure. The data structure itself is responsible for mapping the hash codes to a smaller range since the structure of the data structure will determine the range we map into.

###### Generating Hash Codes

The Java Object class has a `hashCode` method which generates hash codes for any element. The default way to generate a hash code for user defined objects is to hash the memory location of the object. This would be problematic if two identical objects were stored at different memory locations and we want them to be treated the same by the hash map. Thus, we should override the `hashCode` method for user-defined classes, but can generally use the default implementation for basic data types. You also would need to override the `equals()` method to define how hash codes should be compared.

For our purposes, we will not be implementing the `hashCode` function since we care about building hash tables and not hashing data. We will however, worry ourselves about the compression process since this is a component of the data structure.

###### Compression

To map the hash code to our desired range M, we can just apply the modulus operator:

```java
int index = key.hashCode() % M; //where M is the non-inclusive maximum value of the range.
```

The problem with doing this is that as the size of M decreases, we are more likely to have collisions between indices.

#### Handling Index Collisions

A **collision** occurs when more than one key is mapped to the same array index. In any practical application, the set of possible keys is much larger than the set of indices we have available to fill. It would be impractical to have a data structure that is the size of the input set. This is an example of the Pigeon Hole Principle from discrete mathematics.

There are two main collision handling techniques:

##### Open Addressing

This technique says, go to the index of the collision and insert the value for the key at the next available open index. There are different techniques for locating the next open location to insert into which is called **probing**. 

Linear probing is when we just move to the next open index in the list:

```java
int index = getIndex(key);
//if table[index] is occupied, then
for (int i = 0; i < M; i++) {
    index = (getIndex(key) + i) % M; //modulo allows wrapping around to indices before the original index
    //stop the loop when we find an unoccupied index
}
//if we get here and haven't inserted the key, the table is full and we need to expand it
```

This works, however when we delete an element from the hash map, if there is an element after it that hashed to the same thing, our find operation will stop prematurely since there is an empty spot after the ideal index indicating no further keys that map to the same index are in the map. But, this isn't true there is an element after the empty spot. To resolve this, we can insert a sentinel value after removal that functions as a **tombstone** and indicates to the find function to keep searching after the index is removed. The entry is thus removed from the index,  but it is not deleted fully. This can be done by flagging the element as deleted, but without actually doing anything else to the value. This is known as **lazy deletion**.

To implement the tombstone, we can create our array of **Entry** objects that track whether they are deleted or not as well as the generic type they hold. Our remove operation can then work by using an `isDeleted` boolean. Another option is to insert a sentinel object that is an object that we can insert into the hash table.

How will tombstones affect the efficiency of the data structure? If we remove a lot of elements, most of the data structure is populated by useless data. The more tombstones, the more likely we are to have to perform O(N) finding. We can treat deleted nodes as available for insertion. Which can help decrease the number of tombstones. Is it safe to overwrite at tombstones? No! If we tried to insert a value already in the hash table, we would write it into the tombstone potentially before finding that the value is already there. Maybe we could continue the search after marking the position of the tombstones, but this increases the complexity of inserting. Alternatively, we can just ignore tombstones, but this brings us back to the problem of filling the data structure with junk data.

###### Contamination and Rehashing

This problem of of tombstones preventing search from terminating prematurely is because tombstones waste space and reduce search efficiency. In the worst-case scenario, if the table is almost full of tombstones from deleting most of the items, then we have O(N) searching despite only a few items remaining in the table. This problem is called **contamination** and the solution to it is **rehashing**.

Rehashing is analogous to dynamic array resizing. We consider the hash table "full" if we have inserted until there are no more indices available for insertion or if the table becomes contaminated with tombstones. Unlike growing an array, we can't just copy the values from the original collection to the new one. Since we allocate a new hash table with double the size of the original, we have to reinsert the old table entry into the new hash table by recalculating its index with the new table size. We also don't want to re-insert the tombstones which would waste our space.

###### Load Factor ($\alpha$)

The load factor of a hash table is a way of quantifying how full  the table is. Very simply:
$$
\alpha = \frac {number\ of \ filled\ cells}{table\ capacity}
$$
this generates a number between [0, 1] which if it is closer to 0, indicates that the table is nearly empty and if it is closer to 1 indicates that the table is more full.

When the load factor reaches a given threshold, **rehashing** kicks in. Since rehashing increases the capacity, it reduces the load factor. $\alpha \le 0.75$ is a good threshold for rehashing determined by benchmarking which we could give the user the option to set like Java does. Maintaining lower load factors means faster operations at the tradeoff of higher memory overhead. 

With amortized analysis, we want to increase the size of the table by multiplicative size increases. Doubling is easier to prove efficiency in amortized analysis, but there is an added caveat that we want to choose the smallest prime number above double the size of the table to be our new table size.

###### Table Size

Why do we want to choose the smallest prime number larger than the desired table size? The idea is that generally if we choose the index as the hash code with a modulus of M. For every key returned by hash code, every K that shares a common factor with M will be hashed to multiple positions of this factor. To minimize the collisions, we can reduce the number of common factors between K and M by choosing M to be a prime number.

If both the hash code and the size of the table were even as would be created by doubling, the indices generated would always be even. Memory addresses are always even so this would bias the table to only fill even numbers. In real life application from linear probing this doesn't really affect performance that much but theoretically using a prime number is better. 

Rather than having a function that generates prime numbers as this would be expensive, just create a list of known primes and remember which prime was used last incrementing to get the next value. If we exceed the prime number list just start doubling the largest value since it probably wont make much of a difference at this scale.

###### Linear Probing Analysis and Overview

So we have that in the best case, insert/remove/find are done in O(1). The worst-case scenario is when the probing sequence goes over every occupied position. This scenario leads to O(n) performance where n is the number of items stored in the hash table. 

For the average case performance, given an open-address hash table with load factor $\alpha$, the expected number of probes in an unsuccessful search is at most:
$$
O(\frac{1}{1 - \alpha})
$$
this can be proved by assuming the hash table employs a uniform hash function and applying basic probability. This is out of the scope of the class but is good to know that the average performance is some kind of number, not a function of the size of table. The choice of alpha changes the efficiency and is on average constant time.

###### Primary Clustering and Problems with Linear Probing

The problem with linear probing is that it tends to create clusters of keys in the table resulting in long search chains. The existing cluster will act as a "net" that catches many of  the new keys which get appended to the chain and exacerbate the problem. 

If there is a 10% chance for a key to get stored at any index, a 3 element index cluster, the next element after the cluster has a 40% of getting the next element since it is impossible to insert at occupied nodes.

###### Quadratic Probing

This technique says to jump indices in the hash table using a constant size stride increases:

```java
int index = getIndex(key);
// if table[index] is occupied then
for(int i = 0; i < M; i++) {
    index = (getIndex(key) + i*i) % M;
    //stop when table[index] is available
}
```

this creates increasingly large steps in the search sequence and avoids primary clustering. It is possible to miss indices depending on the size of table and the way we are jumping. In this case, we can increase the size of the table or fail to insert. Maintaining a prime table size and reasonable load factor will prevent this from happening.

Since we make exactly the same step sizes, we still get clusters of data when things collide to the same index. However, the clusters should be more spread out and distributed throughout the table. This is called secondary clustering.

###### Double Hashing

To eliminate secondary clustering,  we could use another hash function that takes in the key to be inserted and the hash code informs the jump function of a step size to use. 

```java
int index = getIndex(key);
// if table[index] is occupied then
for(int i = 0; i < M; i++) {
    index = (getIndex(key) + hash(key)*i) % M;
    //stop when table[index] is available
}
```

which is interesting in that the different keys create different step sizes so clustering is less likely to happen and we can find the key the same way every time.

In practice, non-linear probing doesn't really improve efficiency that much so its really only interesting in academic contexts for finding  the  absolute best solutions. 

##### Chaining

This technique stores all colliding elements in an auxiliary data structure like a linked list. Each position in the hash table can be thought of as a bucket that stores multiple entries. Thus, this approach is sometimes called **bucket hashing**.

A linked list can be used where we just addFront any new elements and linear search through the elements in the bucket when we hash to an index.

###### Chaining Analysis

In the best case, we are lucky and the number  of elements  inserted  is smaller than the capacity of the table and unique indices were generated for each key. In this case, insert, remove, and find are all O(1).

In the worst case, a bad hash function has mapped all of the keys to the same index. In this case we just have a singly linked list and insert, remove, and find are all linear time O(N).

Chaining with a uniform hash function should distribute elements evenly among elements. We expect each bucket to be of size $n/M$ where n is the number of items stored in the hash table and M is the size of the hash table. We define this as our load factor for chaining hash maps:
$$
\alpha = n/M
$$
The performance is thus, $O(\alpha)$ in the average case. If we keep $\alpha \lt 1$, we get an expected constant runtime operation. The performance also depends on the choice of auxiliary data structure. The most common is a linked list. We could also use an array or a self-balancing binary search tree.

Java uses chaining hash maps with a linked list which switches to a BST when the number of elements exceeds a pre-set limit determined by benchmarking. 

## Unit 3

### $O(Nlg(N)))$ Sorting

#### Heap Sort

Use a binary heap to improve sort efficiency.

```java
private static void sort(Integer[] data) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();
    for (int i = 0; i < data.length; i++) { //O(N*lg(N))
    	pq.add(data[i]); //O(lg(N))       
    }
	for (int i = 0; i < data.length; i++) { //O(N*lg(N))
    	data[i] = pq.remove(); //O(lg(N))
    }
    //data is now sorted.
}
```

The time efficiency of this algorithm is $O(N*lg(N))$ and the input space efficiency is O(N) and the auxiliary space efficiency is $O(N)$ so total space complexity is $O(N)$. This is like a more efficient form of selection sort. Finding the smallest element in the selection sort is handled by the binary heap which is why it was created.

We can actually further improve this which eliminates the priority queue and reduces the auxiliary space.

#### Floyd's (bottom-up) Heapify

Since the binary heap can be implemented in an array, we can just restructure the input data array into a binary heap. Interpret the input data as a binary heap, then move the values until the problems are solved. Floyd said look at the bottom, find a problem, let that node sink down and repeat until problems are solved. 

To start, look at the leaves. Since they don't have any children, we are done. Next, look at the next layer up, look at the first subtree and its children (which we can calculate based on the index). If the element being looked at is not better than its children, swap with the better of the two children. Move up to the next layer and repeat. 

After swapping with child, need to check child is valid in the context of its children (may need to sink down multiple layers).

Also recall, we ignored `idx==0` in our original implementation of array-based heap, now we need to correct our indices since we are using the zero index. 

We now no longer need the priority queue. 

```java
for (int i = numElements; i > 1; i--) {
    sink(i);
}
```

We improve this by ignoring the leaves at first. Can we calculate where the leaves are from the length of the array? We can since the number of leaves in each layer is just $2^d$ where $d$ is the depth of the layer. If we have n leaves, there are $n = k+(k-1) = 2k-1$ nodes where k is the number of leaves. Solving for k, there are $\lceil n/2 \rceil$ leaves and $\lfloor n/2 \rfloor$ nodes elsewhere.

```java
for (int i = numElements/2; i > 1; i--) { //implicitly floor division
    sink(i);
} 
```

But how is this operation linear $O(N)$? Imagine the worst case where every single layer needs to be moved downwards to the leaves. The first layer requires $0*n/2$ swaps. The second layer requires $1*n/4$ swaps. The third layer requires $2*n/8$ swaps and so on to the last layer which requires $lg(n) * 1$ swaps. We can write this sum taking into account the fact that we are operating on a complete and not perfect binary tree with the following formula:
$$
\sum_{h=0}^{\lfloor lg\ n \rfloor} \lceil \frac{n}{2^{h+1}} \rceil h
$$
where h is the height of the tree.

Using summation rules, we can show that the time complexity of this sum is:
$$
O(n\sum_{h=0}^{\lfloor lg\ n \rfloor} \lceil \frac{h}{2^{h+1}} \rceil) < O(n\sum_{h=0}^{\lfloor lg\ n \rfloor} \frac{h}{2^{h}}) < 
O(n\sum_{h=0}^{\infin} \frac{h}{2^{h}}) =2
$$
so we have a total time complexity of $O(2N) = O(N)$.

The top down algorithm has a larger time complexity. Each level has longer paths to consider and you can't eliminate half of the items in the first pass.

The end result of creating a binary heap in the input array is an array that is ordered for a heap but is not sorted. If we implement the `remove` function to move the root to the end of the array and sink down the promoted element, if we decrement `numElements`, we can repeat the removal process until there are no more elements to remove and at this point, the array will be sorted from smallest to largest assuming we have used a max heap as we will move the largest elements to the end of the array in order.

```java
for (int i = numNodes / 2; i >= 1; i--) {
    sink(data, i, numNodes);
}

for (int i = numNodes; i >= 1; i--) { //still NlgN but improves speed and auxiliary space
    swap(data, 1, numNodes--);
    sink(data, 1, numNodes);
}
```

#### Merge Sort

##### The Merge Algorithm

Suppose we have two sorted arrays of data and want to merge them into a larger sorted array. We can start by looking at the first elements of each array, then copy the lowest element in the two arrays into an output array. Then we increment a pointer to the next element in the array we just copied from. We then compare that element to the element in the first array we are pointing to and then copy to the next index in the output array. We repeat this process until there are no more elements in the two input arrays.

```java
private static void merge(int[] arr, int left, int mid, int right) {
    //sorted portion starts at index left, ends at index right-1
    //mid is the index that separates two sorted portions (second portion starts)
    int i = left;
    int j = mid;
    int k = 0;
    
    int[] tmp = new int[right - left];
    while (i < mid && j < right) {
        if (arr[i] < arr[j]) {
            tmp[k++] = arr[i++];
        } else {
            tmp[k++] = arr[j++];
        }
    }
    
    while (i < mid) {
        tmp[k++] = arr[i++];
    }
    
    for (int l = 0; l < k; l++) {
        arr[left + l] = tmp[l];
    }
    
}
```

##### Recursive Implementation

Begin by viewing each index as a sub array of size 1. They are trivially sorted. Merge them pairwise to get sorted 2 element subarrays. Repeat merging until the whole array is sorted. By only applying the merge process, we can create a completely sorted array.

Apply the divide and merge process where we recursively break the array down into subarrays and then merge them into a sorted array.

```java
public static void mergesort(int[] arr, int left, int right) {
    if (right - left < 2) {
        return;
    }
    
    int mid = (left + right) / 2;
    //arr[left, mid-1]
    mergesort(arr, left, mid);
    //arr[mid, right-1]
    mergesort(arr, mid, right);
    if (arr[mid - 1] > arr[mid]) {
    	merge(arr, left, mid, right);
    }
}
```

The divide process takes $O(lgN)$ steps to break the array down into singletons. Then the merge process takes $O(NlgN)$ steps to combine the singletons and merge the sorted arrays. Overall the runtime complexity is $O(NlgN)$.

##### Early Stop Heuristic

We can optimize merge sort to stop in $O(N)$ when the input is already sorted. Just check if the last element in the left array is less than the first element in the right array before merging, if it is we don't need to merge.

#### Quick Sort

Has an average case runtime of $O(NlgN)$ and worst case runtime of $O(N^2)$. Most sorts in programming languages are implementations of quicksort.

The big picture idea is to randomly pick an index in the array and call it the **pivot element**. We then apply **partitioning** which makes every element to the left of the pivot element less than or equal to it and every item to the right of it greater than or equal to it. This ensures that the list is sorted relative to the pivot element and thus the final position of the pivot element has been found. 

We then apply partitioning to the left subarray and the right subarray independently. This process is naturally recursive.

##### Partitioning

Take the rightmost element as the pivot, take a left pointer that starts at the beginning of the array and a right pointer that starts at the second to last element. Start at left pointer and check if the value is less than the pivot, if it is advance the pointer, otherwise wait. Then check the right pointer, if it is greater than the pivot, advance otherwise wait. If both waiting swap the elements. Once the pointers are equal, swap with the pivot.

```java
private static int partition(int[] arr, int left, int right) {
    int p = right - 1;
    int r = p - 1;
    int l = left;
    
    while (arr[l] < arr[r]) {
        while (arr[l] <= arr[p] && l <= r) { //O(n)
            l = l+1;
        }

        while (arr[r] >= arr[p] && l <= r) { //O(1)
            r = r-1;
        }
    	swap(arr, l, r);
    }
    
    if (l < r) { //O(1)
    	swap(arr, l, p);
    }
    return l;
}
```

##### Sort Implementation

```java
private static void quicksort(int[] arr, int left, int right) {
    if (right - left <= 1) {
        return;
    }
    int pivot = partition(arr, left, right);
    quicksort(arr, left, pivot);
    quicksort(arr, pivot + 1, right);
}
```

To analyze the time complexity of the algorithm, first look at the partition function. Since we never revisit the elements of the array, we only traverse the array once so the partition function is $O(n)$. 

The worst case time complexity of the algorithm overall is when the sequence values are already sorted. The partition algorithm will always select the next smallest or largest element making two subarrays of size n-1 and 0 elements. This means we have to run over all elements $O(n)$ times where we call partition each time meaning the overall time complexity in this case is $O(n^2)$. In the worst case it functions basically like selection sort.

In the best case, the sequence values are not in sorted order and rather in a random order. Each recursive call to quicksort approximately divides the array into two subarrays of size $n/2$. It takes $lg(n)$ calls to quicksort to get down to singleton arrays. Therefore we call partition $O(lg(n))$ times which has a total time complexity of $O(nlg(n))$.

In the average case, we are most likely to select an element in the middle of the distribution of data to sort, so we tend to select items in the average case. The data probably follows a normal distribution. We should try to select the median if we could, but to do this, we would have to sort the data. If you want to improve the runtime, you can select the median of the leftmost, rightmost, and middle element which is called the **median of the three**. Using this median as the pivot tends to work the best in the average case and the improvement can be proven using sampling statistics. Java's implementation works by sampling every 10 elements. If we want to implement the median of three, just find it and swap with the rightmost element and then proceed as normal.

Java switches to insertion sort when `n<7`, merge sort for `collections.sort`, and `arrays.sort` uses quicksort. When sorting over collections (complex types), merge sort ensures that the sort is **stable**. This is not guaranteed for quicksort. The point with this is if you have elements that are distinct but equal in the eyes of the sort algorithm (think unique memory locations or something). Merge sort guarantees that the order of the elements is preserved between sorts. Another example is sorting an Excel table by one column first and then sorting another column. Equal elements in the second sort will not change order from the first sort. This is a **stable** sort. Quicksort is not a stable sort because it can swap the relative positions of 'equal' elements.

Review which algorithms are stable (there is a page on this at the end of the quicksort chapter) before the final exam.

### Graph Basics

Graphs are a way to formally represent a network or collection of connected objects. We call the objects **nodes** or **vertices** and the connections **edges** or **arcs**. 

In mathematics, the vertices are a set and the edges are a set of sets which contain the vertices the edges connect.

```java
public interface Graph<V,E> {  
    Vertex<V> insert(V v) throws insertionException; //inserts a new vertex, exception if v null or already in graph.
    Iterable<Vertex<V>> vertices(); //vertices of the graph, iterable over all graph vertices (in no particular order).
    //Insert a directed edge (from -> to) with data E. Position exception if vertices invalid, Insertion exception if insertion would create a self-loop or a duplicate edge. E is allowed to be null.
    Edges<E> insert(Vertex<V> from, Vertex<V> to, E e) throws PositionException, InsertionException. 
    Iterable<Edge<E>> edges(); //edges of the graph, iterable over all the edges (no particular order)
    //get the vertex the edge is from/to
    Vertex<V> from(Edge<E> e) throws PositionException;
    Vertex<V> to(Edge<E> e) throws PositionException;
    //iterables for getting vertex's outgoing or incoming edges. Position exception if the vertex is invalid.
    Iterable<Edge<E>> outgoing(Vertex<V> v) throws PositionException;
    Iterable<Edge<E>> incoming(Vertex<V> v) throws PositionException;
    //Remove methods. RemovalException for vertex if the vtx still contains incident edges.
    V remove(Vertex<V> v) throws PositionException, RemovalException;
    E remove(Edge<E> e) throws PositionException;

    //Methods to handle vertex and edge labelling. Can be labelled with any Object not necessarily of the same type 
    void label(Vertex<V> v, Object l) throws PositionException;
    void label(Edge<E> e, Object l) throws PositionException;
	Object label(Vertex<V> v) throws PositionException;
	Object label(Edge<E> e) throws PositionException;
    
    void clearLabels();
}

public interface Edge<E> extends Position<E> {
}

public interface Vertex<V> extends Position<V> {
}
```

to use the vertices iterable you can do something like:

```java
for (Vertex<V> v: graph.vertices()) {
    System.out.println(v.get());
}
```

We can implement two types of graphs, directed and undirected graphs which differ in the way the edges are implemented. Our graph implementation is a general interface for **directed graphs**. You can use a directed graph to represent an undirected graph if you just insert two directed edges with the same data in opposite directions. 

Our `insert()` function is overloaded to handle both vertices and edges.

An edge that connects a vertex to itself is called a **loop** and a graph that contains loops is called a **pseudograph**. There can be **multiple** edges (parallel, as in same direction, edges between the same endpoints). Graphs with parallel edges are called **multigraphs**.

A **simple** graph is one in which there are no **loops** or **multiple edges**.

Not every vertex has to have edges attached to it, in this case the vertex is **an isolated vertex**. Graphs with isolated vertices are **not connected**. In a **connected graph** it is possible to get from every vertex to every other vertex in the graph through a series of edges.

Our graph implementation should represent a <u>directed simple graph</u>. 

We include methods to return the vertex that corresponds to the start or end of a given edge called `from` and `to`. By using a position object, the client cannot mutate the values stored in the edge. It just returns the values and does not allow setter methods.

**Adjacent Vertices** are those which are connected directly by an edge. Two adjacent vertices forming an edge are said to be **incident** to the edge they create. **Outgoing** edges are directed edges that the vertex is the origin. **Incoming edges** of a vertex are directed edges that the vertex is the destination. 

Our graph implementation returns iterables which provide the outgoing and incoming edges for a given vertex.

We also provide remove methods to remove a vertex or an edge. We are <u>not</u> allowed to remove a vertex that still has **incident edges**.

A **Labelled Graph** is one in which labels are attached to the vertices or edges or both. When the label values are real numbers, the graph is called a **weighted graph**.

$N$ denotes the number of vertices and it is the size of the vertex set. $M$ denotes the number of edges and is the size of the edge set. Our graphs have a positive integer number of vertices, M can be as small as zero for a not connected graph and a non-simple graph could have infinite edges with finite vertices. For a simple connected graph, the minimum number of edges is $N-1$ since there has to be a path from every node to every other, the maximum number of edges is ${{n}\choose{2}} = \frac{n(n-1)}{2}$ as is in a **complete graph** where every node is connected to every other.

The **degree** of a vertex is the number of edges *incident* to v (a loop counts as two edges) the degree of a vertex is denoted $deg(v)$ furthermore, we have property:
$$
\sum_{v\in V} deg(v) = 2M
$$
We can represent graphs in several different ways:

* Adjacency Matrix Graphs use an NxN matrix where element $(i,j)$ is 1 only if the edge $(v_i, v_j)$ is in E.
  * Takes up $O(N^2)$ storage.
* Adjacency List Graphs are a list of lists where each list corresponds to a vertex $u$ and contains a list of vertices adjacent to it. For an undirected graph every adjacent vertex is in a given vertex's list. For a directed graph, only vertices where an edge originates from a given vertex are included in the list.
  * $O(N+M)$
* An Incidence List Graph has each vertex keep track of a list of edges that are incident to it.
  * Sometimes, other references refer to incidence lists as what we have defined as an adjacency list.
  * $O(N+M)$
  * Because you need a list of vertices, each edge has a list of its adjacent vertices and the size of the list is equal to the degree of that vertex, so the total size is the sum of the degree of all vertices which we showed previously is $2M$

A **sparse** graph has relatively few edges and $M$ is closer to the lower bound $\Omega(N)$. A **dense** graph has many edges and M is closer to the upper bound $O(M^2)$. The choice of graph representation will depend on whether the problem at hand is more likely to be a sparse or dense graph.

If the graph is sparse, adjacency lists are the most efficient.

### Graph Search

There are a lot of interesting problems that can be reduced to a graph search problem.

The **neighborhood** of a vertex is the set of all vertices adjacent to a vertex $v$. We can separate these into the incoming and outgoing neighbors in a directed graph. 

A **path** is a sequence of connected edges in a graph. We can define a path as the sequence of vertices where each vertex is adjacent to the vertex next to it. A **simple** path is a path that does not repeat any nodes or edges we almost always mean **simple paths** when we talk about paths. A directed path is one where you can travel only in the direction the arrows indicate.

The **Graph Search** problem is figuring out if a graph G contains a path from one vertex to another. The general search problem is given a starting vertex, identify the set of all vertices reachable from s in G. By definition, you can reach the vertex itself.

```pseudocode
mark s as "explored" all other vertices as "unexplored"
	while there is an edge (v,w) in E with v explored and w unexplored
		choose some edge (v,w) //this is underspecified
		mark w as explored
```

When we go to choose some edge, we have two choices for how to do this:

* Breadth-First Search **BFS**
* Depth-First Search **DFS**

#### Breadth-First Search

We explore the graph according to a queue which keeps track of the neighbors of A. We add the neighbors to the queue and then pop the first one and look  at its neighbors. The ones that are unexplored, we add to the queue after marking them as explored. Once the queue is empty, we know we have explored everything.

This is the same as level order traversal in a binary tree.

We visit the nodes that are closest to us first and then expand our search.

```pseudocode
mark s as "explored" all other vertices as "unexplored"
queue data structure initialized with s
	while queue is not empty
		remove vertex from front of Q and call it v
		for edge (v,w) in v's neighborhood
			if w is unexplored then
				add w to queue
				mark w as explored
```

#### Depth-First Search

Instead of using a queue, use a stack. Repeat the same process, pushing and popping, but the stack changes the way you explore the tree.

This is the same as something like in-order traversal in the binary search tree. Explores the first branch as far as possible before backtracking.

```pseudocode
mark s as "explored" all other vertices as "unexplored"
stack data structure initialized with s
	while stack is not empty
		remove vertex from front of stack and call it v
		for edge (v,w) in v's neighborhood
			if w is unexplored then
				add w to stack
				mark w as explored
```

#### General Asymptotic Analysis

The while loop executes in O(N) in the worst case. The edge iteration for loop can be done in $O(N)$ for an adjacency matrix or $O(deg(vi))$ since we execute the degree loop N times for each vertex, we have the degree sum formula which tells use we run that block $2M$ times. So, our search can be done in $O(N+M)$ = $O(n)$ linear time.

### Shortest Path Problem

We can modify the graph search problem to identify paths from the root to any node. Rather than tracking just explored vertices, also record previous vertices which got us to the vertex we are currently looking at. Since you have recorded the previous vertex for each vertex, after you run the modified DFS/BFS you can take the endpoint and follow the previous nodes back to the starting node. If the end vertex was unexplored, there is no path.

```pseudocode
previous = {} //map from vertex to vertex
explored = {} //map from vertex to boolean
explored[s] = true
previous[s] = s //special token to tell search we started here could be anything.
queue.enqueue(s)
while (!queue.empty())
	v = queue.dequeue()
	for (w in adjacency[v])
		if (!explored[w])
			explored[w] = true
			queue.enqueue(w)
			previous[w] = v
stack s;
while node != source {
	s.push(node)
	node = previous[node];
}
s.push(node)
while !s.empty()
	print(s.pop())
```

We should probably use a hash map for previous and explored data structures. You could also use parallel arrays as long as you keep track of the index properly and the size, this might cause a linear search if not done properly though so hash maps would give the best performance. You could also incorporate the previous/explored information in the vertex object itself which would make the operations exactly O(1) rather than expected amortized O(1) which is objectively worse.

We can also modify DFS/BFS to give us the distance of a node from a starting node where instead of tracking previous, we track the distance (number of nodes) from the starting node and after exploring the graph, we can just look up the distance from the starting node.

To properly explore a directed graph, we just only consider the outgoing edges.

This gives us a path, however we want the shortest path. If we have edge weights, we need to change the way we consider distance. If we want the minimum total weight (cost), we change our implementation again. 

If the graph is not weighted **BFS gives shortest path** or if all the weights are the same. If the graph is weighted, then BFS is not guaranteed to give the shortest path. This makes sense since we explore the closest vertices first and then the vertices farther away. This guarantees a shortest path.

#### Dijkstra's Algorithm

The algorithm is similar to BFS. We do not mark A as explored by default. We only mark a vertex as explored after we are 'done' with it. We also track the unexplored vertex with the smallest distance where we mark A as explored and travel to the neighbors without marking them as explored.

```pseudocode
for every u: unexplored_neighbor(v)
	d := Distance[v] + Weight[v,u] //add distance from source to current node plus distance to neighbor
	if d < Distance[v]
		Distance[u] = d
		Previous[u] = v
```

There is a comprehensive example for Dijkstra which will make sure you understand so try it before implementing in the homework.
