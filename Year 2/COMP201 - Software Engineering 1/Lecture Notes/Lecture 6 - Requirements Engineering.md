## Requirements Engineering
**Requirements** are all the things that a system must be capable of in a general AND specific sense.

We define the requirements for our systems in terms of **Acceptance criteria** which must be:
- Testable
- Relevant
- Focused on the outcome, not the method

One requirement may through up a number of acceptance criteria, and some requirements may be difficult to define completely in these terms.

**Requirements engineering** is the process of establishing:
- The **services** that the customer requires from the system
- The **constraints** under which is operates and is developed

Requirements are the descriptions of the services and constraints generated during the requirements engineering process.

We need requirements because to ensure that a software solution correctly solves a problem we must:
- Fully understand the problem
- Discover why the problem needs to be solved
- Determine who should be involved
Poorly defined requirements can be very costly in both financial terms as well as added time.

A single requirement could be:
- A high level abstract statement of a service or constraint
- A detailed mathematical functional explanation
## Requirements Analysis Process
Determining requirements is generally an iterative and top down process. There are always multiple versions of requirements.

Large scale services are defined and then broken down into component parts. Acceptance criteria is written for each individual component part.

Acceptance criteria is formatted into:
- Given - The pre-condition for the test
- When - An event that happens
- Then - What the system does

For example for an alarm clock we could have the acceptance criteria:
	"**Given** that at least one alarm has been set, **When** the current time is equal to one of the alarm times and the device is not in silent mode **Then** start sounding the alarm and make the alarm active"

For an example of how we can iterate on requirements you can see:
- The system will support a wide range of the most commonly used graphics file formats (high-level)
- The system may support the following file formats: png, jpeg, tiff and gif (detailed user)
- The system may support the following file formats: png, jpeg, tiff and gif, to a maximum resolution of 1024x1024 pixels (system) 
- The system may support the following file formats: png, jpeg, tiff and gif, to a maximum resolution of 1024x1024 pixels and a maximum file size of 20 megabytes with these parameters being extendable easily using plug ins (software)
## Types of Requirement
There are a ton of different types of requirement.
- **User requirements** which are written for customers - Statements in natural language plus diagrams of the services provided by the system and its operational constraints.
- **System requirements** which are written as a contract between client and contractor - A structured document setting out detailed descriptions of the system services.
- **Software specifications** which are written for developers - A detailed software description which can form the basis of a design or an implementation.

For some examples:

**User requirement:**
- We need to be able to spell check documents in multiple languages

**System requirement:** 
- The system needs to be able to spell check documents and provide autocorrect facilities. 
- There will be support for the following languages, English, Chinese, French and German 
- Will have plug in support for other languages

**Software specification:** 
- CheckResult spellCheck(String word, Dictionary dictionary)
	- Word is defined in UNICODE formatted string
	- The Dictionary structure is defined in S.1.2
	- The CheckResult is defined in S.1.3 and contains a flag if the word has been found or not, plus a Vector object containing a list of possible other word suggestions depending if the word has been found or not
	- spellCheck will ideally use Hashing tables to improve code efficiency
	- ……

Specification focuses on the service provided. They do not specify a particular programming language they simply focus on interface and behaviour. The specification should be detailed enough to act as a base for testing.

Given a complete specification and tests which cover all of it, it can be guaranteed that the product is of high quality.
### Functional Vs Non-Functional
Every requirement can be considered either **functional** or **non-functional**.

Functional requirements describe services that the system should provide such as:
- How the system should react to inputs
- How the system should behave in certain situations

Non-functional requirements describe the constraints on the services or functions offered by the system such as:
- The system should take less than x time to perform a service
- The system should be able to handle 1000000 users concurrently

Domain requirements can be either functional or non-functional and they come from the **domain of the problem** such as:
- Medical
- Banking
These requirements can often be associated with regulations or other needs specific to that domain.
## Requirements Precision
Problems can happen when requirements are not precisely stated. For example ambiguous requirements may be interpreted in different ways by developers and users. 

Consider a requirement which states "There should be a mechanism in place for the user to securely recover their password". This could mean either:
- A way to view the users password after going through an authentication procedure
- A way to reset the users password through an email link

If that requirement was signed off on by a customer, there could be a miscommunication about what the system actually needs to be capable of, and therefore time could be wasted developing a feature which was not wanted/needed.

Before development, requirements should be defined as precisely as possible in a way that can be tested.

In principle requirements should be:
- Complete - Include descriptions of everything required
- Consistent - Not contain any conflicts or contradictions in the descriptions of what's needed

In practice it is very difficult (and sometimes even impossible) to produce a requirements document which is both complete and consistent.
## Non-Functional Requirements
As discussed above, non-functional requirements are requirements of the system that don't come from **what** the system should be able to do. These typically define system properties and constraints such as:
- Reliability
- Response time
- Storage Requirements
They are typically emergent properties of the system.

Another type of non-functional requirement are **process requirements**, which mandate a specific way of making the product such as:
- Development methodology
- Programming language
- etc.

Non-functional requirements can be more important than functional ones. If some of these aren't met, the system may end up being completely useless.

Requirements like this can be classified in 3 ways:
- **Product requirements** - Specify that the product should behave in a particular way
- **Organisational requirements** - Specify organisational policies and procedures
- **External requirements** - Arise from factors external to the system such as legislation and compatibility with other systems

For example:
	"All encryption should use the Advanced Encryption Standard" and
	"The system should respond to a user's request for information in less that 0.1 seconds during peak time and 0.01 seconds during normal time"
Are both **Product requirements**.

Non-functional requirements may be difficult to state precisely and, as seen above, imprecise requirements can be difficult to verify.

As a result we differentiate between:
- Verifiable non-functional statements - A statement using some measure that can be objectively tested
- Goals - A general intention of the user/customer such as "easy to use"

System goal:
	"The system should be easy to use by experienced controllers and should be organised in such a way that user errors are minimised."
Verifiable non-functional requirement:
	"Experienced controllers shall be able to use all the system functions after a total of two hours training. After this training, the average number of errors made by experienced users shall not exceed two per day."

There are a number of ways that we can measure different properties that we will want our system to have. We can see a table of some of these below.

![[requirements_measures.png]]

It's also common to have conflicts between different non-functional requirements in a complex system. For example:
- Username/Password mechanism should be easy for user to use 
- All passwords must be hard to guess and ideally require upper/lower case letters and special symbols to ensure high security

When this is the case it the problem becomes about prioritising which is more important, and how much of each you can still satisfy. For example in this case:
- Security is more important and should be satisfied
- To ensure ease of use you can ensure compatibility with common password managers, or saving passwords on non-public machines
Neither requirement is dropped completely, but one is slightly reduced in priority.
## Domain Requirements
Consider a healthcare information system, a **domain requirement** of this system is:
	"All information systems should be compliant with the data protection act, Health and Social Care Act 2012, NHS Act 2006, etc."

These requirements come with a couple of problems:
- Understandability
- Implicitness

Domain requirements are expressed in the language of the application domain. This is not always understood by software engineers. Considering the above, a software engineer may not fully understand the contents of the NHS Act 2006 for example.

Implicitness means that the requirements are often not specified explicitly. This is because domain specialists understand the area so well that they don't think to specify them explicitly leading to further problems of software engineers understanding the problem.
## User Requirements
User requirements should describe functional and non-functional requirements so that they are understandable by system users who don't have detailed technical knowledge.

They are defined using natural language, tables and diagrams so that non-technical clients can better understand the proposed requirements and provide input and point out potential problems.

There are some problems with using natural language:
- Lack of clarity - It's hard to be precise without making the document difficult to read
- Confusion of functional and non-functional requirements - mixing both in the same document
- Requirements amalgamation - Several different requirements can be expressed together leading to problems when it comes to testing and debugging

When writing requirements it's important to have a **standard format**. Language should also be used in a consistent way:
- **shall** should be used for **mandatory requirements**
- **should** should be used for **desirable requirements**

**Text highlighting** can be used to identify key parts of the requirement, and computer jargon should be avoided if possible.

Documents should be **self contained** meaning that you do not require more than the requirements document to understand the requirements. This can be done through:
- Including a glossary of terms
- Including complete examples

