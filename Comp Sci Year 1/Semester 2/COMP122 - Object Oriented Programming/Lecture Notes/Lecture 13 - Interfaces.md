## Multiple Inheritance
Multiple inheritance is when a class inherits from multiple different disconnected super-classes. When this happens, the inheriting class inherits all attributes and methods of all super-classes.

Most OOP languages allow for some form of multiple inheritance. Python and C++ allow this directly.

Java works a little bit differently, it doesn't allow this for ordinary classes or abstract classes, only for **interfaces**.
## Interfaces
Interfaces are essentially a kind of **abstract class** which are a bit more restrictive but allow for multiple inheritance.

Interfaces can only define two things:
- Public static constants,
- Public abstract methods.

Interfaces are meant to show the parts of a class that we can interact with, hence why we can only define public constants and methods.

We can't define fields/attributes, whether public or private, in interfaces, and every method must be abstract, meaning it must not have a method body.

This means that an interface simply defines a **specification of methods** which must be implemented but the subclass. Therefore, we say that a class that inherits from an interface **implements** that interface.

Knowing this we can define an example interface, `Transformable`, which represents shape objects which can change shape in some way, change colour to a specified colour, and has a method for computing an object. Any object which implements this interface should only be transformable a set number of times, as defined in a constant in this interface.

```java
public interface Transformable {
	public final static int MAX_ITERATIONS = 10;
	
	public abstract void transform();
	public abstract void recolor(int newColor);
	public abstract double computeArea();
}
```

We've explicitly defined `MAX_ITERATIONS` as `public final static` and each method as `public abstract`, but this seems a bit redundant since we can only have these types of methods and constants in the interface at all. 

Luckily, Java agrees. This means we don't need to specify these things. As long we use the `interface` keyword and not the `class` keyword we can omit this.

This means that the following is identical
```java
public interface Transformable {
  int MAX_ITERATIONS = 10;
  
  void transform();
  void recolor(int newColor);
  double computeArea();
}
```

By convention, interfaces typically end in -`able`. For example, `java.lang.Comparable` or `java.io.Serializable`.

>As of Java 8, it is possible to have concrete methods be part of an interface but they must be preceded by the `default` keyword. This course was clearly written before this change, and aside from a footnote in the slides it is not mentioned. 
>
>This means that you won't be expected to ever use the `default` keyword, but it is probably good to know that it exists. 
## Implementing an Interface
Classes can **implement** one or more interfaces like so:
```java
public class myClass implements myInterface1, myInterface2 {}
```

A class which implements an interface can also directly inherit from a class. Meaning that this
```java
public class myClass extends mySuperClass implements myInterface1, myInterface2 {}
```
is also completely valid.

Interfaces can also inherit from each other. Since interfaces never implement anything (i.e. never provide any concrete methods) we don't use the `implements` keyword and instead use the `extends` keyword like so
```java
public interface mySubInterface extends mySuperInterface {}
```
### Example
Imagine we wanted to simulate something to do with different types of birds. We can define a `Bird` superclass as a base for our class hierarchy
```java
public class Bird { 
	protected String name;
	
	public Bird (String myName) { 
		name = myName; 
	}
	
	public String getName() {
		return name;
	}
	
	public boolean flies() { 
		return true
	}
	
	public String type() {
		return "Bird";
	} 
	
	public void printDetails() {
		System.out.println(type() + " " + getName() + " flies : " + flies());
	}
}
```

Now imagine that we want to add some methods to simulate flying. Birds aren't the only things that fly and anything that flies needs a way to go up in the air, move forward in the air, and then come back down again. 

This means we can implement this as an **interface** like so:
```java
public interface Flyable {
	void goUp();
	void goForward();
	void goDown();
}
```

Which lets us add this to our bird class like so
```java
public class Bird implements Flyable { 
	protected String name;
	
	public Bird (String myName) { 
		name = myName;
	}
	
	public String getName() {
		return name;
	}
	
	public boolean flies() { 
		return true
	}
	
	public String type() {
		return "Bird";
	} 
	
	public void printDetails() {
		System.out.println(type() + " " + getName() + " flies : " + flies());
	}
	
	// Newly implemented Interface Methods
	public void goUp() {
		System.out.println(type() + " " + name + " starts to fly.");
	}
	public void goForward() {
		System.out.println(type() + " " + name + " starts to fly.");
	}
	public void goDown() {
		System.out.println(type() + " " + name + " starts to fly.");
	}
}
```

But what about birds that can't fly?

There are 2 ways to handle this:
- Inside of the method bodies defined in `Bird` we check whether the bird can fly using the `flies()` method, and do something different if they can't;
- Define a new subclass of `Bird` called `FlightlessBird` and have it override the methods from `Bird`.

There isn't a "correct" option to go with. In situations like this you need to make the decision depending on:
- How quick can you implement it,
- How clean will your code be after implementing it,
- How will each way of implementing it affect performance.

In the example above either option is completely fine, but when making real decisions about this kind of stuff you will need to consider the **trade-offs** of each options.