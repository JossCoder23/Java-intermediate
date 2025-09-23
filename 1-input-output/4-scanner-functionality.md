## Scanner Functionality

Now that we’re familiar with how to set up our Scanner instances, let’s dive into some of its functionalities and how to actually read input, whether that be from a file or from the console.

The first thing to know about the Scanner class is that it breaks up its input using a defined delimiter, and by default that delimiter is set to whitespace. This means every time there is a space or a new line in our input, the Scanner will recognize it as a new piece of the input, in fact, it can do its best to search the input for the specific type of information you are looking for, whether that be an integer, a word, or a character.

The next most important piece of the Scanner class is blocking. That means if the Scanner is waiting on user input from the terminal, it will block continued execution of the program until it gets its input.

The list below outlines some (but not all) of the different methods associated with the Scanner class that allow us to read the next piece of information we are looking for.

| Variable      | Code                                    |
| ------------- |:---------------------------------------:|
| String        | String myString = input.next();         |
| Int           | int num = input.nextInt();              |
| Double        | double numDouble = input.nextDouble();  |
| Byte          | byte numByte = input.nextByte();        |
| Boolean       | boolean isTrue = input.nextBoolean();   |
| Long          | long numLong = input.nextLong();        |
| Short         | short numShort = input.nextShort();     |

The Scanner class has several additional methods that help support data validation and control flow. We can use these to make sure we don’t try to process data that doesn’t exist and thereby run into errors in our program, also known as exceptions.

| Code                    | Function                                                                                                                                                                                                                    |
| ----------------------- |:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| input.hasNext()         | This function returns a boolean that indicates if there is another token left to process                                                                                                                                    |
| input.hasNextLine()     | This function returns a boolean that indicates if there is another line in the input of the defined scanner.                                                                                                                |
| input.hasNextInt()      | This function returns a boolean that validates if there is another int in the input of the defined scanner.                                                                                                                 |
| input.useDelimiter(",)  | This function helps us specify what delimiters we want to use. A delimiter is used to separate data units. This , delimiter can be especially useful when a program is required to read csv (comma separated values) files. |

Prueba final:

```java
import java.util.Scanner;

public class Introduction {
  public static void main(String[] args) {
    Scanner input = new Scanner(System.in);
    
    // Add code below:
    System.out.print("Whats is your name? ");
    String userName = input.next();
    System.out.printf("Hello %s! It's nice to meet you.", userName);
  }
}
```