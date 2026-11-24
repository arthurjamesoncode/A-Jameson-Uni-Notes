## Exercise
The lecture begins with an exercise about recognising states in a petri net.

Given the net below, answer the following questions:
- How many states are reachable?
- Are there any deadlock states?
- How would you model the situation with 2 writers and 3 readers?
- How to model a "bounded mail box" (buffer size=4)?

![[readers_writers_petri.png]]

To look at reachable states we need  to look at the current state and which transitions are enabled. Currently the state is $(1, 0, 0, 3, 0, 1)$ and the only enabled transition is "begin".

Once begin fires, we have a new state, $(0, 1, 0, 3, 0, 1)$ and now the only enabled transition is send mail, which when it fires gives us the state $(1,0,1,2,0,1)$ now there are two enabled transitions:
- Begin
- Receive mail

If begin fires first we get the state $(0,1,1,2,0,1)$, and there are two enabled transition:
- Send mail
- Receive mail

This cycle (send mail, begin) can continue until all the tokens are sent giving the states:
- $(1,0,2,1,0,1)$
- $(0,1,2,1,0,1)$
- $(1,0,3,0,0,1)$
- $(0,1,3,0,0,1)$

At which point the only enabled transition is receive mail. Since as soon as Receive mail fires, a token is given back to the middle, this means that both of these processes can loop and there are both:
- An infinite number of reachable states (non distinct)
- No deadlock states
If we instead look at the number of distinct states possible there is a finite answer. All the states will follow the format
- $(a, 1-a, 3-b, b, c, 1-c)$

$a$ can have the values 0 and 1, $b$ can have the values $0, 1, 2, 3$, and $c$ can have the values $0$ and $1$.

By combinatorics we can figure out that the total number of distinct states are:
$$
|\{a\}|\cdot|\{b\}|\cdot|\{c\}| = 2 \cdot 4 \cdot 2 = 16
$$

To model it with more writers and more readers you simply need to allocate more tokens to the "rest" states. Remember tokens represent resources, and in this case the token is a reader/writer.

In this model the mailbox is currently bounded to only be able to buffer 3 emails at a time. If we wanted to increase the bound we simply need to add more tokens in the middle.

Notice that increasing the tokens also increases how many reachable states are possible. Every new token in the writers "rest" place would increase the possible values of $a$ by 1, every new token in the writers place would increase the possible values of $c$ by one and every new token in mail box capacity place would increase the possible values of $b$ by one.

All of which increases the number of distinct states.
## High Level Petri Nets
In practice, classical petri nets have some problems with modelling systems:
- The petri nets become too large and too complex
- They take too much time
- They cannot handle time and data

Therefore, we use high-level petri nets which extend classical petri nets with:
- Colour
- Time
- Hierarchy

We'll start to go through this by using a classical petri net of a salon
![[hairdresser_classical_petri.png]]

### Colour
**Colour** refers to the values of an object that a token models. This is essentially a list of attributes specific to that token.

![[hairdresser_petri_colour.png]]

When using colour, each transition has a set of rules which specifies:
- The number of tokens to be produced
- The values of these tokens
- (Optionally) A precondition

You can see some examples below
![[transition_colour_rules.png]]

To do the exercise you could do this by:
- Starting with the top left
- Feeding it into the bottom left
- Connecting $c$ from the bottom left to $b$ from the bottom left through the top right transition
- Then feeding $b$ from the bottom left into the bottom right transition.

### Time
To analyse performance with petri nets we need to model durations and delays and other timed aspects of our system. To do this we associate a pair $(t_{min}, t_{max})$ with each transition.

>The lecture notes other definition for a timed petri net exist but this is the one we need to be concerned with.

This pair tells us the minimum and maximum time that a transition will take to fire **once enabled**. This allows us to model the performance properties of the system. Analysis of these systems can be much more difficult though.

![[timed_petri.png]]
### Hierarchy
A hierarchy is a mechanism to structure complex petri nets comparable to DFDs.

A **subnet** is a net composed of places, transitions and other subnets. These can let us model systems at different levels of abstractions and reduce the complexity of the model.

![[subnet.png]]

This can make petri net models easily extendable and modular. The above petri net could have the complexity of the three subnets $h1,h2,h3$ removed and just have a single transition "pending" replace them.
### More Complex Example
Given the following informal specification from a critical system, identify any ambiguities and model the system with a petri net.

"The message must be triplicated. The three copies must be forwarded through three different physical channels. The receiver accepts the message on the basis of a two-out-of-three voting policy"

Ambiguities include the nature of the channels, and what should be done if all three messages are different. The nature of the channels is outside the scope but the idea of sending an error if there is not a clear winner in the two out of three vote is important.

Our first attempt is below
![[message_triplication_1.png]]

We use:
- 1 transition with 1 input and 3 outputs to split the message into 3.
- 3 transitions with 3 separate inputs and outputs to represent our different physical channels
- 3 transitions which all take 2 inputs and have a precondition that their inputs must match

This is a good start but there are a couple of problems:
- If all three copies match the message is sent three times
- If none of the copies match there is not an error or a second attempt

![[message_triplication_2.png]]

This is a better system since it accounts for none of the copies matching and will only ever send one message. Which message is sent depends on the condition, but that is brushed over.