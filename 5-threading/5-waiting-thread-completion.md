## Waiting for Thread Completion

Another common scenario in multi-threaded programs is to wait for a thread to complete before proceeding in a path of execution.

In other languages, this concept is called “awaiting” or “blocking”. In Java, we say that we wait for the thread to join.

When a thread joins, it means that the thread’s task is complete and the process that was initially forked off has been “joined” back into the main thread.

This is useful when we can only perform a specific task once several prerequisite tasks have been completed. Take a look at BurgerMaker.java in the editor, which describes the process of preparing a cheeseburger. A cheeseburger is generally prepared in the following way:

1. Grill hamburger patty.
2. Once the patty is properly cooked, add cheese on top to melt it.
3. Toast the burger buns.
4. Fry onions.
5. Once all ingredients are ready, assemble the burger.

Many of these steps can be done concurrently. However, notice that some of the steps are dependent on the completion of other steps. Step 2 requires the patty to be grilled before melting cheese on top of it. Step 5 requires all other steps to be completed before it can start (we can’t assemble a burger until everything is ready).

In `BurgerMaker`, we can see how `join()` is used to enforce dependencies between different tasks. By using `start()` and `join()` properly, we can ensure that tasks that can be performed concurrently are started. Still, tasks with dependencies are not started until all dependencies have been joined.

In this exercise, we’ll use the `join()` features we see in BurgerMaker.java to ensure that tasks occur in the correct order while making a cake in our new file, CakeMaker.java. `CakeMaker` describes baking a cake by following these steps: A cake is made in the following way:

1. The oven must be preheated before the cake can be baked.
2. The dry ingredients and wet ingredients should be mixed before the ingredients can be combined.
3. The ingredients must be combined before the cake can be baked.
4. The cake must be finished baking before the cake can be frosted.

Example final:
```java
CakeMaker.java

public class CakeMaker {

    /* Instance Variables */
    private boolean whiskInUse = false;
    private boolean ovenInUse = false;
    private boolean mixingBowlInUse = false;

    /* Main Method */
    public static void main(String[] args) {

        CakeMaker c = new CakeMaker();
        try {

            Thread preheatOven = new Thread(() -> c.preheatOven(), "preheatOven");
            Thread mixDryIngredients = new Thread(() -> c.mixDryIngredients(), "mixDryIngredients");
            Thread mixWetIngredients = new Thread(() -> c.mixWetIngredients(), "mixWetIngredients");
            Thread combineIngredients = new Thread(() -> c.combineIngredients(), "combineIngredients");
            Thread bakeCake = new Thread(() -> c.bakeCake(), "bakeCake");
            Thread makeFrosting = new Thread(() -> c.makeFrosting(), "makeFrosting");
            Thread frostCake = new Thread(() -> c.frostCake(), "frostCake");

            // Add logic to start and initial.join threads here!
            // There should be a .start() and .initial.join() method call for each thread, seven in total.

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
            mixingBowlInUse = true;
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
            mixingBowlInUse = false;
            printTask("Done!");
        } catch (InterruptedException e) {
            System.out.println(e);
        }
    };

    public void mixWetIngredients() {
        try {
            printTask("Mixing wet ingredients...");
            mixingBowlInUse = true;
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
            mixingBowlInUse = false;
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
    };
}
```

```java
import java.lang.Thread;
public class BurgerMaker {
 
 public void toastBuns() {
   try {
     System.out.println("Toasting buns...");
     Thread.sleep(2000);
   } catch (InterruptedException e) {
     System.out.println(e);
   }
 }

 public void grillPatty() {
   System.out.println("Grilling patty...");
   Thread.sleep(1500);
 }

 public void meltCheese() {
   System.out.println("Melting cheese...");
   Thread.sleep(800);
 }

 public void fryOnions() {
   System.out.println("Frying onions...");
   Thread.sleep(1000);
 }

 public void assembleBurger() {
   System.out.println("Assembling burger...");
   Thread.sleep(1500);
 }

 public static void main(String[] args) {
   BurgerMaker burgerMaker = new BurgerMaker();
   Thread t1 = new Thread(() -> burgerMaker.toastBuns());
   Thread t2 = new Thread(() -> burgerMaker.grillPatty());
   Thread t3 = new Thread(() -> burgerMaker.meltCheese());
   Thread t4 = new Thread(() -> burgerMaker.fryOnions());
   Thread t5 = new Thread(() -> burgerMaker.assembleBurger());
 
   t1.start();
   t2.start();
   t4.start();
   t2.join(); // must grill patty before melting cheese on it
   t3.start(); // ready to melt cheese
   t1.join();
   t3.join();
   t4.join();
   // must complete all other steps before assembling burger
   t5.start();
   t5.join(); // waiting for the burger assembly task to complete
   System.out.println("Burger complete!");
 }
 
}

```