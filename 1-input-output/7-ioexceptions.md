## IOExceptions

Errors are unwanted issues that occur in a program that cannot be handled by a program. They may even result in a program crashing. Exceptions are issues that may occur when a program is running that can be foreseen, or caught by the program. For example, if a user passes an incorrect file path in the arguments of a Java program.

There are two types of exceptions: checked and unchecked. Checked exceptions are exceptions that are thrown when a program is compiling and unchecked exceptions typically occur during runtime. A developer can check if a block of code is going to throw an exception by using a try-catch block, essentially trying some code out to see if an exception occurs or not, and then catching the exception and running a separate block of code in those situations. This allows us to prevent the Exception (unless we want it to) from being thrown out of our main method and crashing the program.

IOExceptions are exceptions that are related to input and/or output in a program and are classified as checked exceptions.

Some examples of when IOExceptions occur include:

* Failed attempts at trying to access a file.
* The end of a file has been reached.
* The file a program is attempting to access cannot be found.
* An input/output operation has been interrupted.

We can code our program to handle IOExceptions in areas of our code where we are dealing with input and output. To start off we must first import the IOExceptions class into our program using import java.io.IOException.

Have a look at the block of code below to see how we have modified one of the examples from the previous exercises to use catch IOExceptions. When we catch exceptions in this manner, we no longer have to declare that our method throws the exception, since we’ve handled it at this level. There are many ways we may choose to handle an exception. We may choose to print an error using System.out.println() or run a new instance of the program.

```java
String statement = "Hello World!";

try {
  FileWriter output = new FileWriter("output.txt");
  output.write(statementBytes);
  output.close();
} catch (IOException e) {
  // Handle exception
  System.out.println("There has been an IO exception");
  System.out.println(e); // Prints the actual exception
}
```

Example final:

```java
import java.io.FileReader;
import java.io.IOException;

public class Introduction {
  public static void main(String[] args) {
    String path = "/a/bad/file/path/to/thisFile.txt";
    try {
      FileReader reader = new FileReader(path);  
      while (reader.ready()) {    
        System.out.print((char) reader.read());    
      }    
      reader.close();
    } catch (IOException e) {
      System.out.println("There has been an IO exception!");
      System.out.println(e);
    }
  }
}
```
