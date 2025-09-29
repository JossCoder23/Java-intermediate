## Wildcard Lower Bounds

Recall that generic code can have an upper bound when defined using a type parameter or a wildcard. We can also provide a lower bound when working with wildcards. A lower bound wildcard restricts the wildcard to a class or interface and any of its parent types. For example:

```java
public class Util {
  public static void getBag(Bag<? super Integer> bag) {
    return bag;
  }
}
```

In the example above, we used the `super` keyword to restrict the argument to `getBag()` to be a `Bag` of `Integer`, `Number`, or `Object`. If a call to `getBag()` with `Bag<Double>` is made, it would result in an error because `Double` is not an `Integer` or one of its parents.

Some important things to note about lower bounds are:

* They cannot be used with generic type parameters, only wildcards.
* A wildcard cannot have both a lower bound and an upper bound. In this case, it’s best to use a generic type parameter.

There are some general guidelines provided by Java as to when to use what type of wildcard:

* An upper bound wildcard should be used when the variable is being used to serve some type of data to our code.
* A lower bound wildcard should be used when the variable is receiving data and holding it for later use.
* When a variable that serves data is used and only uses `Object` methods, an unbounded wildcard is preferred.
* When a variable needs to serve data and store data for later use, a wildcard should not be used (use a type parameter instead).

Let’s practice adding a lower bound to a generic method.

Example final:

```java
Bus.java

public class Bus<T> {
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
Main.java

public class Main {
  public static void main(String[] args) {
    Bus<Student> studentBus = new Bus<>(new Student("Mike", "Math"));
    Bus<SchoolPerson> personBus = new Bus<>(new SchoolPerson("Jerry"));

    transferData(studentBus, personBus);
  }

  public static void transferData(Bus<? extends Student> src, Bus<? super SchoolPerson> dsc) {
    System.out.print("dsc bus rider before switch: ");
    dsc.printRider();
    Student studentInSrcBus = src.getRider();
    System.out.print("dsc bus rider after switch: ");
    dsc.setRider(studentInSrcBus);
    dsc.printRider();
  }
}
```

Output:
```terminal
dsc bus rider before switch: SchoolPerson (name = Jerry)
dsc bus rider after switch: Student = (name = Mike, bestSubject = Math)
```