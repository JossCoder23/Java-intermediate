## Custom Serialization

As we’ve learned about serialization, we’ve discussed how the JVM defines a default way to serialize objects when their `classes` implement the `Serializable` interface. Can we modify this default process? We can by implementing the `methods` `readObject()` and `writeObject()` in our class!

Let’s look at some code that implements `readObject()` and `writeObject()`:

```java
public class DateOfBirth {
  private int month;
  private int day;
  private int year;

  // constructors and getters
}

public class Person implements Serializable {
  private String name;
  private DateOfBirth dateOfBirth;

  private void writeObject(java.io.ObjectOutputStream stream) throws IOException{
    stream.writeObject(this.name);
    stream.writeInt(this.dateOfBirth.getMonth());
    stream.writeInt(this.dateOfBirth.getDay());
    stream.writeInt(this.dateOfBirth.getYear());
  }

  private void readObject(java.io.ObjectInputStream stream) throws IOException, ClassNotFoundException{
    this.name = (String) stream.readObject();
    int month = (int) stream.readInt();
    int day = (int) stream.readInt();
    int year = (int) stream.readInt();
    this.dateOfBirth = new DateOfBirth(month, day, year);
  }	
}
```

In the example above:

* We have two classes: `Person` which implements `Serializable` and `DateOfBirth` which does not.
* `Person` has a reference field of type `DateOfBirth`.
* If we were to use the default serialization process, we would get a `NotSerializableException` because `DateOfBirth` does not implement `Serializable`.
* We implement `writeObject()`, which must throw `IOException`, to serialize a `DateOfBirth` object by manually serializing all of its fields separately. We also serialize the serializable `String` field.
* We implement `readObject()`, which must throw `IOException` and `ClassNotFoundException`, to deserialize a `Person` object by reading the `int` fields that are a part of `DateOfBirth` and creating a new `DateOfBirth` object with the provided constructor. This new object is used to set the `dateOfBirth` field in `Person`.

Often, the default process of serialization is enough as long as all references implement `Serializable`. The implementation of `readObject()` and `writeObject()` is useful when we have a reference field that does not or cannot implement `Serializable`. We could also potentially handle `static` field values if we needed to persist them. This, however, is not good practice as a `static` field should belong to a class and not an object.

Let’s practice implementing our custom serialization and deserialization methods.

Example final:
```java
Car.java

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
  private Engine engine;

  public Car(String make, int year) {
    this.make = make;
    this.year = year;
    this.engine = new Engine(2.4, 6);
  }

  private void writeObject(ObjectOutputStream stream) throws IOException {
    stream.writeObject(this.make);
    stream.writeInt(this.year);
    stream.writeDouble(this.engine.getLiters());
    stream.writeInt(this.engine.getCylinders());
  }
 
  private void readObject(ObjectInputStream stream) throws IOException, ClassNotFoundException {
    this.make = (String) stream.readObject();
    this.year = (int) stream.readInt();
    double liters = (double) stream.readDouble();
    int cylinders = (int) stream.readInt();
    this.engine = new Engine(liters, cylinders);
  }    


  public String toString(){
    return String.format("Car make is: %s, Car year is: %d, %s", this.make, this.year, this.engine);
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
    System.out.println("Toyota (Copy) - "+toyotaCopy);
    System.out.println("Toyota (Original) - "+toyota);
    System.out.println("Is same object: "+ isSameObject);

  }
  
}

Engine.java

public class Engine {
  private double liters;
  private int cylinders;

  public Engine(double liters, int cylinders) {
    this.liters = liters;
    this.cylinders = cylinders;
  }

  public double getLiters() {
    return this.liters;
  }

  public int getCylinders() {
    return this.cylinders;
  }

  public String toString() {
    return String.format("Engine liters is: %f, Engine cylinders is: %d", this.liters, this.cylinders);
  }
}
```

Output:
```terminal
Toyota (Copy) - Car make is: Toyota, Car year is: 2021, Engine liters is: 2.400000, Engine cylinders is: 6
Toyota (Original) - Car make is: Toyota, Car year is: 2021, Engine liters is: 2.400000, Engine cylinders is: 6
Is same object: false
```