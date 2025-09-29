## Multiple Type Parameters

As of now, our generic `classes`, `interfaces`, and `methods` have all taken a single parameter type. But what if our program needed to specify two or more parameter types? Java `generics` allow us to do that as well. Let’s look at an example:

```java
public class Box<T, S> {
  private T item1;
  private S item2;
  // Constructors, getters, and setters
}
Box<String, Integer> wordAndIntegerBox = new Box<>("Hello", 5);
```

In the example above, we created a generic class `Box` with two type parameters, `T` and `S`, by providing a comma-separated list of type parameters in the diamond operator. We also instantiated a `Box` reference named `wordAndIntegerBox` by providing the necessary type arguments in a comma-separated list: `<String, Integer>`.

This can also be done for interfaces and methods. Let’s look at an example for a method:

```java
public class Util {
  public static <T, S> boolean areNumbers(T item1, S item2) {
    return item1 instanceof Number && item2 instanceof Number; 
  }
}
  
boolean areNums = Util.areNumbers("Hello", 34);  // false
```

In the example above, we created a `static areNumbers()` method that has two generic type parameters: `T` and `S`. Note that a comma-separated list of type parameters, `<T, S>`, must be specified in the method signature before the return type. A cool thing about the example is if it weren’t for Java’s type inferences, the above method would have to be called like this:


```java
Boolean areNums = Util.<String, Integer>areNumbers("Hello", 34);  // false
```

In the example above, we explicitly specified the type arguments `<String, Integer>` before the method name. Type inferences will infer these types from the arguments passed in, `"Hello"` and `34`, making the explicit arguments unnecessary.

Let’s practice creating a multiple-type parameter class.

Example Final:

```java
Container.java

public class Container<T, S> {
  
  private T item1;
  private S item2;

  public Container(T item1, S item2) {
    this.item1 = item1;
    this.item2 = item2;
  }

  public T getItem1() {
    return this.item1;
  }

  public S getItem2() {
    return this.item2;
  }

}
```

```java
Main.java

public class Main {
  public static void main(String[] args) {
    
    Container<Integer, Double> myContainer = new Container<>(2, 45.98);
    
    System.out.println("Item1: "+ myContainer.getItem1());
    System.out.println("Item2: "+ myContainer.getItem2());
  }
}
```

Output:
```terminal
Item1: 2
Item2: 45.98
```
