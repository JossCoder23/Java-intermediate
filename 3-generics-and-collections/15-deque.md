## Deque

The last of the core `interfaces` in the `collections` framework is the `Deque` interface (pronounced “Deck”). A deque (short for “double-ended queue”) is a type of queue that allows us to access elements from the front and the back of the queue.

The `Deque` interface has two types of `methods` for manipulating the front and back of the collection.

The following are some of the available methods and the exceptions they throw:

* `addFirst()`, `addLast()` - there is no space to add an element.
* `removeFirst()`, `removeLast()` - there is no element to remove.
* `getFirst()`, `getLast()` - there is no element to get.

The following methods return a special value:

* `offerFirst()`, `offerLast()` - `false` when there is no space to add an element.
* `pollFirst()`, `pollLast()` - `null` when there is no element to remove.
* `peekFirst()`, `peekLast()` - `null` when there is no element to get.
A `Deque` has many implementations, but we’ll focus on the `LinkedList` and `ArrayDeque` implementations. The `LinkedList`, although not the most optimized, is flexible enough to not only be used as a `List` and `Queue`, but also a `Deque`. The `ArrayDeque` is the preferred implementation when needing to manipulate elements at the front and back of a collection.

Let’s look at an `ArrayDeque` implementation of a `Deque`: 
```java
Deque<String> stringDeque = new ArrayDeque<>();
stringDeque.addFirst("A"); // Front -> "A" <- end
stringDeque.offerFirst("B"); // Return `true` - front -> "B", "A" <- end
stringDeque.offerLast("Z"); // Returns `true` - front -> "B", "A", "Z" <- end

String a = stringDeque.removeFirst()  // Returns "B" - front -> "A", "Z"
String b = stringDeque.pollLast()  // Returns "Z" - front -> "A" <- back
String c = stringDeque.removeLast()  // Returns "A" - empty deque

String d = stringDeque.peekFirst()  // Returns null
String e = stringDeque.getLast() // Throws NoSuchElementException
```

In the example above, we:

* Called `addFirst()`, `offerFirst()`, and `offerLast()` to add elements. Note that the `offer()` methods return a boolean.
* Called `removeFirst()`, `pollLast()`, and `removeLast()` to remove elements.
* Called `peekFirst()` and `getLast()` to get but not remove the element at the front and back of deque respectively.

If we iterate through a `Deque` using an enhanced for-loop, the elements would be processed from front to back like a standard `Queue`. However, we can also iterate through a `Deque` from front to back by using an `Iterator` from the `descendingIterator()` method and a while-loop like so:

```java
// Assuming `stringDeque` has elements front -> "Mike", "Jack", "John" <- back

Deque<String> stringDeque = new ArrayDeque<>();
stringDeque.addLast("Mike");
stringDeque.addLast("Jack");
stringDeque.addLast("John");

Iterator<String> iterator = stringDeque.descendingIterator();

while(iterator.hasNext()) {
  System.out.println(iterator.next());
}
// OUTPUT TERMINAL:  "John", "Jack", "Mike"
```

Let’s practice creating a `Deque` and iterating through it.

Example final:
```java
import java.util.Deque;
import java.util.ArrayDeque;
import java.util.List;
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    List<Integer> myInts = new ArrayList<>();
    myInts.add(9);
    myInts.add(13);
    myInts.add(2);
    myInts.add(1);
    myInts.add(11);
    myInts.add(39);
    myInts.add(78);
    myInts.add(4);

    Deque<Integer> result = separateInts(myInts);
    for(Integer i: result) {
      System.out.println(i);
    }
  }

  // add your code here to complete separateInts()

  //task
  /*
  Let’s separate even and odd integers.

  In separateInts(), define an enhanced for-loop that iterates over integers using an Integer named myInt. In the body of the for-loop, add myInt to the front of separatedDeque if it’s even and add it to the back if it’s odd.
  */
  public static Deque<Integer> separateInts(List<Integer> integers){

    Deque<Integer> separatedDeque = new ArrayDeque<>();
    for(Integer myInt:integers){
      if(myInt % 2 == 0){
        separatedDeque.offerFirst(myInt);
      }else {
        separatedDeque.offerLast(myInt);
      }
    }

    return separatedDeque;

  }
}
```

Output:
```terminal
4
78
2
9
13
1
11
39
```