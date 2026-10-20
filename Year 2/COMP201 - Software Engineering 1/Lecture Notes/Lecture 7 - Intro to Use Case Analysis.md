## Use Cases & User Stories
Use Cases and User Stories are two different ways to capture requirements.

User stories are good for:
- Capturing requirements quickly
- Prioritizing backlog items
- Discussing with the team
As a result they are very good for customers

Use Cases are good for mapping out:
- Complex workflows
- Edge cases
- Error handling
- System integrations
After the user story is accepted. This makes them good for developers.

User stories follow the format:
	"As a \[user\] I want to \[action\] so that \[result\]."
For example:
	"As a returning user, I want to log in using my username and password to access my account. The login page should display clear labels for username and password fields."
## Use Cases
Use cases are more in depth:
- A **use** is how the system is used
- A **case** is an example scenario
- Used to model **functional requirements**
- Only show the external view, not concerned with implementation
- Shows the systems relative to different users of the system, which are called **actors**.

Use cases are a scenario based technique in UML which:
- Identify actors in an interaction
- Describe the interaction itself

A complete set of use cases describes every possible interaction in a system.

**Sequence diagrams** may be used to add detail to use cases by showing the sequence of event processing in the system. These will be studied later.

In a **use-case diagram**, an **actor** is a user of the system. This means something external to the system, but not necessarily a human, which acts in a particular role.

A use case is a task which the actor needs to perform with the help of the system.
## Actors
An actor is anything external to the system which the system interacts with. 

Could be human:
- Customer
- Player
- Driver
- etc.

Could be non-human:
- Sensor
- Payment service
- Geo location
- Robotic arm
- Email server
- AI agent
## Documenting Use Cases
The details of each use case should be documented by a use case description.

For example:
	"Print Receipt - A customer has paid for an item via a valid payment method. The till should print a receipt indicating the current date and time, the price, the payment type, and the member of staff who dealt with the sale.
	\[Alternate Case\] - No Print paper available - Print out "Please enter new till paper" to the cashier's terminal. Try to print again after 10 seconds."

Alternate cases are used when something could go potentially wrong and they denote another course of action.
## ATM Example
Consider an ATM machine.

In this case the actors could be:
- Customers
- Bank Staff
- ATM service engineer
- API from different banks allowing other cards

Some use cases could be:
- Withdraw cash
- Check balance
- Add cash to machine
- Check security video recording

We can connect all of this into a **use case diagram** which shows all of these actors and their relevant use cases.
![[ATM_use_cases.png]]
## Use Case Diagrams
We have a simple example **use case diagram** above for our ATM system, but we're going to go into a bit more depth on them now.

We denote the **system boundary** by drawing a box around all of our use cases. This separates the **actors** from the **use cases** in a visually distinct way.

We can denote **inheritance** to show that one actor should be able to do everything another actor can do by drawing an arrow from the more privileged actor to the less privileged actor. 

So if we wanted to say that a service engineer can do everything the bank staff can do we could show that like this:
![[use_case_inheritance.png]]

We can also draw lines between use cases to show that they are related. For example:
- If a use case includes another use case - One use case is needed for another to work
- If a use case extends another use case - One use case is needed as an optional outcome due to something happening

We show these relations using labelled, dotted arrows:
![[use_case_relations.png]]

Note the directions of the lines, each use case points to the ones that they **include** or **extend**:
- View Balance, Withdraw Cash, and Print Statement all include Authenticate Customer so they all point to it
- Re-Enter Pin and Reject Transaction both extend Authenticate Customer so they point to it.

There's a note in the lecture slides to be careful when including these advanced features in UML diagrams. This is because using these features can make them harder to walk through with non-technical customers and therefore some of the benefit of UML diagrams is lost.
## Use Case Template
You can structure use cases to follow the following template. After each section description there is a simple example.

ID 
- Short ID (useful for diagrams and reference) - UC1 
Name 
- Full name - Login 
Description 
- Full description User login 
Pre-condition 
- What must be true before the use case can proceed - System is online 
Event flow 
- Flow of behaviour that makes up this use case, can include other use cases - user enters username + password, if credentials correct user is authenticated 
Post-condition 
- Possible change of internal state - authenticated=true if username, password correct, user account locked if wrong password 3 times
Includes 
- What other use cases are used 
Extensions 
- Optional behaviour 
Triggers 
- What makes this use case happen

Note that use cases **DO NOT** describe **internal behaviour** and that they **MUST** describe behaviour involving **external actors**.

Below is an example use case from the ATM example.![[use_case_example.png]]

There are more examples in the slides for the lecture.