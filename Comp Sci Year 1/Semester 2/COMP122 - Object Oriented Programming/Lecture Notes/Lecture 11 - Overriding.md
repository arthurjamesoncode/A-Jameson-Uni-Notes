## Overriding a Superclass Method
When we create a subclass `B` of a class `A`, `B` inherits all public or protected attributes and methods of `A` without needing explicit definitions in the body of `B`.

However if there is a method definition in `B` which has the exact same signature as a method in `A` the method will work as defined in `B` not in `A`. When this happens we say that the method in `A` **overrides** the method in `B`.

>Note that the subclass method must have either the same accessibility or a stronger (more private) accessibility than the superclass method. If not the case, the compiler will complain.

**Overriding** should not be confused with **overloading**:
- **Overriding** - Providing a method definition in a subclass when a method with an identical signature in the superclass exists. The method definition from the subclass is used over the method definition in the superclass.
- **Overloading** - Providing multiple methods with the same name but having different parameter lists, and therefore different signatures. These methods can all be called and java can tell which one should be called by looking at the parameters.

For example consider the definitions for `ClubMember` and `CommitteeMember` from the last lecture note:
```java
public class ClubMember {
	private int idNum;
	private String name;
	
	public ClubMember(int newId, String newName) {
		idNum = newId;
		name = newName;	
	}
	
	public int getIdNum() {
		return idNum;
	}
	
	public String getName() {
		return name;
	}
	
	public String toString() {
		return "id: " + idNum + ", name: " + name;
	}
}
```

and

```java
public class CommitteeMember extends ClubMember {
	private String role;
	
	public CommitteeMember(int newId, String newName, String newRole) {
		super(newId, newName);
		role = newRole;
	}
	
	public String getRole() {
		return role;
	}
	
	public String toString() {
		return super.toString() + ", role: " + role;
	}
}
```

Notice that the `toString()` method is defined in both classes, and in this class it prints out the extra information of which role the committee member has.

This method also calls `super.toString()`. This is the `toString()` method from the superclass `ClubMember`. You can see that this generates a string which consists of the id and the name, which we then add to in our overridden method.
## The Object Class
The most general class in Java's object library is `Object`.

This is a superclass of all other classes, and the root of the class hierarchy. If a class does not explicitly state that it extends another more specific class, then it will directly extend `Object`.

All subclasses of `Object` inherit the public and protected methods in `Object`. One of these is `toString()`.

We added a `toString()` method to both the `ClubMember` and `CommitteeMember` classes. Strictly speaking, we didn't *add* this method we **overrode** it from the `Object` class.

It's also worth noting that whenever you call
```java
System.out.println(obj);
```
It's the same as
```java
System.out.println(obj.toString())
```

This is because the `System.out.println` method is actually overloaded. 

>`System` is a class in Java with an attribute of type `PrintStream` called `out`.
>
>This is just to specify that `System.out` is not actually a class, it is the current runtime output `PrintStream` object assigned to `System`.g
>
>Inside of this `PrintSteam` class is where the `println` methods are defined  

There are actually a lot of methods called `println` which all handle different data types which can be passed to it. The one to handle a string looks like this:
```java
public void println(String x) {
        print(x);
        newLine();
    }
```

And the one to handle an object looks like this
```java
public void println(Object x) {
        String s = String.valueOf(x);
        print(s);
        newLine();
    }
```
This method simply does the same thing, but gets a string from the object first.

This makes a call to `String.valueOf(x)` which looks like this
```java
public static String valueOf(Object obj) {
        return (obj == null) ? "null" : obj.toString();
    }
```
which we can see just either prints `"null"` or `obj.toString()` depending on whether the object is `null`.

From this, you should be able to see that there is almost no difference between 
```java
System.out.println(obj);
```
and
```java
System.out.println(obj.toString())
```

>Note that I simplified the `println` methods to avoid confusion. If curious, you can look at the actual source code yourself [here](https://github.com/openjdk-mirror/jdk7u-jdk/blob/master/src/share/classes/java/io/PrintStream.java).
## Inheritance and Constructors
A subclass does not inherit **constructors** from its superclass. You need to call `super(<args>)` to access their constructors. An example of this was gone over in detail in the [[Lecture 10 - Inheritance#Implementing the Club Example|last lecture note]].

Invoking one of the superclass's constructors by calling `super(<args>)` must be done in the first line of the subclass's constructor. 

If a subclass constructor does not explicitly call `super(<args>)`, `super()` will be called by java before the subclass constructor is run. If the superclass does not have a default constructor then this will cause a syntax error.