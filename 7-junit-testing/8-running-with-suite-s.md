## Running With the @Suite-s

Getting the `@Before`, `@Test`, and `@After` `methods` all put together and tied up in a neat test class is the basis for JUnit testing. However, there’s one more step a programmer can take to apply one last layer of organization.

Test suites.

A test suite is a way to bundle JUnit test `classes` and run them together. The `@RunWith` and `@Suite` annotations are used to accomplish this, and they look like the following:

```java
@RunWith(Suite.class)
@Suite.SuiteClasses({
  // List of test classes to bundle together
})

public class MyTestSuite {
}
```

The above `MyTestSuite` class doesn’t need anything within the class itself to run. It instead will be called via some sort of “runner” class in the following way:

```java
import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;

public class TestSuiteRunner {
  public static void main(String [] args) {
    Result result = JUnitCore.runClasses(MyTestSuite.class);

    for (Failure failure : result.getFailures()) {
      System.out.println(failure.toString());
    }

    System.out.println(result.wasSuccessful());
  }
}
```

The runner will typically always look the same and can be used to run multiple different test suites depending on which test classes a programmer wants to bundle together. The `Result` and `Failure` imports are ways to gather and print the results of all the test cases run within the bundled test classes.

However, this feels like an overcomplicated way to run all of your tests, right? Ordinarily, test suites aren’t conducive to JUnit testing and aren’t always used or needed. However, there are valid reasons for a test suite to be used.

Consider the following scenario: A programmer builds an environment and fills it with objects for testing. Tests have to be done to make sure those objects made it into the environment without problems, and then more tests are done to manipulate those objects within the environment to make sure they can interact with each other. A final test empties the environment and makes sure everything gets cleaned up.

Without a test suite, multiple test classes that interact with this environment would need to recreate both the environment and the objects within that environment between test classes. This could get time-consuming with enough test classes and a large enough environment for testing.

With a test suite, one environment can be created and all of the test classes can interact with it accordingly. The last test class bundled into the suite can then handle the cleanup.

In retrospect, a test suite is really just another way to apply the `@Before` and `@After` methodology to testing, but on a larger class-based scale. It’s not always useful, but when it is, it’s really useful.