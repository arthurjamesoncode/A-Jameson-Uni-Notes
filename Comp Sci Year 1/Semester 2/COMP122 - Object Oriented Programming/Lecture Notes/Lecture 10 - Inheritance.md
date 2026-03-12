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
