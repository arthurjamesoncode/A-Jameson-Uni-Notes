The intelligent entities that we engineer in AI are known as agents.

A popular characterisation by Russell and Norvig is: "An agent is anything that can be viewed as perceiving its **environment** through **sensors** and acting upon that environment through **actuators**."

A human agent has eyes, ears and other sense organs which act as its sensors and hands, legs and other body parts that act as it's actuators.

A robotic agent may have cameras as sensors and various motors as actuators.

A software agent might receive keystrokes and file contents as sensor inputs and might act on the environment by writing files.

This entire module is, at it's core, about various tools that can be used to design and implement rational agents.

If you look below you can see a diagram of the general flow of an agent.
![[general_agent.png]]
## Task Environments
Every agent has an environment within which it acts. The environments they occupy differ depending on the problem the agent is designed to solve.

When we design agents, we must specify the task environment as fully as possible. To do this we we give a PEAS description:
- Performance Measure - The criteria by which we can measure the success of an agents behaviour.
- Environment - The external environment that the agent inhabits.
- Actuators - The means by which the agent acts within it's environment.
- Sensors - The means by which the agent takes in information about it's environment.

Consider a taxi driver agent. Its PEAS description might be as follows:
- Performance measure: safe, fast, legal, comfortable, etc.;
- Environment: roads, other traffic, pedestrians, customers;
- Actuators: steering, accelerator, brake, signal, display, etc.;
- Sensors: cameras, sonar, speedometer, GPS, engine sensors, keyboard

Consider an agent used for medical diagnosis. Its PEAS description might be as follows:
- Performance measure: health of patient, costs of treatment.
- Environment: patient, hospital, staff.
- Actuators: display questions, tests, diagnoses and treatments.
- Sensors: keyboard entry of patient’s symptoms, responses to questions and findings.

## Properties of Task Environments
The properties of the task environment that the agent inhabits may differ greatly, depending upon the particular application area. Russell and Norvig have given a classification of the different types of properties of agent environments:
- Fully observable vs partially observable
- Deterministic vs stochastic
- Episodic vs sequential
- Static vs dynamic
- Discrete vs continuous

### Fully Observable vs partially observable
In a fully observable environment, the agent can obtain complete up-to-date information about the state of the environment. If this is not the case, we call the environment partially observable. Many only moderately complex environments are partially observable.

Fully observable environments are more convenient since the agent does not need to maintain any internal state, including memory, to keep track of the environment.

Examples of fully observable environments:
- Chess
- Crosswords

Examples of partially observable environments:
- The real world
- Poker
### Deterministic vs Stochastic
A deterministic environment is one in which any action has a single guaranteed effect. There is no uncertainty about the state that will result from performing an action. If there is no guaranteed effect we call the environment stochastic. 

Essentially if chance has any impact on an environment, the environment is called stochastic.

If an environment is deterministic except for the actions of other agents, we call the environment strategic.

Deterministic environment examples:
- A crossword puzzle
- The game of chess

Stochastic environment examples:
- Medical diagnosis
- Poker
- The physical world
### Episodic vs Sequential
An episodic environment is one where the performance of an agent is dependent on a number of discrete episodes with no link between it's performance in each episode. In sequential environments, different episodes are linked.

In episodic environments the agent doesn't need to consider interactions between the current episode and future episodes.

In sequential environments the agent's current decision could affect all future decisions.

Episodic environment examples:
- A mail sorting system
- Defect detection on an assembly line

Sequential environment examples:
- A crossword puzzle
- Poker
- Chess
- Driving a car
### Static vs Dynamic
A static environment is one in which the state will not change in the time taken for the agent to make a decision. A dynamic environment has processes operating on it and so changes while the agent is deliberating.

Static environments are easier to deal with as the agent does not need to keep observing the environment while deciding how to act, and it does not need to worry about time elapsing.

Static environment examples:
- A crossword puzzle
- Poker
- Backgammon
- Chess

Dynamic environment examples:
- Medical diagnosis
- The physical world

>Note that games may have some kind of turn timer imposed on them, such as chess or poker, but in the context of whether an environment is static or dynamic we don't really consider this.

### Discrete vs Continuous
A discrete environment is one that contains a fixed, finite number of distinct states. The distinction applies to the state of the environment, the way in which time is handled and the perceptions and  actions of the agent.

A continuous environment, however, has no fixed, finite number of states and provides greater challenges for agent designers.

Discrete environment examples:
- A crossword puzzle
- The game of chess

Continuous environment examples:
- Medical diagnosis
- Driving a car
## Classifying Agents
We can classify agents based on how they map perceptions to their actions. 

Russel and Norvig identify five basic kinds of agents that underpin most intelligent systems:
- Simple reflex agents
- Model-based reflex agents
- Goal-based agents
- Utility-based agents
- Learning agents
### Simple Reflex Agent
Simple reflex agents select actions based on their current perception of the environment. They do not take into account the history of the environment.

These are generally implemented with condition action rules such as "If there is a wall in front of me, then turn right".

These agents are very simple to implement, but are the most limited in their intelligence.

You can see below a diagram of how these agents work.
![[simple_reflex_agent.png]]

As simple reflex agents have no history and do not know how their actions influence the world in different situations. This means that they can't
- Play football, as to decide the next move a striker has to remember where the defenders were a second ago.
- Play poker, as to optimally decide the next move a player must remember the actions taken by their opponent in the previous stages of the hand.
- Drive a car, as an agent must remember where other cars or pedestrians are in order to be safe.
- And many more examples.
### Model-Based Reflex Agents
Model-based reflex agents are similar to simple reflex agents, except that their maintain an internal state that depends on the history of their environment. This essentially means that they can have a memory.

The current state is combined with the previous internal state to update description of the current state. This helps to deal with partially observable environments.

These agents have some knowledge (a model) about "how the world works".

This model tells the agent "how does the world change independently from the agents actions" and "how does the world change due to the agents actions".

You can see below a diagram of how these agents work.
![[model_based_agent.png]]
### Goal-Based Agents
Goal-based agents select appropriate actions to achieve desirable states of the environment, or goals. 

Knowledge of the current state does not automatically mean that the agent knows what to do. There may be a sequence of actions that the agent must take in order to achieve a desired goal. As these sequences become longer decision making may become complicated. Search and planning may be required.

You can see below a diagram of how these agents work.
![[goal_based_agent.png]]
### Utility-Based Agents
Utility-based agents are similar to goal-based agents, but they make use of a utility function to compare the desirability of different states that result from actions. 

Many actions may satisfy a goal, but which is the most desirable? Utility function maps a state, or sequence of states, onto a number to give the degree of usefulness of the state to the agent. The agent tries to maximise the value of its utility function. Tradeoffs may need to be made between conflicting goals.

Consider the card game poker. When playing a hand of poker the player has 2 conflicting goals:
- Lose the least possible money when my hand is worse than my opponents
- Gain the most possible money when my hand is better than my opponents

A poker player agent would need to be a utility agent as they would have to consider the trade offs between these conflicting goals.

>There are actually more conflicting goals than this in poker (such as trying to win money when you have the worst hand by bluffing) but for the sake of a simple example they have been ignored.

You can see below a diagram of how these agents work.
![[utility_based_agent.png]]
### Learning Agents
Learning agents improve the way in which actions are chosen based on previous experience. They use knowledge of the effects of previous actions to inform the action selection procedure when compared to previous versions of the agent.

There are many examples of machine learning algorithms, which we will start to look at near the end of the course. For now, you simply need to understand their existence.