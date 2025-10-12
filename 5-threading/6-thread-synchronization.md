## Thread Synchronization

Another important scenario when working with multi-threaded programs is managing shared resources between threads.

When we access the same data from two different threads, we may cause a race condition. A race condition occurs when some inconsistency is caused by two threads trying to access the same shared data at the same time. Consider this example where two threads are attempting to increment a value simultaneously:

```java
class IntegerMapper{
  public int[] array = {1, 2, 3, 4, 5};    
  public void incrementElement(int i, int j){
    array[i] += j;
  }   
}
public class Main{
  public static void main(String args[]) throws InterruptedException{
    IntegerMapper iMapper = new IntegerMapper();
    Thread thread1 = new Thread(() -> {
      for(int i = 0; i < 100; i++){
        iMapper.incrementElement(2, 4);
        try{
          Thread.sleep(10);
        }
        catch(InterruptedException exception){
          System.out.println("Error!");
        }
      }
            
    });
    Thread thread2 = new Thread(() -> {
      for(int i = 0; i < 100; i++){
        iMapper.incrementElement(2, 3);
        try{
          Thread.sleep(10);
        }
        catch(InterruptedException exception){
          System.out.println("Error!");
        }
      }
    });
        
    thread1.start();
    thread2.start();
        
    thread1.join();
    thread2.join();
        
    System.out.println(iMapper.array[2]);
  }
}
```

If we run this program multiple times, we will get a different output each time! This is because thread1 and thread2 conflict in their access of array[2]. To update the value in the incrementElement() method, the value must be read, incremented, then saved. One thread could be reading the value while the other thread is incrementing it, leading to inconsistencies.

We can prevent race conditions on shared data by using the synchronized keyword in Java. In a threaded program, when we add synchronized to the definition of a function, it will ensure that for a given instance of a class, only one thread can run that method at a time. We can fix incrementElement() by making it synchronized like so:

```java
public synchronized void incrementElement(int i, int j){
    array[i] += j;
}
```

Now, each time the program is run, it will output the same value.

Let’s see how we can use thread synchronization to solve a classic race condition problem.

Example final:
```java
public class Counter {
  private int c = 0;

  public int getCount() {
    return this.c;
  };

  public void setCount(int c) {
    this.c = c;
  };

  public synchronized void increment() {
    this.setCount(this.getCount() + 1);
  }

  public static void main(String[] args) throws InterruptedException {
    Counter c = new Counter();

    Thread a = new Thread(() -> {
      for (int i = 0; i < 100; i++) {
        c.increment();
        try {
          Thread.sleep(10);
        } catch (InterruptedException e) {
          System.out.println(e);
        }
      }
    });

    Thread b = new Thread(() -> {
      for (int i = 0; i < 100; i++) {
        c.increment();
        try {
          Thread.sleep(10);
        } catch (InterruptedException e) {
          System.out.println(e);
        }
      }
    });

    // Start both threads here
    a.start();
    b.start();

    // Join both threads here
    a.join();
    b.join();

    System.out.println("Counter: " + c.getCount());
  }
}
```