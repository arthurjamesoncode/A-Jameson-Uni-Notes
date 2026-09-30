## Notations
This lecture starts with a reminder of some of the maths notation we will need for this lecture. This will have been covered before in COMP109 and COMP116 but I will still include it here.

- $\mathbb Z$ denotes the set of all integers
- $\mathbb R$ denotes the set of all real numbers
- $A = \{a,b,c\}$ denotes a set of 3 elements and gives it the label $A$.
- $a\in A$ means that $a$ is an element of $A$.
- $B\subset A$ means that $B$ is a strict subset of $A$
- $B\subseteq A$ means that $B$ is a subset of $A$ or equal to $A$
- $\sum_{i=1}^n=a_1+...+a_n$

## Starting With Data
For every new dataset we start with a **problem statement**. This is a way to understand and define a problem.

We also need a **data dictionary**. This is centralised repository of information aboout the data such as:
- What it means
- Its relationship to other data
- Its origin
- Its usage
- Its format

These two things give us almost everything we need to know about the **context** we can use to analyse the data.
## Missing Data
There is also the problem of missing data. We rarely (if ever) have the complete set of information relevant to the context we are trying to understand through data analysis. As a result we need to understand how we can deal with data that we know/expect not to be in the dataset.

There are 3 common categories of missing data:
- **Missing Completely At Random (MCAR):** The missingness is independent of both observed variable and unobserved parameters. Almost no data is completely MCAR but may be MCAR in relation to the context the data is being viewed in.
- **Missing At Random (MAR):** The missingness can be fully explained by variables with completely information.
- **Missing Not At Random (MNAR)**: Values are missing for a related reason. This is also called nonignorable nonresponse. An easy example to understand this is if a survey was meant to track something related to depression but datapoints are missing from the most depressed because they were too depressed to show up.

There are a few ways to deal with missingness. The most common techniques include:
- **Omission**. This can be full or partial and can reduce the dataset and its power. 
- **Imputation**. This means to fill in data. This should never be done blindly since it can create new data with different properties.
- **Full analysis**. This can be done in a few ways such as EDA or ML.

It's important for methods to be robust to missingness and any deviations from robustness should be clearly spelled out.
## Descriptive vs Inferential Statistics
**Descriptive statistics** quantitatively summarise features of the sample data at hand by numbers and diagrams.

**Inferential statistics** aim to learn about the whole unobserved population, from a smaller sample at hand. We call the difference between the true population (which you never really have access to) and the sample estimate **bias**.

Essentially the difference is what it's being used for.

For example the average age in a class would be a descriptive statistic, but if we used that to draw conclusions about the average age of all UK students that would be a inferential statistic.
## Data Descriptors
There are a lot of different types of averages, all with various different uses, plus other useful things to describe datasets. This part will be dedicated to defining them and showing why they are used and what is useful.
### Arithmetic Mean
The most simple type of average is the arithmetic mean.

The arithmetic mean $\bar a$ of $n$ values $a_1,...,a_n\in\mathbb R$ is formally defined as
$$
\bar a = \frac1n\sum_{i=1}^na_i = \frac{a_1+...+a_n}n
$$

So the mean of the dataset
$$
A=\{5,3,2,4,5\}
$$
is
$$
\bar a = \frac{5+3+2+4+5}5 = \frac{19}5
$$

We can shorten the process of computing the mean by taking a weighted average of all unique datapoints where the weight is the number of times they appear.

For example, let a sample have $b_1,...,b_m$ unique values that appear $k_1,...,k_m$ times respectively. 

We can calculate the mean of this sample with
$$
\bar a = \frac1n\sum_{j=1}^mk_jb_j
$$

Arithmetic means are:
- Easy to compute
- Usually quite representative of a dataset given a reasonable distribution

Arithmetic means are a bit lacking though when it comes to dealing with outliers. Outliers will have a disproportional effect of the mean compared to those closer to the middle. They also don't always return a result that exists in your sample at all.

We should also be careful of misapplying mean. For example take the graph below: 
![[distance_time_mean.png]]

Here we travel a distance of 3 units over 4 units of time. During this time we travel as 2 speeds:
- $\frac21=2$
- $\frac13$

If tasked to find the average speed we travelled and we found the mean of the two speeds we would get:
$$
\frac12(2+\frac13) = \frac76
$$

The problem is that this doesn't account for the fact that we travelled at one of the speeds for longer. The actual **average speed** here is just $\frac34$.
### Standard Deviation
The mean measures the location of the data but doesn't give any **bounds** for it. As long as data is spread out proportionally, we will see no difference in mean regardless of how spread out it is.

If we try to measure spread of data by finding the mean of how far each point is away from the mean we will (definitionally) get 0. The negative values and the positive values will cancel each other out, and since they mean is the average, the average of both sides of the mean will be the same.

To avoid this we use the **squares** of each difference and then find the mean of that. When dealing with large datasets though this value will always be biased towards the small sample we have. To correct for this bias, instead of dividing by $n$ we divide by $n-1$.

>This is known as **Bessel's Correction** and isn't studied further in this module but you can read about it [here](https://en.wikipedia.org/wiki/Bessel%27s_correction).

After doing all of this we take the square root of the result and get our **standard deviation** $s$.

Putting all this together, the formula for $s$ is:
$$
s = \sqrt{\frac1{n-1}\sum_{i=1}^n(a_i-\bar a)^2}
$$
### Range, Median, & Mode
The **range** of a data sample is the difference between its minimal value and its maximal value. This obviously only works for scalar datasets.

The **median** of a data sample is the most middling value. Exactly half of the values come after it and exactly half of the values come before it. If there is an even number of datapoints, and therefore two middle values, you take the mean of the two.

The **mode** of a data sample is the most common value.

Median and mode are both, like mean, a type of average. They have different strengths and weaknesses though.

Median is:
- Not affected by outliers so good for skewed data
- Good for ordered data
But it:
- Isn't easy to compute with a formula
- Might not be one of the datapoints you collected

Mode is:
- Good for qualitative data
- Always one of the datapoints you've collected
But it:
- Isn't easy to compute with a formula
- Can be away from the middle
- Isn't always unique. Multiple modes can exist. The whole dataset could be modes if all values are distinct.

Median and mean will be the same if the dataset is symmetric around the median.
### Quartiles
The quartiles are like  (and include) the median except they divide the dataset into 4 parts instead of 2:
- The median is $Q_2$, the second quartile
- The lower, or 1st, quartile $Q_1$ separates the lowest 25% of data values from the highest 75%.
- The upper, or 3rd, quartile $Q_3$ separates the highest 25% of data values from the lowest 75%

These can be used to provide the **Tukey 5-number summary** which is:
$$
\min_{i=1,...,n}a_i \leq Q_1 \leq Q_2 \leq Q_3 \leq \max_{i=1,...,n}a_i
$$

The **interquartile range (IQR)** is defined as
$$
IQR = Q_3 - Q_1
$$

We use IQR to classify values as outliers. Any value outside
$$
[Q_1-1.5 \cdot \text{IQR},\;\; Q_3 + 1.5\cdot\text{IQR}]
$$
is considered an outlier.

**Box plots** are a way to quickly represent any sample of scalar values by using the Tukey 5-number summary.

You can see one pictured below
![[box_plot_example.png]]
### Other Means
There are a lot of different types of means.

The **geometric mean** of $a_1,...,a_n\geq0$ is
$$
(\prod_{i=1}^na_i)^\frac1n = (^n\sqrt{a_1a_2\cdots a_n})
$$

Geometric mean is for values which are proportional to each other e.g. compound interest.

It is never larger than the arithmetic mean and they are only equal when all datapoints are equal.

>There is also **harmonic mean** which is useful for  for ratios. 
>
>It was mentioned in the lecture but he didn't put it in the slides so I'm assuming it's not required knowledge. If you want to read about it you can do so [here](https://en.wikipedia.org/wiki/Harmonic_mean).
## Histograms & Skewness
Histograms are a graph which shows the number of datapoints which fall into each of several disjoint categories, called bins.

![[histogram_example.png]]

We can use histograms to quickly see symmetries and other properties. Especially for large datasets.

Take a look at the different shapes below![[histogram_properties.png]]

Generally, when we look at skewed data, the mean lies towards the direction of the skew. You can see this below.

![[skew_graphs.png]]

This is not a rule though, and is frequently violated. When one tail is long at the other is fat, skewness will not fit to what this says. 

>Skewness is a complicated topic that isn't covered in depth in this module. If you want to look at it you can view it [here](https://en.wikipedia.org/wiki/Skewness).
## Summary
- The first thing to do is try to understand your data.
- Missing values must be handled with care.
- Mean, mode, and median all have different uses and limits.
- Histograms, the IQR and box plots can be used to represent the shape of the data.