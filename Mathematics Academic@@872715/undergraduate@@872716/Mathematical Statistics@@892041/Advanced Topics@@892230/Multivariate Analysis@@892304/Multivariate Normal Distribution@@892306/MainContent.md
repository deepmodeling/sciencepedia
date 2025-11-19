## Introduction
The multivariate [normal distribution](@entry_id:137477) represents a fundamental extension of the familiar one-dimensional bell curve, providing a powerful mathematical framework for modeling systems with multiple, interrelated random variables. Its importance in statistics and data science cannot be overstated, yet understanding how its components—the [mean vector](@entry_id:266544) and covariance matrix—govern its behavior in higher dimensions presents a significant conceptual leap. This article bridges that gap by providing a clear and structured exploration of this essential topic.

In the following chapters, you will build a comprehensive understanding of the multivariate [normal distribution](@entry_id:137477). We will begin in "Principles and Mechanisms" by establishing its formal definition, deriving its probability density function, and examining its crucial mathematical properties. Next, "Applications and Interdisciplinary Connections" will showcase the distribution's versatility, demonstrating how it serves as the theoretical backbone for methods in fields ranging from machine learning to quantitative finance. Finally, "Hands-On Practices" will provide opportunities to apply these concepts through guided problems, cementing your theoretical knowledge with practical skills.

## Principles and Mechanisms

The multivariate normal distribution is a cornerstone of statistical theory, extending the familiar bell-shaped curve of the univariate normal distribution to multiple dimensions. Its mathematical properties make it exceptionally tractable for modeling complex phenomena where several random quantities are interrelated. This chapter delves into the core principles and mechanisms of the multivariate normal distribution, from its formal definition to its fundamental properties and geometric interpretations.

### Definition and Probability Density Function

A random vector $\mathbf{X} = (X_1, X_2, \dots, X_p)^T$ is said to have a **$p$-variate normal distribution** if every linear combination of its components, $Y = a_1 X_1 + a_2 X_2 + \dots + a_p X_p$, follows a univariate normal distribution. The distribution is completely characterized by two parameters: the **[mean vector](@entry_id:266544)** $\boldsymbol{\mu}$, a $p \times 1$ vector of the expected values of each component, and the **covariance matrix** $\boldsymbol{\Sigma}$, a $p \times p$ symmetric and [positive semi-definite matrix](@entry_id:155265) containing the variances and covariances of the components. We denote this as $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$.

The [mean vector](@entry_id:266544) $\boldsymbol{\mu}$ is defined as:
$$
\boldsymbol{\mu} = \mathbb{E}[\mathbf{X}] = \begin{pmatrix} \mathbb{E}[X_1] \\ \mathbb{E}[X_2] \\ \vdots \\ \mathbb{E}[X_p] \end{pmatrix}
$$
The covariance matrix $\boldsymbol{\Sigma}$ is defined by its elements $\Sigma_{ij} = \operatorname{Cov}(X_i, X_j)$. Specifically:
$$
\boldsymbol{\Sigma} = \mathbb{E}[(\mathbf{X}-\boldsymbol{\mu})(\mathbf{X}-\boldsymbol{\mu})^T] = \begin{pmatrix}
\operatorname{Var}(X_1) & \operatorname{Cov}(X_1, X_2) & \cdots & \operatorname{Cov}(X_1, X_p) \\
\operatorname{Cov}(X_2, X_1) & \operatorname{Var}(X_2) & \cdots & \operatorname{Cov}(X_2, X_p) \\
\vdots & \vdots & \ddots & \vdots \\
\operatorname{Cov}(X_p, X_1) & \operatorname{Cov}(X_p, X_2) & \cdots & \operatorname{Var}(X_p)
\end{pmatrix}
$$
When the covariance matrix $\boldsymbol{\Sigma}$ is strictly [positive definite](@entry_id:149459) (and therefore invertible), the distribution is said to be non-degenerate and possesses a **probability density function (PDF)**. The PDF for a random vector $\mathbf{x} = (x_1, \dots, x_p)^T$ is given by:
$$
f(\mathbf{x}; \boldsymbol{\mu}, \boldsymbol{\Sigma}) = \frac{1}{(2\pi)^{p/2} |\boldsymbol{\Sigma}|^{1/2}} \exp\left( -\frac{1}{2} (\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu}) \right)
$$
The term $(\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu})$ in the exponent is a quadratic form known as the squared **Mahalanobis distance**. It measures the "distance" of the point $\mathbf{x}$ from the mean $\boldsymbol{\mu}$, accounting for the scale and correlation of the variables. The term $|\boldsymbol{\Sigma}|$ is the determinant of the covariance matrix, and its square root in the denominator acts as a [normalizing constant](@entry_id:752675), ensuring the total probability integrates to one.

To make this formula concrete, consider a bivariate normal random vector $\mathbf{X} = (X_1, X_2)^T$ with [mean vector](@entry_id:266544) $\boldsymbol{\mu} = \begin{pmatrix} -1 \\ 3 \end{pmatrix}$ and covariance matrix $\boldsymbol{\Sigma} = \begin{pmatrix} 4 & -2 \\ -2 & 5 \end{pmatrix}$ [@problem_id:1939216]. To find its PDF, we first compute the determinant and inverse of $\boldsymbol{\Sigma}$:
$$
|\boldsymbol{\Sigma}| = (4)(5) - (-2)(-2) = 20 - 4 = 16
$$
$$
\boldsymbol{\Sigma}^{-1} = \frac{1}{16} \begin{pmatrix} 5 & 2 \\ 2 & 4 \end{pmatrix}
$$
The quadratic form is $(\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu})$, where $\mathbf{x} = \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$ and $\mathbf{x}-\boldsymbol{\mu} = \begin{pmatrix} x_1+1 \\ x_2-3 \end{pmatrix}$. The expansion is:
$$
\begin{pmatrix} x_1+1 & x_2-3 \end{pmatrix} \left( \frac{1}{16} \begin{pmatrix} 5 & 2 \\ 2 & 4 \end{pmatrix} \right) \begin{pmatrix} x_1+1 \\ x_2-3 \end{pmatrix} = \frac{1}{16} (5(x_1+1)^2 + 4(x_1+1)(x_2-3) + 4(x_2-3)^2)
$$
Plugging these components into the general PDF formula with $p=2$, we obtain the explicit function:
$$
f(x_1, x_2) = \frac{1}{(2\pi)^{2/2} |16|^{1/2}} \exp\left( -\frac{1}{2} \left[ \frac{1}{16} (5(x_1+1)^2 + 4(x_1+1)(x_2-3) + 4(x_2-3)^2) \right] \right)
$$
$$
f(x_1, x_2) = \frac{1}{8\pi} \exp\left( -\frac{1}{32} (5(x_1+1)^2 + 4(x_1+1)(x_2-3) + 4(x_2-3)^2) \right)
$$

### Geometric Interpretation

The structure of the multivariate normal PDF lends itself to a clear geometric interpretation. The function's value is constant whenever the Mahalanobis distance is constant. The loci of points in $\mathbb{R}^p$ where the density $f(\mathbf{x})$ is constant are given by the equation:
$$
(\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu}) = c
$$
for some constant $c > 0$. This equation defines an **[ellipsoid](@entry_id:165811)** (or an ellipse in the bivariate case, $p=2$) centered at the [mean vector](@entry_id:266544) $\boldsymbol{\mu}$. These ellipsoids are the **[level sets](@entry_id:151155)** or **contours** of the distribution.

The shape and orientation of these ellipsoids are determined entirely by the covariance matrix $\boldsymbol{\Sigma}$. The **principal axes** of the ellipsoids are aligned with the eigenvectors of $\boldsymbol{\Sigma}$. The length of each principal axis is proportional to the square root of the corresponding eigenvalue. The major axis, which is the longest, corresponds to the direction of maximum variance and is aligned with the eigenvector associated with the largest eigenvalue.

For instance, consider a [bivariate normal distribution](@entry_id:165129) with covariance matrix $\boldsymbol{\Sigma} = \begin{pmatrix} 4 & 2 \\ 2 & 9 \end{pmatrix}$ [@problem_id:1320466]. The orientation of the elliptical contours is found by analyzing the eigenvectors of $\boldsymbol{\Sigma}$. The eigenvalues $\lambda$ are solutions to the [characteristic equation](@entry_id:149057) $\det(\boldsymbol{\Sigma} - \lambda I) = 0$:
$$
(4-\lambda)(9-\lambda) - (2)(2) = \lambda^2 - 13\lambda + 32 = 0
$$
The largest eigenvalue is $\lambda_1 = \frac{13+\sqrt{41}}{2}$. An eigenvector $\mathbf{v} = (v_1, v_2)^T$ corresponding to $\lambda_1$ gives the direction of the major axis. The slope of this axis is $m = v_2/v_1 = (\lambda_1 - 4)/2$. The angle $\theta$ this axis makes with the positive $x$-axis is therefore $\theta = \arctan(m)$. In this case, the angle is approximately $70.7^\circ$, indicating that the data cloud is stretched along a line tilted steeply upward. If the off-diagonal elements of $\boldsymbol{\Sigma}$ were zero (i.e., no correlation), the eigenvectors would align with the coordinate axes, and the ellipses would be oriented horizontally and vertically.

### Fundamental Properties

The multivariate [normal distribution](@entry_id:137477) is distinguished by several powerful properties that facilitate its use in modeling and inference.

#### Linear Transformations

One of the most important properties is its closure under affine transformations. If $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$, and we define a new random vector $\mathbf{Y} = A\mathbf{X} + \mathbf{b}$, where $A$ is a constant $q \times p$ matrix and $\mathbf{b}$ is a constant $q \times 1$ vector, then $\mathbf{Y}$ also follows a multivariate normal distribution. Its parameters are derived straightforwardly:
$$
\mathbb{E}[\mathbf{Y}] = \mathbb{E}[A\mathbf{X} + \mathbf{b}] = A\mathbb{E}[\mathbf{X}] + \mathbf{b} = A\boldsymbol{\mu} + \mathbf{b}
$$
$$
\operatorname{Cov}(\mathbf{Y}) = \operatorname{Cov}(A\mathbf{X} + \mathbf{b}) = A \operatorname{Cov}(\mathbf{X}) A^T = A\boldsymbol{\Sigma}A^T
$$
Thus, $\mathbf{Y} \sim \mathcal{N}_q(A\boldsymbol{\mu} + \mathbf{b}, A\boldsymbol{\Sigma}A^T)$. This property is immensely useful, as many statistical procedures involve creating linear combinations of variables.

For example, imagine three related measurements $\mathbf{X}=(X_1, X_2, X_3)^T$ follow a $\mathcal{N}_3(\boldsymbol{\mu}, \boldsymbol{\Sigma})$ distribution. Suppose we are interested in the distribution of two new metrics: $Y_1 = X_1 - X_2$ and $Y_2 = X_2 - X_3$. This can be expressed as a [linear transformation](@entry_id:143080) $\mathbf{Y} = A\mathbf{X}$, where $\mathbf{Y} = (Y_1, Y_2)^T$ and $A = \begin{pmatrix} 1 & -1 & 0 \\ 0 & 1 & -1 \end{pmatrix}$. Given $\boldsymbol{\Sigma}$, the covariance matrix of $\mathbf{Y}$ is simply $A\boldsymbol{\Sigma}A^T$ [@problem_id:1939221]. This calculation avoids the need to derive the [joint distribution](@entry_id:204390) of $Y_1$ and $Y_2$ from first principles.

#### Marginal Distributions

A direct and important consequence of the linear transformation property is that any subset of variables in a multivariate normal vector also has a multivariate normal distribution. To see this, consider partitioning $\mathbf{X}$ into two sub-vectors, $\mathbf{X}_1$ and $\mathbf{X}_2$. The distribution of $\mathbf{X}_1$ can be obtained by defining a [transformation matrix](@entry_id:151616) $A$ that "selects" the components of $\mathbf{X}_1$.

For example, to find the [marginal distribution](@entry_id:264862) of a single component $X_i$ from $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$, we can use the transformation $X_i = A\mathbf{X}$ where $A$ is a row vector with a 1 in the $i$-th position and 0s elsewhere. Applying the rules for linear transformations, we find that the mean is $A\boldsymbol{\mu} = \mu_i$ and the variance is $A\boldsymbol{\Sigma}A^T = \Sigma_{ii}$. Therefore, the [marginal distribution](@entry_id:264862) of any component $X_i$ is simply a univariate normal distribution:
$$
X_i \sim \mathcal{N}(\mu_i, \Sigma_{ii})
$$
This provides a simple way to inspect the distribution of individual variables. For instance, if the dimensions (length, width, height) of a manufactured part are modeled as $\mathbf{X} \sim \mathcal{N}_3(\boldsymbol{\mu}, \boldsymbol{\Sigma})$, the [marginal distribution](@entry_id:264862) of the length $X_1$ is found by just taking the first element of the [mean vector](@entry_id:266544) and the first diagonal element of the covariance matrix [@problem_id:1939262].

#### Independence and Uncorrelatedness

For any pair of random variables, independence implies zero covariance (uncorrelatedness). The converse is not true in general. However, for random variables that are jointly normally distributed, the two concepts are equivalent. That is, if $(X_1, \dots, X_p)$ are jointly normal, then two components $X_i$ and $X_j$ are independent if and only if their covariance, $\Sigma_{ij}$, is zero.

This can be seen directly from the PDF. For a [bivariate normal distribution](@entry_id:165129), the PDF for $(X,Y)$ with correlation $\rho = \operatorname{Corr}(X,Y)$ is:
$$
f(x, y) = \frac{1}{2 \pi \sigma_X \sigma_Y \sqrt{1 - \rho^2}} \exp\left( -\frac{1}{2(1 - \rho^2)} \left[ \left(\frac{x - \mu_X}{\sigma_X}\right)^2 - 2\rho\left(\frac{x - \mu_X}{\sigma_X}\right)\left(\frac{y - \mu_Y}{\sigma_Y}\right) + \left(\frac{y - \mu_Y}{\sigma_Y}\right)^2 \right] \right)
$$
If $\rho = 0$, the [cross-product term](@entry_id:148190) in the exponent vanishes and $\sqrt{1-\rho^2}=1$. The PDF simplifies and factorizes perfectly [@problem_id:1939205]:
$$
f(x, y) = \frac{1}{2 \pi \sigma_X \sigma_Y} \exp\left( -\frac{1}{2} \left[ \left(\frac{x - \mu_X}{\sigma_X}\right)^2 + \left(\frac{y - \mu_Y}{\sigma_Y}\right)^2 \right] \right)
$$
$$
= \left( \frac{1}{\sigma_X\sqrt{2\pi}} \exp\left(-\frac{(x-\mu_X)^2}{2\sigma_X^2}\right) \right) \left( \frac{1}{\sigma_Y\sqrt{2\pi}} \exp\left(-\frac{(y-\mu_Y)^2}{2\sigma_Y^2}\right) \right) = f_X(x) f_Y(y)
$$
Since the joint PDF is the product of the marginal PDFs, $X$ and $Y$ are independent. This property extends to sub-vectors: if $\mathbf{X}_1$ and $\mathbf{X}_2$ are partitions of a multivariate [normal vector](@entry_id:264185) $\mathbf{X}$, they are independent if and only if their cross-covariance matrix $\boldsymbol{\Sigma}_{12}$ is a [zero matrix](@entry_id:155836).

This equivalence is often exploited in practice. For example, if we have two metrics, $Y_1$ and $Y_2$, that are [linear combinations](@entry_id:154743) of a bivariate [normal vector](@entry_id:264185) $(X_1, X_2)$, then $(Y_1, Y_2)$ is also bivariate normal. To make $Y_1$ and $Y_2$ statistically independent, one only needs to ensure their covariance is zero [@problem_id:1939250]. This simplifies the problem of ensuring independence to an algebraic calculation involving the variances and covariances of $X_1$ and $X_2$.

#### A Crucial Clarification: Marginally Normal vs. Jointly Normal

It is critical to understand that the property of joint normality is stronger than marginal normality. If a random vector $\mathbf{X}$ is multivariate normal, then each of its components $X_i$ is marginally normal. However, the converse is not true: a vector of random variables, each of which is marginally normal, is not necessarily jointly multivariate normal.

Consider the following construction [@problem_id:1939267]. Let $X \sim \mathcal{N}(0, 1)$ and define a new random variable $Y$ as:
$$
Y = \begin{cases}
X  &\text{if } |X| \le c \\
-X &\text{if } |X| > c
\end{cases}
$$
for some positive constant $c$. It can be shown that $Y$ also follows a standard normal distribution, $Y \sim \mathcal{N}(0, 1)$, because the standard normal PDF is symmetric ($f_X(x)=f_X(-x)$) and the transformation preserves this symmetry in the resulting density of $Y$. Thus, both $X$ and $Y$ are marginally normal.

However, their joint distribution is not bivariate normal. If it were, the relationship between $X$ and $Y$ would have to be linear, i.e., $Y=aX+b$. Clearly, the piecewise definition of $Y$ is not linear. The probability mass of the pair $(X, Y)$ is concentrated on the lines $y=x$ for $|x| \le c$ and $y=-x$ for $|x| > c$. A true [bivariate normal distribution](@entry_id:165129) with non-[zero correlation](@entry_id:270141) would spread its probability mass elliptically around these lines, not strictly upon them. This example serves as a powerful reminder that joint normality is a specific and restrictive assumption that must be justified.

### Advanced Topics and Related Distributions

Building on these fundamental principles, we can explore more advanced properties that are central to applications in fields like econometrics, signal processing, and machine learning.

#### Conditional Distributions

If a multivariate normal vector $\mathbf{X}$ is partitioned into two sub-vectors, $\mathbf{X} = \begin{pmatrix} \mathbf{X}_1 \\ \mathbf{X}_2 \end{pmatrix}$, what can we say about the distribution of one part, given that we have observed the other? A remarkable property of the multivariate [normal distribution](@entry_id:137477) is that the conditional distribution of $\mathbf{X}_1$ given $\mathbf{X}_2 = \mathbf{x}_2$ is also multivariate normal.

Let the parameters be partitioned conformably:
$$
\boldsymbol{\mu} = \begin{pmatrix} \boldsymbol{\mu}_1 \\ \boldsymbol{\mu}_2 \end{pmatrix}, \quad \boldsymbol{\Sigma} = \begin{pmatrix} \boldsymbol{\Sigma}_{11} & \boldsymbol{\Sigma}_{12} \\ \boldsymbol{\Sigma}_{21} & \boldsymbol{\Sigma}_{22} \end{pmatrix}
$$
The [conditional distribution](@entry_id:138367) of $\mathbf{X}_1$ given $\mathbf{X}_2 = \mathbf{x}_2$ is $\mathcal{N}(\boldsymbol{\mu}_{1|2}, \boldsymbol{\Sigma}_{11.2})$, where the conditional mean and covariance are:
$$
\boldsymbol{\mu}_{1|2} = \boldsymbol{\mu}_1 + \boldsymbol{\Sigma}_{12}\boldsymbol{\Sigma}_{22}^{-1}(\mathbf{x}_2 - \boldsymbol{\mu}_2)
$$
$$
\boldsymbol{\Sigma}_{11.2} = \boldsymbol{\Sigma}_{11} - \boldsymbol{\Sigma}_{12}\boldsymbol{\Sigma}_{22}^{-1}\boldsymbol{\Sigma}_{21}
$$
The conditional mean is a linear function of the observed value $\mathbf{x}_2$. It adjusts the original mean $\boldsymbol{\mu}_1$ based on the new information provided by $\mathbf{x}_2$. The conditional covariance $\boldsymbol{\Sigma}_{11.2}$ is independent of the value of $\mathbf{x}_2$ and represents the reduction in uncertainty about $\mathbf{X}_1$ after observing $\mathbf{X}_2$. The matrix $\boldsymbol{\Sigma}_{12}\boldsymbol{\Sigma}_{22}^{-1}\boldsymbol{\Sigma}_{21}$ is [positive semi-definite](@entry_id:262808), so the conditional variances (the diagonal elements of $\boldsymbol{\Sigma}_{11.2}$) are less than or equal to the original marginal variances. These formulas are central to Bayesian inference with normal models and are the foundation of the Kalman filter. Applying these formulas is a matter of careful matrix algebra, as demonstrated in calculations for financial stock models where the returns of some stocks are observed [@problem_id:1939195].

#### The Distribution of the Mahalanobis Distance

As mentioned earlier, the quadratic form $S = (\mathbf{X}-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{X}-\boldsymbol{\mu})$ is the squared Mahalanobis distance. This quantity itself is a random variable, and its distribution is fundamental to [hypothesis testing](@entry_id:142556) and constructing confidence ellipsoids.

If $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$ with $\boldsymbol{\Sigma}$ being positive definite, then the random variable $S$ follows a **chi-squared distribution** with $p$ degrees of freedom:
$$
S = (\mathbf{X}-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{X}-\boldsymbol{\mu}) \sim \chi^2_p
$$
This result can be proven by a standardizing transformation. Let $\mathbf{Z} = \boldsymbol{\Sigma}^{-1/2}(\mathbf{X}-\boldsymbol{\mu})$, where $\boldsymbol{\Sigma}^{-1/2}$ is the inverse of the [matrix square root](@entry_id:158930) of $\boldsymbol{\Sigma}$. By the [linear transformation](@entry_id:143080) property, $\mathbf{Z}$ is multivariate normal with mean $\mathbb{E}[\mathbf{Z}] = \boldsymbol{\Sigma}^{-1/2}(\boldsymbol{\mu}-\boldsymbol{\mu})=\mathbf{0}$ and covariance $\operatorname{Cov}(\mathbf{Z}) = \boldsymbol{\Sigma}^{-1/2}\boldsymbol{\Sigma}(\boldsymbol{\Sigma}^{-1/2})^T = I_p$. Thus, $\mathbf{Z}$ is a vector of $p$ independent standard normal random variables. The [quadratic form](@entry_id:153497) can be rewritten as:
$$
S = (\mathbf{X}-\boldsymbol{\mu})^T(\boldsymbol{\Sigma}^{-1/2})^T\boldsymbol{\Sigma}^{-1/2}(\mathbf{X}-\boldsymbol{\mu}) = (\boldsymbol{\Sigma}^{-1/2}(\mathbf{X}-\boldsymbol{\mu}))^T(\boldsymbol{\Sigma}^{-1/2}(\mathbf{X}-\boldsymbol{\mu})) = \mathbf{Z}^T\mathbf{Z} = \sum_{i=1}^p Z_i^2
$$
By definition, the sum of squares of $p$ independent standard normal variables is a chi-squared distribution with $p$ degrees of freedom. This result is used, for example, in [anomaly detection](@entry_id:634040) systems to set a threshold on the Mahalanobis distance, beyond which a measurement is flagged as abnormal [@problem_id:1939245].

#### Degenerate Multivariate Normal Distribution

So far, we have largely assumed that the covariance matrix $\boldsymbol{\Sigma}$ is invertible (positive definite). What happens if $\boldsymbol{\Sigma}$ is singular ([positive semi-definite](@entry_id:262808) but not [positive definite](@entry_id:149459))? This is the case of a **degenerate [normal distribution](@entry_id:137477)**.

A singular $\boldsymbol{\Sigma}$ means its determinant is zero, so the PDF formula is undefined. This is because the random vector does not actually occupy the full $p$-dimensional space. Instead, its probability mass is concentrated on a lower-dimensional affine subspace (a line or a plane passing through the mean $\boldsymbol{\mu}$). A singular covariance matrix implies that there is a perfect [linear relationship](@entry_id:267880) between at least two of the components.

Specifically, if $\boldsymbol{\Sigma}$ is singular, its [nullspace](@entry_id:171336) is non-trivial. This means there exists at least one non-[zero vector](@entry_id:156189) $\mathbf{a}$ such that $\boldsymbol{\Sigma}\mathbf{a} = \mathbf{0}$. Consider the random variable $Y = \mathbf{a}^T\mathbf{X}$. Its mean is $\mathbb{E}[Y] = \mathbf{a}^T\boldsymbol{\mu}$, and its variance is:
$$
\operatorname{Var}(Y) = \operatorname{Var}(\mathbf{a}^T\mathbf{X}) = \mathbf{a}^T\boldsymbol{\Sigma}\mathbf{a} = \mathbf{a}^T(\boldsymbol{\Sigma}\mathbf{a}) = \mathbf{a}^T\mathbf{0} = 0
$$
A random variable with zero variance is a constant. Therefore, with probability 1, we must have $\mathbf{a}^T\mathbf{X} = \mathbb{E}[\mathbf{a}^T\mathbf{X}]$, which means:
$$
\mathbf{a}^T\mathbf{X} = \mathbf{a}^T\boldsymbol{\mu} \quad \text{or} \quad \mathbf{a}^T(\mathbf{X}-\boldsymbol{\mu}) = 0
$$
This equation defines the affine subspace on which the distribution lies. For example, if a bivariate normal vector has a singular covariance matrix $\boldsymbol{\Sigma} = \begin{pmatrix} 4 & 6 \\ 6 & 9 \end{pmatrix}$, we can find a vector in its nullspace, such as $\mathbf{a} = (-3, 2)^T$. The entire distribution is then confined to the line defined by $-3(x_1-\mu_1) + 2(x_2-\mu_2) = 0$ [@problem_id:1939203]. This understanding is crucial for dealing with [high-dimensional data](@entry_id:138874) where collinearity among variables often leads to degenerate or near-degenerate distributions.