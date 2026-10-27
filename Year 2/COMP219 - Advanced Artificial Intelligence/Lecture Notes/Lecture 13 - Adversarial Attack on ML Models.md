## Adversarial Attack
Given a machine learning model $f$ and a genuine example $x$, we can find an **adversarial example** $x'$ which is close to $x$ but on which $f$ produces a different output.

We can extend this problem to ask:
- Can we define an approach that will always be able to find an adversarial example if there is one (Completeness)
- Can we find the $x'$ that is closest to $x$ that still results in a different output

