## Supervising a Thread

So far, you have seen how to start threads with the `start()` method and learned multiple ways to implement threads into sequential programs.

Sometimes, we want to be able to see the status of threads during their execution. In Java, the best pattern for doing so is to use a supervisor thread. This is a pattern where the main thread (or another thread) is able to watch and check on the progress of another thread, as long as it has access to the corresponding `Thread` instance. This kind of thread is implemented just like other threads. Supervisor threads are often used for updating the user of our program on the progress of an ongoing task.

One `Thread` method that a supervisor thread may use to monitor another thread is `isAlive()`. This method returns `true` if the thread is still running, and `false` if it has terminated. A supervisor might continuously poll this value (check it at a fixed interval) until it changes, and then notify the user that the thread has changed state. Here is an example:

```java
import java.time.Instant;
import java.time.Duration;
 
public class Factorial{
 public int compute(int n){
   // the existing method to compute factorials
 }
 
 // utility method to create a supervisor thread
 public static Thread createSupervisor(Thread t){
   Thread supervisor = new Thread(() -> {
     Instant startTime = Instant.now();
     // supervisor is polling for t's status
     while (t.isAlive()) {
       System.out.println(Thread.currentThread().getName() + " - Computation still running...");
       Thread.sleep(1000);
     }
   });
 
   // setting a custom name for the supervisor thread
   supervisor.setName("supervisor");
   return supervisor;
 
 }
 
 public static void main(String[] args){
   Factorial f = new Factorial();
 
   Thread t1 = new Thread(() -> {
     System.out.println("25 factorial is...");
     System.out.println(f.compute(25));
   });
 
 
   Thread supervisor = createSupervisor(t1);
 
   t1.start();
   supervisor.start();
 
   System.out.println("Supervisor " + supervisor.getName() + " watching worker " + t1.getName());
 }
}
```

The thread labeled `supervisor` here is polling the status of `t1` (a “worker” thread) continuously at an interval of 1000 milliseconds (one second). The supervisor checks the status of `t1` using the `isAlive()` method in a `while` loop.

Additionally, the `getName()` method will return a unique name for a thread in the current context. This comes in handy when debugging multi-threaded programs: the programmer can better understand which thread is performing a certain task at a given moment. We can also name a thread ourselves, using the `setName()` method of the `Thread` class.

Now, let’s create a supervisor thread that polls for the status of all of the running `CrystalBall` threads.

Example Final:
```java
CrystalBall.java

import java.util.Random;

public class CrystalBall {

  /* Instance Methods */
  public void ask(Question question) {
    System.out.println(Thread.currentThread().getName() + " - Good question! You asked: " + question.getQuestion());
    this.think(question);
    System.out.println(Thread.currentThread().getName() + " - Answer: " + this.answer());
  }

  private void think(Question question) {
    System.out.println(Thread.currentThread().getName() + " - Hmm... Thinking");
    try {
      Thread.sleep(this.getSleepTimeInMs(question.getDifficulty()));
    } catch (Exception e) {
      System.out.println(e);
    }
    System.out.println(Thread.currentThread().getName() + " - Done!");
  }

  private String answer() {
    String[] answers = {
        "Signs point to yes!",
        "Certainly!",
        "No opinion",
        "Answer is a little cloudy. Try again.",
        "Surely.",
        "No.",
        "Signs point to no.",
        "It could very well be!"
    };
    return answers[new Random().nextInt(answers.length)];
  }

  private int getSleepTimeInMs(Question.Difficulty difficulty) {
    switch (difficulty) {
      case EASY:
        return 1000;
      case MEDIUM:
        return 2000;
      case HARD:
        return 3000;
      default:
        return 500;
    }
  }
}
```

```java
FortuneTeller.java

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FortuneTeller {
  
  public static void main(String[] args) {

    List<Question> questions = Arrays.asList(
        new Question(Question.Difficulty.EASY, "Am I a good coder?"),
        new Question(Question.Difficulty.MEDIUM, "Will I be able to finish this course?"),
        new Question(Question.Difficulty.EASY, "Will it rain tomorrow?"),
        new Question(Question.Difficulty.EASY, "Will it snow today?"),
        new Question(Question.Difficulty.HARD, "Are you really all-knowing?"),
        new Question(Question.Difficulty.HARD, "Do I have any hidden talents?"),
        new Question(Question.Difficulty.HARD, "Will I live to be greater than 100 years old?"),
        new Question(Question.Difficulty.MEDIUM, "Will I be rich one day?"),
        new Question(Question.Difficulty.MEDIUM, "Should I clean my room?")
    );

    CrystalBall c = new CrystalBall();

    List<Thread> threads = questions.stream().map(q -> {
      Thread t = new Thread(() -> {
        c.ask(q);
      });
      return t;
    }).collect(Collectors.toList());
    Thread supervisor = createSupervisor(threads);

    threads.stream().forEach(t -> t.start());
    supervisor.start();
  }

  public static Thread createSupervisor(List<Thread> threads) {

    Thread supervisor = new Thread(() -> {
      while (true) {
        List<String> runningThreads = threads.stream().filter(t -> t.isAlive()).map(t -> t.getName()).collect(Collectors.toList());
        System.out.println(Thread.currentThread().getName() + " - Currently running threads: " + runningThreads);
        if (runningThreads.isEmpty()) {
          break;
        }
        try {
          Thread.sleep(1000);
        } catch (InterruptedException e) {
          System.out.println(e);
        }
      }
      System.out.println(Thread.currentThread().getName() + " - All threads completed!");
    });

    // Set the name here...
    supervisor.setName("Supervisor");

    return supervisor;
  };
}
```