## Shadowing

Now let’s take a look at the concept of shadowing in Java. Shadowing allows for overlapping scopes of members with the same name and type to exist in both a nested class and the enclosing class simultaneously. The value of the variable will depend on which object we use to call it.

Take a look at the example below:

```java
class Outer {
  String name = "string_1";

  // Nested inner class
  class Inner {
    String name = "string_2";

    public void printTypeMethod() {
      System.out.println(name);
      System.out.println(Outer.this.name);
    }
  }
}

class Main {
  // Main driver method
  public static void main(String[] args) {
    Outer outerObj = new Outer();
    Outer.Inner innerObj  = outerObj.new Inner();
    innerObj.printTypeMethod();
  }
}
```

The code above will output the following:
```terminal
string_2
string_1
```

If we take a closer look at the method `printTypeMethod()`, the keyword `this` is used in the second print statement. Using the keyword `this` along with the class name `Outer`, allows us to overlap the variable `name` with the contents of the outer class.

Example Final:
```java
class Book {
  
  String type = "Nonfiction";
	
  // Nested inner class
	class Biography {
    String type = "Biography";

    public void print() {
      System.out.println(type);
      System.out.println(Book.this.type);
    }
	}

}

public class Books {
	public static void main(String[] args) {
		Book book = new Book();
		Book.Biography bio = book.new Biography();
		bio.print();
	}
}
```

Output:
```terminal
Biography
Nonfiction
```