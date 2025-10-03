## Queue

The `Queue` core interface in the `collections` framework is a collection that implements the Queue data structure. A `Queue` is a First In First Out (FIFO) data structure in which elements are inserted at the tail (back) of the collection and removed from the head (front). Think of it like a line (queue) of people waiting to make a purchase: the first people that arrive on the line (queue) will be the first ones to be able to make a purchase.

A `Queue` has two types of access `methods` for inserting, removing, and getting (but not removing) the element at the head of the `Queue`.

The following methods throw an exception when:

* `add()` - there is no space for the element
* `remove()` - there are no elements to remove
* `element()` - there are no elements to get

The following methods `return` a special value:

* `offer()` - `false` there is no space for the element
* `poll()` - `null` there are no elements to remove
* `peek()` - `null` there are no elements to get

The methods that return a special value should be used when working with a statically sized `Queue` and the exception throwing methods when using a dynamic `Queue`.

Like the other collections framework `interfaces`, `Queue` has many implementations. We’ll focus on `LinkedList` and `PriorityQueue`. We’ve seen `LinkedList` be used as a `List` implementation, but it’s also perfect when needing a basic `Queue` implementation. Being able to use a `LinkedList` as both a `List` and a `Queue` is a perfect example of the compatibility within the collections framework. The `PriorityQueue` ensures the top element is the smallest relative to the data type’s natural ordering (or some custom ordering policy you provide).

Let’s look at an example of `Queue` with a `LinkedList` implementation:

```java
Queue<String> stringQueue = new LinkedList<>();
stringQueue.add("Mike"); // true - state of queue -> "Mike"
stringQueue.offer("Jeff"); // true - state of queue -> "Mike", "Jeff" 

String a = stringQueue.remove() // Returns "Mike" - state of queue -> 1
String b = stringQueue.poll() // Returns "Jeff" - state of queue -> empty
String c = stringQueue.peek() // Returns null
String d = stringQueue.element() // Throws NoSuchElementException
```

In the example above we:

* Created a new `String Queue` reference with a `LinkedList` implementation.
* Called `add()` and `offer()` to insert elements into the `Queue`. Note the state of the `Queue` after each call.
* Called `remove()` and `poll()` to remove and retrieve the element at the front of the `Queue`.
* Called `peek()` and `element()` to retrieve but not remove the element at the front of the `Queue`. Note the results when `stringQueue` is empty.

We can iterate through a `Queue` using the enhanced `for-loop`. For example:

```java
// Assuming `stringQueue` has elements -> "Mike", "Jack", "John"
for (String name: stringQueue) {
  System.out.println(name);
}
// OUTPUT TERMINAL: "Mike", "Jack", "John"
```

One thing to note about a `PriorityQueue` is that an enhanced `for-loop` (or `Iterator`) makes no guarantee in the ordering of elements after the head.

Let’s practice creating a `Queue` and iterating through it.

Example final:

```java
import java.util.Queue;
import java.util.LinkedList;
import java.util.PriorityQueue;

public class Main {
  public static void main(String[] args) {
    Queue<String> line = new LinkedList<>();
    line.add("Mike");
    line.add("Isabel");
    line.add("Jenny");

    for(String name: line) {
      System.out.println(name);
    }

    processAlphabetically(line);
  }

  public static void processAlphabetically(Queue<String> queue) {
    // PriorityQueue = tendra el elemento mas pequeño a la cabeza
    Queue<String> alphabeticalQueue = new PriorityQueue<>();
    for(String name: queue){
      alphabeticalQueue.offer(name);
    }
    while(alphabeticalQueue.peek() != null) {
      String headElement = alphabeticalQueue.remove();
      System.out.println("Processing: " + headElement);
    }
  }
}
```

Output:
```terminal
Mike
Isabel
Jenny
Processing: Isabel
Processing: Jenny
Processing: Mike
```