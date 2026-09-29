## Iterators
Can you see an issue with the following code?

```java
ArrayList<Integer> numbers = generateList(); //arbitrary function to generate list of integers

int size = numbers.size();
for (int i; i < size; i++) {
	int j = numbers.get(i);
	//do some stuff with j
	numbers.remove(i);
}
```

The big problem here is that we remove elements of the list, but use the initial size of the list to iterate through it. This will eventually cause an error where `i` will be too large to access the list and crash our program.

**Iterators** provide a way to access elements of an aggregate object sequentially without exposing its underlying implementation.

Iterators are:
- Objects,
- Single use (a new one must be created every time you iterate over the collection),
- Provide safe access to the collection,
- Are often created by the collection itself.

Separating out the traversal mechanism from the collection itself allows there to be different ways of traversing the collection without cluttering the collection class.

For example instead of using a for loop to iterate over `numbers` we can use an `Iterator` like so:
```java
Iterator<Integer> iter = numbers.iterator();

while (iter.hasNext()) {
	int curr = iter.next();
	iter.remove();
} 
```

You must specify the type of the object which the iterator will be getting from the collection using a **generic**, which was covered [[Lecture 14 - Collections#Sidenote on Generics|last lecture]].

The `iter.remove()` method removes the last element returned by `iter.next()`. This can be used to safely remove them from the collection while using the iterator to traverse the collection.

>The `iter.remove()` method is not the same as the `remove()` method of the collection itself.

