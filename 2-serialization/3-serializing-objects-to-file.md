## Serializing Objects to a File

Now that we’ve learned about the `Serializable` interface and how to implement it, let’s take a look at how to serialize an object to a file. To do this we’ll need to use the helper `classes`, `FileOutputStream`, which will help us write to a file, and `ObjectOutputStream`, which will help us write a serializable object to an `output` stream.

Let’s look at how to do this with some code:

```java
public class Person implements Serializable {
  private String name;
  private int age;
  private static final long serialVersionUID = 1L; 

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }  

  public static void main(String[] args) throws FileNotFoundException, IOException{
    Person michael = new Person("Michael", 26);
    Person peter = new Person("Peter", 37);
        
    FileOutputStream fileOutputStream = new FileOutputStream("persons.txt");
    ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
        
    objectOutputStream.writeObject(michael);
    objectOutputStream.writeObject(peter);	
  }
}
```

In the example above we:

* Added a constructor to the `Person` class we defined in the previous lesson.
* Defined `main()` and initialized two `Person` objects - `michael` and `peter`.
* Initialized a `FileOutputStream` object in `main()` which will create and write a stream of bytes to a file named persons.txt.
* Initialized an `ObjectOutputStream` object in `main()` which will help serialize an object to a specified output stream.
* Used `objectOutputStream.writeObject()` in `main()` to serialize the `michael` and `peter` objects to a file.

After the execution of the above program, the persons.txt will contain a stream of bytes that has the type and value information of the fields for the `michael` and `peter` objects respectively.

Let’s practice serializing an object to a file.

Example final:

```java
import java.io.Serializable;
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
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

  public static void main(String[] args) throws FileNotFoundException, IOException {
    
    Car toyota = new Car("Toyota", 2021);
    Car honda = new Car("Honda", 2020);

    FileOutputStream fileOutputStream = new FileOutputStream("cars.txt");
    ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
    objectOutputStream.writeObject(toyota);
    objectOutputStream.writeObject(honda);

  }

}
```
