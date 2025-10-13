# JUnit 4 vs JUnit 5

## JUnit 4 and JUnit 5 are mostly similar but have their differences. Let’s learn about them!

JUnit testing opens a lot of doors for scalability and quality control. Well-written tests can often act as documentation in and of themselves, showing a programmer what a line of code or method should be doing at any given time.

The test-first methodology also acts to streamline the development of an application and formulate a healthy “plan first code after” mentality. After JUnit 4’s induction into coding, a handful of Java versions went by, and improvements were made to JUnit as a whole.

Then JUnit 5 was released.

Traditionally, JUnit 4 is more commonly used in general programming. While JUnit 4 laid the groundwork for JUnit testing, JUnit 5 adopted new Java 8 coding styles and aimed to be more robust and flexible than its previous iteration. This article will cover the major differences between JUnit 4 and JUnit 5.

## Different Annotations

The annotations between the two versions are mostly the same, but with some differences.

| JUnit 4      | JUnit 5      | Functionality                                           |
|:------------:|:------------:|:-------------------------------------------------------:|
| @Test        | @Test        | Declare a test method                                   | 
| @BeforeClass | @BeforeAll   | Execute before all test methods in the current class    |
| @AfterClass  | @AfterAll    | Execute after all test methods in the current class     |
| @Before      | @BeforeEach  | Execute before each test method                         |
| @After       | @AfterEach   | Execute after each test method                          |
| @Ignore      | @Disabled    | Disable a test method/class                             |
| N/A          | @TestFactory | Test factory for dynamic tests                          |
| N/A          | @Nested      | Nested tests                                            |
| @Category    | @Tag         | Tagging and filtering                                   |
| N/A          | @ExtendWith  | Register custom extensions                              |

## Other major JUnit 4 vs JUnit 5 differences

### Architecture

While JUnit 4 bundles everything it has into a single jar file, JUnit 5 breaks itself up into 3 sub-projects: JUnit Platform, JUnit Jupiter, and JUnit Vintage.

* JUnit Platform: Defines the TestEngine API for developing new testing frameworks that run on-platform.
* JUnit Jupiter: Entirely new JUnit annotations and TestEngine implementation to apply those new annotations.
* JUnit Vintage: Supports JUnit 3 and JUnit 4 on the JUnit 5 platform.

### JDK Version

JUnit 4 requires at minimum Java 5, or any higher version. JUnit 5 requires Java 8 or higher.

### Asserts

JUnit 4 supports a way to incorporate an error message into all assert methods as the first argument, the message of which would print if a test fails.

```java
public static void assertEquals(long expected, long actual)
public static void assertEquals(String message, long expected, long actual)
```

JUnit 5 changed the class name, now called “Assertions,” and added new `assertThrows()` and `assertAll()` methods. The new version also changed where the error message is inserted into the assert methods and added a third overloaded method with a way to print the supplier of the message.

```java
public static void assertEquals(long expected, long actual)
public static void assertEquals(long expected, long actual, String message)
public static void assertEquals(long expected, long actual, Supplier messageSupplier)
```

### Assumptions

JUnit 4 supports five `org.junit.Assume` methods, while JUnit 5 supports three.
* JUnit 4: `assumeFalse()`, `assumeNoException()`, `assumeNotNull()`, `assumeThat()`, `assumeTrue()`
* JUnit 5: `assumeFalse()`, `assumeThat()`, `assumeTrue()`

### Test Suites

Both JUnit 4 and JUnit 5 have ways to use test suites for testing, but the syntax has been changed for JUnit 5.

JUnit 4 uses `@RunWith` and `@Suite`.

```java
import org.junit.runner.RunWith;
import org.junit.runners.Suite;

@RunWith(Suite.class)
@Suite.SuiteClasses({
   // List of classes
})
```

JUnit 5 uses `@SelectPackages` and `@SelectClasses`.

```java
import org.junit.platform.runner.JUnitPlatform;
import org.junit.platform.suite.api.SelectPackages;
import org.junit.runner.RunWith;

@Suite
@SelectPackages("com.package.path")
```

JUnit 5 uses a way to locate the package containing the test classes intended to be run in the test suite, which simplifies the overall process and doesn’t require a hardcoded list like JUnit 4 uses.

## Non-public vs Public Test Methods

JUnit 4 has always required its test classes and methods all be public. JUnit 5 changed this to now allow them to be package protected and private. It does this by using “reflection,” which allows JUnit 5 to discover non-public classes and methods despite the limited visibility.

This effect also extends to the constructors within the test classes, and allows the constructors to accept arguments now. JUnit 4 required a public no-argument constructor, whereas JUnit 5 does not.

## 3rd Party Integration

No integration support exists in JUnit 4 for third-party plugins or IDEs. JUnit 5, however, has a dedicated sub-project, JUnitPlatform, for this purpose which uses the TestEngine API defined inside it

Overall, the differences between JUnit 4 and JUnit 5 cover ways to streamline the functionality of JUnit 4 while adopting nuances like third-party integration. The newer version acts as a means of removing the obscurity found in some of the JUnit 4 functionalities, but also goes so far as to incorporate a JUnit Vintage sub-project should somebody want to still use JUnit 4 alongside JUnit 5.

The two versions are very comparable in functionality, and while few major improvements and unique methods came from JUnit 5, it still acts as a pleasant overhaul to the possible obstacles JUnit 4 could present.