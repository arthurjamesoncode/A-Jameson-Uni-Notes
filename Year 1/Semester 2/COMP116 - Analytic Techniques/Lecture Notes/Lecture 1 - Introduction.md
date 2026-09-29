## What is this Module?
This module will give an overview of many important methods and techniques used in modern computer science. These techniques will be seen in many subjects such as:
- Machine Learning
- Data Science
- Algorithm Analysis
- Experimental Computing
- Optimization

This module will be delivered through 30 Lectures, and 10 tutorials. It should be about 150 hours total, including self study.

This module coves the important ideas over 7 main topics:
- **Numbers** - Number types, polynomials, etc.
- **Vectors and Matrices** - How they are used, graphical effects, etc.
- **Calculus** - The background, differential calculus, optimization, etc.
- **CS as Experimental Subject** - Data fitting, regression, etc.
- **Complex Numbers** - Background, forms, uses in CS, etc.
- **Advanced Linear Algebra** - Spectral methods in CS
- Some **Information Theory**.

### Module Resources
All course resources are available on Canvas. There is also a textbook, which can be seen in the **Reading Lists @ Liverpool** section on the module page. It is called "Computation Counts: An Introduction to Analytic Concepts in Computer Science" and is available in the library. I, unfortunately, cannot find a digital copy available online for free.

The textbook mentioned above is written by the previous module coordinator. He also has a dedicated YouTube channel for lectures for COMP116 which you can see [here](https://www.youtube.com/channel/UCQEsz19Suk2uX8f29WFNrAg).

There will be more links to resources given out in lecture slides and on Canvas.

A "student version" of the slides will be made available before each lecture. You should go through this and try to fill in the blanks on each slide. The full slides will be shown during the lecture and uploaded after the lectures.
### Assessments
This module is entirely assessed by in person assessments. You can see the dates, weights and topics below:

**Class Test 1, 17/02/2026 (10%):**
- Numbers
- Polynomials
- Vectors

**Class Test 2, 17/03/2026 (15%):
- Calculus
- Complex Numbers

**Class Test 3, 12/05/2026 (15%):
- Spectral Methods
- Information Theory
- Language

**Final Exam, During Assessment Period (60%):**
- Everything Covered
## This is a Maths Course
Maths is often called the language of the universe, and it is definitely the language of computers and AI.

A big focus of this model is on how we need to know maths in the age of AI.

AI models are often probabilistic and not logical. Because of this, they can generate outputs that *look* correct but are impossible or incorrect.

There is a concept in AI and computing called GIGO, which stands for "Garbage In, Garbage Out". This concept exemplifies the reality that evaluation of data and is incredibly important for training models. We also need these concepts in order to detect non-realistic outputs, shortcuts or just noise in general.

If you task an AI agent to write a function, we need to understand where to test (known as robustness and edge case analysis) to verify that the output matches reality. Without maths, we are blindly trusting a "black box" with the logic of the program.

To get a good result from an AI, your prompt needs to be grounded in technical constraints. In other AI models, the whole pipeline and reinforcement methods should be well structured.

Imagine you want to build an app that handles 5,000 requests per second. If you don't understand how to calculate latency, throughput and concurrency, you can't provide the AI with these constraints. If you don't, it could build a program that works for one user but crashes for two.

Often AI code is "verbose", meaning it takes the long way to solve a problem because it is mimicking common patterns found in the data it is trained on. 

Imagine an AI built app is running slowly or costing too much in hosting fees. We need to know Set Theory and complexity in order to optimise the program. Calculus can help us understand the "rate of change" in our system's performance. Linear algebra can help us optimize how our data is stored in memory.
## Geometry of Language
All the material in this module will be supported by a project written in Python, by the end of the module we will be able to run our own language model. Although we obviously don't have the resources and data to train it on the same quantity of data that LLMs are trained on.

You can see the structure of how these will be done below. Don't worry if you don't understand what something means, it will be expanded one when we get to it.
- Numbers $\to$ Bags of words
- Vectors and Matrices $\to$ Similarity of words
- Calculus $\to$ Optimising word position with gradient descent
- CS as An Experimental Subject $\to$ Zipf's Law
- Complex Numbers $\to$ Sentence cumulative meaning
- Advanced Linear Algebra $\to$ Word connectivity and dimensionality
- Information Theory $\to$ Next word prediction from entropy


