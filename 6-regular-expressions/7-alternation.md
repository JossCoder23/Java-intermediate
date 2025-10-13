## Alternation

Alternation is just the regex way of saying OR. In regex, this is denoted by the following (note the “ab” and “cd” are user-defined):

| Alternation         | Description                |
|:-------------------:|:--------------------------:|
| ab-cd               | Match ab OR cd             | 

The use of alternation works just like the boolean OR. The pattern will search for any text that matches either alternated pattern and only return nothing if neither is found. Otherwise, this pattern will group either match in the search results regardless of which pattern matched.

Alternation is also found implicitly in character `classes`. For instance, a character class like `[A-Z]` grabs a range of characters. This is the equivalent of grabbing `A` OR `B` OR `C` and so on.

This just allows you to get a bit more complicated, especially if you want to look for slight differences between words that share a pattern. For instance, when looking at code, someone might type the following in two possible ways:

```java
i < 10
10 > i
```

Both ways are technically correct and produce the same result. So to make a regex pattern accept both when looking for the same technical thing, you can write a pattern for each and just alternate it with an `|` to ensure you’re finding both feasible ways to write the same code.

Data:
1. We’ve written a pattern in these exercises that searches for both versions of the word `"gray"`. Let’s approach this problem again but this time, we will use alternation. Declare a `pattern` called pattern that uses alternation to find all instances of `"gray"` and `"grey"` in a given text. Run your code.
2. Count the instances of “grey” or “gray” in the given string.

Example Final:
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Example {
  
  public static void main(String[] args) {
    Pattern pattern = Pattern.compile("gray|grey");
    Matcher matcher = pattern.matcher("Vibrant light bloomed across the gray sky, illuminating its grey haze in flashes amidst rolling hills of wispy gray clouds. Colors of gold, pink, and purple painted the horizon, the dull grey of the sky overtaken by brief moments of a quiet twilight storm.");

    int count = 0;
    while(matcher.find())count++;
    System.out.println(count);
  }
}
```

Output:
```terminal
4
```