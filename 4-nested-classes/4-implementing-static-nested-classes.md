## Implementing Static Nested Classes

In this exercise, we will explore the concept of static nested classes. A static nested class is a class that belongs to its enclosing class in the same way that a static variable belongs to its enclosing class. Static nested classes are helpful because they allow related classes to be grouped under an enclosing class. To illustrate this concept, we will use a toolbox as an example. A toolbox contains many tools that a person can use such as a hammer, a tape measure, a wrench, and others. We can implement the concept of a toolbox in Java using static nested classes like so:

```java
class Toolbox{  
  public static String toolboxName = "Awesome Toolbox";
  public String ownerName;

  static class Saw{
    public void cut(){
      System.out.println("Cutting...");
    }
  }
    
  static class MeasuringTape{
    public void measure(){
      System.out.println("Measuring...");
    }
  }

  static class Wrench{
    public void tighten(){
      System.out.println("Tightening...");
    }

    public void loosen(){
      System.out.println("Loosening...");
    }
  }
}
```

We can use the “toolbox” like so:

```java
public class Main{
  public static void main(String[] args) {
    Toolbox.Saw petersSaw = new Toolbox.Saw();
    Toolbox.MeasuringTape amysMeasuringTape = new Toolbox.MeasuringTape();
    Toolbox.Wrench randomWrench = new Toolbox.Wrench();

    petersSaw.cut(); // output: Cutting...
    amysMeasuringTape.measure(); // output: Measuring...
    randomWrench.tighten(); // output: Tightening...
}
```

Static nested classes can access static variables of the enclosing class, but cannot access non-static variables because non-static variables belong to an instance of the class and not the class itself. Modifying Saw in Toolbox like so is okay:

```java
static class Saw{
  public void cut(){
    System.out.println("Cutting...");
  }
  public void printName(){
    System.out.println(toolboxName); // When called, this will print "Awsome Toolbox"
  }
}
```

Modifying Saw like this will cause a compiler error:
```java
static class Saw{
  public void cut(){
    System.out.println("Cutting...");
  }
  public void printName(){
    System.out.println(ownerName); // This will not compile!
  }
}
```

Let’s practice creating and using nested classes.

Example final:
```java
class VendingMachine {
  
  static class ChocolateBar {
    public String getName() {
      return "Chocolate Bar Brands!";
    }
    public double getPrice() {
      return 15.89;
    }
  }

  static class BagOfChips {
    public String getName() {
      return "Bag of Chips Brands!";
    }
    public double getPrice() {
      return 8.55;
    }
  }

}

public class Main{
  public static void main(String[] args){
    VendingMachine.ChocolateBar mikesChocolateBar = new VendingMachine.ChocolateBar();
    VendingMachine.BagOfChips gabbysBagOfChips = new VendingMachine.BagOfChips();
    System.out.println("Mike's "+mikesChocolateBar.getName()+" chocolate bar costs "+mikesChocolateBar.getPrice());
    System.out.println("Gabby's "+gabbysBagOfChips.getName()+" bag of chips costs "+gabbysBagOfChips.getPrice());
  }
}
```

Output:
```terminal
Mike's Chocolate Bar Brands! chocolate bar costs 15.89
Gabby's Bag of Chips Brands! bag of chips costs 8.55
```