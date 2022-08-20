---
title: Cochran's Theorem
author: tqian
date: 2022-08-19 12:00:00 +0800
categories: [Statistics]
tags: [statistics, math]
math: true
mermaid: true
---
# Introduction

This will be a technical write up Cochran's theorem, a theorem on the partitioning of the sum of squares of normal variables. As an example, Bessel's correction can be seen as a special case of this. Similarly, the claims about standard errors can also be seen to be true by Cochran's theorem. 

## Quadratic forms

The overall idea of Cochran's theorem is to split the sum of squares of random variables (RV) into many quadratic forms. Each form is the cause of some variation. 

Theorem: say that $\vec x \sim \mathcal N(\vec\mu, \Lambda)$, with $\Lambda$ positve definite. If $n$  is the dimension of $\vec x$, then 

$$(\vec x- \vec \mu)^T \Lambda^{-1} (\vec x-\vec\mu) \sim \chi^2(n).$$

Proof: Let $\vec y = \Lambda^{-\frac 12} (\vec x - \vec\mu)$. Then we have $E[\vec y]=\vec 0, \mathrm{Cov}[\vec y] = I$. So $y\sim \mathcal N(\vec 0, I)$. We can compute the above quadratic form to be exactly equivalent to $\vec y^T \vec y$. Therefore, the claim is proven.

# The main result

## Cochran's theorem statement

Say we have $X_1, \dots, X_n$ be independent $\mathcal N(0,\sigma^2)$ RVs such that 

$$\sum_{i=1}^n X_i^2 = Q_1 + \dots + Q_k,$$

for positive semi-definite quadratic forms $Q_i$. That is, $Q_i = X^T A_iX$, where $X$ is the vector of $X_i$, and $A_i$ is positive semi-definite. Let the rank of $A_i$ be $r_i$. The following are equivalent

- $r_1 + \dots + r_n = n$
- $Q_i$ are independent
- $Q_i\sim\chi^2(r_i)$

This can be rephrased as if $\sum A_i = A$ where $A$ is idempotent and $\sum r_i = \mathrm{rank}(A)$, we have the same results. This is easily seen by just orthogonalizing $A$. 

## Proof

Lemma: If $X$ is a standard normal vector, then if we have symmetric matrices $Q, Q'$, then if $X^TQX$ and $X^TQ'X$ have the same distribution, then $Q$ and $Q'$ have the same eigenvalues.

Proof: Note that multiplying standard normal vectors by orthogonal matrices doesn't change its distribution. So intuitively $Q, Q'$ are similar. To actually do this, we have to calculate characteristic functions, which isn't that interesting and is left as an exercise to the reader. 

So now we claim that $I = \sum A_i$. We can see this because we have that $X^T(I - \sum A_i)X = 0 = X^T0X$ (just by rearranging our assumptions). Therefore by our lemma, the inner matrices are the same because they all have eigenvalues of all $0$'s. 

Now we have a very important lemma, which is the key point of this proof. 

Lemma: Given $M_i$ symmetric and $M_i$ have eigenvalues of only $0, 1$ (ignore matrices with all eigenvalues of $0$), if $\sum M_i = I$, then these matrices share the same eigenvectors. 

Proof: Consider an eigenvector $v$ of $M_1$. Then $M_1v = v$, or that it has an eigenvalue of $0$. Then we have that $v^Tv = v^T I v = v^T\left(\sum M_i\right) v = v^Tv + \sum_{j\neq i} v^TM_jv$. The latter part is all nonnegative because $M_j$ are all positive semi-definite. Furthermore, because of this, this implies that each term in the sum is $0$, and thus $v$ must be a $0$ eigenvector of $M_j$. So each of the eigenvectors of $M_1$ is an eigenvector of all the other matrices. They must share the same eigenvectors then.

We do some simple casework now to establish each of the claims. 

### Case 1: $Q_i$ are independent. 

Let's diagonalize $A_i$ by $O$. Then note that if we let $C_i = I - A_i$, then $OC_iO^T = I - OB_iO^T$, which means $C_i$ is also diagonalized. Consider $W = OX$. Then we have $Q_i = W^T(OA_iO^T)W, \sum_{j\neq i} Q_j = W^T(I - OB_iO^T)W$. Because $Q_i$ are independent, $Q_i$ is independent to $\sum_{j\neq i} Q_j$. We inspect the diagonal values of the two matrices, and if they're independent, their nonzero diagonal entires are disjoint. This forces all their diagonal values to be $1$ or $0$. This forces all eigenvalues of $A_i$ to be $1$ or $0$. The inner matrices have ranks $r_i$, which implies that $A_i$ has $r_i$ eigenvalues of $1$ and the rest $0$'s, so since these matrices sum to $I$, we have that $\sum r_i = n$. Similarly $Q_i\sim \chi^2(r_i)$. 

### Case 2: $Q_i \sim \chi^2(r_i)$$

Let $O$ be the matrix that diagonalizes $A_i$. Because each quadratic form is $\chi^2(r_i)$, once we diagonalize $A_i$, we can use our first lemma above to show all the eigenvalues are $0, 1$. Then we can choose $O$ so that it simultaneously diagonalizes all of $A_i$. So let's simultaneously diagonalize all the matrices and add them up. They sum to $I$, which implies that $\sum r_i = n$ and that their diagonal entries are disjoint, which implies independence.

### Case 3: $\sum r_i = n$

This is the most complicated case. We first demonstrate that the matrices $A_i$ can be simultaneously diagonalized. 

Note that if we let $C_i = \sum_{j\neq i} A_j$, then the rank of $C_i$ is at most $n - r_i$. But since we have $C_i + A_i$ has rank exactly $i$, it most be exactly rank $n - r_i$. Let's diagonalize $A_i$ such that it has its eigenvalues in the first $r_i$ diagonal values. Since $C_i = I - B_i$, $C_i$ can be simultaneously diagonalized. The fact that the diagonalized version of $C_i$ and $B_i$ sum to $I$, and their ranks are $r_i, n - r_i$, this means that they must only have eigenvalues of $1, 0$. So let's say we did this for $B_1, C_1$. Then we can repeat the argument in this same basis for $B_2, C_1  - B_2$ because $C_1$ is a diagonal matrices with only $1$'s and $0$'s in this basis. We can continue down this root do show the starting claim that all the matrices $A_i$ can be simultaneously diagonalized. 

Let $O$ be a matrix that diagonalizes all of $A_i$ at once. The we diagonalize them all at once, and since they have eigenvalues $1$ and $0$ and have ranks that sum to $n$ and the matrices sum to $I$, we again get they are independent with $\chi^2(r_i)$ distribution. 

# Implications of Cochran's theorem

## Sample mean and sample variance and Bessel's correction

Consider $X_1, \dots, X_n$ with mean $\mu$ and variance $sigma^2$. Then we have that 

$$\sum \left(\frac{X_i-\mu}{\sigma}\right)^2 = \sum \left(\frac{X_i-\overline X}\sigma\right)^2 + n \left(\frac{\overline X - \mu}\sigma\right)^2 = Q_1 + Q_2.$$

Let $J_n$ be the matrix of ones, with rank $1$. Then $A_1 = I_n \frac{J_n}n$ and $B_2 = \frac{J_n}n$. The ranks are $n-1, 1$, we can show this by showing the first matrix is idempotent, and thus the rank is the trace. The first and second must be indpendent. The first part is the sample variance scaled, the second part is the sample mean scaled and squared, and they are shown to independent. Furthermore, we note that the first term is a $\chi^2(n-1)$ distribution. Thus to get an unbiased estimate of $\sigma^2$, since the EV of chi-squared is equal to its degrees of freedom, we must divide by $n-1$. 

A cool fact is the sample mean and sample variance are only independent for normal distributions. 

## Generalized version of Bessel's correction

Let's say we're trying to estimate $Y$ based off $X$, where $X$ is $n\times (p+1)$. This is the standard regression formulation. Then 

$$SSTO = Y^T\left(I - \frac 1n J\right)Y,$$

$$SSE = Y^T(I - H)Y,$$

$$SSR = Y^T\left(H - \frac 1n J\right)Y.$$

Here $H$ is the hat matrix. The rank of the first matrix is $n-1$. Note that a hat matrix is idempotent. So its rank is $p+1$. Similarly $I-H$ is idempotent, so its rank is $n-p-1$. It remains to determine the rank of $H - \frac 1n J$. Note that $H 1 = 1$, where this is the vector of all $1$'s. This is because we have included a constant in $H$, which means the projection of the all $1$ vector must be itself. So we can expand $H - \frac 1n J$ to be symmetric and idempotent. So its trace is its rank, and that's just the difference of the two traces, which is $p$. Therefore the conditions of Cochran are satisfied. $SSE$ thus is $\chi^2(n - p - 1)$. This is important because it shows we must divide by $n-p-1$ when calculating the standard error. Furthermore, when computing significance tests on $\beta$, the coefficient vector from linear regression, we must use a $t$ distribution with $n-p-1$ degrees of freedom. 






