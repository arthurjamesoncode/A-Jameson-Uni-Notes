## Monty Hall Problem
The game show “Let’s Make a Deal”, hosted by Monty Hall, let contestants choose one of three doors. Behind one of the doors was a prize; behind the other two were goats. 

The contestant chooses one of the doors, but before it is opened, Monty Hall always opens another door with a goat behind it, and asks:
	“Do you want to switch doors, or stick to your original choice?”

How should you answer?

The key to this riddle is that Monty Hall knows where the car is. So he is always opening a door that doesn't have the car.

When you first make the choice, your odds of choosing the car are $\frac13$. Now there are two possibilities:
- You choose the door with the car ($\frac13$), in which case switching will always give you the goat.
- You choose a door that doesn't have the car ($\frac23$), in which case switching always gives you the car

When we break the problem down like this, we can see that the probability that switching gives you the car is the same as the probability that you didn't pick the car in the first place. As a result, switching offers a $\frac23$ chance of picking the car, while staying put offers a $\frac13$ chance of picking the car.

>The slides offer another explanation using bayes theorem, which would probably be a good exercise to replicate, but I don't think it's worth it for me to do here.
## Cromwell's Rule
Cromwell's rule is simple.

It states that if $P(Hypothesis)=0$ then
$$
P(Hypothesis|Evidence)=\frac{P(Evidence|Hypothesis)P(Hypothesis)}{P(Evidence)}=0
$$

Similarly if $P(Hypothesis = 1)$ then
$$
P(Hypothesis|Evidence)=\frac{P(Evidence|Hypothesis)P(Hypothesis)}{P(Evidence)}=1
$$

This essentially says that hard convictions are insensitive to counter evidence.

>This is all the slides say, and they give a quote from Oliver Cromwell as well. I find this ironic because Cromwell was a bit of tyrant and a total asshole who trusted himself over anything else.
>
>As it relates to this module, I guess the point here is to say that assume $P(X)=1$ or $P(X)=0$ (that events are either certain or impossible) should only be done with good reason. 
>
>To be honest I think this "rule" goes without saying and I really don't understand why there's even a slide on it.
## Simpson's Paradox
Simpson's paradox, also called the amalgamation paradox, is when a trend in different groups can reverse when these groups are combined.

![[simpson's paradox.png]]

You can see this purely in vector form below, although we will look at some concrete examples too.
![[simpson's_paradox_vectors.png]]

Notice in this image we can see that the slope of $A_1$ is greater than $B_1$, with the same being true for $A_2$ and $B_2$. 

However when the $A$ vectors are added, and the $B$ vectors are added the $B$ vectors have a combined greater slop than the $A$ vectors.

This is important as it reminds us not to take too strong conclusions from seeing repeated trends in different subsets of populations.
### Vaccines
A real example of Simpson's paradox comes from looking at SARS-CoV-2 variants of concern and variants under investigation in England.

![[vaccines_data.png]]

We can see from this that
$$
P(death | vaccinated) = \frac{70}{27192}=0.026
$$
and that
$$
P(death | unvaccinated) = \frac{44}{53822}=0.008
$$

which seems to suggest that vaccinated people are more than 3x as likely to die.

However when we recalculate the data looking at 2 age groups:
- Under 50
- Over 50
We see a different trend.

For ages <50:
$$
\begin{split}
P(death | vaccinated) = \frac{2}{19693}=0.00010 \\
P(death | unvaccinated) = \frac{6}{52846}=0.00011
\end{split}
$$
while for ages >50:
$$
\begin{split}
P(death | vaccinated) = \frac{68}{7499}=0.009 \\
P(death | unvaccinated) = \frac{38}{976}=0.039
\end{split}
$$
Now it simply suggests that there is very little difference to the outcome of those under 50 by getting the vaccine, but for those over 50 it reduces the chance of death by more than 4x.

This is an example of Simpsons paradox. When measured as different groups, neither group provides evidence against vaccines being effective (a difference of 0.00001 is not anywhere close to being called significant, and can be dismissed as noise) and one group provides significant evidence that they are significant.

However when the groups are combined, since:
- The sample of under 50s is so much larger than the sample of over 50
- More over 50s died
- A much higher proportion of over 50s are vaccinated

The trends in these populations reverse.

>Note they go over other fallacies in this lecture, but I think they are somewhat intuitive and the examples aren't that illustrative so I'm going to just ignore them for the purposes of these notes.
>
>Plus some of them, like the pi bill example, have been covered in 116 anyway.
