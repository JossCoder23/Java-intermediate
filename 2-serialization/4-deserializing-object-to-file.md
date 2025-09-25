## Deserializing an Object to a File

Knowing how to serialize our objects is great, but it becomes more useful when we can turn serialized objects back into Java objects with deserialization. As the name suggests, deserialization does the opposite of serialization and transforms a stream of bytes into a Java object.

Like with serialization, we’ll make use of helper `classes` `FileInputStream`, which helps us read a file, and `ObjectInputStream` which helps us read a serialized stream of bytes.

Assuming we have the file persons.txt we created in the last exercise, let’s understand how to do this by looking at some code:

```java
public class Person implements Serializable {
  public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {

    FileInputStream fileInputStream = new FileInputStream("persons.txt");
    ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
        
    Person michaelCopy = (Person) objectInputStream.readObject();
    Person peterCopy = (Person) objectInputStream.readObject();
  }
}
```

In the example above we:

* Initialized `FileInputStream` and `ObjectInputStream` in `main()` which will read a file and transform a stream of bytes into a Java object.
* Created a `Person` object named `michaelCopy` by using `objectInputStream.readObject()` to read a serialized object.
* Created a `Person` object named `peterCopy` by using `objectInputStream.readObject()` to read a serialized object.

It’s important to note that deserialization creates a copy of the original object. This means that the deserialized object shares the same field values as the original object but is located in a different place in memory. Also, The deserialized objects will be in the order that they were serialized in and we need to explicitly typecast the `readObject()` return value back into the type of object we serialized.

The JVM ensures it deserializes the object using the correct class file by comparing the `serialVersionUID` in the class file with the one in the serialized object. If a match is not found an `InvalidClassException` is thrown. Also, `readObject()` throws a `ClassNotFoundException` when the `class` of the serialized object cannot be found.

Let’s practice deserializing objects from a file.

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

  public Car(String make, int year) {
    this.make = make;
    this.year = year;
  }

  public String toString(){
    return String.format("Car make is: %s, Car year is: %d", this.make, this.year);
  }

  public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {

    Car toyota = new Car("Toyota", 2021);
    Car honda = new Car("Honda", 2020);

    FileOutputStream fileOutputStream = new FileOutputStream("cars.txt");
    ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);

    objectOutputStream.writeObject(toyota);
    objectOutputStream.writeObject(honda);

    FileInputStream fileInputStream = new FileInputStream("cars.txt");
    ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);

    Car toyotaCopy = (Car) objectInputStream.readObject();
    Car hondaCopy = (Car) objectInputStream.readObject();

    boolean isSameObject = toyotaCopy == toyota;
    
    System.out.println(toyotaCopy);
    System.out.println(toyota);
    System.out.println(isSameObject);

  }
}
```