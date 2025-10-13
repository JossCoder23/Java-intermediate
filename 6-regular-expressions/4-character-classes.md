## Character Classes

Character classes are one of the primary means of “grouping” characters in a regex pattern without necessarily enforcing an order to those characters. For instance, a character class marks the difference between searching for a specific word and searching for any occurrence of any characters found in that word.

A character class matches a character from a specific set, including predefined character classes and custom user-defined sets. The following are examples of how character classes are used (note that any references to “abc” are just examples. These are user-defined, so anything can be used):

| Character Class    | Description                                             |
|:------------------:|:-------------------------------------------------------:|
| [abc]              | Includes any of the contained characters                |
| [^abc]             | Excludes all of the contained characters                |
| [a-z]              | Includes any of the contained characters across a range |
| .                  | Any character except newline                            |
| \w                 | Any word character (alphanumeric and underscore)        |
| \d                 | Any digit [0-9]                                         |
| \s                 | Whitespace (spaces, tabs, line breaks)                  |


These can all be defined as or included in a regex search pattern. Let’s go over a quick example using a character class. Suppose the following is your search pattern:

```java
Pattern pattern = Pattern.compile("[ABCDQ]");
```

The above pattern first creates a character class that checks for any letters from the set {A, B, C, D, Q}.

To see this in action, consider the example of counting the total number of occurrences of characters “B”, “C” and “N” in the string “A BANANA CAN FLY BETTER THAN A BIRD”:

```java
import java.util.regex.*;
public class Main {
  public static void main(String args[]){
    Pattern pattern = Pattern.compile("[BCN]");
    Matcher matcher = pattern.matcher("A BANANA CAN FLY BETTER THAN A BIRD");                                                                                                        
    int count = 0;
    while(matcher.find())count++;
    System.out.println(count); 
  }
}
```

The output of this program will be 8.

Let’s practice using character classes.

Example final:
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Example {
  public Example() {}

  public static void main(String[] args) {
    Pattern pattern = Pattern.compile("gr[ae]y", Pattern.CASE_INSENSITIVE);
    Matcher matcher = pattern.matcher("Vibrant light bloomed across the gray sky, illuminating its grey haze in flashes amidst rolling hills of wispy gray clouds. Colors of gold, pink, and purple painted the horizon, the dull grey of the sky overtaken by brief moments of a quiet twilight storm.");

    int count = 0;
    while(matcher.find())count++;
    System.out.println(count);
    
  }
}
```

