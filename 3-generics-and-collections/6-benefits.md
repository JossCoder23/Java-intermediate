## Benefits

We’ve done great work learning about generic `classes`, `interfaces`, and `methods`. Let's discuss some benefits of using `generics` besides making our code more scalable. We can get away with not providing a type argument to a generic class or interface. This is known as using a raw type and they were prevalent before the introduction of generics in Java 5. For example:

```java
public class Box <T> {
  private T data;

  public Box(T data) {
    this.data = data; 
  }

  public T getData() {
    return this.data;
  }  
}

Box box = new Box<>("My String");  // Raw type box
String s2 = (String) box.getData();  // No incompatible type error
String s1 = box.getData();  // Incompatible type error
```

In the example above:

* Using the generic class `Box`, we created a raw type `Box` and passed `"My String"` as an argument.
* We called `getData()` and typecast the result in `String` `s2`. This has no error because we are explicitly downcasting to `String`.
* We called `getData()` to store the result in `String` `s1`. We get an `Incompatible` type error as `getData()` returns an `Object` type and we are trying to implicitly downcast to a `String`.

Raw types should be avoided because generics:

* Avoid “incompatible type” `errors` when retrieving data from raw types.
* Avoid a potential runtime `ClassCastException` error when explicitly typecasting.
* Give us compile-time type checking, which helps detect bugs before our code runs.
* Help when the JVM applies type erasure

When using generics, type erasure is applied by the JVM and will cause all type parameters to be replaced by `Object` or their type bounds (we’ll learn about this later). The type erasure will also apply any necessary type casting to ensure our code is type-safe and that the final byte code produced has non-generic types.

Great job learning about generics so far!

Example final:

```java
public class Main {
  public static void main(String[] args) {

    Container raw1 = new Container<>("My String");  // raw type box
    String s1 = (String) raw1.getData();  // no incompatible type error
    System.out.println("s1 is: "+ s1);

    /* Uncomment to see error
        String s2 = raw1.getData();  // incompatible type error
    */

    Container<String> stringContainer = new Container<>("Not raw");
    Container raw2 = stringContainer;
    
    raw2.setData("new string");// Unchecked warning produced
  }
}
```

output:
```terminal
s1 is: My String
Note: Main.java uses unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
```