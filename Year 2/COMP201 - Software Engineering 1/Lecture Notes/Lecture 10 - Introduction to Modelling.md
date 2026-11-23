## System Models
System models are abstract descriptions of systems used during the requirements analysis process.

Its important for user requirements to be written in such a way that non-technical domain experts can understand them. For example, by using natural language. This requires something other than detailed system requirements because these are very technical in nature.

A common approach is to document the system as a set of **system models**, graphical representations of the system which describe business processes and the system to be developed. These act as a bridge between the requirements analysis and the design process.

Models help the analyst to understand the functionality of the system and are used to communicate with customers. Different models present the system from different perspectives:
- **External perspective** - Shows the systems context or environment
- **Behavioural perspective** - Shows the behaviour of the system
- **Structural perspective** - Shows the system or data architecture

Below you can see an example model of (some of) the data in a school system using UML (unified markup language)
![[model_example.png]]

These sorts of models tend to be easier to understand at a glance compared to more verbose natural language descriptions. They also tend to leave out many unnecessary details and focus on what is important. 

Exactly what/how much is important depends on the specific purpose of the model:
- System **representations** should maintain all the information of a system
- An **abstraction** is a deliberate simplification which picks out only the most important characteristics
Depending on the model, different things will be abstracted in different ways.

There are some problems with system models as well:
- They do not model non-functional requirements of a system
- They *can* produce too much documentation
- They can sometimes be too detailed and difficult for users (defeating a lot of the purpose of using them in the first)
- They can be costly to produce when there is pressure to complete the project quickly

Because of these weaknesses there are two commonly used approaches:
- Lightweight UML - Which is focused mostly on data modelling first
- C4 Lightweight - Which is an agile friendly modelling
## Model Types
There are a number of different model types that we need to know about.

Some ones not covered in detail are:
- Composition Model - Shows how entities are composed of other entities
- Classification Model - Shows how entities have common characteristics

We will now spend time going over some other models in more detail. Specifically we will cover **context models** as well as two types of **behavioural models**:
- Data processing models
- State machine (or stimulus/response) models
Both of the above models are needed to describe the systems behaviour.
### Context Model
Context models are used to illustrate the boundaries of a system. Identifying these boundaries is not always a straightforward task.

Often social and organisational concerns affect the decision on where the position or how to identify the system boundaries.

Context models are often done in the form of an **architectural model** but with a scope external to the system. This shows the system and its relationship with other systems.

Take the following architectural model for an ATM system![[atm_architectural_system.png]]

The centre box is the boundary for the ATM itself, and the rest of the boxes represent other parts of the bank ecosystem that the ATM must interact with.
### Data-Processing Models
Data-processing models use **data flow diagrams (DFDs)** to model the system's data processing. These show the processing steps as data flows through the system.

These are very important as part of the analysis process, and should:
- Have simple and intuitive notation
- Show end-to-end processing of data

DFDs track and document how the data associated with a process moves through the system. This is helpful for analysts to develop an overall understanding of the system.

DFDs can also be used to show the **data exchange** between a system an other systems in its environment.

Developing data flow diagrams is usually a top down process. The overall process we wish to model is evaluated before we consider sub processes. Each transformation in a DFD represents a single function or process. This shows end-to-end processing and is very useful as part of requirements analysis.

Below you can see a context DFD showing all of the inputs/outputs a drinks machine controller receives/sends to the other sub systems of the drinks machine.
![[DFD_context.png]]

Below you can see a lower level DFD where the drinks machine controller has been broken down into many of the sub processes
![[DFD_lv0.png]]

Below you can see an even lower level DFD that breaks this operation control process down into its sub processes

![[operation_control_level_1_dfd.png]]

**Note on DFD levels**: The labelled levels for the DFD diagrams from the slide are pretty confusing, so I will break them down here.

As you start to model at a lower and lower level, number of the level gets bigger. 
- Level 0 DFDs are typically context diagrams with the system being represented as a single process
- Level 1 DFDs typically break the system down into its principle sub processes
- Level 2 DFDs typically break a specific sub process down into its sub processes
- etc.
This forms a tree of DFDs.

The slide labels differ from this definition slightly, he simply labels what would usually be level 0 as a context diagram, and labels what would be level 1 as level 0 and level 2 as level 1.

This only makes sense if you change the level of the green background diagrams to be in relation to **operation control** specifically, rather than the whole drinks system.

All in all, I doubt we will be assessed on labelling or recognising the level of the diagram but this confused me so I thought I should make a note of it.

