## Module Overview
This module presents a conceptual and practical introduction to object oriented programming, using the high level programming language **Java**.

**We will learn:**
- Programming in Java
- Class Hierarchies
- Polymorphism
- UML diagrams and other tools to document and test code.
- Design Patterns

### Assessment Structure
The grade for this module is made up of 3 **portfolios** made up of a number of smaller assignments and a final **programming exam**. 

The portfolios are worth **15%** each and the final exam is worth **55%**.

Weeks 1-4 will be dedicated to the first portfolio, which is "Imperative Programming with Java". We will learning about about variables, types, loops, methods, etc. The simple programming stuff. This should be very easy for anyone with any significant programming experience, but may be something less experienced people struggle with.

Weeks 5-7 will be dedicated to the second portfolio, which is "Object Oriented Programming". Here we will learn about objects, classes, inheritance, polymorphism, interfaces etc. This will be a bit trickier but still very manageable for those with any OOP experience.

Weeks 8-11 will be dedicated the third portfolio, which is "OOP design patterns". We will learn about collections, iterators, streams etc.

## What is OOP?
Object oriented programming is a programming paradigm that aims to model problems using interacting **objects**. These objects contain both data, and procedures and are instances of a whole **class** of similar objects.

It is based on 4 main principles
- **Encapsulation:** Grouping data and code that acts on it into a single unit.
- **Abstraction:** Hiding implementation details from the user. This refers to programmers who use the classes and objects we create, not the end user of the program.
- **Inheritance:** Using known classes of objects as blueprints for more specific ones. 
- **Polymorphism:** This refers to different behaviour of subclasses by redefining their methods.

If you struggle to understand any of these concepts don't worry, they will be covered in a lot more detail.

For example, suppose we're building an application that deals with people's names, addresses, student IDs (for students), university position and salary (for employees), etc.

We could create a **Person** class that has some of this information on it, along with some code that can act on this data. We call this **encapsulation**.

Below you can see a representation of a person class.
![[class_diagram.png]]

>This is an example of a class diagram from **Unified Modelling Language** we will cover these in more depth as we go further through the course.

We can see that a person, as we've defined it, contains a some data, which we call attributes (`firstName: String`, `surname: String`, `address: String`), and some methods (`greet(String name)`, `getFirstName(): String`). Each individual person will be an object (also called an instance) of this class.

The `getFirstName(): String` method is called a getter function. The attributes are hidden and cannot be accessed directly so we require getter functions in order to view the value of these attributes in code. Hiding these attributes is as example of **abstraction**.

### Inheritance Example
A student is also a person, but needs some extra information to be stored, such as a student ID.

So to model this we can create a new class which **extends** (or **inherits** from) our person class to add this attribute.

The idea here is that if we have a well-defined and well-tested class, we can extend it to add more attributes and methods, without modifying the already existing class. So we can create a student, which is a person with an extra attribute and method. You can see below a UML class diagram for student.

![[inheritance_diagram.png]]

Every student is also a person, but not every person is also a student. Each student will have all the attributes and methods of a person, plus additional ones only present on students.

Similarly, we can extend the **Person** class to create a **Lecturer** class by adding attributes such as *office* and *telephoneNo* and methods to access or change these attributes.

We could also extend student to add multiple subclasses depending on the type.

Below you can see what an extended UML class diagram might look like.
![[inheritance_2.png]]
### Polymorphism Example
Polymorphism means many forms. In OOP it means that we can treat multiple different subclasses as the same class. The class they are treated as must be a superclass of all the different subclasses.

Consider the example above. 

In Java, we can only store one **data type** in an array. This can be your primitive data types (string, Boolean, etc.) or a class of objects such as Person. 

Imagine the method `greet(String name)`, publishes a message greeting the person on which it is called. If we wanted to publish a message greeting everyone, we can create a **Person** array, `Person[]`, which stores all the different instances of different types of people, such as **Student** (and it's subclasses) and **Lecturer**.

Since these different subclasses are being treated as the same superclass by being in this array, this is an example of **Polymorphism**