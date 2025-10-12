## Implementing the Runnable Interface

In the previous exercise, you learned that we can convert a class to run as a thread by extending the `Thread` class. We can also create threaded `classes` in Java by implementing the `Runnable` interface.

This approach is preferred because we are only allowed to extend one class, and wasting it on `Thread` might not be beneficial to our program. Here, rather than extending the capability of the built-in `Thread` class, we just want to use its threading capability. Because of this, implementing the Runnable interface (which is what the `Thread` class does anyway) and passing in the object into a new `Thread` object is the preferred way of implementing multithreading. Here’s an example of how we would implement a `Factorial` thread by implementing `Runnable` instead of extending `Thread`:

```java
public class Factorial implements Runnable {
 private int n;
 
 public Factorial(int n) {
   this.n = n;
 }
 
 public int compute(int n) {
   // ... the code to compute factorials
 }
 
 public void run() {
   System.out.print("Factorial of " + String.valueOf(this.n) + ":")
   System.out.println(this.compute(this.n));
 }
 
 public static void main(String[] args) {
   Factorial f = new Factorial(25);
   Factorial g = new Factorial(10);
   Thread t1 = new Thread(f);
   Thread t2 = new Thread(f);
   t1.start();
   t2.start();
 }
}
```

A more succinct way of using the `Runnable` interface is to use lambda expressions. This is a more modern syntax that allows us to define the `run()` method we want to use inline without requiring the class to implement `Runnable` or extend `Thread`. For the above example, the syntax looks like this:

```java
public class Factorial {
 public int compute(int n) {
   // ... the code to compute factorials
 }
 
 public static void main(String[] args) {
   Factorial f = new Factorial();
 
   // the lambda function replacing the run method
   new Thread(() -> {
     System.out.println(f.compute(25));
   }).start();
 
   // the lambda function replacing the run method
   new Thread(() -> {
     System.out.println(f.compute(10));
   }).start();
 }
}
```

Behind the scenes, this syntax is still using the `Runnable` interface. This is because Java will translate this lambda syntax into something like this:

```java
new Thread(new Runnable() {
 void run() {
   System.out.println(f.compute(25));
 }
}).start();
```

Using the lambda expression syntax for starting threads, we can create a threaded version of our class in only a few lines!

This syntax has several benefits:

* Our class no longer needs to extend `Thread` OR implement `Runnable`. We can make a thread from anything!
* Our class no longer needs a constructor to store arguments! Since we can pass an argument directly into the compute function when we create our thread, we no longer need to create a separate instance of our object any time we want to perform a threaded task with it.
* Our class is easier to read! The lambda syntax makes it so that people reading our code can immediately identify what task is being performed in our thread without having to read our class first to find the `run()` method.

Now, let’s try both of these `methods` of implementing `Runnable` with our `FortuneTeller` class.

Note: Sometimes you will see developers specifically import the Thread and Runnable classes from `java.lang`. This is not necessary since all Java programs naturally import the `java.lang` package anyway. It is often used to help with readability or remind an author to add a specific feature.

Example final:

```java
Question.java

public class Question {

    enum Difficulty {
        EASY, MEDIUM, HARD;
    }

    private String question;
    private Difficulty difficulty;

    public Question(Difficulty difficulty, String question) {
        this.difficulty = difficulty;
        this.question = question;
    }

    public Difficulty getDifficulty() {
        return this.difficulty;
    }

    public String getQuestion() {
        return this.question;
    }
}
```

```java
CrystalBall.java

import java.util.Random;

public class CrystalBall{

  /* Instance Variables */

  /* Constructors */

  /* Instance Methods */
  

  public void ask(Question question) {
    System.out.println("Good question! You asked: " + question.getQuestion());
    this.think(question);
    System.out.println("Answer: " + this.answer());
  }

  private void think(Question question) {
    System.out.println("Hmm... Thinking");
    try {
      Thread.sleep(this.getSleepTimeInMs(question.getDifficulty()));
    } catch (Exception e) {
      System.out.println(e);
    }
    System.out.println("Done!");
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
FortunneTeller.java

import java.util.Arrays;
import java.util.List;

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
    questions.stream().forEach(q -> {
      new Thread(() -> {
        c.ask(q);
      }).start();
      
      // CrystalBall c = new CrystalBall();
      // Thread t = new Thread(c);
      // t.start();
    });
  }
}
```