## Serializable Fields

When serializing objects, we often need to handle static class fields or exclude non-static fields in the serialization. Recall that the JVM defines a default way of serializing objects; this default includes ignoring static class fields, which belong to a class and not an object. The JVM also serializes all fields in an object, even those marked `private` and `final`.

Although the JVM implicitly serializes non-static fields, we can instruct the JVM to ignore them using the `transient` keyword. A field marked as `transient` will have its value ignored during serialization and instead receive the default value for that type of field.

Let’s visualize this with some code:

```java
public class Person implements Serializable {
  private String name;
  private int age;
  private static int numberOfPeople = 10;
  private transient int yearBorn;  
} 
```

In the example above, we defined a `static` field called `numberOfPeople` with a value of `10`. Since it belongs to the class, it will not be included in the serialization process. We also defined a `transient` field called `yearBorn` of type `int`. The JVM will ignore the initialized value of this field and instead serialize the field with its default value for its type (`0` in this case).

Let’s discuss some interesting aspects of deserializing objects with `transient` and `static` fields:

* The deserialized (copy) object will not get the default value for a `static` field (in our example the value `0`). Since a `static` field belongs to the class and not the object, a deserialized `static` field will receive the value it corresponds to in the current class.
* A constructor is not called during deserialization for the deserialized type object. Object fields are set using reflection.
* A constructor is only called for the first non-serializable class in the parent hierarchy of the deserialized object.

We often want to serialize all non-static fields in an object. However, sometimes we may need to serialize `transient` fields if a field’s value is dependent on other fields or, more importantly, if we have a reference field that is not serializable (we’ll talk about this later).

Let’s practice using different types of serializable and non-serializable fields.

Example final:

```java
import java.io.Serializable;
import java.io.FileOutputStream;
import java.io.FileInputStream;
import java.io.ObjectOutputStream;
import java.io.ObjectInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class Car implements Serializable {
  private String make;
  private int year;
  private static final long serialVersionUID = 1L;
  private transient String model;

  public Car(String make, int year, String model) {
    this.make = make;
    this.year = year;
    this.model = model;
  }

  public String toString(){
    return String.format("Car make is: %s, Car year is: %d, Car model is: %s, serialVersionUID: %d", this.make, this.year, this.model, serialVersionUID);
  }

  public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {
    Car toyota = new Car("Toyota", 2021, "Corolla");
    Car honda = new Car("Honda", 2020, "Civic");
    FileOutputStream fileOutputStream = new FileOutputStream("cars.txt");
    ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
    objectOutputStream.writeObject(toyota);
    objectOutputStream.writeObject(honda);

    FileInputStream fileInputStream = new FileInputStream("cars.txt");
    ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);

    Car toyotaCopy = (Car) objectInputStream.readObject();
    Car hondaCopy = (Car) objectInputStream.readObject();

    boolean isSameObject = toyotaCopy == toyota;
    System.out.println("Toyota (Copy) - "+ toyotaCopy);
    System.out.println("Toyota (Original) - "+ toyota);
    System.out.println("Is same object: "+ isSameObject);
  }
}
```

Output:
```terminal
Toyota (Copy) - Car make is: Toyota, Car year is: 2021, Car model is: null, serialVersionUID: 1
Toyota (Original) - Car make is: Toyota, Car year is: 2021, Car model is: Corolla, serialVersionUID: 1
Is same object: false
```
