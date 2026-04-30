## Principle Component Analysis (PCA)
PCA is a dimensionality reduction method that linearly transforms a set of data onto a new coordinate system made of eigenvectors. We will be considering 2 dimensional spaces.

Essentially we are looking for a set **directions** or **principle components**,  which are:
- Principle Component 1 (PC1) - The direction with the highest variance
- Principle Component 2 (PC2) - The direction with the second highest variance
It is always the case that the PC2 vector is perpendicular to the PC1 vector.

>There are as many principle components, as there are variables in the dataset. If there are less samples than variables, then the number of principle components is equal to the number of samples instead.

The purpose of PCA is to eliminate **noise** from a dataset, essentially compressing it to only contain important information.

All of the principle components are eigenvectors of the **covariance-matrix** of the data. The corresponding eigenvalue connected to these eigenvectors indicate the level of variance.

>A covariance matrix is a representation of data that shows how different variables change together.

If one component has a significantly smaller eigenvalue associated with it, then the other component, then we can consider the component with the smaller eigenvalue **noise**, and the component with the larger eigenvalue the **signal** of the data.

Since we are working in 2-dimensional space, and therefore only have 2 principle components, I will now be referring to PC1 as the **signal** and PC2 as **noise** for simplicity.

>In actual analysis, you would decide is a principle component was noise or not depending on whether it's associated eigenvalue is near 0, or below some threshold.

![[PCA_example_graph.png]]

We can use the **signal-to-noise ratio** (SNR) to help us determine what data is worth keeping. 

If a dataset has a very **high SNR** then it means that most of the variance can be explained by the **signal component**(s), and therefore much of the data is redundant. We can then get a good representation our data by using our signal component(s) alone.

If a dataset has a very **low SNR** then it means that a quite lot of the variance is explained by the **noise component**. This means that we cannot reduce the number of components necessary to represent our data.

Below you can see some example datasets:
![[snr.png]]

Dataset **(a)** has a very low SNR, meaning that it is very hard to determine what is important data **(signal)** and what is unimportant noise.

Dataset **(c)**, however, has a very high SNR, meaning that almost all of the information in the dataset can be captured by a single principle component.

PCA is obviously more useful when working in higher dimensions, however even in this example you can see how, when there is a high SNR, we can go from storing 2 dimensions of data to a single dimension.

>I'm not sure, but I don't think there will be an exam question on this. The slides explain it so poorly and shallowly that I don't really see how they could ask a question on it. Also, Olga has started to show example questions in the slides and there is not one on this.
>
>Considering the above, and that much of this module is bonus stuff/applications that we won't see on the test, I don't think we will be asked a question on this.
## Image Compression
Much of the internet is built on sending images between people. Images are data, and sending data on a network is not completely free and therefore we want to make this data as **small as possible** but while losing as little information as possible. 

Essentially, we have a need to **compress our images**.

To look at **how** we do this we first need to understand **what** a digital image actually is.

A digital image is essentially a table of integers, where each integer represents the colour of the corresponding pixel.

Any table can be represented by a matrix, meaning that we can understand images and **matrices of integers**.

We want a way to **decrease the size** of this matrix, but without losing information. The way we can do this is by **singular value decomposition**.
### Singular Value Decomposition (SVD)
Given an $n\times k$ image $P$, let $W$ be the corresponding matrix.

The SVD of any $n\times k$ matrix $W$ is $U\Sigma V^T$, where $U$ and $V$ are rotation matrices and $\Sigma$ is a diagonal (or scaling) matrix with ordered values $(\sigma_1,..,\sigma_k)$ along the diagonal. $U$ is an $n\times n$ matrix, $V$ is a $k\times k$ matrix, and $\Sigma$ is an $n\times k$ matrix.

![[svd_figure.png]]

Exactly how we get these matrices will be covered [[Lecture 24 - Image Compression#How do we get $U$, $ Sigma$, and $V T$?|below]].

Geometrically, this means that any matrix can be decomposed into a **rotation** followed by a **scaling** followed by another **rotation**.

At first, this actually uses more space since we have to store:
- $U$ which is a $n\times n$ matrix using $n^2$ space
- $V^T$ which is a $k\times k$ matrix using $k^2$ space
- The diagonal values of $\Sigma$, which uses $\min(n, k)$ space. We can discard the other values since we know that are all 0. 
So the total space is $n^2 +k^2 + \min(n, k)$ which is greater than the previously needed $nk$ space, so we need some kind of trick to decrease the space.

The trick we use is to take the **Truncated SVD** of the image instead. This means that we keep only the top $p$ singular values, or the top $p$ diagonal values of $\Sigma$.

This means that we can represent $W$ as the product of:
- $U_p$ an $n\times p$ matrix requiring $np$ space
- $\Sigma_p$ a $p\times p$ diagonal matrix requiring $p$ space (we only need to store the diagonal)
- $V^T_p$ a $p\times k$ matrix requiring $pk$ space
So the total required space is
$$
np + pk + p = p(n + k + 1)
$$
As long as we choose a value $p$ which is much smaller than $n$ or $k$ this is far less space than $nk$. 

We are free to choose whatever value of $p$ we like. Higher values of $p$ will lose less information, but also compress the image less, while lower values of $p$ will result in a smaller image but more information is lost.
### How do we get $U$, $\Sigma$, and $V^T$?
We talked a lot about using these different types of matrices, but how do we actually derive them?

Well first given $W$ we need to find the matrices $W\cdot W^T$ and $W^T\cdot W$.

Any matrix multiplied by it's transpose are **symmetric**, **square**, **positive semi-definite** matrices. 
You don't need to know what [positive semi-definite](https://en.wikipedia.org/wiki/Definite_matrix) means, but this has an important property that we can use: Their eigenvalues are exclusively **real** and **non-negative**.

This means that $W\cdot W^T$ and $W^T\cdot W$, both have exclusively **real**, **non-negative** eigenvalues. The spectra are also identical to each other, meaning that every non-zero element is the same.

If we find the spectra $(\lambda_1,\lambda_2,...,\lambda_i,...,\lambda_n)$ of these matrices we can use it to derive $U$, $\Sigma$ and $V^T$.

- $\Sigma$ is defined as containing elements $s_{ij}$ such that
$$
s_{ij}=\cases{
\begin{split}
0\;\; & \text{ if } i\neq j \\
\sqrt{\lambda_i}\;\; & \text{ if i = j}
\end{split}
}
$$
- $U$ is defined as containing columns such that the $i^{th}$ column of $U$ is an eigenvector of $W\cdot W^T$ with eigenvalue $\lambda_i$.
- $V^T$ is defined as containing rows such that the $i^{th}$ row of $V^T$ is an eigenvector of $W^T\cdot W$ with eigenvalue $\lambda_i$
### What Can We Throw Away?
Now that we have a definition of $\Sigma$ in terms of the spectra of $W\cdot W^T$ we can revisit what it means to keep only the top $p$ singular values.

Let $\Sigma$ be an $n\times k$ matrix. The singular values in $\Sigma$ are ordered, like the eigenvalues, by size. The largest eigenvalues make a lot more difference to the final result then the smallest eigenvalues.

This means our decision to keep the top $p$ singular values of $\Sigma$ is the same as saying we want to **throw away** all but the largest $p$ most important values from $\Sigma$ and the corresponding eigenvectors from $U$ and $V$.

>Note for the images below, I don't have the original files. I just took screenshots of the lecture slides. This means he **actual** image size, will be different to the original.

Below you can see an example image
![[compressable_image.png]]
The original image is 388rows by 504 columns. This requires $388\times 504=195552$ pixels. Each pixel uses 24 bytes to store the colour (8 bytes each for the red, green, and blue components) so the full image needs 4693248 bytes in total to store this.

If we find the **truncated SVD** of this image for $p=10$, we can see we get the result.
![[compressed-p-10.png]]
While a lot worse than the original image, we are now storing much less. We have 3 matrices:
- A $388\times 10$ matrix $U$
- A $10\times10$ matrix $\Sigma$ stored as 10 singular values
- A $10\times 504$ matrix $V^T$
So the total size is $388\times 10 + 10 + 10\times 504=8930$ elements. Assuming all elements, like the pixels, take 24 bytes this needs 214320 bytes in total.

That's nearly 22 times less space. While the image isn't great, considering how much less space it takes this is a good result.

Now let's look at the result of getting the truncated SVD of this image when $p=100$.
![[compressed-p-100.png]]
This is a much better result, not much information is lost at all. If seen on a small smartphone screen, it may look identical to the original. Let's see how much space we save.

We have 3 matrices.
- A $388\times 100$ matrix $U$
- A $100\times100$ matrix $\Sigma$ stored as 100 singular values
- A $100\times 504$ matrix $V^T$
So the total size is $388\times 100 + 100 + 100\times 504=89300$ elements. Assuming all elements, like the pixels, take 24 bytes this needs 2143200 bytes in total. This is still less than half of the required bytes to store the original image.
### Example Exam Question
The slides include an example exam question which goes as follows:

"A square image consists of 1000 rows and 1000 columns, occupying $1000 ⋅ 1000 ≈ 1Mb$ space. Its owner wishes to forward the image in an encoding as 3 matrices which will use a total space of ≤ $0.75Mb$. What size of the $S$ matrix (the diagonal matrix formed from eigenvalues in an SVD encoding) both achieves this aim and maximizes the quality of the compressed encoding?"

To solve this is to essentially find a value minimum value of $p$ which we could choose to end up with 3 matrices with less than $1000\cdot 1000 \cdot 0.75= 750,000$ elements.

The total size to store the 3 matrices we will use in terms of $p$ is:
- $U:1000\times p=1000p$
- $S:p$
- $V^T:p \times 1000=1000p$

From this we can derive the inequality
$$
\begin{split}
1000p + p + 1000p &\leq 750,000 \\
2001p &\leq 750000 \\
p &\leq \frac{750000}{2001} \\
p &\leq 374.81
\end{split}
$$

Since $p$ must be an integer, we know the maximum value of $p$ which satisfies this inequality is $374$ and therefore the matrix $S$ should $374\times 374$.