## Map

Previously, we saw the `collections` framework hierarchy and how `Collection` is the root of it. There exists another interface that didn’t quite fit into that hierarchy but is an extremely important part of the collection framework: the `Map`.

`Map` defines a generic interface for an object that holds key-value pairs as elements. The key is used to retrieve some value (like the index in an array or `List`). A key must be unique and map to exactly one value. There are many implementations of `Map`, but we’ll focus on the `HashMap` implementation.

The `HashMap` defines no specific ordering for the keys and is the most optimized implementation for retrieving values. This is Java’s implementation of a `hash table`.

A `Map` has the following `methods` for accessing its elements:

`put()`: Sets the value that a key maps to. Note that this method replaces the value a key mapped to if the key was already present in the `Map`.

`get()`: Gets, but does not remove, the value the provided key argument points to if it exists. This method returns `null` if the key is not in the `Map`.
Let’s see how we can use them:

```java
Map<String, String> myMap = new HashMap<>();

myMap.put("Hello", "World") // { "Hello" -> "World" }
myMap.put("Name", "John") //   { "Hello" -> "World" }, { "Name" -> "John" }

String result = myMap.get("Hello") // returns "World" 
String noResult = myMap.get("Jack") // return `null`
```

In the example above, we:

* Created a `Map` reference that maps a `String` key to a `String` value using the `HashMap` implementation. Note that a `Map` needs a type argument for the key and value.
* Added key-value pairs to `myMap` using `put()` where the first argument is the key and the second is the value the key maps to.
* Retrieved the value the key “Hello” maps to using `get()`. The `String` “World” is returned since the key “Hello” exists. `get()` returns `null` because the key “Jack” does not exist.

We can iterate over a `Map` with an enhanced `for-loop` like so:

```java
// Given a map, `myMap`, with the following key-value pairs { "Hello" -> "World" }, { "Name" -> "John"}
for (String s: myMap.keySet()){
  System.out.println("key: "+s+", value: "+myMap.get(s));
}
// OUTPUT TERMINAL:
// key: Name, value: John
// key: Hello, value: World
```

In the example above, we:

* Called `keySet()` to return the `Set` of the keys contained in this `HashMap`.
* Iterated through the set of keys of this map.
* Called `myMap.get(s)` to get the value associated with key `s`.

Let’s practice working with `Map`.

Example Final:
```java
import java.util.List;
import java.util.ArrayList;
import java.util.Map;
import java.util.HashMap;
import java.util.Random;
public class Main {
  public static void main(String[] args) {
    List<Integer> myInts = new ArrayList<>();
    Random random = new Random();

    for(int i =0; i < 20; i++) {
      myInts.add(random.nextInt(5));
    }

    System.out.println("myInts: " + myInts);

    Map<Integer, Integer> intCount = countNumbers(myInts);
    for(Map.Entry<Integer, Integer> entry: intCount.entrySet()) {
      System.out.println("Integer: "+ entry.getKey()+" appears: "+ entry.getValue());
    }
  }

  public static Map<Integer, Integer> countNumbers(List<Integer> list) {
    Map<Integer, Integer> intCount = new HashMap<>();
    for(Integer i:list){
      if(intCount.get(i) == null) {
        intCount.put(i, 1);
      }else {
        int counter = intCount.get(i); //encuentra el valor "si" esta
        counter++; // sumale uno
        intCount.put(i, counter);
      }
    }
    return intCount;
  }
}
```

Output:

```terminal
myInts: [3, 4, 4, 1, 1, 3, 3, 2, 2, 3, 4, 0, 2, 1, 0, 3, 1, 2, 1, 3]
Integer: 0 appears: 2
Integer: 1 appears: 5
Integer: 2 appears: 4
Integer: 3 appears: 6
Integer: 4 appears: 3
```