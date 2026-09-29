## Injective, or 1 to 1, Functions
We call a function, $f: A\to B$, injective if $f(a) = f(b) \implies a=b\; \forall a,b\in A$.

>$\implies$ means implies. $x$ implies $y$ if every time $x$ is true, $y$ is also true.
>
>The above statement, read in plain English is this: "We call a function, $f: A\to B$, injective if whenever $f(a)=f(b)$, $a$ and $b$ are the same for all values $a, b$ in $A$"

This is equivalent to: $\forall a,b\in A, a\neq b\implies f(a) \neq f(b)\;$. 

>The above in plain English is read as: "For all values $a$ and $b$ in $A$, if $a$ does not equal $b$ then $f(a)$ does not equal $f(b)$."

Essentially an injective function does not repeat values. Different inputs will always given different outputs.

For Example:
- $f: \mathbb{Z}\to\mathbb{Z}$ given by $f(x)=x^2$ is not injective as $f(-1)=f(1)=1$.
- $g: \mathbb{Z}\to\mathbb{Z}$ given by $g(x)=2x$ is injective.
## Proving Injectivity
In order to disprove injectivity all we need to do is find example values $a, b$, where $a\neq b$ and $f(a)=f(b)$.

For example: $f: \mathbb{Z}\to\mathbb{Z}$ given by $f(x)=x^2$ can be shown to lack injectivity just by providing any example of $a$ and $b$ where $a=-b$. Such as $1$, and $-1$ as shown above.

To prove injectivity we do this by showing that when we have fixed but arbitrary values $a$ and $b$ such that $a\neq b$, it is also true that $f(a)\neq f(b)$.

For example to prove that $g: \mathbb{Z}\to\mathbb{Z}$ given by $g(x)=2x$ is injective we can do:
	Let $a,b\in\mathbb{Z}$ such that $a\neq b$
	$g(a)=2a$
	$g(b) = 2b$
	Since $a\neq b$, we know that $2a\neq2b$ and therefore $g(a)\neq g(b)$
	Therefore $g$ is injective as whenever $a\neq b$ it means that $g(a) \neq g(b)$

### Surjective, or Onto, Functions
A function, $f: A\to B$ is surjective if the range of the function, $f(A)$, coincides with the codomain of the function.

So a function,$f: A\to B$, is surjective if $f(A) = B$.

If a function is surjective it means that for every $b\in B,\exists a\in A$ such that $b=f(a)$.

>Reminder: $\exists$ means "there exists".

This is why they are called "onto" functions, because they map "onto" the whole of the codomain.

For Example:
- $f: \mathbb{Z}\to\mathbb{Z}$ given by $f(x)=x^2$ is not surjective as -1 has no value $a\in \mathbb{Z}$ such that $f(a)=-1$.
- $g: \mathbb{Z}\to\mathbb{Z}$ given by $g(x)=2x$ is not surjective as 3 has no value $a\in\mathbb{Z}$ such that $g(a) = 3$.
- $h: \mathbb{Q}\to\mathbb{Q}$ given by $h(x)=2x$ is surjective.

>Notice how when the domain and codomain changes, a function that wasn't surjective can become surjective as the only difference between $g$ and $h$ is their domain and codomain.

### Proving Surjectivity
In order to prove surjectivity of a function, $f: X \to Y$, we take an arbitrary $y\in Y$ and show that it can be gotten from some value, $x\in X$.

To do this for the above example $h: \mathbb{Q}\to\mathbb{Q}$ given by $h(x)=2x$ we do the following:
	First choose a fixed but arbitrary value in $\mathbb{Q}$ and let that be the result of the function
		Let $y = h(x)$
	Rearrange to find the value of $x$ in terms of $y$
		$y=2x$ 
		$x=\frac{y}{2}$
	Show that $x\in Q$
		Since $y \in Q$, by definition of $\mathbb{Q}$, $y=\frac{a}{b}$ where $a,b\in \mathbb{Z}$.
		Therefore $x=\frac{a}{2b}$.
		Since $a,b\in\mathbb{Z}$ by definition of $\mathbb{Q},\; x\in\mathbb{Q}$.
	As each arbitrary value, $y\in\mathbb{Q}$ can be gotten by applying the function $h$ to some $x\in\mathbb{Q}$, we know that this function is surjective.

## Bijective Functions
We call a function, $f: X\to Y$, bijective if $f$ is both injective and surjective. A bijective function is also called a bijection from $X\to Y$.

For Example:
- $f: \mathbb{Q}\to\mathbb{Q}$ given by $f(x)=2x$ is bijective.
### Proving Bijectivity
In order to prove bijectivity of a function, $f: X\to Y$, we need to first prove that $f$ is injective and then that $f$ is surjective. 

This has been gone through above so there is no need to repeat that here.
### Inverse Functions
If $f$ is a bijection from a set $X$ to a set $Y$, then there is a function $f^{-1}: Y\to X$ that undoes the action of $f$. $f^{-1}$ maps every element of $Y$ back the element of $X$ that it came from and is called the inverse function of $f$.

If an inverse function exists then $f(a) = b \iff f^{-1}(b)=a$.

>$\iff$ means "if, and only if".

For example, take the function $f: \mathbb{R}\to\mathbb{R}$ given by $f(x)=4x+3$. This is a bijective function, and as such has an inverse function. In order to find the inverse we do this:
	Let $y=f(x)$
	$y=4x+3$
	$x=\frac{y-3}{4}$
	$f^{-1}(y)=\frac{y-3}{4}$

The steps are as follows:
- Set $y=f(x)$
- Rearrange for $x$ in terms of $y$
- Replace $x$ with $f^{-1}(y)$

For another example, let $A=\{x\;|\;x\in\mathbb{R},x\neq 1\}$ and $f: A\to A$ be given by $f(x)=\frac{x}{x-1}$.

We will show that $f$ is bijective and then determine the inverse function of $f$.

First we must prove injectivity:
	Let $a,b\in A$ such that $f(a) = f(b)$
	$f(a) = \frac{a}{a-1},f(b) = \frac{b}{b-1}$
	$\frac{a}{a-1} = \frac{b}{b-1},ab-a=ab-b,a=b$
	Since $a=b$, must be true when $f(a)=f(b)$, $f$ is injective.

Next we must prove surjectivity:
	Let $y=f(x)$.
	$y= \frac{x}{x-1},yx-y=x, yx-x=y, x(y-1)=y,x=\frac{y}{y-1}$.
	Since $y\in A$, and $x=\frac{y}{y-1}$ this means that $x\in A$ as well.
	Therefore the function is surjective.

Now we find the inverse function. We actually already found this as part of proving that $f$ is surjective, all we need to do is substitute $x$ for $f^{-1}(y)$.

So the inverse function of $f$ is $f^{-1}(y) = \frac{y}{y-1}$.
## Classifying Functions
The following is just a series of examples of functions, their classification, and reasoning why.

$f: \{a,b,c\} \to \{1,2,3\}$ given by:
- $f(a) = 1$
- $f(b) = 1$
- $f(c) = 3$

$f$ is not injective as both $a$ and $b$ map onto $1$.
$f$ is not surjective as no value maps onto $2$

$g: \{a,b,c\} \to \{1,2,3\}$ given by:
- $g(a) = 1$
- $g(b) = 3$
- $g(c) = 2$

$g$ is injective as no 2 values map onto the same value.
$g$ is surjective as all the elements in the codomain are mapped to.

$h: \{a,b,c\} \to \{1,2\}$ given by:
- $h(a) = 1$
- $h(b) = 1$
- $h(c) = 2$

$h$ is not injective as both $a$ and $b$ map onto $1$.
$h$ is surjective as all the elements in the codomain are mapped to.

