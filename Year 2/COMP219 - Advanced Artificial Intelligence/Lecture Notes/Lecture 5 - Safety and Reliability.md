## Safety Concerns
Machine learning has been very successful in a lot of areas but there are serious concerns about applying machine learning to safety critical systems such as self-driving cars or automatic medical diagnosis.

The main problem here is that machine learning models may express erroneous behaviour. Since a learned model $f$ seeks to approximate a target function $h$, there is erroneous behaviour of $f$ when there exists an input $x$ such that
$$
f(x)\neq h(x)
$$

This lecture is spent going over a number of reasons that machine learning models may exhibit erroneous behaviour, and how to think about these concerns.
## Generalisation Error and Overfitting
**Generalisation Error** is a metric which allows us to gauge how reliably a machine learning model performs on unseen data compared to its training data.

First we must define a few things.
- $\mathcal L(y, f(x))$ is the loss between the prediction $f(x)$ and the truth $y$
- $D$ is the training dataset
- $\mathcal D$ is the underlying data distribution
- $\mathcal L_{emp}(f, D)$ is the **empirical loss**, or the average loss given by $f$ on the training dataset. It is given by
$$
\mathcal L_{emp}(f, D) = \frac1{|D|}\sum_{(x,y)\in D}\mathcal L(y, f(x))
$$
- $\mathcal L_{exp}(f, \mathcal D)$ is the **expected loss**, or the theoretical average loss of the loss across every possible example drawn from the real distribution $\mathcal D$ it is given by
$$
\mathcal L_{exp}(f, \mathcal D) = \frac1{|\mathcal D|}\sum_{(x,y)\in \mathcal D}\mathcal L(y, f(x))
$$

>Note: the slides use a different notation to say that $\mathcal L_{exp}$ is the expected value of the loss function over $\mathcal D$ but the above notation is simpler and means the same thing. 
>
>I don't know if they avoid it because $|\mathcal D|$ will inevitably be unknown, but so will $\mathcal D$ so I don't understand the choice to change it from $\mathcal L_{emp}$.

Now given these two things we can define **generalisation error** $GE(f,D)$ as
$$
GE(f, D) = |\mathcal L_{emp}(f, D) - \mathcal L_{exp}(f, \mathcal D)|
$$

In practice, we cannot find the true value of $\mathcal D$ so we instead just hold back a separate known dataset to use as validation data with which we can estimate $\mathcal L_{exp}(f, \mathcal D)$.

Generalisation error is closely related to **overfitting**. This is when a machine learning model learns quirks specific to the training data and therefore:
- Performs very well on training data
- But performs badly on validation data
## Adversarial Examples
Adversarial examples are pieces of data which are very close to other pieces of but which are classified differently.

Essentially given an instance $x$ with the true counterpart $y$, the function may classify $x$ correctly
$$
f(x) = y
$$
but when adding a small mutation to $x$ this changes the classification
$$
f(x+\epsilon)\neq f(x)
$$

This is a problem when $\epsilon$ is not a big enough difference to actually change the *correct* classification.

![[adversarial_example.png]]

An adversarial example $x'$ is usually measured from two aspects:
- Magnitude of perturbation $\epsilon=||x-x'||$
- Probability gap between before and after the perturbation $|f_y(x)-f_y(x')|$

Finding adversarial examples is an optimisation problem. 

Given a real example $x$ the goal is find the $x'$ which minimises
$$
||x-x'|| - \lambda|f_y(x)-f_y(x')|
$$
while 
$$f(x) \neq f(x')\text{ and } ||x-x'||\leq\delta$$

In these formulas:
- $\lambda$ is a positive weighting parameter that is used to balance the trade off between keeping the perturbation small and seeing a large drop in confidence
- $\delta$ is a hard upper bound for the perturbation. This is used to try and ensure that the found adversarial example is not far enough away that the classification should change.
## Data Poisoning & Backdoor Attack
Poisoning attacks occur when malicious data is injected into the training process, causing the learning algorithm to learn something incorrectly.

This can be used for targeted attacks, such as changing the labels of a certain sample, but it can also be used for **backdoor attacks**.

The idea of a backdoor attack is to compromise a model $f$ such that when given a **triggered input** $x'=x+\alpha$ which is a an new input created by adding a trigger $\alpha$ to a clean input $x$, $f(x')$ will always be the label $y_\alpha$ which is set by the attacker.

When given clean inputs, the model will behave as normal without any observable performance reduction.

Backdoor attacks can be done via data poisoning, but they could be done in other ways as well such as directly manipulating the server architecture.
## Model Stealing
Given a model $f$, model stealing is when an agent attempts to reconstruct a model $f'$ by querying the model $f$. $f'$ is now essentially a substitute of $f$.

There is also the problem of model inversion, when inputs or sensitive attributes are are recovered from the model outputs. For example a face is reconstructed from the model outputs.

Distillation is like model stealing, but authorised. It is when a student model is trained on the outputs of a teacher model. Inversion can be used to generate data for distillation.

Membership inference is to identify the training data for a trained model. Given a a model $f$ and an instance $x$ it is the problem of determining if the instance $x$ was in the model's training dataset.
## GenAI
The rest of this lecture goes over safety and reliability issues with GenAI such as:
- Robustness
- Hallucinations
- AI agent cyber attacks

It's all very interesting and applicable, but I don't think that it is something we will be tested on, and therefore I am not going to spend time adding this to my notes here.