## Collections Introduction

In Java, we often need to write programs that work with groups (or collections) of objects. Recall that an array is an object that holds multiple objects of the same type (also known as its elements) but is limited by its fixed size and functionality. Java provides a Collections Framework to help overcome the limits of an array and provide more complex functionality to meet different collection needs.

The `collections` framework provides data structures (through `interfaces` and implementing classes) and algorithms, which perform common tasks on collections. The collections framework allows us to focus on the important parts of our program and not on low-level implementation details (like needing to implement a dynamic sizing collection).

The collections framework provides a hierarchical relationship between its interfaces, making the various implementations compatible with each other and thus making our code scalable and flexible. All the interfaces in the collections framework are generic, which allows us to use optimized and tested “plumbing” for our specific `data types`.

As we go through the lesson, we will explore the collections framework interfaces and implementations, their relationship to `generics`, and the operations we can perform.