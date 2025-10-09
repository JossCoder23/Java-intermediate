## Extending the Thread Class

There are multiple ways to implement `threading` in Java. The first that we will try involves extending the `Thread` class. In Java, there is a built-in class that handles threads: `java.lang.Thread`. To create a thread, we create a class that extends the built-in `Thread` class and then overrides its `public void run()` method. Beyond these two requirements, the rest of our class can have anything we want in it!

The `public void run()` method that we override performs the actual work that our thread should be responsible for. This may be performing a long-running computation, calling out to another application or service, or other tasks that involve some waiting.

Notice that the `run()` method is a `void` and accepts no parameters. Every `run()` method must be of this signature. If `run()` requires some external information, that information must be a field declared in the class and initialized in the constructor. However, be very careful of using external information as this may present some synchronization issues.

When we defined our class in this way, we can then create an instance of our class in any other part of our program and call `start()` on the instance to trigger the thread’s execution.

Here’s an example of a sequential program in Java that computes the meaning of life:

```java
public class HugeProblemSolver{

  public HugeProblemSolver(){
    // Required constructor used for passing information to the start() method.
  }

  private static void solveComputation(){
    // Solves random computation
    // Takes anywhere from 1 second to 10 minutes
    System.out.println("The answer is: 42");
  }

  public static void main(String[] args){
    HugeProblemSolver.solveComputation();
    HugeProblemSolver.solveComputation();
  }
}
```

In this program, we will only see the answer to the second question after the first question has been answered. A threaded solution would allow us to start the computations at the same time, and receive the answers as soon as they are available.

Let’s take a look at the threaded approach:

```java
public class HugeProblemSolver extends Thread{

  public HugeProblemSolver(){
    // Required constructor used for passing information to the start() method.
  }

  private static void solveComputation(){
    // Solves random computation
    // Takes anywhere from 1 second to 10 minutes
  }

  @Override
  public void run(){
    solveComputation();
    System.out.println("The answer is: 42");
  }

  public static void main(String[] args){
    HugeProblemSolver m1 = new HugeProblemSolver();
    HugeProblemSolver m2 = new HugeProblemSolver();
    m1.start();
    m2.start();
  }
}
```

Now, you can see that all that changed was:

* Extended the `Thread` Class.
* Created and Overrode the `run()` method from `Thread`.
* Instantiated `HugeProblemSolver` and called `start()` which starts a new thread and searches in the class for the `run()` method to execute.

Now, both `Thread`s we created are working on solving their own problems simultaneously. Whichever one finishes first will print to the console first. There is no need to wait on sequential order.

Let’s see how we can implement this in our `CrystalBall` class.

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
import java.lang.Thread;

public class CrystalBall extends Thread {

  private Question question;

  public CrystalBall(Question question) {
    this.question = question;
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

  private void think(Question question) {
    System.out.println("Hmm... Thinking");
    try {
      Thread.sleep(this.getSleepTimeInMs(question.getDifficulty()));
    } catch (Exception e) {
      System.out.println(e);
    }
    System.out.println("Done!");
  }

  public void ask(Question question) {
    System.out.println("Good question! You asked: " + question.getQuestion());
    this.think(question);
    System.out.println("Answer: " + this.answer());
  }

  @Override
  public void run() {
    this.ask(this.question);
  }

}
```

```java
FortuneTeller.java

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

    questions.stream().forEach(q -> {
      CrystalBall c = new CrystalBall(q);
      // c.ask(q);
      c.start();
    });
    
  }
}
```