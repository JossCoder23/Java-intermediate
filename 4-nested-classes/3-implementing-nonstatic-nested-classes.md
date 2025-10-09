## Implementing Non-Static Nested Classes

Now that we’ve reviewed the main differences between non-static nested and static nested classes, let’s break down how to implement the use of a non-static nested class. For more clarity, from here on, we may refer to the non-static nested class as the inner class and the class that it is encapsulated within as the outer class.

To declare a non-static nested class within an outer class, you may use the following code:

```java
class Outer {
  String outer;
  // Assign values using constructor
  public Outer(String name) {
    this.outer = name;
  }

  // private method
  private String getName() {
    return this.outer;
  }
    
  // Non-static nested class
  class Inner {
    String inner;
    String outer;
  }
}
```

Notice how the Inner class does not have the keyword static preceding it. It is also important that we review what the keyword this means in Java code. this is a keyword that a class uses to reference itself.

To instantiate a non-static nested class that can access other members of the outer class, first, we need to instantiate an object of the outer class:

```java
Outer outer = new Outer();
```

Next, we can instantiate an inner class object:

```java
Outer.Inner inner = outer.new Inner();
```

Note that we use the outer object along with the keyword new to create an instance of the inner class.

This step shows us an example of how a non-static class can access other static and non-static classes from the outer class. In the code below, take a look at a modified version of the Inner class from our previous example:

```java
// Non-static nested class
class Inner {
  String inner;
  String outer; 
  public String getOuter() {
  // Instantiate outer class to use its method
  outer = Outer.this.getName();
}
```

Example final:
```java
class Lib {
  String objType;
  String objName;

  // Assign values using constructor
  public Lib(String type, String name) {
    this.objType = type;
    this.objName = name;
  }

  // private method
  private String getObjName() {
    return this.objName;
  }

  // Inner class
  class Book {
    String description;

    void setDescription() {
      if(Lib.this.objType.equals("book")) {
        if(Lib.this.getObjName().equals("nonfiction")) {
          this.description = "Factual stories/accounts based on true events.";
        } else {
          this.description = "Literature that is imaginary.";
        }
      } else {
        this.description = "Not a book!";
        }
    }
    String getDescription() {
      return this.description;
    }
  }
}

public class Main {
  public static void main(String[] args) {

    Lib fiction = new Lib("book", "fiction");
    Lib.Book bookFiction = fiction.new Book();
    bookFiction.setDescription();
    System.out.println("Fiction Book Description = " + bookFiction.getDescription());

    Lib nonFiction = new Lib("book", "nonfiction");
    Lib.Book bookNonFiction = nonFiction.new Book();
    bookNonFiction.setDescription();
    System.out.println("Non-fiction Book Description = " + bookNonFiction.getDescription());

  }
}
```

Output:
```terminal
Fiction Book Description = Literature that is imaginary.
Non-fiction Book Description = Factual stories/accounts based on true events.
```