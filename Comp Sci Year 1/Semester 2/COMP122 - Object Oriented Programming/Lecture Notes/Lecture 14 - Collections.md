## Collections
A Collection (also called an Aggregate) is an object which stores objects, and can be dynamically resized.

Collections/Aggregates come in a lot of different forms and can differ by:
- The type of the elements they store
- How to access its contents
- The data structure used to store it's contents

Java comes with a number of ready to use **interfaces** for different types of Aggregates:
- `Collection` for a generic group of objects
- `Queue` for a FIFO (and LIFO) data structures
- `Set` for a collection with no duplicate elements
- `List` for an ordered collection with duplicates allowed
- `Map` which stores key-value pairs with no duplicate keys

These classes are interfaces, which mean that they define operations that these types of aggregate must allow, but don't have any concrete implementation. 

There are classes such as `ArrayList` or `HashSet` which implement these interfaces while providing some kind of implementation.

For example, if you wanted to create a collection which holds a list of strings you could write
```java
import java.util.* //top line of file, contains the collections framework

List<String> customers = new ArrayList<String>();
```

Note that we use the interface `List` as the type of our collection but have to use the concrete implementation `ArrayList` to initialise our object. 

You can still use the more specific of the two types (`ArrayList`) as the type, but after creating the object we only ever need the interface methods, so we might as well use the interface as a type, since this separates how we can use it from the internal implementation. If we keep the implementation separate from how we can use it, we could change the implementation later much more easily. 

Imagine if we wanted to change from an `ArrayList` to a `LinkedList` because we saw there would be performance boosts based on the operations we need to perform on `customers`. If we use the `List` interface then the only line we need to change is where the list gets created.
### Sidenote on Generics
Also note that we use a special syntax to show that the `List` and `ArrayList` must store strings. 

```java
List<String> customers = new ArrayList<String>();
```

By adding `<String>` after the data type, we tell Java that these collections can only hold `String` values. 

This syntax is called **parameterised types** or **Java generics**. It essentially allows us to avoid having to create an entirely different class for each type of object we would like to store.

You can also have generics which take multiple types.

For example if we wanted to make a map object which maps from `String` to `int` we can do so with
```java
Map<String, Integer> myMap = new HashMap<String, Integer>();
```

Again we use the interface `Map` as the type and then construct it using the `HashMap` implementation.

Here though you can see that we actually need two types in our generic, to indicate the types of our **keys** (`String`), and the types of our **values** (`Integer`).

Also note that we use `Integer` instead of `int`. This is because aggregates can only store other objects, not primitive data types. This means that we need to use `Integer`, as the generic type since this is the **wrapper class** for `int` (essentially the object version of `int`).
### Useful Collections
This section is just going to be a list of links to the oracle pages for various useful aggregates from the `java.util` package
- [ArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)
- [LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/List.html)
- [Stack](https://docs.oracle.com/javase/8/docs/api/java/util/Stack.html)
- [ArrayDeque](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html) (Deque is short for double ended queue)
- [HashSet](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html)
- [HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
