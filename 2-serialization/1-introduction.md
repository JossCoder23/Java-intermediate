## Introduction

Often when creating Java applications and working with objects, we find the need to persist them. Specifically, we need to be able to store an object’s state (member fields) in files, in memory, or in a database. Java provides the Serializable interface to do just that.

Remember that an interface describes the behavior a class should have and by having our class implement Serializable it can be serialized by the Java Virtual Machine (JVM).

Let’s look at how this is done:

```java
public class Person implements Serializable {
  private String name;
  private int age;
} 
```

In the example above we’ve defined a Person class that implements Serializable. By implementing Serializable, the JVM will know how and what to do when a Person object needs to be serialized (we’ll look at this more later).

Notice that we didn’t need to override a method and implement it for us to be able to serialize a Person object. This is because Serializable is a marker interface. A marker interface provides run time information to the JVM about the class and does not have any methods associated with it.

Over the course of this lesson, we’ll continue learning about the Serializable interface and how serialization works in Java.

