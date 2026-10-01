## Before Learning: Data Collection
We often assume that instances we use for training our models are **Independent and Identically Distributed (i.i.d.)**.

A set of random variables, $X_1,...,X_n$ are i.i.d. if:
- The are independent of each other
- They are drawn from the same distribution

This assumption does not always hold. For example:
- Instances sampled from the same medical image
- Instances from a time series
- etc.

If test data comes from a different distribution than the training data this can have a negative effect on accuracy.

Consider the example below
![[iid_breaks.png]]

This happens because the model learns shortcuts tied to the origin of the instance. In the case of the hospitals this could be:
- Scanner type
- Image markers
- How common the disease was at each site
## Learning Tasks
There are three canonical learning problems:
- **Regression** - This is a supervised learning problem where we try to estimate parameters to do with some kind of continuous output
- **Classification** - This is a supervised learning problem where we try to estimate the class of an input
- **Unsupervised Learning** - This is when we try to use a model to model the data. For example by clustering related groups or by reducing the dimensions of the data.
### Supervised Learning
The supervised learning problem setting is this:
- There is a set of possible instances $X$
- An unknown target function $f: X \to Y$
- A set of models/hypotheses $H = \{h\;|\;h: X\to Y\}$

Given a training set of $m$ instances $x\in X$ with labels $y\in Y$ where $y = f(x)$
$$
(x_1, y_1),...,(x_m,y_m)
$$

Try and output a model $h\in H$ which best approximates $f$.

When $y$ is discrete, we call this a classification task (also know as concept learning). When $y$ is continuous, we call this a **regression task**.

There are also tasks where $y$ is not quite continuous but is a more structured object. Something like a sequence of discrete labels.

Over the semester we will be looking at a number of different models including:
- Decision Trees
- Neural Networks
- Linear/Logistic Regression
- Bayesian Networks
- etc.

Lets quickly look at an example of a decision tree.

Last lecture we considered a hypothetical model which is able to predict whether a mushroom is edible or poisonous. Below you can see a list of input features, with a bunch of possible values for each feature.

![[mushroom_features.png]]

If we trained a model on a bunch of datapoints about mushrooms, it could possible output the following **decision tree**.

![[mushroom_decision_tree.png]]

Now, in order to make its prediction it goes through each possibility for the odors first and either:
- Predicts edible or poisonous straight away
- Considers some values of another feature, or features before predicting.
## Unsupervised Learning
In unsupervised learning we are given a set of instances $X$ without labels.

The goal of this type of learning is to discover interesting things about the data such as:
- Regularities
- Structures
- Patterns

This type of learning is commonly used for:
- Clustering
- Anomaly Detection
- Dimensionality Reduction

For example, in **clustering**, the goal is to divide the training set into clusters such that:
- Everything in the same cluster is similar
- Everything in different clusters is dissimilar

For example, below you can see how a model might cluster different flowers based on a few features
![[flower_clusters.png]]

In **anomaly detection**, the model's task is to take a previously unseen $x$ and determine if $x$ looks *normal* or *anomalous*.

In **dimensionality reduction** the model's task is to represent each $x$ with a lower dimension feature vector that still preserves all the key properties of the data.

For example, a model which can represent an image of a face as a linear combination of different *eigenfaces*. See below.

![[eigenfaces.png]]

The above example can represent each face with only 20 features, instead of features equal to the number of pixels in each image.

Note: He added some detail on the active learning slide so redownload the slides.
## Semi-Supervised Learning & Self Supervised Learning
Semi-Supervised Learning uses a mix of labelled and unlabelled data to perform learning tasks.

For example, a model could be trained on a small labelled dataset and then used to label a much larger dataset. This **pseudo-labelled** dataset could then be used to train a model. This resulting model would typically be better than the original one which labelled the data.

![[semi-supervised-learning.png]]

LLMs are trained using **self-supervised learning**.

At first the model does **pre-training**. This is the self-supervised step. The model just predicts the next token on trillions of different word of web text. Since this step uses unlabelled data, it is very cheap to acquire and process relative to labelled data.

The next step is **fine-tuning**. Here the model is trained from (prompt, good answer) pairs written by humans. This is **supervised learning again**. 

The final step is **preference tuning**. Essentially the AI learns from feedback. Humans, or other AI, rank answers. The model is rewarded for better answers.

The latter two-steps use much more expensive human data by comparison.

We will learn about other types of learning which don't strictly fit into **unsupervised** or **supervised** later on such as:
- Reinforcement learning
- Transfer learning
## Training Schemes
**Batch learning** is when the learner is given the training set all at once.

**Online leaning** is when the learner receives instances sequentially, and updates the model after each. For some tasks it might make a prediction for a given instance before seeing the label.

**Active learning** means cases where the learner can select instances that are used for training. The learner essentially chooses which instances get labelled:
- A medical imaging tool asks a radiologist to label only the scans it's least sure about, to save on expensive human input
- LLM developers select the most informative prompts for human ranking

**Concept drift** is when the desired target function changes over time. Once accurate models become worse:
- Spam filters degrade as spammers change tactics
- Demand models break as shopping habits suddenly change (for example covid)

To defeat concept drift we need to monitor the accuracy of our models and retrain them. One method of doing this is **online learning**.

AI's can also learn from feedback:
- RLHF (Reinforcement Learning From Human Feedback) trains AI by using direct human preferences to guide the model
- RLAIF (Reinforcement Learning From AI Feedback) uses an AI model to generate preference labels instead of humans.

RLHF is hard to scale but accurate, while RLAIF is easy to scale but requires moderation to ensure alignment.

## Generalisation
The primary goal in supervised learning is to find a model that generalises. That means to accurately predict labels for unseen instances.

We only measure error on data we have, so we need to hold back some labelled data to estimate our performance on unseen data.

As seen [[Lecture 2 - Machine Learning Overview|last lecture]] we must only fit our model based on the training data. The degree to which we do this matters greatly.

![[different_fittings.png]]

