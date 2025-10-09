## Introduction

So far, we have learned about threads and how they work in theory. Before we put it into practice, we should have a strong understanding of what kinds of problems multi-threaded programs are best suited to solve.

Threading can solve problems where there is a lot of waiting to be done. When one task is in a “waiting” or “blocked” state, another one can start. This is useful for programs in which a long-running computation needs to be done, or when a task must wait on a response from an external source such as fetching an image from a server.

In the following exercise, you’ll see how a program could be forced to “wait” for a task’s completion. As you complete it, start thinking about what tasks could be performed in threads, concurrently, to save some time.

Example Final:
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

import java.lang.Thread;
import java.util.Random;

public class CrystalBall {

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
      CrystalBall c = new CrystalBall();
      c.ask(q);
    });
  }
}
```
