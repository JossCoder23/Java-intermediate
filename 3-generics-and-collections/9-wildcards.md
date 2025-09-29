## Wildcards

We’ve seen that generic code can take type arguments to help generalize our code. We can make our code even more general when we don’t need the more strict type checking of using type parameters by using wildcards. A wildcard, denoted by the `?` symbol, represents an unknown type when used with generic methods. Let’s look at an example:

```java
public class Util {
  public static void printBag(Bag<?> bag) {
    System.out.println(bag.toString()); 
  }
}
Bag<String> myBag1 = new Bag("Hello");
Bag<Integer> myBag2 = new Bag(23);
Util.printBag(myBag1);  // Hello
Util.printBag(myBag2);  // 23
```

In the example above, we defined a `static` generic method that works on `Bag` types. We specify that `Bag`, which is a generic class, can be of any type by using the wildcard `Bag<?>`. We also created two `Bag` references of different types, `String` and `Integer`, and used them as arguments to `printBag()`.

You may be thinking how this is different than using a type parameter because we could write the above method as:

```java
public static <T> void printBag(Bag<T> bag) {
  System.out.println(bag.toString()); 
}
```

In the example above, we’ve defined the parameter as `Bag<T>` as opposed to `Bag<?>`. This implementation makes no difference, but you may notice that the wildcard version is better as it does not need the extra `<T>` before the return type making the signature easier to read.

In general, we should use type parameters, when we have a relationship between the type of arguments and the return type. For example:

```java
public static <T> Bag<T> getBag(Bag<T> bag) {
  return bag;
}
```

In the example above, we created a method that accepts a `Bag` of some type `T` and returns a `Bag` of the same type `T`. This use of type parameters maintains strong type checking throughout our code.

We can also create upper bounds and lower bounds (we’ll see this later) when using wildcards. For example:

```java
public static void printBag(Bag<? extends Number> bag) {
  System.out.println(bag.toString()); 
}
```

In the example above, `printBag()` accepts any `Bag` that is a `Number` and will produce an error when passing a type of `Bag` that does not extend `Number`. For example, `Bag<String>` will produce an error.

Let’s practice using wildcards in our generic code.

Example Final:

```java
Container.java

public class Container<T> {
  private T data;

  public Container(T data) {
    this.data = data;
  }

  public void setData(T data) {
    this.data = data;
  }

  public T getData() {
    return this.data;
  }

  @Override
  public String toString(){
    return "Container(data="+this.data+")";
  }
}
```

```java
Main.java

public class Main {
  public static void main(String[] args) {
    Container<String> stringContainer = new Container<>("Hello");
    Container<Integer> intContainer = new Container<>(34);

    printContainer(stringContainer);
    printContainer(intContainer);
  }

  public static void printContainer(Container<?> container) {
    System.out.println(container.toString());
  }
}
```

Output:
```terminal
Container(data=Hello)
Container(data=34)
```