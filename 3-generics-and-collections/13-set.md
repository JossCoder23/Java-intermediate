## Set 

Another core interface provided by the `collections` framework is the `Set` interface. A `Set` is a collection of unique elements and all of its `methods` ensure this stays true. The collections framework provides different implementations of a `Set` (we’ll focus on a subset of them) that each have different use cases.

The `HashSet` implementation has the best performance when retrieving or inserting elements but cannot guarantee any ordering among them.

The `TreeSet` implementation does not perform as well on insertion and deletion of elements but does keep the elements stored in order based on their values (this can be customized).

The `LinkedHashSet` implementation has a slightly slower performance on insertion and deletion of elements than a `HashSet` but keeps elements in insertion order.

Let’s look at how we can create `Set` with a `HashSet` implementation:

```java
Set<Integer> intSet = new HashSet<>();  // Empty set
intSet.add(6);  // true - 6  
intSet.add(0);  //  true - 0, 6 (no guaranteed ordering)
intSet.add(6);  //  false - 0, 6 (no change, no guaranteed ordering)

boolean isNineInSet = intSet.contains(9);  // false
boolean isZeroInSet = intSet.contains(0);  // true
```

In the example above, we:

* Created a `Set` reference named `intSet` with a `HashSet` implementation.
* Called `add()`, which adds elements to the `Set` and returns `true` if an element was successfully added or `false` if not.
* Called `add()`, noting that the program will not throw an error if we try to insert a non-unique element into the set.
* Called `contains(9)`, which returns `false` because the `9` does not exist in `intSet`.
* Called `contains(0)`, which returns `true` because the `0` does exist in `intSet`.

All of these methods work for other `Set` implementations too.

We can iterate through a `Set` using the enhanced `for-loop` and notice that we can’t guarantee the ordering of elements looped. For example:

```java
// Assuming `intSet` has elements -> 1, 5, 9, 0, 23
for (Integer number: intSet) {
  System.out.println(number);
}
// OUTPUT TERMINAL: 5 0 23 9 1
```

Let’s practice creating a `Set` and iterating through it.

```java
import java.util.Set;
import java.util.TreeSet;

public class Main {
  public static void main(String[] args) {

    Set<Integer> sortedSet = new TreeSet<>();

    sortedSet.add(3);
    sortedSet.add(7);
    sortedSet.add(27);
    sortedSet.add(7);

    for(Integer element : sortedSet) {
      System.out.println(element);
    }

  }
}
```

Output:
```terminal
3
7
27
```