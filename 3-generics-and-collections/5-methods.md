## Methods

We’ve covered generic classes and interfaces, but what can we do if we want one of our methods to be generic and not the whole class or interface? We can create generic methods to do just that. For example:

```java
public class StringBox {
  private String data;

  public <T> boolean isString(T item) {
    return item instanceof String; 
  }
}

StringBox box = new StringBox();
box.isString(5); // Returns false
```

In the example above, using the class `StringBox`, we created the generic method `isString()` with a generic type `T` as a method parameter. It’s important to note that generic methods need to include the type parameter, `<T>` in our example, before the return type, even if the return type is `void`. The generic method is called like any other method as shown.

We can also do this with `static` methods. Their signatures have the same requirements except for also needing the `static` keyword. For example:

```java
public class StringBox {
  private String data;

  public static <T> boolean isString(T item) {
    return item instanceof String; 
  }
}
StringBox.isString(5);  // Returns false
```

In the example above, we see how we made the `isString()` a `static` method by adding `static` to the method signature. We call it by using the class name instead of an object.

Let’s practice creating generic methods.

Example final:
```java
public class Main {

  public static void main(String[] args) {
    
    String test1 = "Double";
    double test2 = 5.8;

    // Enter code below...  
    boolean isTest1Double = isDouble(test1);
    boolean isTest2Double = isDouble(test2);
    System.out.println(isTest1Double);
    System.out.println(isTest2Double);

  }

  public static <T> boolean isDouble (T object) {
    return object instanceof Double;
  }

}
```

Output:
```terminal
false
true
```