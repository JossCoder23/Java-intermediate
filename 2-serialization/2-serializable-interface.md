## Serializable Interface

Previously, we learned that to serialize an object, we needed our class to implement the `Serializable` interface. Notice that although we implemented the interface, we did not need to implement any `methods`. You may be thinking, “If we don’t need to implement any methods, why do we need our class to implement `Serializable`?”

In Java, the JVM defines a default way for `classes` that implement `Serializable` to have their objects serialized. The interface provides run-time information about the object field’s type and value for serialization and it takes care of converting it into a stream of bytes.

Although there is no need to implement any methods for serialization, it is important for the implementing class to provide a `serialVersionUID`:

```java
public class Person implements Serializable {
  private String name;
  private int age;
  private static final long serialVersionUID = 1L; 
} 
```

In the example above, the `serialVersionUID`, a `static final long` type number, acts as an identifier for the JVM to choose the proper class to convert a stream of bytes back into an object (we’ll cover this process in-depth later). Our serializable class can get a `serialVersionUID` in one of the following ways:

* You can have the JVM define one for you. This is not ideal because, depending on the JVM you have, you’ll get a different value and this may cause deserialization to fail.
* You can have your IDE generate one for you. This is better than the first option but you’ll need to ensure that your IDE has this feature.
* You can define the `serialVersionUID` explicitly in the class. This is the preferred option because you don’t need to rely on the JVM or your IDE to ensure proper deserialization.

Although the JVM uses the `serialVersionUID` to locate the proper class, it does not store the class file as part of the serialization. We need to ensure we load the class file into our program (if it’s not there already). With a default process of serializing objects and the `serialVersionUID`, Java makes serialization easy to implement.

Let’s practice adding a `serialVersionUID` to our serializable class.

Example final:

```java
import java.io.Serializable;

public class Car implements Serializable {
  
  private String make;
  private int year;
  private static final long serialVersionUID = 1L;
  
  public Car(String make, int year) {
    this.make = make;
    this.year = year;
  }

}
```