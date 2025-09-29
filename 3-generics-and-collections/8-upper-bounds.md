## Upper Bounnds

We’ve seen how generics make our code scalable by allowing us to provide type arguments to classes, interfaces, and methods. What if we needed to restrict what class or interface could be used as a type argument? We can accomplish this by assigning an upper bound. An upper bound will restrict a generic type to be a specific type or any type that `extends` it. Let’s see how this is done:

```java
public class Box <T extends Number> {
  private T data; 
}
```

In the example above, we defined a type parameter `T` and added an upper bound type `Number` for `T` with `extends Number`. The `extends` in this example means that `T` can be a `Number` or any of its subclasses (or interfaces).

We can create references to `Box` as follows:

```java
Box<Integer> intBox = new Box<>(2);  // Valid type argument
Box<Double> doubleBox = new Box<>(2.5);  // Valid type argument
Box<String> stringBox = new Box<>("hello");  // Error
```

In the example above we:

* Created two `Box` references with type arguments `Integer` and `Double`, which are both child classes of `Number`.
* Attempted to create a `Box` reference with type argument `String` and received an error because `String` is not a Number nor is it a subclass of `Number`.

We can also add upper bounds to generic methods as follows:

```java
public static <T extends Number> boolean isZero(T data) {
  return data.equals(0);
}
```

In the example above, it’s important to note that we added the `Number` upper bound before the return type.

Java also allows us to create a type parameter with multiple bounds. Let’s look at an example:


```java
public class Box <T extends Number & Comparable<T>> {
  private T data; 
}
```

In the example above, we specified multiple bounds (`Number` and `Comparable`) for type parameter `T` using the `&` operator between the different upper bounds. It’s important to note that when defining multiple bounds, any upper bound that is a `class` (in our example `Number`) must come first followed by any interfaces (in our example `Comparable<T>`).

Let’s practice adding an upper bound to a generic class.

Example Final:

```java
Teacher.java

public class Teacher extends SchoolPerson {
  private String subject;

  public Teacher(String name, String subject) {
    super(name);
    this.subject = subject;
  }

  public void setSubject(String subject) {
    this.subject = subject;
  }

  public String getSubject() {
    return this.subject;
  }

  public String toString() {
    return "Teacher = (name = "+this.getName()+", subject = "+ this.subject+")";
  }
}
```

```java
Student.java

public class Student extends SchoolPerson {
  private String bestSubject;

  public Student(String name, String bestSubject) {
    super(name);
    this.bestSubject = bestSubject;
  }

  public String getBestSubject() {
    return this.bestSubject;
  }

  public void setSubject(String bestSubject) {
    this.bestSubject = bestSubject;
  }

  public String toString() {
    return "Student = (name = "+this.getName()+", bestSubject = "+ this.bestSubject+")";
  }
}
```

```java
SchoolPerson.java

public class SchoolPerson {
  private String name;

  public SchoolPerson(String name) {
    this.name = name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return this.name;
  }

  public String toString() {
    return "SchoolPerson (name = "+ this.name + ")";
  }
}
```

```java
Bus.java

public class Bus<T extends SchoolPerson> {
  private T rider;

  public Bus(T rider) {
    this.rider = rider;
  }

  public void setRider(T rider) {
    this.rider = rider;
  }

  public T getRider() {
    return this.rider;
  }

  public void printRider() {
    System.out.println(rider.toString());
  }
}
```

```java
Main.java

public class Main {
  public static void main(String[] args) {
    SchoolPerson person = new SchoolPerson("Peter");
    Bus<SchoolPerson> busWPerson = new Bus<>(person);
    busWPerson.printRider();    
  }
}
```

Output:

```terminal
SchoolPerson (name = Peter)
```

