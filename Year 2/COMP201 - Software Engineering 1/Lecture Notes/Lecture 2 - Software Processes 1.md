## What is a Process?
A process is any number of steps that we need to do something.

If we think about building a house, for example, we need to:
- Figure out what to build
- Figure out where to build
- Figure out how much it will cost
- Get the money
- Design the build
- Get permissions
- Build the foundations
- Build up from the foundations
- Fully test everything
- Make sure it looks right after every step
- Show to customer
- Adjust to feedback

That full list applies to software.

The other important of a process is the order of the steps. You wouldn't put up the drywall before you install the wiring for example.

This lecture will go over examples of software development processes that are used to ensure we develop software in a systematic and relatively efficient way.

Any process will:
- Prescribe all major activities
- Uses resources and produces products, either intermediate or final
- May include sub-processes
- Orders all activities into a sequence
- Applies constraints to activities based on availability of resources

Below you can see a basic flowchart of the process to design and build a house
![[house_process.png]]
## Software Processes
A process that involves building of some product is called a **life cycle**.

For the **software life cycle** we have the following set of activities:
- Specifying,
- Designing,
- Implementing and,
- Testing
Software systems.

Software is somewhat unique compared to buildings since:
- It can be changed at any time
- It is often required to change after construction

This is good because it means that software can almost always be improved without limit but can lead to some problems:
- Software gets faults as it evolves
- Software cost is hard to manage
- Problems with UX and expectations
- Software complexity grows exponentially with size

Some process models include:
- The Waterfall Model - Used in classic engineering like bridge building
- Evolutionary Development - Used for product engineering
- Agile and Scrum - The modern standard for software engineering
### Waterfall model
The waterfall model describe a development process where every step is completely distinct and falls after the prior one.

You can see this pictured below
![[waterfall_model.png]]

This model partitions the project into distinct stages. The prior steps must be fully complete before you continue with the next step.

The limit of this model are that it's very difficult to respond to changing customer requirements. This means that the model should only be used when the final requirements are well understood.

This is almost never the case in software, but this model is widely used in:
- Classic engineering
- Aerospace
- Military

While this is barely used in the software industry, it does provide some key lessons:
- Each stage of it is an important step
- The order of the steps is very important
- It's easy to remember
### Evolutionary Development
Evolutionary development is a process that is defined by:
- Developing an initial implementation
- Exposing it to the user
- Refining it based on their response

Exploratory development:
- Objective is to work with customers and to evolve a final system from an initial outline specification.
- Needs to start with well understood requirements
- The system then evolves by adding new features as they are proposed by the customer
- Or removing features that are deemed not to work

Part of evolutionary development is exploratory development.

You can see the flow of this process pictured below
![[evolutionary_development_model.png]]

The main problems of this process are:
- There isn't much **processes visibility** - I.e. it's hard to understand how work/data/code are moving through the workflow
- Can result in systems being poorly structured

This process can be used in all types of systems but is rarely used for safety critical systems.

In reality this type of development is a part of all modern development. Modern processes tend to mix this with a bunch of other ideas.

Sometimes the spec would be mostly finished at the start and then added to as the project proceeds. 

The evolution cycles could be pre-determined to work on different use cases. For example if there were 500 use cases:
- In phase 1 develop use cases 1-50
- In phase 2 develop use cases 51-100
- In phase 3 develop use cases 101-200
- In phase 4 develop use cases 201-500
## Agile Development
Agile development is a group of lightweight approaches to software development. Examples include:
- Scrum
- XP

It focuses on:
- Code development as code activity
- Test driven development 
- Pair programming (often)
- Iterative development
- Self-organised teams (people sign up for tasks)

**Scrum** or incremental development, means that rather than delivering the system as a single delivery, the development and delivery is broken down into increments, called sprints. Each sprint delivers part of the full functionality.

Different requirements are prioritised and the highest priority ones are included in the early sprints.

Once the development of an sprint is started the **requirements are frozen**, although requirements for future sprints can still change.

The advantages of Scrum are:
- Value to the customer is delivered with each sprint so system functionality is available earlier
- Early sprints act as a prototype to help elicit requirements for later sprints
- Lower risk of overall failure
- The most testing goes to the highest priority system services.

In reality, most software processes include both:
- Prototyping
- Iterative Building

This is because it reduces the risk of making the wrong product and allows the software to undergo more testing. It also means that the product is viable from an early stage.

It's important to remember that what process is preferred depends heavily on context. There will be different emphasis put on building a system for a nuclear power station than a website for instance.

In all cases, the specification is the most important step of any software process because everything else comes from that.