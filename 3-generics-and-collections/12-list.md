## List

The `collections` framework provides a core set of `interfaces` to define different collection behaviors. One of the core interfaces is the `List` interface. A `List` is a collection where elements are ordered in a sequence. `Lists` allow us to have duplicate elements and fine-grain control over where elements are inserted in the sequence. Like `arrays`, the position of a `List` is known as the index and is `0` based. Unlike arrays, which have a static size, `Lists` are dynamically sized.

The collections framework provides many `List` implementations, but we’ll focus on the `ArrayList` and `LinkedList`. The ArrayList is the overall preferred implementation for most use cases but the `LinkedList` performs better than an `ArrayList` if your program mostly inserts and deletes elements at the beginning or end of a list.

Let’s create a `List` using an `ArrayList` as its implementation and see some operations:

```java
List<Integer> intList = new ArrayList<>(); // Empty `List`
intList.add(4); // 4
intList.add(6); // 4, 6
intList.add(3); // 4, 6, 3
intList.set(1, 3); // 4, 3, 3

int a = intList.get(2); // a = 3
int b = intList.indexOf(3); // b = 1

List<Integer> subIntList = intList.subList(1,3); // subIntList -> 3, 3
```

In the example above, we:

* Created a `List` reference named `intList` with an `ArrayList` implementation.
* Called `add()`, which appends elements to the end of the `List`. We can see the state of `intList` after each call.
* Called `intList.set(1, 3)`, which replaces the element at index `1` (the second element in 0-based indexing) with `3`.
* Called `get()`, which gets the value at index `2` (the third element in 0-based indexing).
* Called `indexOf()`, which returns the index of the first occurrence of `3` (the first `3` is at index `1`). -Called `subList()`, which returns a sublist in a new `List` with the elements specified by the starting index `1` (inclusive) and ending index `3` (exclusive).

We can iterate through a `List` using the enhanced `for-loop`. For example:

```java
// Assuming `intList` has elements -> 1, 5, 2, 6, 1
for (Integer number: intList) {
  System.out.println(number);  
}
// OUTPUT TERMINAL: 1 5 2 6 1
```

In the example above, we used the enhanced `for-loop`, which iterates through the elements in `intList` from index `0` to the end of the list. Note that we use the `int` wrapper class `Integer` to iterate through the elements in `intList`. However, we could have also used an ‘int’.

Let’s practice creating a `List` and iterating through it.

