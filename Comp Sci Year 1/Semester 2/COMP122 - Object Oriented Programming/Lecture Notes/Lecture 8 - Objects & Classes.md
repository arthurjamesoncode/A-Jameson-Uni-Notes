## Objects
Objects are the core of OOP. 

An **object** is a model or representation of part of the word. They have:
- **Attributes** - Which hold the data our object uses 
- **Methods** - These are functions which determine what our objects can do, and they they can interact with other objects.
Each object refers to a **particular individual**, so a person, book, shape, etc. but not all people, books, shapes etc.

For example we could have a **rectangle** object which has:
- An **attribute** holding its width
- An **attribute** holding its height
- A **method** which calculates and returns it's area
## Classes
A **class** is a template or blueprint of all objects of a certain type.

**Classes**:
- Can be instantiated
- Specifies which attributes and methods each instance has, but not their values.
- Defines a data type

For example, the 3 squares below could all be **instances** (individual objects) of the class `Square`. They all have `size` and `colour` attributes, but they all hold different values.

![[squares.png]]

Classes have **constructors**. These are special methods that are used to create **instances** of a given class.

The syntax for constructor methods is almost the same as normal methods, with two key differences:
- It must have the **same name** as the class;
- It has no declared **return type**.

For example we could define a `Square` class like so:
```java
public class Square { 
	private int size; 
	private String colour; 
	
	public Square (int s, String c) {
		size = s; 
		colour = c; 
	} 
}
```

This class just defines two attributes, an integer to represent the size and a String, which represents the colour.

It also defines 1 method, which is our **constructor**. This method allows us to instantiate an **specific** square like so:
```java
Square r = new Square(5, "red");
```

Note that to instantiate an **instance** of a class you must use the `new` keyword. This tells Java that this is an instantiation and not just a method call.

Note that there are restrictions on how we can access certain attributes and methods. This will be discussed in detail in the [[Lecture 9 - Accessibility|next lecture]].
