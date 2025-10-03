## Algorithms

We’ve seen the many benefits of the collections framework and how they provide ready-to-use implementations so we don’t have to create them ourselves. What should we do when we need to sort a collection or get some statistic like the maximum or minimum element in the collection? The collections framework provides the `Collections` class that has many `static` `methods` that perform these types of operations for us.

Here are some of the methods provided by the `Collections` class:

* `binarySearch()`: Performs `binary search` over a `List` to find the specified object and returns the index if found. This method is overloaded to also accept a `Comparator` to define a custom ordering policy. Note: this method only provides the correct value if the elements in the `List` are sorted.
* `max()`: Returns the maximum element in the `Collection`. This method is overloaded to also accept a `Comparator` to define a custom ordering policy.
* `main()`: Returns the minimum element in the `Collection`. This method is overloaded to also accept a `Comparator` to define a custom ordering policy.
* `reverse()`: Reverses the order of elements in the `List` passed in as an argument.
* `sort()`: Sorts the `List` passed in as an argument. This method is overloaded to also accept a `Comparator` to define a custom ordering policy.

These utility methods for the collections framework make performing complex calculations or gaining insight into the collection of data we have easy and efficient.

Let’s practice using some `Collections` methods.

Example Final:

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Collection;
import java.util.Set;
import java.util.HashSet;
import java.util.Iterator;

public class Main {
  public static void main(String[] args) {
    List<Integer> myList = new ArrayList<>();
    myList.add(3);
    myList.add(-1);
    myList.add(57);
    myList.add(29);

    Set<String> mySet = new HashSet<>();
    mySet.add("Hello");
    mySet.add("World");

    System.out.println("mySet max: \""+ Collections.max(mySet)+"\"");
    System.out.println();

    System.out.println("myList min: "+ Collections.min(myList));
    System.out.println();

    System.out.println("Index of 57 in myList is: "+Collections.binarySearch(myList, 57));
    System.out.println();


    System.out.println("myList prior to reverse: ");
    printCollection(myList);

    System.out.println();

    Collections.reverse(myList);
    System.out.println("myList reversed: ");
    printCollection(myList);

    System.out.println();

    System.out.println("myList prior to sort: ");
    printCollection(myList);

    System.out.println();

    Collections.sort(myList);
    System.out.println("myList after sort: ");
    printCollection(myList);


  }

  public static void printCollection(Collection<?> collection){
    Iterator<?> myItr = collection.iterator();

    while(myItr.hasNext()){
      System.out.println(myItr.next());
    }
  }
}
```

Output:
```terminal
mySet max: "World"

myList min: -1

Index of 57 in myList is: 2

myList prior to reverse: 
3
-1
57
29

myList reversed: 
29
57
-1
3

myList prior to sort: 
29
57
-1
3

myList after sort: 
-1
3
29
57
```