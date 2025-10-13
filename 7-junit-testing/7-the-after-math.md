## The @After-math

The `@After` annotation acts just like the `@Before` but will run after each test method. Particularly if this cleanup needs to occur after each test.

```java
@After
public void afterEachTest() {
  // Cleanup
}
```

`@After` is used for cleaning up `variables` and objects, and freeing memory. If a file needs to be closed, an object needs to be removed, or an environment or array needs to be emptied, this is perfect.

If the cleanup needs to happen only once after all of the tests conclude, much like `@BeforeClass`, an `@AfterClass` annotation exists for this purpose. This will ensure the method runs after all tests within the class have already run.

Example final:
```java
// Test imports
import org.junit.Test;
import org.junit.After;
import org.junit.Before;

import static org.junit.Assert.fail;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.hamcrest.CoreMatchers.equalTo;
// File imports
import java.io.File;
import java.io.FileWriter;
import java.util.Scanner;
// Possible exceptions to detect
import java.io.IOException;

public class TestExample {

  static File file;
  static FileWriter w;
  static Scanner s;

  @Before
  public void beforeEachTest() throws IOException {
    file = new File("test.txt");
    w = new FileWriter("test.txt");
    s = new Scanner(file);
  }

  @Test
  public void test1() throws IOException {
    w.write("Testing testing 1 2 3!");
    w.close();
    assertThat(s.nextLine(), equalTo("Testing testing 1 2 3!"));
  }

  @Test
  public void test2() throws IOException {
    w.write("Poking poking 4 5 6!");
    w.close();
    assertThat(s.nextLine(), equalTo("Poking poking 4 5 6!"));
  }

  @After
  public void afterEachTest() throws IOException {
    s.close();
  }

}
```