## Requirements Engineering Processes
The goal of requirements engineering is to create and maintain a **system requirements document** including:
- User stories
- Use cases
- Testing and Acceptance Criteria

The processes used for requirements engineering vary widely depending on:
- Domain
- People involved
- Organisation
but there are a number of generic activities that we will study today.

These activities are:
- Requirements management

>Go into more detail on all of theseelicitation - What services are required?
- Requirements analysis - How do we classify, prioritise and negotiate requirements?
- Requirements validation - Does the proposed system fit the users needs?
- Requirements management - How do we manage the changes to the requirements document?

Analysis is a step here that is part of all of the steps, so for the purpose of this we will consider it as part of elicitation.

Consider a Patient records system 
1. (Elicitation) Talk to patients, doctors, nurses, receptionists, managers to find out Current system practise, legal restrictions DPA, problems with current system, needs for improvement, security issues, costs 
2. (Elicitation) Develop draft documentation and review what is most important, what will it cost, what is the timescale, is new hardware required
3. (Validation) Send requirements to end users. Present them with Q&A. Go back to step 1, discuss requirements again
4. (Management) Have a yearly review of requirements between all stakeholders. Have a system of reviewing the cost and feasibility of change to system.
## Elicitation and Analysis
The process of requirements elicitation, sometimes called requirements discovery, involves technical staff working with customers to find out about:
- The application domain
- The services that the system should provide
- The system's operational constraints

Can involve:
- Managers
- Engineers involved in maintenance
- Domain experts
- Trade unions
- etc.
We call these people stakeholders.

There are a number of problems that require analysis:
- Stakeholders don't know exactly what they want until they see it
- Stakeholders express requirements in their own terms, possibly ambiguously
- Stakeholders may have conflicting priorities
	- Staff want easy use
	- Management wants high security
	- Patients want to change appointments easily
	- Management wants easy way to plan staff resources
- Requirements can be influenced by organisational and political factors

After performing analysis, the requirements change.

In the real world requirements often come from:
- Copying or Modifying the requirements of other systems
- Fixing the requirements of a legacy system
- Looking at what competitors do to improve on it
- Prototyping

Lots of requirements are discovered by prototyping. It's common for initial requirements to be be very thin and for a prototype to be created as early as possible.

Viewpoints are a way of structuring the requirements to represent the perspectives of different stakeholders. This multi-perspective analysis is important as there is no single correct way to analyse requirements.

We can identify viewpoints using:
- Providers and receivers of system services;
- Systems that interact directly with the system being specified;
- Regulations and standards
- Sources of business and non-functional requirements
- Engineers who have to develop and maintain the system
- Marketing and other business viewpoints

Interviewing often makes up part of the requirements elicitation process. It can be formal or informal, but always involves the RE team putting questions to stakeholders about:
- The system they use
- The system to be developed

There are two types of interview:
- Closes interviews - A pre-defined list of questions are asked
- Open interviews - There is no strict, pre-defined agenda and a range of issues are discussed with stakeholders.
## Security Requirements
Most modern systems have some security requirements. This is obviously massively important to systems which handle money or sensitive data. 

Security requirements are also often tied in legislation, and not complying with legislation can result in being:
- Sued
- Fined
- Shut down

Security requirements can be broken down in 4 main issues:
- Confidentiality
- Integrity
- Authentication and Authorization
- Non-repudiation
And one auxiliary issue:
- Availability

### Confidentiality
Confidentiality Means:
- Encryption - Storing data in a secure way so that it can not be understood by others
- Permissions - Understanding and enforcing who can do what

It's vital that data be kept secure for as long as reasonably possible.
### Integrity
Integrity means that data cannot be modified with knowledge of the change.

This has a bunch of different approaches:
- Cyclic Redundancy Check - Not good, the check value is easy to forge
- Hash Value over Data - Similar to CRC
- Hash Value over Data + Secret Key - Can have problems with distributing keys
- Hash Value encrypted with an asymmetric cipher - Current standard
### Authentication/Authorization
Authentication and Authorization means checking who people are and what they are allowed to do.

This is commonly done with:
- Usernames
- Passwords
- Hardware
- Biometrics

This is often the first point of attack. It is important, therefore, that a person cannot credibly deny performing an action. This is a concept call **non-repudiation**, and is based on authentication, integrity, and recording or time stamping.

![[non_repudiation.png]]
### Availability
Availability is the auxiliary concern to security and is massively important. The service offered by your app can be rendered pointless in some cases if your app experiences significant downtime.

The availability of a system is measured in **9s** meaning the number of digits before the first non-9 digit in your uptime as a percent.

| Uptime      | Uptime   | Maximum Downtime per Year |
| ----------- | -------- | ------------------------- |
| Six nines   | 99.9999% | 31.5 seconds              |
| Five nines  | 99.999%  | 5 minutes 35 seconds      |
| Four nines  | 99.99%   | 52 minutes 33 seconds     |
| Three nines | 99.9%    | 8  hours 46 minutes       |
| Two nines   | 99.0%    | 87 hours 36 minutes       |
| One nine    | 90.0%    | 36 days 12 hours          |
This is not always useful terminology.

For example if you have three 9s but unavailability spread as 78 seconds per day, or five nines but it failed once in 10 years for 50 minutes.

What really needs to be specified is worst case scenarios.
### Logs and Alerts
Good security depends on knowing what activity has happened on the system.

There are a few important logs that may exist in a system:
- Standard log - Logins/Logouts, Database access requests
- Failed Login Log
- Unusual Activity Log - High volume transactions etc.
- Alert Log

### Bell-LaPadula model
The Bell-LaPadula model is a standardised model for designing the security of a system.

Each item is given a security clearance level:
- Top-Secret (4)
- Secret (3)
- Sensitive (2)
- Unclassified (1)

There is no read up, meaning that no one can read items that are above their clearance level.

There is no write down, meaning that a document cannot be copied/included into a document with a lower clearance level.

Trusted subjects can write documents down. They must be shown to be trusted with regard to the security policy.
### Specifying Security
When specifying security the exact specifics should be kept as open as possible to allow for upgrading encryption algorithms and protocols. These have a habit of changing as increased computing power and new threats begin to come up.

It's important to consider security policy as part of this specification such as:
- Shredding documents
- Secure disposal
- Password reset protocols
- Security training
- Security audits

It's also important that we work under security standards such as The Payment Card Industry Data Security Standard.
## Requirements Checking
We need to ensure that requirements satisfy a number of properties:
- Validity - Does the system provide the functions which best support the customer's needs?
- Consistency - Are there any requirements conflicts?
- Completeness - Are all functions required by the customer included?
- Realism - Can the requirements be implemented given budget and technology?
- Verifiability - Can the requirements be checked?

Verifiability is especially important since this reduces the potential for disputes between customers and contractors. A set of tests should be possible.

One way of verifying requirements are "**Scenarios**" these are essentially test cases running in a given situation:
- Try and withdraw cash with a stolen credit card
- Try and withdraw cash when the machine doesn't have enough
- Try and withdraw cash with a specific card number
- etc.

Scenarios are not tests, since they are essentially just specific cases specified to show what behaviour should be, reducing ambiguity. They can make up the basis of tests.
## Cucumber
Cucumber is a tool for making user stories. It helps write requirements that are directly linked to tests.

I think it's worth mentioning this, as it's in the slides, but I very much doubt I will actually need this unless I start to work on it. 

As a result I'm just going to paste the link to it here and do no more: https://cucumber.io/docs/terms/user-story/

