## Collection

We’ve discussed the core `interfaces` and their implementations, but the thing that keeps the `collections` framework polymorphic (compatible) is the `Collection` interface. The `Collection` interface provides a generic, general-purpose API when our program needs a collection of elements and doesn’t care about what type of collection it is. 

Implementing `classes` may implement `Collection` `methods` and add restrictions to them like a `Set` does to only contain unique elements. Also, implementing classes or extending interfaces do not need to implement all methods and instead will throw an `UnsupportOperationException` when a `Collection` method is not implemented correctly. 

We’ve seen `add()` and `remove()`, but some other methods Collection defines are:

* `addAll()` - receives a `Collection` argument and adds all the elements.
* `isEmpty()` - returns `true` if the collection is empty, false otherwise.
* `iterator()` - returns an `Iterator` over the collection.
* `size()` - returns the number of elements in the collection.
* `stream()` - returns a `Stream` over the elements in the collection.
* `isArray()` - returns an array with all elements in the collection.

Here is an example of how we can use some of these methods:

```java
Collection<Integer> collection = new ArrayList<>();
collection.add(4);
collection.add(8);

boolean isEmpty = collection.isEmpty(); // false
int collectionSize = collection.size(); // 2

Integer[] collectionArray = collection.toArray(new Integer[0]);
```

In the example above, we:

* Created an `Integer` `Collection` with an `ArrayList` implementation.
* Called `add()` to add elements to the end of the `Collection`.
* Called `isEmpty()` to check if `collection` has elements.
* Called `size()` to get the number of elements in `collection`.
* Called `toArray()` to transform our collection into an array. Note the `new Integer[0]` argument that specifies the type of array we want returned.

We can iterate through a `Collection` with an enhanced `for-loop` as we’ve seen with the other core interfaces.

Let’s practice working with `Collection`.

Example final:

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Set;
import java.util.HashSet;
import java.util.Queue;
import java.util.LinkedList;
import java.util.Deque;
import java.util.ArrayDeque;
import java.util.Collection;

public class Main {
  public static void main(String[] args) {
    List<Integer> intList = new ArrayList<>();
    Set<String> stringSet = new HashSet<>();
    Queue<Double> doubleQueue = new LinkedList<>();
    Deque<Integer> intDeque = new ArrayDeque<>();

    intList.add(5);
    intList.add(8);
    intList.add(5);
    intList.add(1);

    stringSet.add("Hello");
    stringSet.add("World");
    stringSet.add("World");

    doubleQueue.add(3.89);
    doubleQueue.add(889.64);

    intDeque.addFirst(7);
    intDeque.addFirst(8);
    intDeque.addLast(40);

    System.out.println(intList.getClass());
    printCollection(intList);
    System.out.println();
    System.out.println(stringSet.getClass());
    printCollection(stringSet);
    System.out.println();
    System.out.println(doubleQueue.getClass());
    printCollection(doubleQueue);
    System.out.println();
    System.out.println(intDeque.getClass());
    printCollection(intDeque);
  }

  private static <T> void printCollection(Collection<T> collection) {
    for(T item:collection){
      System.out.println(item);
    }
  }
}
```

Output:
```terminal
class java.util.ArrayList
5
8
5
1

class java.util.HashSet
Hello
World

class java.util.LinkedList
3.89
889.64

class java.util.ArrayDeque
8
7
40
```