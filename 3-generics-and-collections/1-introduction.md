## Introduction

When using Java, we often write `classes` and algorithms that work around certain `data types`. Let's look at the following `class` as an example:

```java
public class StringBox {
  public String myString;
} 
```

In the example above, we have a `StringBox` class which represents a real-world box of words. This class’s `methods` perform all of their computations with regards to the `String` `myString` field. What if we wanted a box of `int`s? We could create a new class:

```java
public class IntegerBox {
  public int myInt;	
} 
```

The example above meets our requirements, but as the program grows and we need more types of boxes, it will become unmanageable. We can solve this problem by using `generics`.

Generics, like the name implies, allow us to create generic classes and methods by specifying a type parameter. We can make `StringBox` and `IntegerBox` into a generic `Box` class like so:

```java
public class Box<T> {
  private T data;
}
```

In the example above, we created a generic `Box` class with a type parameter `T`. All class methods perform their computation around the `T`-type parameter We can now specify that we want a `String`, `Integer`, or any other type of `Box` by specifying a type argument.

In the example above, we created a generic `Box` class with a type parameter `T`. All class methods perform their computation around the `T`-type parameter

Over the course of this lesson, we’ll continue learning about generics in Java and their use cases.