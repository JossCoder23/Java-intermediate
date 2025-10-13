## Quantifiers

Remember that `+` character used in the character class example? That’s what regex calls a quantifier.

Quantifiers look at preceding tokens and indicate how many matches to look for, defaulting to trying to match as many characters as possible unless otherwise defined. The following are examples of quantifiers (note that “a” is user-defined and can be any character or group of characters. Any numerical digits used are also user-defined):

| Quantifier      | Description                                 | 
|:---------------:|:-------------------------------------------:|
| a*              | 0 or more                                   |
| a+              | 1 or more                                   |
| a?              | 0 or 1                                      |
| a{5}            | Exactly five                                |
| a{3,}           | Three or more                               |
| a{1,3}          | Between one and three                       |
| a+?             | Match as few as possible                    |
| a{2,}?          | Match as few as possible with a lower bound |

Patterns with quantifiers are generally straightforward. All they do is grab and group the quantified amount of characters together when found. Let’s cover a quick example:

```java
Pattern pattern = Pattern.compile("a*b");
```

This pattern searches for text that includes 0 or more “a”s followed by a “b.” It’ll find any “ab,” “aab,” “aaaaaaab,” but also, because it can match any text that has 0 “a”s followed by a “b,” it will also find “b.”

Let’s practice this concept.

Data:

1. You are given an array of strings called `strings`. Let’s see how many of these strings are exactly at least one “C” followed by exactly two “Q”s. First, define a `Pattern` called `pattern` that will check a string for at least one “C” and exactly two “Q”s.Example: The string “CCCCCCCCQ” will return not match, but the string “CCCCCCCQQ” will.
2. Define a `Matcher` called `matcher`. Inside the for-loop, use the `matcher` to match the `pattern` against every string.
3. Finally, use the `matcher` to check if a string is exactly at least one “C” and two “Q”s. For every string, print “true” if it is a match and “false” otherwise, on a separate line.

Example final:
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Example {

  public static void main(String[] args){
    String[] strings = {"CCQQ", "QQCC", "CQQ", "QUACK", "CCQ", "CQC", "CQQQ", "CCCQQ"};

    Pattern pattern = Pattern.compile("C+Q{2}");

    for(String s: strings){
      Matcher matcher = pattern.matcher(s);
      System.out.println(matcher.matches());
    }
  }
}
```

Output:
```terminal
true
false
true
false
false
false
false
true
```