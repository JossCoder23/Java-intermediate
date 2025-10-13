## @Test Methods and Asserts

A typical `@Test` method involves assertions.

Assertions are found in the `junit.org.Assert` class library. Each “assert” is a way to perform a specific test in JUnit testing.

Below are a couple of common assert `methods` (note: they all have a return type of `void`):

| Assert Method                                 | Description                            |
|:---------------------------------------------:|:--------------------------------------:|
| assertEquals(expected, actual)                | Checks if two values are equal         |
| assertNotEquals(expected, actual)             | Checks if two values are not equal     |
| assertTrue(boolean condition)                 | Checks if a condition is true          |
| assertFalse(boolean condition)                | Checks if a condition is false         |
| assertNotNull(Object object)                  | Checks if an object isn’t null         |
| assertNull(Object object)                     | Checks if an object is null            |
| assertArrayEquals(expectedArray, actualArray) | Checks if two arrays are equal         |

When called, each “assert” is considered as a test case by the `compiler`, and any given assert can either pass or fail. A `@Test` method can only pass if all test cases inside of it pass. If any case fails, the whole test method will be marked red and considered a failed test.

Let’s walk through an example to best display how these asserts can be used.

Suppose we have a class object called `Human`. We assign that object a `name`, represented by a string, and an integer value to represent their `hitpoints` upon creation.

```java
Human sam = new Human("Sam", 100);
```

We want to test whether or not Sam gets properly created and also test a `takeDamage()` method within the `Human` class to ensure any damage taken is being recorded. Because this implies two different tests, let’s create two different test methods:


```java
@Test
public void testHuman() {
  Human sam = new Human("Sam", 100);
  assertEquals(100, sam.getHitpoints());
  assertEquals("Sam", sam.getName());
}

@Test
public void testHumanTakeDamage() {
  Human sam = new Human("Sam", 100);
  assertEquals(100, sam.getHitpoints());
  sam.takeDamage(10);
  assertEquals(90, sam.getHitpoints());
}
```

Take note that `assertEquals()` is overloaded to account for different variable types.

Each assert method is a tool a programmer can use to uniquely test their code. They typically follow the pattern of “expected value first,” then find the “actual” value in the second parameter to check against the expected.

There are a few exceptions to this rule. When checking a boolean or an object’s existence, one parameter is used. When checking a decimal value, a third parameter (range) can be included to indicate that a value plus or minus this range is considered passable. For example:

```java
assertEquals(25.5, sam.calculateDamage(), 0.9);
```

This will pass if `sam.calculateDamage()` returns a value anywhere within the range of `24.6` and `26.4`.

Example final:
```java
Example.java

public class Example {
  // Constructor
  public Example() {
  }

  public int factorial(int n) {
    int result = 1;
    for (int i = n; i > 0; i--) {
      result *= i;
    }
    return result;
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
  Example ex = new Example();

  @Test
  public void testFactorial() {
    assertThat(ex.factorial(4), equalTo(24));
    assertThat(ex.factorial(5), equalTo(120));
    assertThat(ex.factorial(1), equalTo(1));
    assertThat(ex.factorial(0), equalTo(1));
  }
}
```