## Software Design
The problem of software design is essentially to derive a solution which satisfies all specified requirements.

This can be a problem if you have a large number of developers and a huge requirements specification. How do you break up the work in a structured controlled manor?

There are a few key things that must be done:
- Each developer must not overlap/duplicate functionality
- Interfaces between common elements must decided
- Database formats must be agreed

The end goal is to design software which is:
- Simple
- Understandable
- Flexible
- Portable
- Re-usable

To make complex ideas/implementations simple relies on a lot of **abstraction**.

In practice, design and implementation are very interlinked. The software is often designed while being coded and the design document doesn't reflect the final product. 

This lecture will go over some ways to consider design as part of the software development lifecycle.
## C4 Modelling
C4 modelling is a simplified system architecture modelling system suitable to Agile environments. There are 4 different levels of model.

Level C4 is the code level. UML is used to model the code.

We will go through the other levels now.
### C1 Diagrams - Context View
C1 modelling is the context model. This is very similar to the level 0 DFDs we saw or other context diagrams.

![[C1_model.png]]

This view can model other systems too, not just the one being developed. The external systems are shown as software systems not Actors as in UML.

A **persona** represents a user role, actor, or human user.

C1 diagrams are good for customers and developers. They shouldn't show much technical detail.
### C2 Diagrams - Container View
In C2 Diagrams the software system being modelled is broken into interacting components called containers.

![[C2_diagram.png]]

Containers have typically have a web interface using JSON to transfer requests and responses. 

They can be located in different physical systems and therefore can support features such as:
- Scaling
- Fail Over

They can be implemented internally or by third parties. For example the Amazon S3 store in the diagram above, but in both cases inside this context they are considered to be controlled by the software system.
### C3 Diagrams - Component View
C3 Diagrams break the containers down further into a series of components. These components will be made up of code, and exactly how they will look will depend on the technology used to create them.

![[C3_diagram.png]]

In **OOP languages** components are made up of classes and interfaces. They could be **Façade code** (simplified entry point class, that is used to interact with a more complicated group of classes) wrapped up in a package or DLL. Typically each component will have a single interface class which other components can interact with.

In **Procedural programming languages** a component could be a number of code files in a particular directory.

In JavaScript, a component could be a JavaScript module which is made up of objects and functions.

Components should be as modular and reusable as possible.
### C4 Diagrams - Code View
C4 Diagrams are used to model the code itself. They tend to use UML to model classes as collections of attributes and methods, and show the relations between these classes.

Typically the diagrams themselves show the names of classes, attributes, and methods but don't show details of their implementation. This may be documented elsewhere. The relations between classes are also shown through a number of verbs.

![[C4_diagram.png]]

C4 is usually only included for the most complex of services and is often generated automatically from the source code.
## Stages of Design
Using the C4 approach with lightweight UML, we work from top level C1 down to C4:
- Start with the context diagram (C1) and work out the system boundary
- Take the system and break it down into a series of containers (C2)
- Break the containers down into components (C3)
- Write and possibly model the code (C4)

The containers need to have:
- A clear set of responsibilities
- Defined interfaces
- Defined performance (Non-Functional Requirements)

This gives rise to various phases of the design process:
- Architectural Design - Identifying containers
- Abstract Specification - Specifying container responsibilities
- Interface Design - Describe container interfaces
- Component Design - Decompose containers into components
- Data Structure Design - Design data structures to hold problem data (database schema and class structure)
- Algorithm Design - Design algorithms for problem functions
## Modular Programming
It is very important to keep containers and components modular. This is key to cheap (in terms of time as well as resources), high quality software.

The goal of system design is to recognise:
- What the modules are
- What the modules should do
- How the modules interact with each other

For modularity to bring benefits, it is important to ensure that:
- Modules are autonomous
- Modules are coherent
- Modules are robust

Autonomous means that modules should be able to function independently without relying on the state or inner workings of another module.

Coherent means that everything included in the module belongs together.

Robust means that the module handles unexpected inputs, edge cases, etc. It shouldn't rely on the user to be validating inputs for example, it should decrease the friction on the users side as much as possible.
## Views of Programs
Functional decomposition is a core of the most obvious design methods. This leads to programs in which procedures represent distinct logical functions in a program for example:
- "Display menu"
- "Get user option"

This is called **procedural abstraction**.

There is also the view of a programs as functions $f:I\to O$ where $I$ is a set of legal inputs and $O$ is a set of legal outputs. 

There are functional programming languages which directly support this style of programming such as:
- ML
- Miranda
- LISP
- Haskell

This is well suited to some domains, such as a compiler, but not quite as well suited to other non-terminating systems.

Another common view is **Object-Oriented Design** in which the system is is viewed as a collection of interacting objects. The system state is decentralised and each object manages its own state.

This conflicts with functional programming which does not have any internal state.

