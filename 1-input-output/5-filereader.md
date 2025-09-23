## FileReader

`FileReader` and `FileWriter` are two of Java’s built-in input stream `classes` and can be extremely useful when your program is working with external `files` when those files contain text information. Both of these classes are specifically made to write character information to and from files.

As with `Scanner`, we will need to import these classes in order to use them in our program. They both reside in the `java.io` package. Unlike with Scanner however, these classes throw a specific type of exception, an `IOException`, if something goes wrong during the read/write process. This `IOException` also needs to be imported from the same package. We’ll dive into how exceptions work later in the lesson, for now we’ll add a line to our main method declaration that simply throws the `IOException` out of the program.

```java
public static void main (String[] args) throws IOException {}
```

Now, let’s take a look at how to implement a `FileReader` instance into our program to read text from a file.

### Step 1: Declare and initialize your FileReader.

As with nearly all Java objects, we follow the pattern `ObjectClass objectName = new ObjectClass();`

```java
FileReader reader = new FileReader(filePath);
```

You will notice here in the constructor that we are passing in a `filePath`, this is a String that represents the path of the file to be read.
* An example of how an absolute path may look is 
  
  `FileReader input = new FileReader("C:/SampleFolder/input.txt")`
* An example of how a relative path may look is

  `FileReader input = new FileReader("../documents/SampleFolder/input.txt")`

Alternatively, you may choose to create an object of the variable type `File` to pass into the `FileReader`. This is useful if you plan to have the user pass in a path to the input file. The code block below shows an example of how you may do this.

```java
//Option 1: Pass file path/name directly to FileReader
FileReader input1 = new FileReader("input.txt");

// Option 2: Use File object to pass file info to FileReader
// Save file path that has been passed in by the user into a string variable.
String fileName = args[0];
// Pass path to File object
File inputFile = new File(fileName);
// Pass File object to FileReader
FileReader input2 = new FileReader(inputFile);
```

### Step 2: Read your file.

Also much like `Scanner`, `FileReader` has `methods` to validate content and read contents, these are `.ready()` and `.read()`. The `.ready()` method makes sure that there is content to read and the `.read()` method reads the file one character at a time. The following code shows how to print each character in the file, which will effectively print the contents of the file as written.

```java
while (reader.ready()) {
  System.out.print((char) reader.read());
}
```

### Step 3: Wrapping Up Loose Ends

It is critically important to close resources such as files and input streams. These can tie up memory on the processor and in some file systems only one asset can access a file at a time, essentially blocking all access to the file from other sources. These resources can either be manually closed like we will do here, or automatically closed with a `try-with-resources` block like we will implement in future exercises.

Closing `FileReader` also has the added benefit of `flushing` the stream as well, making sure that any information that is still in the `FileReader‘s` buffer is written to the console.

```java
input.close();
```

Example final:
```java
import java.io.FileReader;
import java.io.IOException;

public class Introduction {
  public static void main(String[] args) throws IOException {
    String path = "./input.txt";
    FileReader reader = new FileReader(path);
    int data = 0;
    while((data = reader.read()) != -1) {
      System.out.print((char)data);
    }
    reader.close();
  }
}
```