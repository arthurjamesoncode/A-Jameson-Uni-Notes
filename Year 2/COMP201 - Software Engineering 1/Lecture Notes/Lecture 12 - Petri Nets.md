## Tools
The first slide of the lecture is two links to some useful tools for playing around with Petri nets:
- Igor Kim Petri Net Simulator - The link is broken, and I can't find where it would point to in google. I guess it must have come down, but the second link seems more useful anyway
- [Petri Net Editor](https://pes.vsb.cz/petrineteditor/#/model)
## Petri Net Overview
**Petri Nets** were developed by Carl Adam Petri when he was 12. Their purpose was originally to model chemical reactions.

Since then, they have been extended and applied in a variety of areas. For software modelling they are useful for a couple of reasons:
- They have interesting/useful mathematical properties
- They are a graphical tool and therefore can be more intuitive for beginners

The basic idea is that a petri net is a collection of directed edges connecting places and transitions. Each place can hold tokens, and the current *state* (or **marking**) of a petri net is the current assignment of tokens to places.

You can see some example petri net structures that occur in real systems. Exactly what these are will become clear as we study the notation.
![[petri_structures.png]]

While originally designed for use in chemistry, they are very useful for modelling software systems. Due to their non-deterministic nature (since many transitions can fire and we do not the order in which they do), we can use them to model **discrete distributed systems**.

Their rigorous mathematical notation means that many questions about the system can be verified by studying the properties of it's corresponding petri net.
## Places, Arcs, & Transitions
Places are essentially storage for tokens in petri nets, arcs are directed edges between a place an a transition or vice versa. Arcs cannot join a transition to a transition or a place to a place.

Places have a capacity, infinite by default, saying how many tokens they can have. They are denoted by circles, with a number of dots (representing tokens) inside.

Arcs have a weight, 1 by default, which is the amount of tokens they will fire in a single firing. They are represented by arrows.

Transitions do not have a weight or capacity. They do not store tokens, and fire as many as the connected arcs would suggest. They are represented as either boxes or solid bars. The two notations are equivalent, but one may be easier to read on a given diagram.

You can see two equivalent example petri nets below
![[petri_net_box_trans.png]]

![[petri_net_bar_trans.png]]

The **state** or **marking** of the petri net is how many tokens are currently in each place. For example the above could have the marking
$$
(1,2,1,1)
$$
corresponding to
$$
(p1, p2, p3, p4)
$$

Transitions can have multiple inputs and outputs. For example below
![[multiple_in_out_trans.png]]

The transitions T1 has 3 inputs and 2 outputs with $p3$ being both an input and an output.
### Firing
Transitions are the **active components** of the petri net. They are what drives changes in state.

A transition is enabled when the number of tokens in each of the input places is at least equal to the arc weight going from the place to the transition, as long as the firing wouldn't push any output place over it's capacity.

In the diagram below, $t1$ is enabled and $t2$ is disabled.
![[enabled_disabled_transitions.png]]

Enabled transitions can fire at any time, they do not need to fire as soon as they become enabled. Once they do fire, this results in a new marking of the net.

Firing is **atomic** meaning only 1 transition fires at a time even if more than 1 are enabled. There is no set order to the firing meaning that petri nets are non-deterministic.

Upon firing, a number of tokens equal to each corresponding arcs weight is removed from the inputs and added to the outputs. This means that, depending on the number of inputs/outputs and the weight of the arcs, the total number of tokens can change upon firing, if there are more/less inputs than outputs or if the arc weights are different for inputs/outputs.

Below you can see an example petri net. Since there is only 1 transition, this petri net is actually deterministic.
![[example_petri_firing.png]]
You can see upon each firing, the top output increases its tokens by one and the top input decreases its tokens by 1. The bottom output/input maintains one token the whole time since every time it fires, it loses and gains a token.

A transition with no input is **always enabled** (as long as there isn't a capacity limit on its output) and when it fires this will create new tokens equal to the sum of its output weights.
![[petri_net_creation.png]]

A transition with no output will remove or consume the tokens from its inputs when it fires.
![[petri_net_consumption.png]]

If a place is the input to two transitions, this is a conflict. The transitions will be competing for any tokens in that place.
![[petri_conflict.png]]

Which transition fires, and therefore consumes the token, is arbitrary. This means petri nets are **non-deterministic**.

**Inhibitor arcs**, denoted by a line with a circle at the end instead of another arrow, stop the transition from firing if the place it is connected to holds a token.
![[inhibitor_arc.png]]
## Modelling With Petri Nets
We can model the states of a process with tokens in places, and then model state transitions with transitions:
- Tokens represent resources (humans, goods, machines, information, conditions, states of objects)
- Places represent buffers, channels, geographical locations, conditions or states
- Transitions represent events, transformations or transportations

Lets now model a traffic light as an example.
![[traffic_light.png]]

As seen in the image above we want to transition from red, to yellow, to green (we're ignoring red and yellow). So how can we do this with a petri net?

Well since only 1 light is able to be on at a time, we can use a closed petri net with a single token. Where this token is will determine which light should be on, and each transition simply will change the light from one token to another.

This looks like so
![[single_traffic_petri.png]]
(Note that this is simplified and switches straight from red to green rather than red to yellow to green)

Now if we expand the system to be two traffic lights (for example at a crossroad) with the added condition that when one of the traffic lights is yellow or green, the other must be red.

We can use the above petri net to model each individual traffic light, but now we also need to add some connections between them. We need to make it impossible for one of the traffic lights to turn to green, unless the other is currently red.

To do this we can add a "safe" place in the middle. The idea being that when there is a token in the safe place, both of the traffic lights are red. 

We can do this by:
- Making "safe" an input to the $rg$ transitions, meaning that either $rg$ cannot fire unless "safe" has a token
- Making "safe" an output of the $yr$ transitions, meaning that after one of the traffic lights transitions back to red, "safe" will have a token again.

![[double_safe_traffic_petri.png]]
If we start with them both on red, after one of them fires and transitions to green, the safe token will be used, and the other one won't be able to fire until it comes back to "safe".

The problem with this design is that the traffic light which didn't just cycle through the colours is not guaranteed to go next, since the transition which fires is arbitrary. To fix this, we can simply add another place called "safe2" and make it so they cycle through having tokens.

![[safe_and_fair_traffic_light.png]]
Now each "safe" place enables a different traffic light, creating a cycle which means that at least one of the traffic lights will be red at all times.
## Reachable States & Deadlock States
The current state, or current marking, of a petri net is the configuration of tokens over the places. 

A **reachable state** is a state which can be reached from the current state through a series of enabled transitions.

A **deadlock state** is a state in which no transitions are enabled.

We can denote states by given the places an order and then using a tuple to show the number of tokens in each state currently.

This allows us to graph states where we have these tuples as the nodes and the enabled transitions as the edges.

For example if we have the following petri net we can graph the states like so
![[reachable_deadlock.png]]
Here we can see that there are 6 reachable states (7 including current), one of which is a deadlock state.