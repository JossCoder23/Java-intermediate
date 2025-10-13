## @Before We Go Further

The `@Before` annotation can be used to accompany the `@Test` `methods`. Methods tagged with `@Before` will run before each test method and look like the following:

```java
@Before
public void beforeEachTest() {
  // Something multiple tests use
}
```

They’re typically used if multiple test methods share a similarly created object or set of `variables`. Placing those inside the `@Before` annotated method ensures those objects are always freshly created and have the same starting attributes upon instantiation. This allows each test to work with those objects and variables without needing to create them inside their test bodies.

If we look at the example we covered in the previous exercise, we created the `Human` named “Sam” twice in the exact same fashion. Now that we know about the `@Before` annotation, we could instead place the creation of `sam` inside of the `@Before` method:

```java
Human sam;

@Before
public void createSam() {
  sam = new Human("Sam", 100);
}

@Test
public void testHuman() {
  assertEquals(100, sam.getHitpoints());
  assertEquals("Sam", sam.getName());
}

@Test
public void testHumanTakeDamage() {
  assertEquals(100, sam.getHitpoints());
  sam.takeDamage(10);
  assertEquals(90, sam.getHitpoints());
}
```

This is different from just making `sam` a class variable, which is also visible by all tests because the `@Before` will be re-run before each test. This means if tests modify the `sam` variable in any way, it ensures `sam` gets reset before the next test runs.

There’s another variant of the `@Before` annotation that will let us create a method that will run one time before all tests instead of multiple times before each test. This is done by using the `@BeforeClass` annotation.

`@Before` and `@BeforeClass` both have their unique uses, making them valuable tools for JUnit testing.

Example final:
```java
import org.junit.Test;
import org.junit.Before;

import static org.junit.Assert.fail;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.CoreMatchers.equalTo;

public class TestExample {
  static int a;

  @Before
  public void beforeEachTest() {
    a = 10;
  }

  @Test
  public void test1() {
    a = a - 5;
    assertThat(a, equalTo(5));
  }

  @Test
  public void test2() {
    a = a + 7;
    assertThat(a, equalTo(17));
  }

  @Test
  public void test3() {
    assertThat(a, equalTo(10));
  }
}
```

