## What is Machine Learning?
Learning is the process of converting experience into expertise or knowledge.

Machine learning algorithms take, as an input, a set of training data and output something like a computer program which can perform some task.

You can think of the training data as experience and the outputted program as expertise.

There are many different types of machine learning, which we will briefly cover
### Supervised Learning
In supervised learning algorithms, the learner is presented with examples of labelled data. This takes the form$$
(x_1,L(x_1)),...,(x_n,L(x_n))\in X \times Y
$$where $L(x_n)$ is the label for $x_n$.

>$X \times Y$ means the cartesian product of $X$ and $Y$. It is a set of ordered pairs representing every combination of elements from $X$ and $Y$, where the first element of each pair is from $X$ and the second element of each pair is from $Y$. You can read more about this in [[Lecture 20 - Relations]] from the COMP109 module.

The algorithm then tries to find some way to generalise the examples to a function $f:X\to Y$. If $Y$ is finite, then we call $f$ a classier.

For one algorithm, $X$ could be the set of images of cats and dogs, and $Y$ could be $\{cat, dog\}$, and the goal could be to determine a classifier that can label an image as either a cat or a dog.

Supervised learning is the kind we will focus on for the rest of this module, looking at two simple but popular supervised learning algorithms, that aim to create classifiers.
### Unsupervised Learning
In unsupervised learning, the learner aims to find structure (or patterns) in data without using labelled examples. A typical problem of this type would be to group similar data into clusters.
### Reinforcement Learning
In reinforcement learning, the learner learns from rewards or punishments in a dynamic setting in which the the agent has a long-term goal, like winning a game or driving car a certain route. This is different from supervised learning as the possible actions of the agent are not directly classified.
### Supervised Learning Examples

### Hand-Written Digits
One task could be to determine a function that can recognise hand-written digits.

The image below represents a set of $28\times 28$ pixel images that could be taken as input. Each image could be represented as a vector $\vec{x}=(x_{1\times1},...,x_{28\times28})$ of real numbers. 
![[hand_written_digits.png]]
The agents job would then be to learn a classifier$$f:\{images\}\to\{0,1,2,3,4,5,6,7,8,9\}$$
This was actually one of the first commercial uses of machine learning, to recognise ZIP codes. You can read more it about [here.](https://en.wikipedia.org/wiki/MNIST_database) 
### Face Detection
Another task could be to recognise faces.

The image below could represent a set of labelled image windows indicating whether each image is a frontal-face, profile-face, or non-face.
![[faces.png]]
The agents job could then be to learn a classifier$$f:\{image\;windows\}\to\{\text{non-face, frontal-face, profile-face}\}$$
### Spam Detection
Another goal could be to detect whether an incoming email is spam or not.

The goal here would be to learn a classifier $$f:\{emails\}\to\{\text{spam, not-spam}\}$$from a set labelled input data representing emails.

It could take word-count as input data, as some words, like Viagra, may indicate spam.

This requires a learning system as the authors of spam emails are searching for ways to cut through spam filters. In other words, our enemy keeps innovating.

## Why Machine Learning?
We need machine learning, rather than directly programming our computers by hand for two main reasons:
- The problems complexity
- The need to adaptivity
### Tasks Too Complex to Program
Many tasks, that are performed by either humans or animals, are performed routinely. The problem is that we lack sufficient introspection in order to elaborate a well defined program.

There are countless examples:
- Hand-written digit recognition
- Face detection
- Spam detection
- Driving
- Speech recognition
- Playing games

Machine learning programs have achieved pretty satisfactory results.

There are also plenty of task that are beyond humans that machine learning techniques can be used to solve. Tasks that benefit from machine learning techniques are usually related to the analysis of very large and complex data sets.

Examples include:
- Astronomical Data
- Turning medical archives into medical knowledge
- Weather prediction
- Analysis of genomic data
- Search engines
- Stock prediction

These are all examples of meaningful information buried in data archives that are too large and too complex for humans to makes sense of.
### Adaptivity
One limiting feature of programmed tools is their rigidity. Once a program is written down and installed, it stays unchanged. However, many takes change over time or between users.

Machine learning tools, which can adapt their behaviour to their input data, offer a solution to this issues. They are, by nature, adaptive to changes in their environment.

For example:
- Decoding handwritten text - A fixed program can't adapt to variations between the handwriting of different users.
- Spam detections programs - Adapting automatically to the new strategies implemented by spammers.
- Speech recognition programs - Adapting to different people's voice