# Java YouTube Crash Course

*Benjamin Fry* - 06/18/21



### Introduction

We need to use classes for everything. 

```java
//single line comment

//Import statements
import java.util.Scanner;
import java.util.*;

public class Animal {
    
    //create a variable that is accessable to everyone [public] with value shared between all instances of the class [static] that cannot be changed [final] that is a double
    public static final double FAV_NUMBER = 1.6180;
    
    //Probably want class attributes to be private.
    private String name;
    private int weight;
    private boolean hasOwner = false;
    private byte age;
    private long uniqueID;
    private char favoriteChar;
    private double speed;
    private float height; //less accurate that doubles
    
    //value can only be accessed by other code in the package
    protected static int numberOfAnimals = 0;
    
    //accepts user input
    static Scanner userInput = new Scanner(System.in);
    
    //define the Animal constructor
    public Animal() {
        //super(); //calls constructor of super-class. don't need there isn't a superclass
        numberOfAnimals++;
        
        int sumOfNumbers = 5+1;
        System.out.println("5 + 1 = " + sumOfNumbers); 
        
        //print doesn't output the newline
        System.out.print("Enter the name: \n");
        
        //hasNextInt, hasNextFloat, hasNextDouble, hasNextByte, hasNextBoolean return true or false depending on the type of userInput
        //userInput.nextInt(), userInput.nextFloat() and so on return that type
        if (userInput.hasNextLine()) {
            //refer to object (instance of class) that was created
            this.setName(userInput.nextLine());
        }
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    //would need to define getters and setters for all other member vars
    
    public void setUniqueID(long uniqueID) {
        this.uniqueID = uniqueID;
    }
    
    //method overloading
    public void setUniqueID() {
        long minNumber = 1;
        long maxNumber = 1000000;
        //cast a double to a long, then shift to range we want and cast to long.
        this.uniqueID = minNumber + (long)(math.random() * ((maxNumber - minNumber) + 1));
        //convert long to string
        String stringNumber = Long.toString(maxNumber); //call Long primitive method
        //parse integer from string
        int numberString = Integer.parseInt(stringNumber);
    }
    
    public void setFavoriteChar(char favchar) {
        this.favoriteChar = favchar;
    }
    public void setFavoriteChar() {
        int randomnumber = (int) (Math.random() * 126) + 1;
        this.favoriteChar = (char) randomNumber;
        
        //comparisons: <, >, ==, !=
        //logic ops: ! is negation, & returns and if both values true but always evaluates both
        //&& returns and if both values true but only evaluates one if first is false.
        if (randomNumber == 32) {
            System.out.println("Fav character set to space");
        } else if(randomNumber == 10) {
            System.out.println("Fav character set to newline");
        } else {
            System.out.println("Favorite char set to " + this.favoriteChar);
        }
    }
    
}

public class Dog extends Animal {
    
}

public class Cat extends Animal {
    
}

//cmd line args get passed to main
public static void main(String[] args) {
    Animal theAnimal = new Animal();
    
}
```

`public` means anyone can access it

Java also has the ternary operator used as so:

```java
int whichIsBigger = (50 > num) ? 50 : randomNumber;
```

it also has Switch statements:

```java
switch(randomNumber) {
    case 8:
        System.out.println("8");
        break;
    case 9:
    case 10:
    case 11;
        System.out.println("9, 10, or 11");
        break;
    default:
        System.out.println("none of the above");
        break;
}
```



we can do some looping as such (looks like its the same as JavaScript and cpp)

```java
for(int i = 0; i < 10; i++) {
    if (i == 5) continue; //skip everything below
    System.out.println(i)
}

int i = 0;
while(i < 10) {
    if (i == 5) break; //stop execution
    System.out.println(i);
}

int number = 10;
do {
    System.out.println("Guess a Number up to 100");
    
    //wait for user to input an integer
	while (!userInput.hasNextInt()) {
     String numberEntered = userInput.next();
     System.out.printf("%s is not a number\n", numberEntered);
    }
    
    number = userInput.nextInt();
} while(number != 50); // this is the do-while check
```



here is some polymorphism practice

within the `Animal` class say this function exists:

```java
public String makeSound() {
    return "Grrrr";
}

public static void speakAnimal(Animal randAnimal) {
    System.out.println("Animal says " + randAnimal.makeSound());
}
```

then within the dog class:

```java
public class Dog extends Animal {
    public Dog() {
    }
    public String makeSound() {
        return "woof";
    }
}
```

which would let us do this:

```java
public static void main(String[] args) {
    Animal fido = new Dog();
    Animal fluffy = new Cat();
    
    //make an array of objects
    Animal[] theAnimals = new newAnimal[10];
	theAnimals[0] = fido;
    theAnimals[1] = fluffy;
    
    System.out.println(theAnimals[0].makeSound());
}
```

more on arrays:

```java
int[] favNumber;
favNumber = new int[20]; //creates an array of 20 integers
//the arrays are zero-indexed.

String[] stringArray = {"Random", "Words", "Here"};

for (String word : stringArray) {
    //loop through every element of the stringarray
    System.out.println(word);
}

//to print the array with indexing:
for (int i = 0; i < stringArray.length; i++) {
    System.out.println(stringArray[i]);
}

```

more array functions:

```java
//copy to a new array
String[] arrayclone = Arrays.copyOf(stringArray, 3); //second is how many values to copy

//print as a string
System.out.println(Arrays.toString(cloneOfArray));

//search an array
System.out.println(Arrays.binarySearch(cloneOfArray), "Random");
```

