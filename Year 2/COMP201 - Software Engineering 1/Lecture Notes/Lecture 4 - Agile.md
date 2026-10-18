## Heavyweight VS Agile Processes
By the 80s and 90s Software development had become split between lightweight and heavyweight styles.

Heavy weight systems were used for large institutional information systems and they:
- Used waterfall approach with rigid steps
- Were slow and cumbersome
- Were heavily dependent on paperwork and diagrams
- Had documentation and code which were entirely separate

Lightweight systems were used for games and smaller projects and they:
- Used a more informal ad hoc method. E.g. code was not always formally designed for example
- Focus on coding development, documentation existed purely to support this
- Had faster development
- Had more varying quality

Agile is the name for the collection of lightweight frameworks that people started to use.

The NHS, for example, requires a very rigorous specification. There are many different specification documents for NHS systems. Due to the high stakes of what could happen if something goes wrong it makes sense that a strict, heavyweight approach for this kind of system is the only suitable one. The other part of this is that is very important that it complies with the existing legal frameworks.

Some examples of Agile alternatives are:
- XP Extreme Programming
- SCRUM
- Kanban

These are the types of processes which often make more sense more less significant products than the NHS, and are the majority of what will be studied in this course.

## Agile Values and Principles
Agile development started to become mainstream after the publication of the Agile manifesto in 2001 at a conference of 17 software developers. This manifesto wasn't a detailed guide on how to develop software, but just laid out the general values that they thought were the most important when it came to developing software:
- Individuals and Interactions over processes and tools
- Working software over comprehensive documentation
- Customer collaboration over contract negotiation
- Responding to change over following a plan
This is what forms the core of the agile methodology.

There are 10 basic agile principles:
- Customer satisfaction by rapid delivery of useful software
- Welcoming changing requirements, even late
- Working software is delivered frequently
- Working software is how you measure progress
- Sustainable development or being able to maintain a constant pace
- Face to face conversation is the best form of communication
- Projects are built around trusted, motivated individuals
- Constant attention to technical excellence and good design
- Simplicity
- Self organizing teams
- Adapting to changing circumstances
## Extreme Programming & User Stories
Extreme Programming is one agile methodology categorised by a few things:
- Requirements are expressed as "user stories"
- Pair programming - One person types the other watches, discusses and assists
- Test driven development - Tests are written before the code
- Program must pass all tests before it is integrated and a new release is built
- The new release then becomes the working system

"User Stories" are short descriptions of program functionality with allows the user to do something specific. Good user stories are:
- Small
- Independent
- Negotiable
- Valuable
- Estimable
- Testable

An Epic is an amount of work which is larger than a user story and is made up of multiple user stories. These can be broken down into smaller units.

**Small**er modules are easier to estimate and less risky. They also allow you to measure progress clearly. This is on top of keeping code simpler, coherent, and making tests easier.

**Independent** means that each story shouldn't rely on another user story. This has a few benefits:
- Stories can be developed in parallel meaning more developers can increase the speed
- Ensures less code coupling, making it easier to amend or change

For example it makes it simpler when you can separate functionality such as:
- Forgot password
- Login
Despite this functionality being related.

**Negotiable** simply means that aspects of a user story can change or be removed. This could be done to:
- Make the story quicker to implement
- Make the story more useful
Sometimes a bit of functionality can be difficult to implement but also not that useful. In cases like those it makes more sense to scrap them in favour of other more important functionalities.

**Valuable** means that the user story should show value to the stakeholder. It can be worth giving a metric that shows the value of each story. This can be used to prioritise different stories:
- Give every story a value from 1-10
- 10 is the most important
- All core features will get a 10

**Estimable** stories are important for scheduling. In general highly estimable stories are:
- Shorter
- Don't rely on a lot of unknown code
- Well understood by the the developer
Splitting big stories down can make this much easier.

A good way to help estimate stories is to use **story points**. This is a relative estimation time. Essentially 2 stories that has 5 points should take the same time if:
- They have the same team
- The same conditions
Given the above a story that has 10 points should take twice the time of a story with 5 points.

**Testable** means that there has to be a simple, objective test to show that something serves it's purpose. For a lot of conditions automated unit-tests and integration tests can do this well, but for other conditions we might have to do something different.

A condition like "The login screen must look nice and be liked by many users" is not very good because it's hard to test. However "The login screen must score better than 7/10 when we assess the aesthetic of the screen using a random group of 20 users" is much easier to test.
### Format of a User Story
User stories can be formatted using the following:
	"As a \[user\], I want \[goal\] so that \[reason\]"

For example
	"As a user closing the application, I want to be prompted to save anything that has changed since the last save so that I can preserve useful work and discard erroneous work"

User stories can be used to inform how the UI/UX should look like, and how it should be produced.

For example
	As a registered user of the system I want to be able to login to the system so that I can access my records securely.
The above could inform the following UI/UX

![[Login-UI-UX.png]]