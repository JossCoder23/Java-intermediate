# Running Java Programs

This article will cover running complex Java programs and passing multiple arguments.

### Housekeeping

Let’s begin by revisiting some foundational knowledge:

* `Java and the Command Line`: This article walks through how to download Java and run a basic Java program through the command line.
* `What is an IDE`: This article provides an overview of the benefits of an IDE and links to how to download the IDE IntelliJ on your computer.

After having successfully run a basic Java program, and exploring the uses of the IDE you have installed, it is time to take it one step further by learning how to run complex Java programs and how to pass multiple arguments.

### Running Complex Java Programs

We have already seen how to run a Java program that is exclusively one single file and class. Now, let’s learn how to run a program that has multiple files. It is common to find that developers use multiple files to organize code, especially when defining multiple objects. It is also recommended that you save your files for a single Java program in one directory for ease of access.

Let’s start off by creating the following files:

Note: Often, you will find that the Java file which holds the main method follows the naming convention _____Driver.java. This is because this is the class that “drives,” or carries out, the tasks of the program. This practice stems from C++ programming which divides its files into more complex `header` files and `implementation` files.

__TransportBike.java__
```java
import java.io.*;
public class TransportBike {
  public void wheels() {
    System.out.println("A bike has two wheels.");
  }
}
```

__TransportCar.java__
```java
import java.io.*;
public class TransportCar {
  public void wheels() {
    System.out.println("A car has four wheels.");
  }
}
```

__TransportationDriver.java__
```java
import java.io.*;
public class TransportationDriver {
  public static void main(String[] args) {
    TransportBike harley = new TransportBike();
    TransportCar toyota = new TransportCar();
    harley.wheels();
    toyota.wheels();
   }
}
```

### Compilation Method 1

Once we have saved the following files in the same directory, our first step will be to compile all the files using the following commands:

```cmd
javac TransportBike.java
javac TransportCar.java
javac TransportationDriver.java
```

### Compilation Method 2

You may also choose to compile all files in the same line:

```cmd
javac TransportBike.java TransportCar.java TransportationDriver.java
```

### Compilation Method 3

Since these files all start with the same title, you may also choose to compile them using a regex as follows:

```cmd
javac Transport*.java
```

### Compilation Method 4

One more way to compile these files is by calling the `javac` command on the file that holds the main method:

```cmd
javac TransportationDriver.java
```

This works because as the compiler reaches a definition that is unknown to it, such as the first instance of `TransportBike`, it will search the current folder for any `.class` files that match that signature. If no `.class` files are found, it will look for .java files and then attempt to compile them so that it knows how to represent the `TransportBike` object.

## Running the Program

The next step after compiling is running the program. For the example we are using, you will enter the following into the command prompt to tell the JVM (Java Virtual Machine) which file has the `main` method that you want to run:

```cmd
java TransportationDriver
```

The program will output the following:

```cmd
A bike has two wheels.
A car has four wheels.
```

## Passing Multiple Arguments

In the article Java and the Command Line, we learned how to pass a single string argument into a program. Let’s now look at how to pass multiple arguments to the main function.

In the main function of a Java program, you will see that an array gets passed into a parameter variable. This means that multiple variables can get passed in and will be saved as a string array.

Let’s modify the code from our TransportationDriver.java file to require two arguments to be passed in:

```java
import java.io.*;
public class TransportationDriver {
  public static void main(String[] args) {
    TransportBike harley = new TransportBike();
    TransportCar toyota = new TransportCar();
    harley.wheels();
    toyota.wheels();
    System.out.println(args[0] + " and " + args[1] + " want to purchase a bike.");
    System.out.println(args[1] + " wants to purchase a car.");
  }
}
```

## Method 1: From the command line

Once we have compiled our files, we will run this program using the following command:

```cmd
java TransportationDriver Customer1 Customer2
```

Note: A space between the variables we pass acts as a delimiter. It lets the program know that these are two separate arguments that are being passed in.

## Method 2: Input file

You may also choose to pass input into a program using a text file. Let’s first save the following text to a file:

```cmd
Customer1 Customer2
```

The code in TransportationDriver.java will also have to be modified to use the Scanner class. The scanner class is what will help the program read our .txt file.

```java
import java.io.*;
import java.util.Scanner;
public class TransportationDriver {
  public static void main(String[] args) {
    TransportBike harley = new TransportBike();
    TransportCar toyota = new TransportCar();
    String fileName = args[0];
    Scanner input = new Scanner(fileName);
    String person1 = input.next();
    String person2 = input.next();
    harley.wheels();
    toyota.wheels();
        
    System.out.println(person1 + " and " + person2 + " want to purchase a bike.");
    System.out.println(person2 + " wants to purchase a car.");
  }
}
```

Once we have saved our text file to the same directory and compiled our Java files, we will run this program using the following command:

```cmd
java TranportationDriver input.txt
```

The program will output the following no matter which method we use:

```cmd
A bike has two wheels.
A car has four wheels.
Customer1 and Customer2 want to purchase a bike.
Customer2 wants to purchase a car.
```

# REview
You now have the skills and tools required to run complex Java programs that are made up of multiple files. You also know how to pass multiple arguments when running a program. Great job!