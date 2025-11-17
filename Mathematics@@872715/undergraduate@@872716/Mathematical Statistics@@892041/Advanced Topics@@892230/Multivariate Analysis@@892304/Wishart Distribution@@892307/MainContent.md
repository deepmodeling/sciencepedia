## Introduction
In the realm of [multivariate statistics](@entry_id:172773), understanding the joint variability of multiple random variables is a central challenge. While the chi-squared distribution provides a solid foundation for inference on the variance of a single variable, a more powerful tool is needed when we move to higher dimensions. This tool is the Wishart distribution, a family of probability distributions over symmetric, [positive-definite matrices](@entry_id:275498) that serves as the multivariate analog to the [chi-squared distribution](@entry_id:165213). Its primary importance lies in describing the distribution of the [sample covariance matrix](@entry_id:163959), making it an indispensable concept for anyone working with multivariate data. This article demystifies the Wishart distribution, bridging the gap from univariate variance to the complex world of covariance matrices.

The following chapters are structured to provide a complete and accessible understanding of this topic. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork by formally defining the distribution, exploring its fundamental properties, and establishing its direct connection to the [chi-squared distribution](@entry_id:165213). The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the practical utility of the Wishart distribution in fields ranging from finance to robotics, showcasing its role in [hypothesis testing](@entry_id:142556), [linear models](@entry_id:178302), and Bayesian inference. Finally, the **Hands-On Practices** chapter will offer guided problems to solidify your understanding and apply the theoretical concepts you've learned.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the Wishart distribution. We will begin by formally defining the distribution through its construction, then explore its essential mathematical properties, interpret its parameters, and establish its crucial connection to the more familiar [chi-squared distribution](@entry_id:165213). Finally, we will examine its moments and their application to the pivotal statistical task of estimating covariance matrices.

### The Constructive Definition of the Wishart Distribution

The Wishart distribution is most intuitively understood through its construction. It arises as the distribution of a specific type of matrix formed from samples of a [multivariate normal distribution](@entry_id:267217). This construction serves as its formal definition.

Let $\mathbf{x}_1, \mathbf{x}_2, \dots, \mathbf{x}_n$ be $n$ independent and identically distributed (i.i.d.) $p$-dimensional random column vectors, each drawn from a [multivariate normal distribution](@entry_id:267217) with a zero [mean vector](@entry_id:266544) and a $p \times p$ population covariance matrix $\mathbf{\Sigma}$. That is, $\mathbf{x}_i \sim N_p(\mathbf{0}, \mathbf{\Sigma})$ for $i=1, \dots, n$.

The **scatter matrix** $\mathbf{S}$ is defined as the sum of the outer products of these vectors:
$$
\mathbf{S} = \sum_{i=1}^{n} \mathbf{x}_i \mathbf{x}_i^T
$$
The distribution of this $p \times p$ random matrix $\mathbf{S}$ is the **Wishart distribution** with $n$ **degrees of freedom** and **[scale matrix](@entry_id:172232)** $\mathbf{\Sigma}$. This is denoted by $\mathbf{S} \sim W_p(n, \mathbf{\Sigma})$.

To make this construction concrete, consider a simple numerical example. Suppose we have $n=3$ data vectors from a $p=2$ dimensional process, given by:
$$
\mathbf{x}_1 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}, \quad \mathbf{x}_2 = \begin{pmatrix} -1 \\ 0 \end{pmatrix}, \quad \mathbf{x}_3 = \begin{pmatrix} 3 \\ -1 \end{pmatrix}
$$
These three vectors can be seen as specific realizations from an underlying $N_2(\mathbf{0}, \mathbf{\Sigma})$ distribution. The corresponding realization of the Wishart-distributed matrix $\mathbf{S}$ is calculated by summing the outer products [@problem_id:1967870]:
$$
\mathbf{x}_1 \mathbf{x}_1^T = \begin{pmatrix} 1 \\ 2 \end{pmatrix} \begin{pmatrix} 1  2 \end{pmatrix} = \begin{pmatrix} 1  2 \\ 2  4 \end{pmatrix}
$$
$$
\mathbf{x}_2 \mathbf{x}_2^T = \begin{pmatrix} -1 \\ 0 \end{pmatrix} \begin{pmatrix} -1  0 \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}
$$
$$
\mathbf{x}_3 \mathbf{x}_3^T = \begin{pmatrix} 3 \\ -1 \end{pmatrix} \begin{pmatrix} 3  -1 \end{pmatrix} = \begin{pmatrix} 9  -3 \\ -3  1 \end{pmatrix}
$$
Summing these matrices gives the resulting scatter matrix:
$$
\mathbf{S} = \begin{pmatrix} 1  2 \\ 2  4 \end{pmatrix} + \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} + \begin{pmatrix} 9  -3 \\ -3  1 \end{pmatrix} = \begin{pmatrix} 11  -1 \\ -1  5 \end{pmatrix}
$$
This matrix $\mathbf{S}$ is a single sample drawn from the Wishart distribution $W_2(3, \mathbf{\Sigma})$.

### Fundamental Properties of Wishart Matrices

The constructive definition of the Wishart distribution directly implies several fundamental properties that any matrix drawn from this distribution must possess. These properties define the [sample space](@entry_id:270284) of the Wishart distribution.

#### Symmetry

A Wishart matrix is always symmetric. This property follows directly from its construction as a sum of outer products. For any vector $\mathbf{x}_i$, the [outer product](@entry_id:201262) $\mathbf{x}_i \mathbf{x}_i^T$ is a [symmetric matrix](@entry_id:143130), because $(\mathbf{x}_i \mathbf{x}_i^T)^T = (\mathbf{x}_i^T)^T \mathbf{x}_i^T = \mathbf{x}_i \mathbf{x}_i^T$. Since the sum of [symmetric matrices](@entry_id:156259) is itself symmetric, the scatter matrix $\mathbf{S} = \sum_{i=1}^{n} \mathbf{x}_i \mathbf{x}_i^T$ must be symmetric. In terms of its elements, this means that for any valid indices $j$ and $k$, $S_{jk} = S_{kj}$ [@problem_id:1967864].

#### Positive Semi-Definiteness

A more profound property is that any Wishart matrix $\mathbf{S}$ must be **[positive semi-definite](@entry_id:262808)** (PSD). A matrix $\mathbf{A}$ is PSD if for any non-[zero vector](@entry_id:156189) $\mathbf{v}$, the [quadratic form](@entry_id:153497) $\mathbf{v}^T \mathbf{A} \mathbf{v}$ is non-negative, i.e., $\mathbf{v}^T \mathbf{A} \mathbf{v} \ge 0$.

To see why this holds for a Wishart matrix, consider the quadratic form for $\mathbf{S}$:
$$
\mathbf{v}^T \mathbf{S} \mathbf{v} = \mathbf{v}^T \left( \sum_{i=1}^{n} \mathbf{x}_i \mathbf{x}_i^T \right) \mathbf{v} = \sum_{i=1}^{n} \mathbf{v}^T (\mathbf{x}_i \mathbf{x}_i^T) \mathbf{v}
$$
Let $c_i = \mathbf{v}^T \mathbf{x}_i$. Since this is a scalar value (the dot product of $\mathbf{v}$ and $\mathbf{x}_i$), we can rewrite the term in the sum as:
$$
\mathbf{v}^T \mathbf{x}_i \mathbf{x}_i^T \mathbf{v} = (\mathbf{v}^T \mathbf{x}_i)(\mathbf{x}_i^T \mathbf{v}) = c_i \cdot c_i = c_i^2 \ge 0
$$
Thus, the [quadratic form](@entry_id:153497) becomes a sum of squares, $\mathbf{v}^T \mathbf{S} \mathbf{v} = \sum_{i=1}^{n} c_i^2$, which is guaranteed to be non-negative. This confirms that $\mathbf{S}$ is [positive semi-definite](@entry_id:262808).

This property is a critical check for validating whether a given matrix could be a realization from a Wishart distribution. A [symmetric matrix](@entry_id:143130) is PSD if and only if all of its eigenvalues are non-negative. A practical test for this is to check that all of its principal minors are non-negative. For instance, the matrix $S_C = \begin{pmatrix} 1  2  0 \\ 2  1  0 \\ 0  0  3 \end{pmatrix}$ cannot be a Wishart realization because one of its principal minors is negative: $\det \begin{pmatrix} 1  2 \\ 2  1 \end{pmatrix} = 1 - 4 = -3$. This violation of the PSD property disqualifies it [@problem_id:1967836].

#### Rank and the Singular Wishart Distribution

The rank of a Wishart matrix $\mathbf{S} \sim W_p(n, \mathbf{\Sigma})$ is determined by the relationship between the degrees of freedom $n$ and the dimension $p$. Let the $p \times n$ data matrix $\mathbf{X}$ be formed by taking the vectors $\mathbf{x}_1, \dots, \mathbf{x}_n$ as its columns. Then the scatter matrix can be written compactly as $\mathbf{S} = \mathbf{X} \mathbf{X}^T$.

From linear algebra, we know that the rank of $\mathbf{S}$ is the same as the rank of $\mathbf{X}$, and the rank of $\mathbf{X}$ cannot exceed the minimum of its dimensions, i.e., $\text{rank}(\mathbf{S}) = \text{rank}(\mathbf{X}) \le \min(p, n)$.

If the underlying [normal distribution](@entry_id:137477) is non-degenerate (i.e., $\mathbf{\Sigma}$ is non-singular), the $n$ vectors $\mathbf{x}_i$ will be linearly independent with probability one, provided $n \le p$. The rank of $\mathbf{S}$ will therefore be $\min(n, p)$ [almost surely](@entry_id:262518).

A crucial consequence arises when the degrees of freedom are less than the dimension ($n \lt p$). In this case, the rank of the $p \times p$ matrix $\mathbf{S}$ will be at most $n$, which is strictly less than $p$. A square matrix whose rank is less than its dimension is singular (i.e., its determinant is zero and it is not invertible). Therefore, if $n \lt p$, the matrix $\mathbf{S}$ is guaranteed to be singular. Such a distribution is referred to as a **singular Wishart distribution** [@problem_id:1967829]. Conversely, if $n \ge p$ and $\mathbf{\Sigma}$ is non-singular, the matrix $\mathbf{S}$ will be non-singular (positive definite) with probability one.

### Interpreting the Parameters

The Wishart distribution $W_p(n, \mathbf{\Sigma})$ is fully specified by two parameters: the [scale matrix](@entry_id:172232) $\mathbf{\Sigma}$ and the degrees of freedom $n$.

#### The Scale Matrix $\mathbf{\Sigma}$

The **[scale matrix](@entry_id:172232)** $\mathbf{\Sigma}$ is a $p \times p$ symmetric, [positive definite matrix](@entry_id:150869) that dictates the shape and orientation of the distribution. Its direct interpretation comes from the constructive definition: $\mathbf{\Sigma}$ is precisely the **population covariance matrix of the underlying multivariate normal vectors** $\mathbf{x}_i$ that are used to generate the Wishart matrix.

Consider a practical scenario in [geodesy](@entry_id:272545), where a high-precision GNSS receiver records its position to determine its 3D coordinates. The error in each measurement is a 3D vector $\mathbf{e}_i$, assumed to be drawn from $N_3(\mathbf{0}, \mathbf{\Sigma})$. Here, the [scale matrix](@entry_id:172232) $\mathbf{\Sigma}$ is the true, unobservable covariance matrix of a single position error vector. The diagonal elements of $\mathbf{\Sigma}$ represent the variances of the error in each of the three spatial dimensions, and the off-diagonal elements represent the covariances between these directional errors. The matrix $S = \sum \mathbf{e}_i \mathbf{e}_i^T$ would follow $W_3(n, \mathbf{\Sigma})$, and $\mathbf{\Sigma}$ remains the parameter governing the underlying error structure, not an estimate derived from the sample [@problem_id:1967878].

#### The Degrees of Freedom $n$

The **degrees of freedom** $n$ is a positive integer that corresponds to the number of independent vectors summed to form the scatter matrix. In the context of statistical sampling, $n$ is typically the sample size (or related to it).

The degrees of freedom parameter controls the concentration of the Wishart distribution. As $n$ increases, the random matrix $\mathbf{S}$ becomes a more precise representation of the scaled [population structure](@entry_id:148599) $n\mathbf{\Sigma}$. This is analogous to the Law of Large Numbers, where a sample mean converges to the [population mean](@entry_id:175446) as the sample size grows.

We can quantify this concentration by examining the [coefficient of variation](@entry_id:272423) (CV) of the elements of a Wishart matrix $\mathbf{A} \sim W_p(n, \mathbf{\Sigma})$. The [expected value and variance](@entry_id:180795) of an element $A_{ij}$ are given by $E[A_{ij}] = n \sigma_{ij}$ and $\text{Var}(A_{ij}) = n(\sigma_{ij}^2 + \sigma_{ii}\sigma_{jj})$. The [coefficient of variation](@entry_id:272423) for a non-zero off-diagonal element is:
$$
CV(A_{ij}) = \frac{\sqrt{\text{Var}(A_{ij})}}{|E[A_{ij}]|} = \frac{\sqrt{n(\sigma_{ij}^2 + \sigma_{ii}\sigma_{jj})}}{|n \sigma_{ij}|} = \frac{1}{\sqrt{n}} \frac{\sqrt{\sigma_{ij}^2 + \sigma_{ii}\sigma_{jj}}}{|\sigma_{ij}|}
$$
This expression shows that the [coefficient of variation](@entry_id:272423) is proportional to $1/\sqrt{n}$. This means that increasing the degrees of freedom by a factor of $k$ decreases the relative variability of the [matrix elements](@entry_id:186505) by a factor of $\sqrt{k}$. For example, if we increase the degrees of freedom nine-fold, the CV is reduced by a factor of $\sqrt{9}=3$, indicating that the distribution becomes significantly more concentrated around its expected value [@problem_id:1967884].

### Relation to the Chi-Squared Distribution

The Wishart distribution is the multivariate generalization of the chi-squared ($\chi^2$) distribution. This relationship is fundamental to understanding its role in statistics, as the $\chi^2$ distribution is central to inference on the variance of a univariate normal population.

Let's examine the simplest case of the Wishart distribution, where the dimension is $p=1$ [@problem_id:1967825]. In this case:
- The multivariate normal vectors $\mathbf{x}_i$ become scalar random variables $X_i$.
- The population covariance matrix $\mathbf{\Sigma}$ becomes a scalar variance $\sigma^2$.
- The underlying distribution is the univariate normal, $X_i \sim N(0, \sigma^2)$.
- The Wishart-distributed matrix $\mathbf{S}$ becomes a scalar random variable $W = \sum_{i=1}^n X_i^2$.
- The distribution is $W \sim W_1(n, \sigma^2)$.

Now, let's analyze the distribution of $W$. By definition, if $X_i \sim N(0, \sigma^2)$, then the standardized variable $Z_i = X_i/\sigma$ follows the standard normal distribution, $Z_i \sim N(0, 1)$. We can express $W$ in terms of these standard normal variables:
$$
W = \sum_{i=1}^{n} X_i^2 = \sum_{i=1}^{n} (\sigma Z_i)^2 = \sigma^2 \sum_{i=1}^{n} Z_i^2
$$
Dividing by the variance $\sigma^2$, we get:
$$
\frac{W}{\sigma^2} = \sum_{i=1}^{n} Z_i^2
$$
By the definition of the chi-squared distribution, the [sum of squares](@entry_id:161049) of $n$ independent standard normal variables follows a $\chi^2$ distribution with $n$ degrees of freedom. Therefore:
$$
\frac{W}{\sigma^2} \sim \chi^2(n)
$$
This demonstrates that a $W_1(n, \sigma^2)$ distributed variable is simply a scaled chi-squared variable: $W \sim \sigma^2 \chi^2(n)$. The Wishart distribution can thus be seen as the natural extension of this concept to higher dimensions, where it describes the [joint distribution](@entry_id:204390) of sums of squares and sums of cross-products of multivariate normal variables.

### Moments and Applications in Estimation

The moments of the Wishart distribution are essential for its use in [statistical inference](@entry_id:172747), particularly in the estimation of covariance matrices.

#### The Expected Value

The most important moment is the expected value. For a random matrix $\mathbf{S} \sim W_p(n, \mathbf{\Sigma})$, its expectation is:
$$
E[\mathbf{S}] = n \mathbf{\Sigma}
$$
This result can be derived directly from the constructive definition. Using the linearity of expectation:
$$
E[\mathbf{S}] = E\left[ \sum_{i=1}^{n} \mathbf{x}_i \mathbf{x}_i^T \right] = \sum_{i=1}^{n} E[\mathbf{x}_i \mathbf{x}_i^T]
$$
For a random vector $\mathbf{x}_i \sim N_p(\mathbf{0}, \mathbf{\Sigma})$, the covariance matrix is defined as $\text{Cov}(\mathbf{x}_i) = E[(\mathbf{x}_i - E[\mathbf{x}_i])(\mathbf{x}_i - E[\mathbf{x}_i])^T]$. Since the mean is zero, this simplifies to $\mathbf{\Sigma} = E[\mathbf{x}_i \mathbf{x}_i^T]$. As all $\mathbf{x}_i$ are identically distributed, we have:
$$
E[\mathbf{S}] = \sum_{i=1}^{n} \mathbf{\Sigma} = n \mathbf{\Sigma}
$$
This fundamental result shows that the expected value of a Wishart matrix is directly proportional to its [scale matrix](@entry_id:172232), with the degrees of freedom acting as the proportionality constant [@problem_id:1967879].

#### Unbiased Estimation of the Covariance Matrix

This expectation property is the cornerstone for constructing an [unbiased estimator](@entry_id:166722) for the population covariance matrix $\mathbf{\Sigma}$.

**Case 1: Known Population Mean.**
Suppose we have samples $X_1, \dots, X_n$ from $N_p(\mathbf{\mu}, \mathbf{\Sigma})$, where the mean $\mathbf{\mu}$ is known. We can center the data to get $\mathbf{x}_i = X_i - \mathbf{\mu}$, where $\mathbf{x}_i \sim N_p(\mathbf{0}, \mathbf{\Sigma})$. The scatter matrix is then $S_A = \sum_{i=1}^{n} (X_i - \mathbf{\mu})(X_i - \mathbf{\mu})^T$. As shown, $S_A \sim W_p(n, \mathbf{\Sigma})$ and has expectation $E[S_A] = n\mathbf{\Sigma}$.

To find an [unbiased estimator](@entry_id:166722) $\hat{\mathbf{\Sigma}}$ for $\mathbf{\Sigma}$, we need an estimator whose expectation is $\mathbf{\Sigma}$. By scaling $S_A$, we can define:
$$
\hat{\mathbf{\Sigma}} = \frac{1}{n} S_A
$$
Taking the expectation, we get $E[\hat{\mathbf{\Sigma}}] = E[\frac{1}{n} S_A] = \frac{1}{n} E[S_A] = \frac{1}{n} (n\mathbf{\Sigma}) = \mathbf{\Sigma}$. Thus, $\frac{1}{n}S_A$ is an [unbiased estimator](@entry_id:166722) for $\mathbf{\Sigma}$ when the mean is known [@problem_id:1967840].

**Case 2: Unknown Population Mean.**
In most practical applications, the [population mean](@entry_id:175446) $\mathbf{\mu}$ is unknown and must be estimated from the data using the sample mean, $\bar{X} = \frac{1}{n} \sum_{i=1}^{n} X_i$. The scatter matrix is then computed using deviations from the [sample mean](@entry_id:169249):
$$
S_B = \sum_{i=1}^{n} (X_i - \bar{X})(X_i - \bar{X})^T
$$
Estimating the mean from the data introduces a constraint on the centered vectors $(X_i - \bar{X})$, as their sum is now zero. This constraint reduces the degrees of freedom by one. It can be rigorously shown that the distribution of this new scatter matrix is Wishart with $n-1$ degrees of freedom:
$$
S_B \sim W_p(n-1, \mathbf{\Sigma})
$$
The expectation of this matrix is therefore $E[S_B] = (n-1)\mathbf{\Sigma}$. This "loss" of one degree of freedom is a fundamental concept in statistics, analogous to the use of $n-1$ in the denominator of the univariate [sample variance](@entry_id:164454). We can see this effect by comparing the expected traces of $S_A$ (known mean) and $S_B$ (unknown mean) [@problem_id:1967844]:
$$
E[\text{tr}(S_A)] = \text{tr}(E[S_A]) = \text{tr}(n\mathbf{\Sigma}) = n \cdot \text{tr}(\mathbf{\Sigma})
$$
$$
E[\text{tr}(S_B)] = \text{tr}(E[S_B]) = \text{tr}((n-1)\mathbf{\Sigma}) = (n-1)\text{tr}(\mathbf{\Sigma})
$$
The ratio $\frac{E[\text{tr}(S_A)]}{E[\text{tr}(S_B)]} = \frac{n}{n-1}$ clearly illustrates the effect of estimating the mean.

Given that $E[S_B] = (n-1)\mathbf{\Sigma}$, the unbiased estimator for $\mathbf{\Sigma}$ in the far more common case of an unknown mean is:
$$
\hat{\mathbf{\Sigma}}_{\text{sample}} = \frac{1}{n-1} S_B = \frac{1}{n-1} \sum_{i=1}^{n} (X_i - \bar{X})(X_i - \bar{X})^T
$$
This is the familiar formula for the **[sample covariance matrix](@entry_id:163959)**, and its distributional properties are directly linked to the Wishart distribution.