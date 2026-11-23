## State Machine Models
Statechart diagrams, or state machine models, show the behaviour of a system in response to **external and internal events**. They are an integral part of UML.

They are commonly used in all types of systems including:
- Embedded Systems
- Data communication software

They show the systems responses to stimuli, consistent with the **event-action** paradigm, so they are often used for modelling real-time systems.

Statechart diagrams show system states as nodes, and events as arcs connecting the nodes. When an event occurs the system moves from one state to another.

An **initial state** is denoted by a solid circle. They are optional since sometimes the system can start in multiple places meaning that the initial state should be omitted.

A **final state** can also be used (if it makes sense for the system); this is denoted by a solid circle with a ring around it.

Every **other state** is represented with a rounded rectangle with a line separating the states two components:
- The **state name**
- A short description of the **action performed** in that state

You can look at an example state machine for a microwave below
![[microwave_state_model.png]]

To answer the question posed: It has no final state since it doesn't need one since the microwave can just continue to be used. This state machine doesn't model turning off and, even if it did, since it can turn on again it would just be another state, not the final state.

The stimulus/events of the system are shown by the table below

| Stimulus | Description |
| --- | --- |
| Half power | The user has pressed the half power button |
| Full power | The user has pressed the full power button |
| Timer | The user has pressed one of the timer buttons |
| Number | The user has pressed a numeric key |
| Door open | The oven door switch is not closed |
| Door closed | The oven door switch is closed |
| Start | The user has pressed the start button |
| Cancel | The user has pressed the cancel button |
You could also complement a state machine model with a similar table showing the states, although that is not strictly necessary.
## More Complex State Charts
We can advance past the simple state machine showed above by adding some more complicated notation.

We can allow decomposition of the model into sub models, by drawing boundary boxes around certain parts of the state machine.

We can also use **guards** to restrict if a state can be moved to based on some condition. This notation also more closely follows code, so now our **label** can be the name of the method (or event) that is used to transition state.

You can see all of these elements on the UML statechart diagram below
![[uml_statechart.png]]

You can also put actions after an event, separate from the state by using a slash /.

For example consider the simple statechart below
![[event_action.png]]

Other things of note are:
- State machines often have an idle state where the process isn't active
- Every state (except final) must have some exit
- Using multiple state charts keeps the design simple, you do not need to have a state chart as a sub state of another chart
- The system can be described by multiple state machines running concurrently
## Finite State Machines
Finite state machines, or finite state automata, are a formalisation of the state chart diagrams we have looked at.

They are a model of computation consisting of:
- A set of states
- A start state
- An input alphabet
- A transition function (which maps input symbols and current states to a next state)

Computation begins in the start state with an input string and then changes to the new states depending on the transition function.

The states define behaviour and may produce some actions. The state transitions are movement from state to the next. 

There are rules and conditions (similar to guards) that must be met to allow an input event to trigger a state transition

Input events trigger state transitions based on the rules.

Certain states may be designated as **acceptance states**.

Lets look at an example modelling of a spell checker using a finite state machine.

![[fsm_spell_check.png]]

This is a very simple spell checker that can check for the words:
- All
- Alp
- Alpine
- Alligator

The FSM forms a tree structure where the input of a new letter moves it along. If the input is consistent with one of the words above then the state machine is in an acceptance state, otherwise, it is not and would display an spelling error.
## Semantic Data Models
Semantic Data Models are used to describe the logical structure of the data processed by the system.
## Entity-Relation-Attribute Model
The **Entity-Relation-Attribute** model sets out the entities in the system, the relationships between them and the attributes that they have. This is widely used in database design since it can be easily implemented using relational databases.

Below you can see an example of how a diagram of this model might look
![[entity_relation_attribute.png]]
### Object Models
Object models describe the system in terms of object classes.

An **object class** is an abstraction over a set of objects with common attributes and operations provided by each object.

There are a number of object models which may be produced, some of which will be covered in much greater detail later in the course, including:
- Inheritance models
- Aggregation models
- Interaction models

These types of models are natural ways of reflecting real world entities that the system manipulates but the more abstract entities are much more difficult to model using this approach.

Recognising object classes is a very difficult problem that requires a deep understanding of the application domain, but the object classes reflecting domain entities can be reused across many systems.
### Unified Markup Language (UML)
UML is an effective standard for object oriented modelling. UML will be studied in greater depth in later lectures, but is earning an early mention here.

It contains many different types of diagram that can be used to model systems (some of which have been seen already) including:
- Use-Case Diagrams
- Class Diagrams
- Sequence Diagrams
- Statechart Diagrams
- Deployment Diagrams
- Etc. 

The notation for class diagrams, used to show object models, is:
- Object classes are 3 section rectangles where
	- The name is at the top
	- The attributes are in the middle
	- The operations are at the bottom
- Relationships between the classes are shown as lines linking objects
- Inheritance is referred to as generalisation as is shown "upwards" rather than "downwards"
### Data Dictionaries
A data dictionary is a list of all the names used in the system models. It also includes descriptions of all the entities, relationships, and attributes.

It is a store of organisational information so that all data is stored in one location. It can also be used for **name-management** to ensure that all the names used in the system are consistent and do not clash.

![[data_dictionary.png]]