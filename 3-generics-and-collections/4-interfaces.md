## Interfaces

We’ve seen how to create a generic class, but we can also create a generic interface. Let’s look at an example:

```java
public interface Replacer<T> {
  void replace(T data);
}
```

The generic interface `Replacer` is created like a generic class where the type parameter `<T>` must be appended to the interface name. Interface method declarations are similar to non-generic interfaces and can include non-generic methods as well.

A generic interface can be implemented by a generic class and its generic type parameter can be used as the argument to the interface type parameter. For example, let’s have our `Box` generic class implement the interface `Replacer`:


```java
public class Box <T> implements Replacer<T> {
  private T data;
  
  @Override
  void replace(T data) {
    this.data = data; 
  }
}
```

In the example above, the `Box` type parameter `<T>` will be used as the type argument for the `Replacer` type parameter `<T>`.

We can also have a non-generic class implement a generic interface by specifying the type argument to the interface. For example:

```java
public class StringBag implements Replacer<String> {
  private String data;
  
  @Override
  void replace(String data) {
    this.data = data; 
  }
}
```

In the example above, the `StringBag` is a non-generic `class` that implements `Replacer` and provides `String` as the argument to the type parameter. Notice that the `replace()` parameter `data` has a `String` type as opposed to the generic `T` in the previous example.

Now let’s create `interface` type references similarly to how we created generic `class` references:

```java
Replacer<Integer> boxReplacer = new Box<>();  // Using generic `Box` implementation
Replacer<String> bagReplacer = new StringBag();  // Using non-generic `StringBag` implementation
```

In the example above we created two `Replacer` references. The `Box` implementation can be of any type but the `StringBag` implementation needs to be a `<String>` type because of the non-generic class implementation.

Let’s practice creating generic interfaces and references.

Example final:
```java
Retriever.java

public interface Retriever<T> {
  T retrieveData();
}
```

```java
Book.java

public class Book implements Retriever<String> {
  private String name;

  public Book(String name) {
    this.name = name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return this.name;
  }

  @Override
  public String retrieveData() {
    return this.name;
  }

}
```

```java
Container.java

public class Container<T> implements Retriever<T> {
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
  public T retrieveData() {
    return this.data;
  }

}
```

```java
Main.java

public class Main {
  public static void main(String[] args) {
    
    int myNumber = 24;
    String bookName = "Hello Book!";
    // Enter your code below...
    Retriever<Integer> containerRetriever = new Container<>(myNumber);
    Retriever<String> bookRetriever = new Book(bookName);

    System.out.println(containerRetriever.retrieveData());
    System.out.println(bookRetriever.retrieveData());

  }
}
```

Output:
```terminal
24
Hello Book!
```