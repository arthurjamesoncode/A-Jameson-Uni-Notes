## What is Machine Learning?
Machine learning describes software that can improve their performance by applying a learning algorithm on training data. Typically the program has a large number of parameters whose values are obtained via the training data.

![[machine_learning_flowchart.png]]

But if the design of the program can be improved, why do this by machine learning and not just program the improvement ourselves?

This is because:
- The agent may find itself in situations which could not have been predicted.
- The designers can't know all the changes that would need to be made over time
- Programming a solution is sometimes very difficult or not even possible by a human

Machine learning has uses in:
- Face detection
- Speech Recognition
- Stock Prediction

For algorithms which are able to be programmed with reasonable efforts, you should not use machine learning. ML models often have some degree of error, so if a robust program is possible then we should prefer that.
### Examples
One of the earliest examples of a useful machine learning algorithm was one which could recognise handwritten digits.

This system took 28px by 28px images of digits (represented as a vector $x\in\mathbb R^{784}$) and learnt a classifier $f(x)$ which could map unseen images to one of the 10 digits:
$$
f: \mathbb R^{784} \to \{0,1,2,3,4,5,6,7,8,9\}
$$
This worked by applying a **supervised learning algorithm** to a training dataset of 6000 examples of each digit, and could achieve a testing error of 0.4%.

A similar example is facial detection. This also used a supervised learning algorithm to learn a classifier which could classify an image into three classes:
- Non-face
- Frontal-face
- Profile-face

Now the images were not grayscale, so they were now represent as 3 overlapping matrices which represented the red, green, and blue colours respectively.

The training data for this needed contain many different faces, all labelled and all from a variety of:
- Ages
- Races
- Genders
- Lightings

And all faces needed to be normalised in terms of scale and translation.

Another use of ML is spam detection. This uses a vector of word counts. For this algorithm constant improvement was important since there is an "enemy" in this case which is very capable of learning.

Machine learning can also be used for continuous outputs as well. One example is stock price prediction. This is not a case of classifying into one of a few discrete classes but instead a case of generating a continuous number.
## Representing Data as Fixed Length Feature Vectors
When we want to train a machine learning model on a piece of data, we need some way of representing that data in a way that the model can understand.

For example, consider we wanted to make a classifier which took a mushroom and placed it into 1 of two categories:
- Edible
- Poisonous

We would need a way to represent each instance of these mushrooms in a way that the computer could understand. One way to do this is to use **fixed length feature vectors**. These are vectors which contain labels for various categories of features.

For example, if we wanted to represent mushrooms this way we could use:
- Cap Shape
- Cap Surface
- Cap Colour
- Has Bruises
- Odour

So a specific mushroom could be represented as:
$$
\langle
bell, fibrous, gray, false, foul
\rangle
$$
where each item of that vector is a possible value for the features above in order.

There are a number of different feature types:
- **Nominal** - There is no ordering among possible values e.g. A colour feature which can be red, green, or blue.
- **Ordinal** - Possible values of the feature have an order e.g. A size feature which can be small, medium or large.
- **Numeric** - A continuous number
- **Hierarchical** - Possible values are partially ordered in a hierarchy. View the image of the tree below.

![[hierarchical_features.png]]

We can think of these features as forming a **d-dimensional feature space** where $d$ is the number of features and each instance represents a point depending on what features it has.

![[feature_space.png]]

We can also view this representation as just a single database table.
![[feature_table.png]]
## Data Pre-Processing
Real data is very messy. As a result most of the effort on a machine learning project goes into pre-processing the data.

This is done through a few steps:
- **Cleaning the data** - Removing duplicates, dealing with missing values, detecting errors/outliers
- **Encoding the data** - Turning the data into a format that the model can understand such as a feature vector
- **Scaling the data** - This is done to stop features with large ranges from dominating other features. We will see why this matters more when we start to look at specific algorithms.
- **Split the data** - The data is split into training, validation, and test datasets. This is to give us a way to assess how well the model is doing, which we wouldn't be able to do if we trained it on all available data.

To scale the data we do a few things:
- Mean normalisation
- Standardisation
- Whitening

Mean normalisation means that we remove the mean of each feature from each datapoint. So each datapoint $x$ becomes $x'$ where $\bar x$ is the mean and
$$
x' = x - \bar x
$$
This centers every feature on 0.

Standardisation puts every feature on the same scale as well as normalise the mean. It does this by dividing the mean normalised values by the standard deviation of the sample
$$
x' = (x-\bar x)/\sigma
$$
The result of this is that the all features are centered on 0 and have a standard deviation of 1.

Note that $\bar x$ and $\sigma$ should be calculated only on the training dataset.

>Standard deviation hasn't actually been covered in this module or a mandatory module from last year, but you can see it in [[Lecture 2 - EDA with Descriptive Statistics]] of COMP229.

The goal of **whitening** is to make the **covariance matrix** of the transformed dataset the identity matrix.

The **covariance matrix** is a matrix which shows how different values of a dataset change together:
- The diagonal values represent the variance of each individual variable
- The non-diagonal values represent the covariance value of the two corresponding variables

For covariance values:
- A positive value means both variables tend to increase or decrease together
- A negative value means that one variable will increase while the other decreases
- Zero means there is no linear relationship between the variables

The full steps to **whiten** a dataset $D$ are:
- Mean normalise $D$ to get $D'$
- Find the covariance matrix of $D$, $\Sigma$ (must be non singular for this to work)
- Apply a whitening matrix $W$ to every sample:
$$
x'' = Wx', \text{ with }W^TW=\Sigma^{-1}
$$

There are a few different choices of a whitening matrix $W$:
- **Mahalanobis / ZCA Whitening**:
$$
W = \Sigma^{-\frac12}
$$
- **Cholesky Whitening:**
$$
W=L^T \text{ where } L \text{ is the Cholesky factor of } \Sigma^{-1} \;\; (\text{obtained from }\Sigma^{-1}=LL^T) 
$$
- **PCA Whitening:** $W$ is built from the eigenvectors and eigenvalues of $\Sigma$

>This all seems really complicated for right now and was barely touched on in lecture, but I do think he's going to come back to it later on.
### Data Leakage
If test data influences pre-processing, this will cause the test score to be too optimistic.

The way to avoid this is to compute the mean and standard deviation on only the training data, so as not to inflate the accuracy of the test.

![[pre-processing_order.png]]

The test data **HAS** to look to look like future unseen data so it should not be used to choose anything at all.

Other data leaks could be:
- Duplicate datapoints across training and test data
- Features that encode the label