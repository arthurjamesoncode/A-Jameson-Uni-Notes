## What is Data Science?
Data Science is an interdisciplinary field that uses scientific meths and algorithms to extract knowledge from data - Wikipedia.

This basically means using data to:
- Deduce Stuff
- Explain Stuff
- Predict Stuff

This course does not focus on any specific software/language. We will focus on applications of scientific and mathematical foundations. 

Science is A systematic enterprise that builds and organises knowledge in the form of testable explanations - Wikipedia.

Daniel specifically highlights the importance of "testable explanations".

There are a number of difficulties that come with trying to draw conclusions from a specific dataset:
- The data could be from untrusted sources
- Could contain with duplications or measurement errors
- Could be highly complex
- Anonymity can be lost (with data relating to humans)
- Datasets could be huge
## Data Analysis
Most of the time spent working with data is spent on **data wrangling** which refers to collecting, cleaning, or transforming data. Not analysing it.

We refer to data analysis when we are analysing a specific dataset, where as data science would be the general processes we could use to analyse data. 

The Methods:
- Statistics looks for underlying patterns in data
- Machine learning can generalise conclusions to unseen data (can predict)

So how should we evaluate predictions?

One way to evaluate would be accuracy, but this has it's pitfalls. If we were trying to design a test for a disease which only 1% of the population has we could achieve a 99% accuracy by making the test always deliver an answer of false.

Therefore we can't use accuracy as a measure of a model. We have to be able to explain WHY the model is that accurate.

There's also another problem when it comes to predicting datapoints. It is impossible to do without **context**.

Take the sequence:
$$
1,2,4,8,16,...
$$

If asked to predict the next element of the sequence you would probably guess 32, given that so far it looks to be the powers of 2.

What this sequence actually is however is the sequence formed by placing $n$ points around a circle, joining each pair with a straight line, and then counting the regions the circle is cut into.

![[circle_regions.png]]

The solution of $2^{n-1}$ fits perfectly for the first 5 data points but when we look at $n=6$ we see that
![[circle_regions_n=6.png]]

The lesson to take from this is: "A model that fits the data perfectly does not equal a model that **explains the data! Only the latter can be used to predict new cases.**"

There is another problem that comes from linking data without explanations.

From 1999 to 2009, Nicholas Cage made a number of films. This number closely track the number of people who drowned in swimming pools. 

This is one of many **spurious correlations**. You can see a list of similar things [here](https://www.tylervigen.com/spurious-correlations). This is something that happens all the time due to the sheer quantity of variables that we track. 

The lesson from this is that correlation without context does not imply causation.

>Daniel really emphasised that **true correlation**, as opposed to spurious correlation, does imply causation. Any spurious correlation would disappear if enough data points were gathered. The direction of causation is never implied though.
## Module Delivery
The module will be delivered through:
- 30 Lectures
- 10 Tutorials
Each 1hr, with an expected 110hours of self study.

The syllabus for the module is:
- Exploratory Data Analysis, location, spread, and shape of data
- Probability, Bayes’ theorem and accuracy measures
- Random variables and distributions, the normal distribution and the Central Limit Theorem
- Hypothesis testing: p-values, errors and pitfalls
- Vectors, correlation and linear regression
- Equivalence relations, metrics and clustering (hierarchical, k-means, DBSCAN)
- Linear algebra: linear maps, isometries, invariants, eigenvectors
- Dimensionality reduction: Principal Component Analysis and SVD together with justifications and suitable evaluators to ensure the results are meaningful in real-life applications.

The module is assessed by:
- An MCQ class test worth 30% in November
- A written exam worth 70% in January
