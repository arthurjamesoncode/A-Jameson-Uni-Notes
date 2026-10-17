## Software Specification
Software specification is the process of establishing what services are required and the constraints on the system's operation and development. 

The main part of this is **requirements engineering**, which has it's own process:
- Feasibility study - Discovering/Deciding what is possible
- Requirements elicitation and analysis - Deciding what the requirements should be
- Requirements specification - Writing up the requirements
- Requirements validation - Ensuring that the requirements fit the needs of the user

You can see the full requirements engineering life cycle below
![[requirements_engineering.png]]

It's very important that the resulting requirements document is the **single source of truth** for the requirements for the process.
## Software Design and Implementation
Software design and implementation is the process of converting the system spec into an executable system.

Software design should result in a design documents which illustrates a software structure that realises the spec. It could include:
- Designing the database
- Designing the website
- Designing data structures that will be used
- Choosing communication protocols

Like the spec it's important for the design document to be a **single source of truth** for the project.

Implementation is the process of turning the structure of the design into an executable program. In reality, the design of something will change based on things discovered by implementing parts of it, or attempting to. As a result both of these parts of the process are inter-leaved.

When making a change to the design, it's very important to continue to update this **single source of truth**.

We will now go through the main activities that are part of the **design process**.

**Architectural Design**:
- The structure of the sub-systems which make up the system. Their relationships should be identified and documented.
**Abstract Specification:**
- For every sub-system, an abstract spec of its operational constraints and the services should be produced.
**Interface Design:**
- For each sub system, the way it interacts with other sub-systems should be designed and documented. The interface should be unambiguous. A formal spec may be used, this will be studied later on.
**Component Design:**
- Services are allocated to components and the interfaces of these components are designed.
**Data Structure Design:**
- The data structures used in the system implementation are designed in detail.
**Algorithm Design:**
- The algorithms used in components to provide services are designed and specified.

Two extreme design philosophies are:
- **Data driven design**
- **Responsibility driven design**

In data driven design:
- We start by looking at all the data the system must handle
- Describe how the data is related and how it can be manipulated
- Describe how each data item can be operated upon

In responsibility driven design:
- We start by looking at the functions of the system
- Break these functions down into smaller functions
- Consider the data each function needs to support its action
### Example Design
Consider the scenario of developing a Coffee/drinks machine software. 

What are the major sub-systems?
- Graphical display
- Cash handling
- Accounting
- Safety system
- Recipe handling
- Stock control

Now lets look at one of these and come up with an abstract specification. Lets choose stock control:
- Needs to be able to track the weight of different ingredients
- Needs to be able to signal to an engineer/maintainer when a certain stock item is low
- Needs to interface with the graphical display to mark certain items as out of stock or in stock
### Design Methods
Design methods are systematic approaches to developing a software design.

The design is then documented as a set of graphical models. For example:
- Data-flow model
- Entity-relation-attribute model
- Structural model
- Object models
- A state transition model showing system states and triggers 
We will study these in detail in later lectures.
## Programming and Debugging
Programming and Debugging consist of translating a design into a program and removing errors from that program.

This is a personal activity. There is no generic programming process but there are good programming practices and organisational standards to be followed.

Part of programming is to test your program. The point of which is to discover faults in the program and then remove these faults in the debugging process.

Good programming is iterative. It follows a cycle of:
- Write a small piece of code
- Test it
- Commit it to version control
- repeat.

When testing code there are many different stages, which all test a different amount of the code. You can see these pictured below.

![[testing_process.png]]

**Unit testing**
- Tests individual components
**Module testing**
- Test related collections of components which depend on each other
**Sub-system testing**
- Modules are collected into sub-systems and tested. The focus is testing the interfaces of the different modules.
**System testing**
- Testing the whole system as a whole, including emergent properties of the system (such as speed)
**Acceptance testing**
- Testing with customer data to see that the system is acceptable