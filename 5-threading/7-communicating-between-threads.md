## Communicating Between Threads

Previously, we learned how to block thread execution using `join()`. However, this is only to block thread execution from the context where the thread was started. For example, if a thread was created and started in the main thread, we can only call `join()` on it from the main thread and wait on its completion from there.

In Java, to control thread execution from within other threads, we can use the `wait()`, `notify()`, and `notifyAll()` methods. These are primarily used to protect shared resources from being used by two threads at the same time or to wait until some condition has changed in a thread.

When using `wait()` and `notifyAll()`, it is important to do so in a `synchronized(this)` block. When we create a `synchronized(this)` block, we are telling Java that we want it to be the only thread accessing the fields of the class at a given moment. In the `synchronized(this)` block, we must:

1. Check the condition on which to wait.
2. Decide whether to `wait()` (block the execution of the current thread) or `notifyAll()` (allow other threads to check their condition again and proceed)

```java
import java.lang.Thread;
 
public class OrderDinnerProcess {
 private boolean foodArrived = false;
 
 private void printTask(String task) { 
   System.out.println(Thread.currentThread().getName() + " - " + task);
 }
 
 public void eatFood() {
   printTask("Wow, I am starving!");
   try {
     synchronized (this) {
       while (!this.foodArrived) {
         printTask("Waiting for the food to arrive...");
         wait();
       }
     }
   } catch (InterruptedException e) {
     System.out.println(e);
   }
   printTask("Finally! Yum yum yum!!!");
 }
 
 public void deliverFood() {
   printTask("Driving food over...");
   try {
     Thread.sleep(5000);
     synchronized (this) {
       this.foodArrived = true;
       printTask("Arrived!");
       notifyAll();
     }
   } catch (InterruptedException e) {
     System.out.println(e);
   }
 }
 
 public static void main(String[] args) {
   OrderDinnerProcess p = new OrderDinnerProcess();
   try {
     for (int i = 0; i < 5; i++) {
       Thread eatFood = new Thread(() -> p.eatFood());
       eatFood.start();
     }
     Thread.sleep(1000);
     Thread delivery = new Thread(() -> p.deliverFood());
     delivery.start();
   } catch (InterruptedException e) {
     System.out.println(e);
   }
 }
}
```

In the example, we are simulating a family of five eager to eat some dinner! However, they can’t eat until the food has arrived. We could have controlled this behavior before by defining, starting, and joining the `delivery` thread before the five `eatFood()` threads began. However, using `wait()` and `notifyAll()`, we can start them in any order, and each `eatFood()` thread will `wait()` until a call to `notifyAll()` by another thread tells them to proceed to check again.

The `synchronized` block is used here to tell Java that only one thread should be able to read from and write to the `foodArrived()` field at a time.

The `wait()` function is used to pause execution for a thread until a call has been made to `notifyAll()`, which triggers another check of the condition.

The `notifyAll()` function is used to tell all threads that are currently waiting that they may now proceed.

In addition to being used to coordinate thread execution, we can use the `synchronized(this)` block, `wait()`, and `notifyAll()` to control access to shared resources. If a resource is currently in use, a thread should `wait(`) until a call to `notifyAll()` is made, which indicates that the shared resource may have been released and is ready for use.

In this exercise, you’ll use the `synchronized(this)` block, `wait()`, and `notifyAll()` to update our `CakeMaker` class so that only one thread can use the mixing bowl at a given time. The other threads must `wait()` until the mixing bowl is released, and are instructed to continue with execution with a call to `notifyAll()`.


Example final:

```java
public class CakeMaker {

  /* Instance Variables */
  private boolean whiskInUse = false;
  private boolean ovenInUse = false;
  private boolean mixingBowlInUse = false;

  /* Main Method */
  public static void main(String[] args) {

    CakeMaker c = new CakeMaker();
    try {

      Thread preheatOven = new Thread(c::preheatOven, "preheatOven");
      Thread mixDryIngredients = new Thread(c::mixDryIngredients, "mixDryIngredients");
      Thread mixWetIngredients = new Thread(c::mixWetIngredients, "mixWetIngredients");
      Thread combineIngredients = new Thread(c::combineIngredients, "combineIngredients");
      Thread bakeCake = new Thread(c::bakeCake, "bakeCake");
      Thread makeFrosting = new Thread(c::makeFrosting, "makeFrosting");
      Thread frostCake = new Thread(c::frostCake, "frostCake");

      preheatOven.start();
      mixDryIngredients.start();
      mixWetIngredients.start();
      makeFrosting.start();
      mixDryIngredients.join();
      mixWetIngredients.join();
      combineIngredients.start();
      combineIngredients.join();
      preheatOven.join();
      bakeCake.start();
      makeFrosting.join();
      bakeCake.join();
      frostCake.start();
      frostCake.join();

      System.out.println("Cake complete!");
    } catch (Exception e) {
      System.out.println(e);
    }
  } // End of Main

  /* Instance Methods */
  public void preheatOven() {
    try {
      printTask("Oven pre-heating...");
      ovenInUse = true;
      Thread.sleep(10000);
      ovenInUse = false;
      printTask("Done!");
    } catch (InterruptedException e) {
      System.out.println(e);
    }
  }

  public void mixDryIngredients() {
    try {
      printTask("Mixing dry ingredients...");
      synchronized(this) {
        while(mixingBowlInUse) {
          printTask("Waiting for the mixing bowl...");
          wait();
        }
        mixingBowlInUse = true;
        printTask("Using mixing bowl!");
      }
      Thread.sleep(200);
      printTask("Adding cake flour");
      Thread.sleep(200);
      printTask("Adding salt");
      Thread.sleep(200);
      printTask("Adding baking powder");
      Thread.sleep(200);
      printTask("Adding baking soda");
      Thread.sleep(200);
      whiskInUse = true;
      printTask("Mixing...");
      Thread.sleep(200);
      whiskInUse = false;
      synchronized(this) {
        printTask("Releasing mixing bowl!");
        mixingBowlInUse = false;
        notifyAll();
      }
      printTask("Done!");
    } catch (InterruptedException e) {
      System.out.println(e);
    }
  };

  public void mixWetIngredients() {
    try {
      printTask("Mixing wet ingredients...");
      synchronized(this) {
        while(mixingBowlInUse) {
          printTask("Waiting for mixing bowl...");
          wait();
        }
        printTask("Using mixing bowl!");
        mixingBowlInUse = true;
      };
      Thread.sleep(1000);
      printTask("Adding butter...");
      Thread.sleep(500);
      printTask("Adding eggs...");
      Thread.sleep(500);
      printTask("Adding vanilla extract...");
      Thread.sleep(500);
      printTask("Adding buttermilk...");
      Thread.sleep(500);
      whiskInUse = true;
      printTask("Mixing...");
      Thread.sleep(1500);
      whiskInUse = false;
      synchronized(this) {
        printTask("Releasing mixing bowl!");
        mixingBowlInUse = false;
        notifyAll();
      }
      printTask("Done!");
    } catch (InterruptedException e) {
      System.out.println(e);
    }
  };

  public void combineIngredients() {
    try {
      printTask("Combining ingredients...");
      mixingBowlInUse = true;
      Thread.sleep(1000);
      printTask("Adding dry mix to wet mix...");
      Thread.sleep(1500);
      whiskInUse = true;
      printTask("Mixing...");
      Thread.sleep(1500);
      whiskInUse = false;
      mixingBowlInUse = false;
      printTask("Done!");
    } catch (InterruptedException e) {
      System.out.println(e);
    }
  };

  public void bakeCake() {
    try {
      printTask("Baking cake...");
      ovenInUse = true;
      Thread.sleep(10000);
      ovenInUse = false;
      printTask("Done!");
    } catch (InterruptedException e) {
      System.out.println(e);
    }
  }

  public void makeFrosting() {
    try {
      printTask("Making frosting...");
      whiskInUse = true;
      mixingBowlInUse = true;
      printTask("Adding butter...");
      Thread.sleep(200);
      printTask("Adding milk...");
      Thread.sleep(200);
      printTask("Adding sugar...");
      Thread.sleep(200);
      printTask("Adding vanilla extract...");
      Thread.sleep(200);
      printTask("Adding salt...");
      Thread.sleep(200);
      whiskInUse = false;
      mixingBowlInUse = false;
      printTask("Done!");

    } catch (InterruptedException e) {
      System.out.println(e);
    }
  }

  public void frostCake() {
    try {
      printTask("Frosting cake...");
      Thread.sleep(1500);
      printTask("Done!");

    } catch (InterruptedException e) {
      System.out.println(e);
    }
  }

  private void printTask(String task) {
    System.out.println(Thread.currentThread().getName() + " " + " - " + task);
  }
} 
```