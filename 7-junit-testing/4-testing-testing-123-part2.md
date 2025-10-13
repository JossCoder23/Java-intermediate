## @Test-ing, @Test-ing, 1 2 3 Continued

“Red — Green — Refactor!”

By the end of this lesson, this mantra should be playing in your mind whenever you think about testing your code.

This mantra emphasizes the “test-first” approach to programming. In the simplest sense, this just means that a program’s tests are written before the code is made.

But how does that work? How can a test be written to test code that doesn’t exist yet?

The answer lies in the mantra.

“Red” is the start of the mantra and the first thing a programmer needs to do in test-first development. In other words, a programmer needs to write a test and make it go red as the first step for testing.

The act of doing this establishes a test to exist first, which is good practice for coverage but also lays the requirements for the code. A skeleton of the method they want to be testing is then created, which often will be set to return `0` (or some other arbitrary value) to ensure the test has something to compare against. This arbitrary value will be different from what the test is “expecting” and make the test go red.

“Green” is the second step of the mantra. Now that we have our red test, we can write code into the skeleton method to make it work. We then run the test again and watch the test method go green.

These two steps help ensure the following things: we have good test coverage, our tests are testing what they should be testing, and the code works as expected.

The last step of the mantra is “Refactor,” which is often the last “clean-up” step of any coding. This step cleans up and polishes the code now that its bare minimum processing is tested and functional.

Now, let’s explore what makes these `@Test` `methods` tick and why this `junit.org.Assert` class library is so important.

Example final:
```java
Example.java

public class Example {
  public int isPositive(int n) {
    if (n > 0) {
      return 1;
    } else if (n == 0) {
      return -1;
    }
    return 0;
  }
}
```

```java
TestExample.java

import org.junit.Test;

import static org.junit.Assert.fail;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.CoreMatchers.equalTo;

public class TestExample {
  int a = 3;
  int b = -5;
  int c = 0;

  Example ex = new Example();

  @Test
  public void testIsPositive() {
    assertThat(ex.isPositive(a), equalTo(1));
    assertThat(ex.isPositive(b), equalTo(0));
    assertThat(ex.isPositive(c), equalTo(-1));
  }
}
```

```terminal
run.bat

export JUNIT4_CLASSPATH="/usr/share/java/junit4-4.12.jar:/usr/share/java/hamcrest-core-1.3.jar"
javac -cp .:$JUNIT4_CLASSPATH ./*.java
java -cp .:$JUNIT4_CLASSPATH org.junit.runner.JUnitCore TestExample


$ ./run.bat
  JUnit version 4.12.
  Time: 0.005

  OK(1 test)
```
