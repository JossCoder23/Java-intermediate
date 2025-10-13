## @Test-ing, @Test-ing, 1 2 3

`@Test` will be the bulk of any JUnit testing. Anything that needs to be “checked” and “verified” will likely occur within a method marked with the `@Test` annotation.

A test method looks like this:

```java
@Test
public void test() {
  // Test cases
}
```

The way this method functions is atypical of `methods` found in traditional Java `classes`. These `@Test` annotated methods will always run unless otherwise annotated as `@Ignore`, which tells the `compiler` to skip over that particular method. These test methods also don’t have to be called, as they’re automatically detected and run by the compiler.

Typically, there will be a test method for every class object and class method in the program. For instance, if a method exists called `takeDamage()`, there will often also be a `testTakeDamage()` test method verifying the functionality of that method.

The word coverage may arise at some point during a programmer’s testing journey, which in the case of JUnit just means “test coverage.” In other words, it asks the question “how much of the code is actually tested?” Or in other other words, “do the test methods touch all of the code?” A good program will have full coverage.

Most Java IDEs will make it easy to detect coverage, often supporting ways to visibly see all the code touched by testing and all the code missed. Eclipse, an example of a Java IDE, does this by tinting the code green or red depending on whether or not a test case hits that area of the program.

The test cases themselves, regardless of the coverage algorithm, will actually follow a similar color pallet when run. JUnit makes it a standard to use the colors green and red to indicate whether or not a test method passes or fails. A test will go green if it passes, and red otherwise.

Programmers have created a mantra around this JUnit standard: “Red — Green — Refactor!”

Let’s talk about why that mantra is indicative of good test practices and how it’s understood by programmers working with JUnit testing.