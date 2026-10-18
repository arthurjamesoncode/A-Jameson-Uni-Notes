## Scrum
Scrum is an agile methodology. 

It covers all aspects of development:
- Product requirements
- Hardware engineers
- Software engineers
- Production engineers

It's characterised by a move from a sequential approach to an iterative approach. Every iteration moves towards the final goal of producing the product.

The key aspects of scrum are:
- Iteration
- Flexibility
- Testing
- Scheduling

There are a few roles that people working on a project using SCRUM methodology must take on:
- Product Owner - Liaises with stakeholders and is responsible for deciding what is built.
- Scrum Master - Organises the scrum process and removes blockages. They are not necessarily the manager or boss, usually just another team member.
- Development Teams - Groups of people who deliver the software being worked on

The general scrum process is pictured below
![[scrum_process.png]]
### Daily SCRUM & Product Backlog
The daily SCRUM or daily stand-up is a short meeting that happens at the start of the day.

In this meeting everyone says:
- What progress they made since yesterday
- What they are planning to do today
- Anything that might stop them from completing todays work

This helps the scrum master remove friction/blockages in anyone's workflows. It also keeps the whole team, including scrum master and product owner informed on progress, risks etc.

The Product Backlog is the list of all outstanding and completed features on the project, and should be maintained throughout the project.

A good product backlog:
- Describes all features
- Assigns a priority to each feature
- Assigns a time/cost estimate to each feature
Features can be defined as user stories or use cases depending on context.

The product owner takes care of the backlog. They can:
- Remove items
- Add items
- Change priority
### Sprints
Sprints are short iterations of 1 to 4 weeks, that should produce a deliverable user testable version of the product.

Sprints are **time boxed** meaning that the interval of time is treated as fixed an not extendable. As a result it is the features and requirements which shift by the end of the sprint if the initial requirements are not achievable.

Any functions that are not completed or tested are not presented in the product at the end of the sprint.

Before each sprint the team engages in **sprint planning**, which is essentially deciding what should be done in the next sprint:
- The product owner (with the team) presents priorities and proposes the sprint goal.
- The scrum master facilitates the meeting.
- The developer team selects items and plans how to deliver them. 
- The selected items are moved from the product backlog to the sprint backlog.

The sprint backlog is the list of all tasks for the current sprint:
- Every task should be doable in 4-16 hours (typically)
- Developers should sign up for tasks rather than being assigned them
- Every task in the backlog should be functional and tested before it is removed
- Priorities can help schedule task completion

Sprint progress is measure with a sprint burndown
![[sprint_burndown.png]]

Each sprint ends with a **sprint review** including **backlog refinement**:
- Features are presented to stakeholders
- Stakeholders comment and provide feedback on the product
- Decisions are made on what might be changed in the product backlog.

This could involve:
- Adding items to backlog
- Removing items from backlog
- Changing priority of items
- Clarifying criteria/requirements

Similar to sprint burndown there is a release burndown for the project as a whole
![[release_burndown.png]]
## Kanban
Kanban started life in Toyota. The goal of Kanban was to limit the amount of inventory that wasn't saleable. 

For example is there was demand for 5000 cars, you would not make 20000 engines. This helped with cash flow, reduced the need for storage and warehousing and reduces risk.

In software the idea is similar, except instead of reduced the amount of redundant inventory you reduce the amount of things being worked on at one time. The items being worked on are labelled as WIP and the aim is the keep the count as low as possible.

This is all organised with a Kanban board
![[kanban_board.png]]

The purpose of the board is to help deliver items from the left to the right while minimising the amount of work started and not finished.

Kanban is not mutually exclusive with SCRUM, and both methodologies can be used together.