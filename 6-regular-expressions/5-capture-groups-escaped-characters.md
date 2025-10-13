## Capture Groups and Escaped Characters

We discussed character classes as one of the means to group characters in regex. The other is known as a capture group. Capture groups maintain the order but allow you to section the pattern and allow for substring searching.

The following is known as a capture group (note the “aab” here is user-defined, so anything can be used):

| Capture Group | Description                                        |
|:-------------:|:--------------------------------------------------:|
| (aab)         | Groups tokens together and creates a capture group |

Grouped tokens can be used for extracting a substring. Let’s go over an example.

```java
Pattern pattern = Pattern.compile("(co)+");
```

Here, the “+” is known as a quantifier (these are covered in a later exercise). The “+” means “occurring 1 or more times”.

The above regex pattern matches any text that contains the character combination “co” one or more times. What this will actually match could look like “co” but it would also match with the following: “coco”, “cococo”, “cocococo”, etc.

Character classes and capture groups may look a little similar but just remember: `[]` denotes character class and `()` denotes capture group.

Now let’s get into some unique character specifications in regex.

The `\` is called an escape character, which when used in this manner, helps define special characters with special functions. For example, “\n” represents a new line, and “\s” represents a white space. Here are some others:


| Escaped Character | Description               |
|:-----------------:|:-------------------------:|
| \.                | Escaped period            |
| \*                | Escaped asterisk          | 
| \\                | Escaped backslash         |
| \t                | Tab                       |
| \n                | Newline or linefeed       |
| \r                | Carriage return           |

For example, to search for the . to mark the end of a sentence without regex trying to interpret it as “any character except newline”, we use “\.” in the pattern.

Escaped characters insert reserved, special, and Unicode characters into the regex pattern. All escaped characters begin with the \ character, which also allows the pattern to search for special characters without enacting their special properties by treating the special character as plaintext.

Note: Some escape character examples could also be found in the character class examples listed in the previous exercise.

Data:
1. Let’s count the number of new lines in this string: `"1\n2\n3\n4\n5\n6\n7\n8\n9\n10"`. Declare a `Pattern` called `pattern` that searches for new lines.Declare a `Matcher` called `matcher` with the text to match being the string shown above.
2. Use a `while` loop to count the number of occurrences.

Example final:
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Example {
  public Example() {}

  public static void main(String[] args) {
    Pattern pattern = Pattern.compile("\n");
    Matcher matcher = pattern.matcher("(1\n2\n3\n4\n5\n6\n7\n8\n9\n10)+");

    int count = 0;
    while(matcher.find())count++;
    System.out.println(count);
  }
}
```

Output:
```terminal
9
```
