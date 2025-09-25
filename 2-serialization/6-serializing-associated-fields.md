## Serializing Associated Fields

As we’ve been serializing objects, we’ve not only had primitive type fields, but also reference types. For example:

```java
public class Person implements Serializable {
  private String name;
  private int age;
  private static final long serialVersionUID = 1L; 
}
```

In the example above, we’ve defined two primitive types, age and serialVersionUID, and a reference String type name. For reference types to be serializable, they must also implement the Serializable interface, which the String class does. If the reference type did not implement Serializable, then we would get a NotSerializableException thrown. When the JVM encounters a reference type, it will try to serialize the reference type first before trying to serialize the encapsulating object.

Let’s look at class definitions and go through the steps of serializing a Person object:

```java
public class Address implements Serializable{
  private String streetName;
}

public class Person implements Serializable{
  private Address address;
}
```

In the example above, when serializing a Person object the JVM will:

* Check that the Person object is serializable and try to serialize the Address type.
* Check that the Address object is serializable and try to serialize the String type.
* Check that the String object is serializable and serialize the value.
* Finish serializing the Address object after serializing streetName.
* Finish serializing the Person object after serializing address.

Our serializable classes will often have a combination of reference and primitives types, but the JVM will perform the same steps as above. If an exception were to be thrown at any point while serializing a reference type, a NotSerializableException would be thrown and propagated up.

Let’s practice serializing objects with reference-type fields.

Example Final:

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

  public String toString() {
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
```

```java
Engine.java

import java.io.Serializable;

public class Engine implements Serializable{
  private double liters;
  private int cylinders;

  public Engine(double liters, int cylinders){
    this.liters = liters;
    this.cylinders = cylinders;
  }

  public String toString(){
    return String.format("Engine liters is:%f, Engine cyclinders is: %d", this.liters, this.cylinders);
  }
}
```