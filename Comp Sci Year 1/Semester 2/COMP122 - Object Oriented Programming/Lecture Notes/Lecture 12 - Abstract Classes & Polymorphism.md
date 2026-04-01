## Abstract Classes
When we construct a class hierarchy, it is sometimes helpful to include a class which acts as a blueprint for all subclasses but we would never want to instantiate. **Abstract classes** let us do exactly that.

An abstract class is a type of class which can not be instantiated, but can be extended/inherited from. We refer to classes that are not abstract, which is all the ones seen so far, as **concrete classes**.

We indicate a class as abstract when we define it by using the abstract keyword like so.
```java
<modifiers> abstract class ClassName { ... }
```

Abstract classes can include **abstract methods**. These are methods which are defined using the abstract keyword and don't include a method body. The lack of a method body means that the there are no square brackets, instead the line just ends with a semi-colon like so.
```java
<modifiers> abstract <type> methodName (<args>); 
```

The purpose of an abstract method is to enforce that all the subclasses of this abstract method include a method with this signature and define a method body for it. If a concrete subclass of an abstract class doesn't **override** an abstract method with a concrete method, then this will cause an error at compile time.

For example, consider the club example from [[Lecture 10 - Inheritance#Implementing the Club Example|recent lectures]]. Imagine we wanted to extend this system so now instead of just storing information on club members, it also stores information on gym members or members of a university.

We know that any member will be a member of something more specific, for example a club or a gym, and so we will never want to instantiate just a member. This means we can make member an **abstract class**.

We also know that each `Member` will have a name and some kind of ID number which we will want to be able to access, but what we don't know is how that will be stored for each system. Maybe one system stores them as attributes of the object itself and another has to send a query to a database or a website.

This means that we want every concrete instance of `Member` to have a **public** way of getting the `idNum` and `name` of a member, but we don't know what code will need to be written to do that. This means we need to define **abstract getter methods**.

We could define this class like so
```java
public abstract class Member {
	public abstract String getName();
	
	public abstract int getIdNum();
}
```

The **abstract methods** don't do anything, except cause a compiler error if I ever try to extend member with a concrete class without providing method bodies for these two abstract methods.

>While causing more compiler error's may seem counter intuitive, this actually acts as a guard-rail. Any instance of a class which extends `Member` could at some point be asked to perform `getName()`. If there isn't a definition for it, this can cause your program to crash at runtime.
>
>If your code doesn't compile, you know it doesn't work. If your code does compile, it might work but it also might not. By enforcing checks at compile time, we decrease the amount of debugging we ultimately have to do.

We can then edit our `ClubMember` implementation to be a subclass of `Member`. This class already had both of the required methods so the only change is in the class declaration itself.
```java
public class ClubMember extends Member {
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
### Polymorphism of Abstract Classes
One example of polymorphism is when an object can actually be multiple different types of object. We've seen a little bit of this so far, but it hasn't been well explained yet. An exact definition of polymorphism, will be given later in this note.

Continuing with our club example, imagine we want to instantiate some objects. We could do so like this:
```java
ClubMember member1 = new ClubMember(123, "Fred");
CommitteeMember member2 = new CommitteeMember(22, "Helen", "Chair");
```
Here we use the `ClubMember` and `CommiteeMember` as the types for `member1` and `member2`.

What we can also do is use a superclass of these types as the type for `member1` and `member2`. For example:
```java
Member member1 = new ClubMember(123, "Fred");
Member member2 = new CommitteeMember(22, "Helen", "Chair");
```

Now, if we call `member1.getName()`, java knows that `member1` has this method, since it inherits from `Member`. The code that actually runs is the the code associated with the **concrete instance** `member1`, i.e. the method body defined inside `ClubMember` since `member1` was instantiated with the `ClubMember(int newId, String newName)` constructor.

Here we have only used the `ClubMember` and `CommiteeMember` classes, as were defined in previous lectures, but we could also define a `GymMember` class which also inherits from `Member`. 

One very important use of this is if we wanted to store members of any organisation in an array. If we do we can define the type as `Member[]`, which would allow each individual member of the array to be either a `ClubMember` or `GymMember`.
## Polymorphism
Polymorphism has been shown in these lectures but hasn't been defined exactly yet. It is much simpler than it sounds. It simply means when 1 thing can be multiple different things. For example `Member` is a polymorphic class since it can mean `ClubMember`, `GymMember`, or `CommitteeMember`. 

Similarly `ClubMember` is also polymorphic since any instance of `ClubMember` can also be an instance of `CommiteeMember`.

>We have seen polymorphism in COMP105 as well when we looked at [[Lecture 12 - Polymorphic Types|polymorphic types]].

In the context of Java we say any class that has been inherited from is polymorphic, as this class can either be an instance of itself or it's child.

Next lecture we will look at **interfaces** which are like a special type of **abstract class**. These are usually also polymorphic, since they can be implemented by multiple classes. 