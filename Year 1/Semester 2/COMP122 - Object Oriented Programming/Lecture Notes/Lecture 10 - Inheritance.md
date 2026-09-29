## Inheritance
In OOP, inheritance is the word we use to describe the "is a" relationship between a subclass and a superclass.

Imagine a new subclass `Student` which inherits from a superclass `Person`. You can think of `Person`, our superclass, as the **base** for our sub class `Student`.

"Student" has all the defined attributes and methods of `Person`, but can have additional methods. Imagine `Person` has attributes of name and address, `Student` would also have those attributes but may have additional information, such as `course` and `student_id`.

It is also possible for a subclass to **override** a method of their superclass. This means it overwrites the method with a different one for that class. 

Consider a class for `Mammal` which has a `make_sound` method which just prints `"Sound"` to the console. Let's now define a sub class of `Dog`, which inherits from `Mammal`, and give it a `make_sound` method which prints `"Woof!"` to the console. 

If we ever have a dog object, and call the `make_sound` method, it will print `"Woof!"` and not `"Sound"` because the method implementation in `Dog` **overrides** the method implementation in `Mammal`.

It is also possible for **multiple** subclasses to inherit from a single superclass, but each subclass can only inherit from **one** superclass.

You can see an example hierarchy of classes below
![[inheritance_uml.png]]
## UML
We use **Unified Modelling Language** (UML) to illustrate and define classes and their relationships to other classes.

UML diagrams are made up of 3 boxes laid out in a column:
- The top box contains the **name** of the class;
- The middle box contains the **attributes** of the class;
- The bottom box contains the **methods** of the class.

The visibility of each **class member** (attribute or method) is indicated by the symbol to the left of the **member:**
- `+` indicates public;
- `-` indicates private;
- `#` indicates protected;
- `~` indicates package.

We also use `/` to indicate **derived** attributes, which is any attribute which is not an attribute of the class themselves but is instead computed from the other attributes of the object. 

To show that a subclass **extends** (inherits from) a **superclass**, we use an arrow with a white head which points from the subclass to the superclass. If a class uses another club then we 

Below you can see an example UML diagram for a club system
![[full_club_uml.png]]

We can see here that there are also **uses** arrows, indicated by the word **uses** and the solid colour tips. These arrows indicated that `Club` has attributes of type `ClubMember` and `CommitteeMember`, or lists/collections of that type.
## Implementing the Club Example
One could end up with the above UML diagram if they were working on the following brief:
	"Design and implement a Java program that stores details about clubs and their members, e.g. their name and club ID number. 
	Additionally, some of the club members are committee members. 
	Committee members have all the attributes and behaviour of a club member, but additionally need their position on the committee (e.g. treasurer, chair, secretary, etc) to be stored."

From this brief, we can try and pick out the **objects** that we want to represent. There are 3 of these:
- Club
- Club Member
- Committee Member

Then we should look at the relationships between these objects. We know that a committee member must also be a club member, but needs some extra information. This means that we can make `CommitteeMember` a **subclass** of `ClubMember`.

We know that Clubs have members, and so we can make these members (including committee members), attributes of the club. 

>The way this is done in the UML you are shown is to have `member1` be an attribute of type `ClubMember` and `member2` be an attribute of type `CommitteeMember` but this is a bad way of doing it.
>
>We don't know how many members we will have, and won't want to change the code if another member gets added. This means that the best way to do this would be to have a `members` attribute of type `ClubMember[]`.

First lets draw up an implementation of `ClubMember`
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

Now we can add an implementation for `CommitteeMember`, we're going to make this a subclass of `ClubMember`, which we can do by using the extends keyword. 

We also need a **constructor** which takes the same arguments as `ClubMember` (the superclass), with an additional one. The attributes from `ClubMember` are private, and so we can't change them in our subclass. The way we get around this is by using the special keyword `super`.

`super` refers to the superclass of the current class. You can use it to refer to overridden methods from the superclass or the superclass's constructors.

`super(<args>)` represents the constructors of the superclass. When you call `super(<args>)` from a subclass, it checks the arguments you pass to it to see if the superclass has a constructor which matches the signature of the `super(<args>)` call. This check happens at compile time, and won't work if the superclass doesn't have a matching constructor.

The `super(<args>)` call must happen on the first line of the constructor of the subclass. If `super(<args>)` isn't called explicitly by the programmer, java calls `super()` (the superclass's default constructor). If the superclass doesn't have a default constructor (like in this example), it will cause an error at compile time.

We can use this to pass the id and name of our committee member to the constructor of the `ClubMember`, setting these private attributes in a safe way.

We can also use `super.toString()` inside our `toString` method to simplify our logic.

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

And finally we can write our `Club` class
```java
public class Club {
	private ClubMember[] members;
	private CommitteeMember[] committee;
} 
```

Note that we can store objects of type `CommitteeMember` in the `members` attribute since any `CommitteeMember` is also a `ClubMember`

This isn't a very useful class at the moment but shows how we can use our other classes as types of attributes for our class.

As an exercise, try to add a constructor method for this class, as well as a `toString` method, and methods to add and remove members or committee members.