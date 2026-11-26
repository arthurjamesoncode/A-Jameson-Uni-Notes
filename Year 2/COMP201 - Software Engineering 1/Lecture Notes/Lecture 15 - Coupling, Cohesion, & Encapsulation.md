## What Makes a Good System
A good system usually has the following properties:
- Useful
- Useable
- Reliable
- Flexible
- Affordable
- Available

Modules can help us to make software which has the above properties by:
- Simplifying the development process, allowing quick creation of software which works (Affordable, Useable, Useful, Available)
- Separating functionality and allowing us to test specific parts (Reliable)
- Allowing us to extend functionality quickly (Flexible)

This lecture will be spent looking at design properties of modules which best allow us to meet the above goals of the system.
## Modules
In OO languages, a module is an object class. It defines:
- Some data (state)
- Some code (behaviour)

In other paradigms, modules may be other collections of functionality such as a group of related functions.

Modules are added to other modules to make components, which then work together to form a software system.

**Interfaces** define the features of a module upon which other modules may rely. They are abstractions of the module that show only the publicly facing parts of it.

**Encapsulation** is the OOP concept that bundles data and functionality together internally. Another tenant of encapsulation is that access to the internal state should be restricted. The interface dictates what information about this encapsulation the users of the module are allowed to know.

Any assumptions about the interface should be documented in the interface.

Any changes to the internals of a module should not require changing other parts of the system **unless it changes the interface**. This is the primary benefit of doing it this way.

>Interfaces have been seen in [[Lecture 13 - Interfaces]] of COMP122.

Below you can see an example java interface defining a the publicly accessible methods of a vector class
```java
/* A Java interface to perform mathematical calculations */ 
/* All Vector arguments should be normalized */ 

Public interface IVector { 
	public Vector(float x, float y, float z); 
	public float dotProduct(Vector inVector); 
	public Vector crossProduct(Vector inVector); 
	public void setVector(float x, float y, float z); 
}; 

public class Vector implements IVector { 
	private x,y,z; // private interface 
	//implementations of the above methods (ommitted)
}
```

This interface means that if we wanted to change the implementation of the method which computes dot product, we would not need to do anything except change the method itself. Anything which used that method could continue to use it.

This means that we can easily change logic to be better/more efficient, without worrying about what uses the code.

This change would be completely hidden from users of the module since they don't need to know this.

## Principles for Good Design
There are 5 principles that should be adhered to for good system design:
- Linguistic modular units
- Few interfaces
- Small interfaces
- Explicit interfaces
- Information hiding

We will now look at all of them in detail.
### Linguistic Modular Units
The principle of linguistic modular units is a principle of programming languages or design languages. It essentially means "Modules must correspond to linguistic units in the language used".

This is true inherently in languages like Java and Python, where modules would correspond to thing like classes and packages. 

Alternatively consider something like in something else like BASIC, where subroutines are called by giving a line number. It is not always clear that a section of code will be a subroutine and therefore modules don't necessarily correspond to linguistic units (subroutine) in the language.
### Few Interfaces & Small Interfaces
**Few interfaces** is a bit of strange principle since a system being large (and therefore requiring many interfaces) does not mean it is poorly designed.

What this principle actually states is that the total number of communication channels should be as **small as possible**.

What this means is that modules should be designed in such a way that they have to communicate with each other as little as possible.

The purpose of this is to minimise coupling and ensure that modules are as **autonomous** as possible.

One way of doing this is to wrap classes into packages, to limit scope. Theses classes can communicate with each other but a single **façade** interface is built to allow the rest of the program to interface with this package.

**Small interfaces** is a very similar principle. The main idea is that if two modules communicate, they should exchange as little information as possible.
### Explicit Interfaces
Explicit interfaces means that if two modules must communicate they should do so in a way that is clearly visible.

Essentially, the fact that they communicate should be obvious from the documentation of one or both modules. 

We have to be able to see what other modules may be affected when changing a module. This may be done using a **traceability matrix**, which is just a structured grid which shows which modules need to communicate with each other.
### Information Hiding
This principle means that all information about a module should be private to the module unless explicitly declared otherwise.

Essentially anything beyond the interface of the module should be hidden. This refers to hiding variables and methods as private, but also means that the details of how modules implement things should not be known outside of the module.

This is a core part of **encapsulation**
## Coupling
Coupling is a measure of how many connections you have between system components.

**Loose coupling** is preferred and means that changes to components are unlikely to affect other components. 

Having a lot of shared variables or information exchange can lead to **tight coupling** meaning that changes to one module are very likely to affect changes to another module. This can cause massive problems when trying to add or change functionality.

Occasionally tight coupling will be necessary, for example if performance is incredibly important and there is limited shared memory, but if possible tight coupling should always be avoided.

Loose coupling can be achieved with decentralised state and allowing components to communicate via parameters or message passing. Object Oriented systems are loosely coupled because they adhere to those ideas. OO languages can be used to build non-OO systems so be careful to adhere to the above design principles when building them.

Its worth noting that **inheritance** will inherently (see what I did there) introduce coupling between the super-classes and subclasses. 

>This is one of the reasons for the common OO design adage "Prefer Composition over Inheritance".
## Cohesion
Cohesion is a measure of how well a component fits together. 

What this means is that a component should implement a single **logical entity** or function. This is desirable because it means when a change has to be made it is localized in a single cohesive component.

There are many different levels of cohesion.

Weak levels include:
- Coincidental cohesion - Components are simply bundled together
- Logical association - Components which perform similar functions are grouped
- Temporal cohesion - Components which are activated at the same time are grouped

Medium levels include:
- Communicational cohesion - All elements of a component operate on the same input or produce the same output
- Sequential cohesion - The output for one part of a component is the input to another part

Strong levels include
- Functional cohesion - Each part of a component is necessary for the execution of a single function
- Object cohesion - Each operation provides functionality that allows object attributes to be modified or inspected

The concept of cohesion is not very well defined and can be difficult to classify. 

Inheriting attributes from super classes also weakens cohesion since now to understand a component you must also look at the super-classes. There are tools to assist with this such as object class browsers.

>This is another of the reasons for "Prefer composition over inheritance".
## Reusability
High cohesion, low coupling, and a well defined interface mean that a module is easier to reuse in other systems.

This can be great thing for expanding a system or creating new similar systems, but how feasible this is depends on the architecture of the system that the module is developed for.

Architectural decisions can be important for the design of all modules, and should therefore be decided early on. For example the module may sacrifice efficiency for reusability depending on if we want to use this module later on.

