## The Matcher Class

The `Matcher` class is Java’s “search” feature, allowing it to take a regular expression defined by the `Pattern` class and perform a search based on a compiled pattern. The syntax for the `Matcher` class is as follows:

```java
Pattern pattern = Pattern.compile("Codecademy"); 

// String to match: "Welcome to Codecademy!"
Matcher matcher = pattern.matcher("Welcome to Codecademy!"); 
```

Note that the `Pattern` object is called when using the `matcher()` method.

The `matcher()` method used by a `Pattern` object returns a `Matcher` object with information about the search. We can then use this `Matcher` object to sift through that information in various ways, with many `methods` within the `Matcher` class at our disposal. We’ll start by talking about the two most useful methods:

```java
boolean matchFind = matcher.find();
boolean matchExact = matcher.matches();
```

In the above two methods, `find()` searches the string for the next match based on the pattern and returns `true` if it finds an occurrence of it. For example, if the string is “Codecademy” and the pattern is “cad”, `find()` will return `true`. The `find()` function retains a pointer to indicate where it should start searching in the text. The pointer initially starts at the beginning of the text and stops at the next character after matching. If `Matcher` is not reset, the next time `find()` is called it will start searching where it left off. Example:

```java
Pattern pattern = Pattern.compile("ABC"); 
Matcher matcher = pattern.matcher("ABCdefgABCdefAB");

matcher.find() // Starting at index 0 - return true
matcher.find() // Starting at index 4 - return true 
matcher.find() // Starting at index 11 - return false
```

This is useful if we are trying to count the number of occurrences of a substring.

The `matches()` function returns `true` if the string matches exactly the pattern with no other characters in the string. Note: this does not necessarily mean that the `strings` must be the same. We will see why in later exercises.

The `Matcher` class also includes methods to find and replace text, create search regions, append text, display how the matcher is interpreting the pattern, and many more functional and very useful utilities.

Example final:
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Example {
  public Example() {}

  public static void main(String[] args) {
    Pattern pattern = Pattern.compile("nap time", Pattern.CASE_INSENSITIVE);
    Matcher matcher = pattern.matcher("Every morning starts with some nap time!");
    boolean findPattern = matcher.find();
    System.out.println(findPattern);
  }
}
```