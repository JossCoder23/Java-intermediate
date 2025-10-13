## JUnit Classes and Methods

JUnit testing takes place in a traditional Java `class`, just like the classes written for the application you want to test. The functionality for those tests comes from JUnit classes, most commonly the `Assert` class and annotation classes.

“Annotating” is a general term that refers to ways of marking `methods` for testing, changing how these methods are compiled, and establishing when they’ll be run by the `compiler`. The four most essential annotations are `@Before`, `@Test`, `@After`, and `@Ignore`.

The above annotations can be imported in the following ways:

```java
import org.junit.Before;
import org.junit.Test;
import org.junit.After;
import org.junit.Ignore;
```

Additionally, the following line will grab all functionality from the Assert class library, but note that each assert method can be imported individually:

```java
import static org.junit.Assert.*;
```

Let’s cover what all these annotations and classes mean and how they’re used for JUnit testing!


Data:
Move on once you’ve checked out the example test methods!

If you want to try running them, enter the following into the console:

```terminal
$ export JUNIT4_CLASSPATH="/usr/share/java/junit4-4.12.jar:/usr/share/java/hamcrest-core-1.3.jar"
$ javac -cp .:$JUNIT4_CLASSPATH ./*.java
$ java -cp .:$JUNIT4_CLASSPATH org.junit.runner.JUnitCore JUnitExample
```

You can highlight each line (excluding the `$`) above then copy and paste them into the terminal.

Example final:
```java
import org.junit.Before;
import org.junit.Test;
import org.junit.After;
import org.junit.Ignore;

import static org.junit.Assert.fail;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.CoreMatchers.equalTo;

public class JUnitExample {
  int a;

  @Before
  public void beforeTest() {
    a = 10;
  }

  @Test
  public void test() {
    assertThat(a, equalTo(10));
  }

  @Ignore
  public void ignoredTest() {
    assertThat(a, equalTo(50));
  }

  @After
  public void afterTest() {
    a = 0;
  }
}
```
