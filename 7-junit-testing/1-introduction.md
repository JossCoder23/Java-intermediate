## Introduction to JUnit

JUnit testing operates in a Test Driven Development setting, or TDD, usually utilized specifically in “test-first” programming. Java programming as a whole is often synonymous with TDD due to the incorporation of JUnit.

As you learn more about what JUnit is and how it works, you’ll pick up a particular mantra along the way:

“Red — Green — Refactor!”

This is the leading chant for test-first practices, and you’ll be chanting it too before this lesson is over! While you think about what that might mean, let’s talk about JUnit.

JUnit is a unit testing framework for Java that tests the functionality of an application to ensure it runs as expected. The “units” being tested are single entities, like classes and methods.

Programmers write JUnit tests for quality reasons, but they also do so to reduce stress and the time spent debugging code. Proper testing practices can not only keep code organized and maintain a solid direction, but it also ensures maintainability in the future and is friendly to a team-based setting.

These “tests” might be hard to wrap your head around at first but think of them as additional classes that are created to “build and test” elements of an application’s Java classes.

For instance, say you have a Java class called `Human` with stored values for `health`, `thirst`, and `hunger` upon instantiation. To make sure a `Human` is properly storing their values, a JUnit test might create a `Human` object with those values filled, then check to see if they were properly stored. It can also manipulate those values and check if those changes are reflected.

In this lesson, we will learn about JUnit 4 testing.