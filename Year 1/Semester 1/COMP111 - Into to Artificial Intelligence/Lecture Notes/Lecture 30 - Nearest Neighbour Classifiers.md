## Distance Measures
Assuming we can measure the similarity between items in $X$ to be classified, we could classify a new item $x$ by looking at the labels of the items most similar to $x$ in the training data to classify $x$ accordingly.

For example on how we can measure similarity, we could measure how similar two emails are by counting the number of words from the English dictionary they both contain, and compare it to the number of words only one of the two emails contain.

We measure similarity between data items by using a **distance measure** $d$ which assigns to data items $x$ and $x'$ a non-negative number.$$d(x,x')\in \mathbb{R}$$
We call $d(x,x')$ the distance between $x$ and $x'$.

Typically, we require the following of $d$:
- $d(x,y)=0\iff x=y$, which means that $x$ and $y$ are the same or indiscernible from each other. This is called the "identity of indiscernibles"
- $d(x,y)=d(y,x)$, which means that the distance measure must be symmetrical between items
- $d(x,y)+d(y,z)\geq d(x,z)$, this is called the "triangle inequality"

### Numerical Features
The main way we can measure numerical distance between 2 data points is by the Euclidean distance. 

The Euclidean distance gives, in the 2 and 3 dimension case, the length of the straight line between two points. While the straight line only applies to the 2 and 3 dimensional case (cases in which our data points are made up of 2, 3 features), we can still use it to measure the distance for an arbitrary $n$ amount of features.

The Euclidean distance $$d((e_1,...,e_n),(f_1,...,f_n))$$between data points $(e_1,...,e_n)$ and $(f_1,...,f_n)$ is $$
\sqrt{\sum_{i=1}^n(e_i-f_i)}
$$always taking the positive root.

So for $n=1$: $$
d(e,f)=\sqrt{(e-f)^2}=|e-f|
$$And for $n=2$: $$d((e_1,e_2),(f_1,f_2))=\sqrt{(e_1-f_1)^2+(e_2-f_2)^2}$$and so on.
### Non-Numerical Features
Consider qualitative data like the training data we used in the Tennis example (pictured below).

![[tennis_training.png]]

When we have data with non-numerical features, we obviously can't use a Euclidean distance. So how can we measure distance between D1 and D2 then.

Instead of Euclidean distance, we can use the **matching distance** between values of features. This means the number of features on which $Di$ and $Dj$ do not coincide.

So from the table above:
- $d(D1, D2)=1$ since they only differ by the value of wind
- $d(D1,D4)=2$ since they differ by both the values of outlook and temp
- And so on

## Nearest Neighbour Classifiers
Now that we have some ways to measure distance between data points, we can start to define a classifier that will use this distance measure.

Assume the data in $X$ comes with a distance measure $d(x,x')\in \mathbb{R}$ which states how similar $x,x'\in X$ are. Then the nearest neighbour classifier works as follows.

Given training data$$(x_1,L(x_1)),...,(x_n,L(x_n))$$for a new $x\in X$ to be classified, let $x_i$ be the element of the training set that is nearest to $x$:$$d(x,x_i)\leq d(x,x_j),\;\forall x_j\neq x_i$$And then we define the value $f(x)$ of the classifier $f$ by setting $f(x)=L(x_i)$.

Below you can see the full algorithm for the nearest neighbour classifier in pseudocode:
```
Input: 
	training data (x0, L(x0)), . . . ,(xn, L(xn))
	new x ∈ X to be classified
	
for i = 0 to n do
	Compute distance d(x, xi)
endfor

return L(xi) such that d(x, xi) is minimal
```

A nearest neighbour classifier partitions $X$ into regions. Boundaries are equal distance from training points (See below).
![[regions.png]]

You can see below an example of the visual representation of the classifier for the classes "blue circle" and "red triangle", where the new $x$ is represented by the black square:
![[classifier_red_blue.png]]
As you can observe, this classifier would label the new $x$ as a "red triangle".
### The Problem with the Nearest Neighbour Classifier
There is a big reason why the nearest neighbour classifier can be problematic.

Mainly, it is very close to the training data, and does not generalise the training data. If the training data is noisy, the classifier will be noisy as well.

For example, if a spam email is erroneously labelled as non-spam, then all similar emails will also be classified as non-spam.
### $k$-Nearest Neighbour Classifier
The $k$-nearest neighbour classifier works similarly to the nearest neighbour classifier except, instead of taking the label of the nearest data point, it takes the majority label of the nearest $k$ data points. 

So, for $x$ to be classified we take the $k$ nearest points $x_{i_1},...,x_{i_k}$ in the training data, we then classify $x$ to be the majority vote of their class labels.

Below you can see a visual representation of a $k$-nearest classifier with $k=3$ for the classes "red triangle" and "blue circle":
![[k-nearest-red-blue.png]]
We can see that, as the majority of the three nearest are labelled "red triangle", this classifier labels our new $x$ as "red triangle".

Below you can see the full algorithm for the $k$-nearest neighbour classifier in pseudocode:
```
Input: 
	training data (x0, L(x0)),...,(xn, L(xn))
	new x ∈ X to be classified

for i = 0 to n do
	Compute distance d(x, xi)
endfor

Let xi1,..., xik be the list of items such that
	d(x, xij) is among the k smallest distances
	
return label L which occurs most frequently in L(xi1),..., L(xik ) (majority vote)
```
## Learning a "good" $k$
To learn a "good" $k$ we can divide labelled training data into **training data** $T$ and **validation data** $V$.

The **classification error** of a classifier $f$ on a set of data items is the number of incorrectly classified data items divided by the total number of data items.

Let:
- $f_1$ be the $1$-nearest neighbour classifier obtained from the training data $T$;
- $f_2$ be the $2$-nearest neighbour classifier obtained from the training data $T$;
- and so on up to some chosen $m$

We then choose the $f_k$ for which the classification error is minimal on the **validation data**.

>It should be noted that, for binary classifiers, we should choose an odd value for $k$ as this means the votes will never tie.

The aim of supervised learning is to create a program that will do well on test data that is not known during learning.

Because of that, choosing values for $k$ which minimize the classification error on the training data is not necessarily the best policy.

We want the learning algorithm to model true regularities in the data, ignoring noise.

Below you can see some sample graphs and classification errors for various $k$ and see observe how the classification errors change as $k$ does.

$k=1$
![[k1_t_v.png]]
$k=3$
![[k3_t_v.png]]
$k=7$
![[k7_t_v.png]]
$k=21$
![[k21_t_v.png]]

We can see that, as $k$ increases:
- The classification boundary becomes smoother, which may reflect regularity in the data.
- The error on the training data can, but doesn't have to, increase.

### Summary of $k$-Nearest Neighbour
Advantages:
- $k$-nearest neighbour is a simple but effective classifier.
- Decision surfaces can be non-linear
- As there is only a single parameter, $k$, it is easy to choose a good one via cross validation.
Disadvantages:
- We must specify a distance measure
- There is a lot of computational cost as we must store and search through the entire training set at test time.
