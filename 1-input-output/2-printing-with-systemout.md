# Review: Printing with System.out

By now, you should be very familiar with how to print information to the console using `System.out.print()`, `System.out.println()`, and `System.out.printf()`, but have you ever asked yourself how or why these statements actually work? Let’s take a look!

* `System` is a class in the `lang` package that is part of every Java installation. It contains several properties and `methods` to interface with various high-level aspects of the computer environment.
* `out` is an instance of a `PrintStream`, included as part of the `System` class, that is already open and provides `output` to the user’s default console or display.

The `PrintStream` instance of `out` is a robust class. Let’s take a look at some of the functions that `out` provides through the examples provided below.

`System.out.print()` prints to the same line when a program is running. The example below shows us how two `System.out.print()` statements called in the `main` method, print on the same line.

```java
System.out.print("Hello ");
System.out.print("World!");
```

This code would show the following output in your program:

```terminal
Hello World!
```

You may also choose to concatenate the string you wish to print with other `strings` or `variables`. To concatenate simply means to join multiple strings together, and in Java, we use the `+` symbol to achieve this:

```java
String world = "World";
int day = 1;
System.out.print("Hello " + world + "! Today is Day: " + day + " of your Intermediate Java course!");
```

This code would show the following output in your program:

```terminal
Hello World! Today is Day: 1 of your Intermediate Java course!
```

`System.out.println()` prints output to a new line:

```java
System.out.println("Hello");
System.out.println("World!");
```

This code would show the following output in your program:

```terminal
Hello
World!
```

Concatenation using `System.out.println()` works similar to `System.out.print()`, using the ‘+’ symbol to combine strings.

`System.out.printf()` allows us to output strings that are formatted in the code using `format specifiers`. Format specifiers begin with the ‘%’ sign, followed by the type of variable we want to print. Some examples include `%s` for a string, `%c` for a character, and `%d` for an integer.

Let’s look at a modified version of the Java program that uses `System.out.printf()`. Notice that variables in our print statement are stated in the order that the format specifiers appear.

```java
String world = "World";
int day = 1;
System.out.printf("Hello %s! Today is Day: %d of your Intermediate Java course!", world, day); 
```

This code would show the following output in your program:

```terminal
Hello World! Today is Day: 1 of your Intermediate Java course!
```

Java also allows special characters to be included in our print statements to help with formatting. One such character is the new line indicator, `\n`. We can insert this anywhere in our strings to break the string and start processing on the next line.

```java
System.out.print("Name: Will\nAge:35\nBirthplace: Cincinnati");

// Prints:
Name: Will
Age: 35
Birthplace: Cincinnati
```

Example final:
```java
public class Introduction {
  public static void main(String[] args) {
    String name = "Jose Pardo";
    String hobbies = "Tocar instrumentos, Leer libros, Hacer cursos";
    int age = 29;
    System.out.println("My name is "+name);
    System.out.printf("I am %d years old\n", age);
    System.out.print("My hobbies are "+hobbies);
  }
}
```