## FileWriter

Now, let’s take a closer look at `FileWriter`. As the name suggests, `FileWriter` is used to `output` data, specifically text or character data, from a program into a file. Like `FileReader`, `FileWriter` writes to the file using the standard character encoding (this is set by your computer and locale).

`FileWriter` also is contained in the `java.io` package and needs to be imported so we can use it:

```java
import java.io.FileWriter;
```

### Step 1: Declare your output stream.

The statement `FileWriter output = new FileWriter("output.txt")` will create a file named output.txt in the same folder where your Java program is saved. You may also choose to place an absolute or relative file path in the parenthesis. Creating a file this way WILL NOT create directories (folders), only the file. If the directories don’t exist, you will end up with a `FileNotFoundException` being thrown, which is a subclass of `IOException`.

Alternatively, you may choose to create an object of the variable type `File` to pass into the `FileWriter`. This is useful if you plan to have the user pass in a path for storing the output or if you want to test if it’s a viable file before writing to it:

```java
//Option 1: Pass file path/name directly to FileWriter
FileWriter output1 = new FileWriter("output.txt");

// Option 2: Use File object to pass file info to FileWriter
// Save file path that has been passed in by the user into a string variable.
String fileName = args[0];
// Pass path to File object
File outputFile = new File(fileName);
// Pass File object to FileWriter
FileWriter output2 = new FileWriter(outputFile);
```

### Step 2: Write to your file.

This is achieved using the `.write()` function. Since `FileWriter` is specifically tailored to writing text and character data to an output file, the `.write()` function accepts a string as an argument.

```java
// Declare FileWriter
FileWriter output = new FileWriter("output.txt");

// Declare statement
String statement = "Hello World!";

// Option 1:
// Write all contents to file
output.write(statement);

// Option 2:
// If you want to write specific portions of a string to a file you may choose to use the following statement
// output.write(String str, int offset, int length);
output.write(statement, 0, 5);
// Writes only "Hello" to the file
```

### Step 3: Close the file.

It is important we close a file once we are done writing to it. To do this, we use the .close() method.

```java
output.close();
```

In Java, most `classes` that write output use a buffer-style memory, you can think of it as a middleman between the information you want to write and the file. The information gets loaded into the buffer, and as it gets full, it comes out the other side and into the file. One way to make sure the information makes it out of the buffer and into the file is to `.flush()` it out. If we are done with the `FileWriter` we can simply `.close()` it, which will flush the stream, destroy the internal memory holdings of the `FileWriter`, and free up the file for use elsewhere.

Example Final:

```java
import java.io.FileWriter;
import java.io.IOException;

public class Introduction {

  public static void main(String[] args) throws IOException {
    // Your code here:
    FileWriter output = new FileWriter("output.txt");
    String outputText = "Its my message!";
    output.write(outputText);
    output.close();
  }

}
```
