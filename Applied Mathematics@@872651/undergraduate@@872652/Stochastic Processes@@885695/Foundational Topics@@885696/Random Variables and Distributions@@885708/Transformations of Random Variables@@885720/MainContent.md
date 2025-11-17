## Introduction
In the study of probability, understanding a single random variable is just the beginning. The real world is driven by interactions, functions, and derived quantities. An engineer might need to know the distribution of the kinetic energy of a particle, which is a function of its velocity. A financial analyst might model a portfolio's value as a sum of multiple, correlated asset returns. A data scientist might apply a logit function to a probability parameter to perform [unconstrained optimization](@entry_id:137083). In all these cases, we start with random variables whose distributions we know and seek to find the distribution of a new variable that is a transformation of the originals. This process is a cornerstone of [applied probability](@entry_id:264675) and statistics.

This article provides a comprehensive guide to the methods used for [transforming random variables](@entry_id:263513). It addresses the crucial knowledge gap between understanding basic probability distributions and applying them to complex, real-world systems where quantities of interest are derived, not directly measured. By mastering these techniques, you will gain the ability to model a vast range of phenomena across numerous disciplines.

The article is structured to build your expertise systematically. First, the **Principles and Mechanisms** chapter will lay the mathematical foundation, introducing universal tools like the CDF method and more direct techniques such as the change-of-variables formula, convolution, and the multivariate Jacobian method. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these principles are applied to solve practical problems in signal processing, [reliability engineering](@entry_id:271311), statistical mechanics, and finance. Finally, the **Hands-On Practices** chapter offers a curated set of problems to help you solidify your understanding and develop practical skills in applying these transformative methods.

## Principles and Mechanisms

Understanding the behavior of a single random variable is a foundational skill. However, in most scientific and engineering applications, we are interested in quantities that are derived from one or more random variables. A sensor reading might be squared to calculate energy, signals from multiple sources might be added together, or a complex system's output might be a nonlinear function of several random inputs. This chapter explores the principles and mechanisms for determining the probability distribution of a new random variable that is a function of others.

### The Cumulative Distribution Function (CDF) Method: A Universal Approach

The most fundamental and universally applicable method for finding the distribution of a [transformed random variable](@entry_id:198807) is the **Cumulative Distribution Function (CDF) method**. For a random variable $X$ with a known distribution and a transformation $Y = g(X)$, the core idea is to find the CDF of $Y$, denoted $F_Y(y)$, by using its definition and then, if needed, differentiate it to obtain the probability density function (PDF) or probability [mass function](@entry_id:158970) (PMF).

The definition of the CDF is $F_Y(y) = P(Y \le y)$. By substituting $Y = g(X)$, this becomes:
$$F_Y(y) = P(g(X) \le y)$$
The task then reduces to expressing the event $\{g(X) \le y\}$ as an equivalent event involving $X$ and then using the known distribution of $X$ (typically its CDF, $F_X(x)$) to calculate the probability.

This method is powerful because it works for any type of function $g$, including those that are not strictly monotonic or one-to-one, and it naturally handles discrete, continuous, and even mixed distributions.

Consider a practical application in signal processing where an electrical signal, modeled as a standard normal random variable $X \sim \mathcal{N}(0,1)$, is passed through a **[half-wave rectifier](@entry_id:269098)**. The rectifier's output is given by the function $Y = \max(0, X)$. This transformation is not invertible in the usual sense; any negative input for $X$ results in an output of $Y=0$. The CDF method handles this situation gracefully [@problem_id:1347096].

To find the CDF of $Y$, $F_Y(y)$, we consider two cases for $y$:

1.  If $y  0$: Since $Y = \max(0, X)$, the output $Y$ can never be negative. Therefore, the probability that $Y$ is less than or equal to a negative number is zero.
    $F_Y(y) = P(Y \le y) = 0$ for $y  0$.

2.  If $y \ge 0$: We evaluate $P(Y \le y)$. The condition $Y \le y$ is equivalent to $\max(0, X) \le y$. This inequality holds true if and only if $X \le y$. Why? If $X$ is negative, then $Y=0$, and since $y \ge 0$, the condition $0 \le y$ is met. If $X$ is positive, then $Y=X$, and the condition becomes $X \le y$. Combining these, the event $\max(0, X) \le y$ for a non-negative $y$ is identical to the event $X \le y$.
    Therefore, for $y \ge 0$:
    $$F_Y(y) = P(Y \le y) = P(X \le y) = \Phi(y)$$
    where $\Phi(\cdot)$ is the standard notation for the CDF of a standard normal random variable.

Combining these cases, we obtain the complete CDF for the rectified signal:
$$F_Y(y) = \begin{cases} 0,  y  0 \\ \Phi(y),  y \ge 0 \end{cases}$$

An interesting feature of this resulting distribution is the jump discontinuity at $y=0$. We have $F_Y(0) = \Phi(0) = 0.5$, while $\lim_{y \to 0^-} F_Y(y) = 0$. This jump indicates a discrete probability mass at $y=0$. The size of the jump is $P(Y=0) = F_Y(0) - \lim_{y \to 0^-} F_Y(y) = 0.5 - 0 = 0.5$. This makes perfect sense, as $Y=0$ whenever $X \le 0$, and for a [standard normal distribution](@entry_id:184509), $P(X \le 0) = 0.5$. For $y > 0$, the distribution is continuous. This type of distribution, with both discrete and continuous components, is known as a **[mixed distribution](@entry_id:272867)**.

### The Change-of-Variables Method for Continuous Random Variables

While the CDF method is universal, a more direct technique, known as the **change-of-variables method**, exists for [continuous random variables](@entry_id:166541) and invertible transformations. This method provides a formula for the transformed PDF directly, based on the principle of conservation of probability. For a small interval $dx$, the probability mass is $f_X(x)dx$. This mass must be equal to the probability mass in the corresponding interval $dy$, which is $f_Y(y)dy$. This gives the heuristic relationship $f_Y(y) |dy| = f_X(x) |dx|$, leading to $f_Y(y) = f_X(x) \left|\frac{dx}{dy}\right|$.

#### Monotonic Transformations

When the function $Y=g(X)$ is strictly **monotonic** (either always increasing or always decreasing), it has a unique inverse $X = g^{-1}(Y)$. The formula for the PDF of $Y$ is:
$$f_Y(y) = f_X(g^{-1}(y)) \left| \frac{d}{dy} g^{-1}(y) \right|$$
The term $\left| \frac{d}{dy} g^{-1}(y) \right|$ is the absolute value of the **Jacobian** of the one-dimensional transformation. It accounts for how the transformation stretches or compresses the density.

For example, consider a quantum dot photosensor where the detection time $T$ is an exponential random variable with rate $\alpha > 0$, so its PDF is $f_T(t) = \alpha \exp(-\alpha t)$ for $t \ge 0$. The sensor's activation level is given by $A = g(T) = 1 - \exp(-\alpha T)$ [@problem_id:1347100]. Since $T \ge 0$, the term $\exp(-\alpha T)$ is in $(0, 1]$, making $A$ fall in the range $[0, 1)$. The function $g(T)$ is strictly increasing for $T \ge 0$, so we can use the change-of-variables formula.

First, we find the inverse transformation by solving for $T$ in terms of $A$:
$$A = 1 - \exp(-\alpha T) \implies \exp(-\alpha T) = 1-A \implies T = -\frac{1}{\alpha} \ln(1-A)$$
This is our [inverse function](@entry_id:152416), $T = g^{-1}(A)$.

Next, we calculate the derivative of the inverse with respect to $A$:
$$\frac{dT}{dA} = \frac{d}{dA} \left( -\frac{1}{\alpha} \ln(1-A) \right) = -\frac{1}{\alpha} \left( \frac{-1}{1-A} \right) = \frac{1}{\alpha(1-A)}$$
The absolute value is the same, since $a  1$.

Now, we apply the formula:
$$f_A(a) = f_T(g^{-1}(a)) \left| \frac{d}{da} g^{-1}(a) \right| = \left(\alpha \exp(-\alpha \cdot g^{-1}(a))\right) \cdot \left(\frac{1}{\alpha(1-a)}\right)$$
Substituting $g^{-1}(a) = -\frac{1}{\alpha} \ln(1-a)$:
$$f_A(a) = \left(\alpha \exp\left(-\alpha \left(-\frac{1}{\alpha} \ln(1-a)\right)\right)\right) \cdot \frac{1}{\alpha(1-a)}$$
$$f_A(a) = \left(\alpha \exp(\ln(1-a))\right) \cdot \frac{1}{\alpha(1-a)} = (\alpha (1-a)) \cdot \frac{1}{\alpha(1-a)} = 1$$
This result is valid for $a$ in the range of the transformation, which is $0 \le a  1$. For any $a$ outside this range, the probability is zero. Therefore, the activation level $A$ follows a [uniform distribution](@entry_id:261734) on $[0,1)$:
$$f_A(a) = \begin{cases} 1,  0 \le a  1 \\ 0,  \text{otherwise} \end{cases}$$

#### The Probability Integral Transform: A Cornerstone of Simulation

The result from the quantum sensor example is an instance of a remarkable and general theorem known as the **Probability Integral Transform (PIT)**. It states that if $X$ is a [continuous random variable](@entry_id:261218) with CDF $F_X(x)$, then the random variable $Y = F_X(X)$ is uniformly distributed on the interval $(0, 1)$.

Let's prove this general result [@problem_id:1347074]. Assume $F_X(x)$ is continuous and strictly increasing. The transformation is $Y = g(X) = F_X(X)$. The range of this transformation is $(0, 1)$. We can use the CDF method to find the distribution of $Y$. For any $y \in (0,1)$:
$$F_Y(y) = P(Y \le y) = P(F_X(X) \le y)$$
Since $F_X$ is strictly increasing, it has a well-defined inverse, $F_X^{-1}$, which is the [quantile function](@entry_id:271351). Applying this inverse to both sides of the inequality inside the probability does not change the direction of the inequality:
$$F_Y(y) = P(X \le F_X^{-1}(y))$$
By the definition of the CDF of $X$, $P(X \le z) = F_X(z)$. Therefore:
$$F_Y(y) = F_X(F_X^{-1}(y)) = y$$
This is the CDF of a [uniform random variable](@entry_id:202778) on $(0,1)$. Differentiating $F_Y(y) = y$ with respect to $y$ gives the PDF $f_Y(y) = 1$ for $y \in (0,1)$.

The PIT is of immense practical importance. Most computer programming languages can generate pseudo-random numbers from a uniform distribution. The PIT (in reverse) provides a method, called **[inverse transform sampling](@entry_id:139050)**, to convert these uniform random numbers into random numbers from *any* desired distribution. If we want to generate a sample from a distribution with CDF $F_X$, we can generate a [uniform random variable](@entry_id:202778) $U$ and compute $X = F_X^{-1}(U)$. The resulting $X$ will have the desired distribution.

#### Non-Monotonic Transformations

When the function $Y=g(X)$ is **non-monotonic**, a single value of $y$ may correspond to multiple values of $x$. For example, if $Y=X^2$, then $y=4$ corresponds to both $x=2$ and $x=-2$. The change-of-variables formula must be adapted to account for this by summing the contributions from all such roots. If for a given $y$, the equation $y=g(x)$ has roots $x_1, x_2, \ldots, x_n$, then the PDF of $Y$ is:
$$f_Y(y) = \sum_{i=1}^{n} f_X(x_i(y)) \left| \frac{dx_i}{dy} \right|$$
where each $x_i(y)$ represents one of the [inverse functions](@entry_id:141256) valid in a specific region.

A physical example can be found in the statistical mechanics of a trapped nanoparticle [@problem_id:1347067]. If the particle's position $X$ follows a Gaussian distribution with mean 0 and variance $\sigma^2$, its potential energy is $E = \frac{1}{2}\kappa X^2$, where $\kappa$ is a constant. We want to find the PDF of the energy, $f_E(e)$.

The transformation is $E = g(X) = \frac{1}{2}\kappa X^2$. For any energy level $e > 0$, there are two corresponding positions:
$$x^2 = \frac{2e}{\kappa} \implies x_1 = -\sqrt{\frac{2e}{\kappa}} \quad \text{and} \quad x_2 = +\sqrt{\frac{2e}{\kappa}}$$
We need the derivatives of these [inverse functions](@entry_id:141256):
$$\frac{dx_1}{de} = -\frac{1}{2}\sqrt{\frac{2}{\kappa}}e^{-1/2} \quad \text{and} \quad \frac{dx_2}{de} = +\frac{1}{2}\sqrt{\frac{2}{\kappa}}e^{-1/2}$$
The absolute value of both derivatives is the same: $\left| \frac{dx}{de} \right| = \frac{1}{\sqrt{2\kappa e}}$.

The PDF of $X$ is $f_X(x) = \frac{1}{\sqrt{2\pi \sigma^2}} \exp(-\frac{x^2}{2\sigma^2})$. Now we apply the formula for non-monotonic transformations:
$$f_E(e) = f_X(x_1(e))\left|\frac{dx_1}{de}\right| + f_X(x_2(e))\left|\\frac{dx_2}{de}\right|$$
Since $f_X(x)$ depends only on $x^2$, and $x_1^2 = x_2^2 = 2e/\kappa$, the terms $f_X(x_1(e))$ and $f_X(x_2(e))$ are identical.
$$f_E(e) = 2 \cdot f_X\left(\sqrt{\frac{2e}{\kappa}}\right) \cdot \left|\frac{dx}{de}\right|$$
$$f_E(e) = 2 \cdot \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left(-\frac{2e/\kappa}{2\sigma^2}\right) \cdot \frac{1}{\sqrt{2\kappa e}}$$
$$f_E(e) = \frac{2}{\sqrt{4\pi \sigma^2 \kappa e}} \exp\left(-\frac{e}{\kappa\sigma^2}\right) = \frac{1}{\sqrt{\pi \kappa\sigma^2 e}} \exp\left(-\frac{e}{\kappa\sigma^2}\right)$$
Using the equipartition theorem from thermodynamics, $\sigma^2 = k_B T / \kappa$, which implies $\kappa\sigma^2 = k_B T$, where $k_B$ is the Boltzmann constant and $T$ is the temperature. Substituting this gives the energy distribution:
$$f_E(e) = \frac{1}{\sqrt{\pi k_B T e}} \exp\left(-\frac{e}{k_B T}\right), \quad \text{for } e > 0$$
This reveals that the energy follows a Gamma distribution, a common result in statistical physics.

### Functions of Multiple Random Variables

Often, a quantity of interest is a function of several random variables, for instance $Z = g(X, Y)$. The principles extend from the single-variable case, though the mechanics can be more involved.

#### Sums of Independent Variables: The Convolution Formula

One of the most common operations is summing two independent random variables: $Z = X+Y$. The distribution of $Z$ is given by the **convolution** of the distributions of $X$ and $Y$.

For **discrete** random variables, the probability [mass function](@entry_id:158970) of the sum $Z$ is found by summing the probabilities of all mutually exclusive pairs $(x, y)$ that add up to $z$:
$$P(Z=z) = \sum_{k} P(X=k, Y=z-k)$$
Since $X$ and $Y$ are independent, $P(X=k, Y=z-k) = P(X=k)P(Y=z-k)$, so the **[discrete convolution](@entry_id:160939) formula** is:
$$P(Z=z) = \sum_{k} P(X=k)P(Y=z-k)$$
where the sum is over all possible values $k$ of the random variable $X$.

For example, if the number of Type A defects ($X$) and Type B defects ($Y$) on a wafer are independent [discrete random variables](@entry_id:163471), the PMF of the total number of defects $Z=X+Y$ can be calculated this way. To find $P(Z=4)$ [@problem_id:1347089], we identify all pairs $(x,y)$ such that $x+y=4$ and both $x$ and $y$ are possible outcomes. If the possible values for $X$ are $\{0, 1, 2\}$ and for $Y$ are $\{0, 1, 2, 3\}$, the valid pairs are $(1, 3)$ and $(2, 2)$. The probability is then:
$$P(Z=4) = P(X=1, Y=3) + P(X=2, Y=2) = P(X=1)P(Y=3) + P(X=2)P(Y=2)$$

For **continuous** [independent random variables](@entry_id:273896), the equivalent operation for PDFs is the **[convolution integral](@entry_id:155865)**:
$$f_Z(z) = \int_{-\infty}^{\infty} f_X(x) f_Y(z-x) dx$$
This formula can be derived by considering the joint PDF $f_{X,Y}(x,y) = f_X(x)f_Y(y)$ and integrating it over the region where $x+y \le z$.

As an illustration, consider two sequential production stages with independent, exponentially distributed durations $X \sim \text{Exp}(\lambda_1)$ and $Y \sim \text{Exp}(\lambda_2)$, where $\lambda_1 \neq \lambda_2$ [@problem_id:1347104]. The total time is $Z=X+Y$. Since $X$ and $Y$ must be positive, the integration limits change. The integrand $f_X(x)f_Y(z-x)$ is non-zero only for $x \ge 0$ and $z-x \ge 0$ (i.e., $x \le z$). So for $z \ge 0$:
$$f_Z(z) = \int_{0}^{z} (\lambda_1 e^{-\lambda_1 x}) (\lambda_2 e^{-\lambda_2 (z-x)}) dx$$
$$f_Z(z) = \lambda_1 \lambda_2 e^{-\lambda_2 z} \int_{0}^{z} e^{(\lambda_2 - \lambda_1)x} dx$$
Since $\lambda_1 \neq \lambda_2$, we can evaluate the integral:
$$f_Z(z) = \lambda_1 \lambda_2 e^{-\lambda_2 z} \left[ \frac{e^{(\lambda_2 - \lambda_1)x}}{\lambda_2 - \lambda_1} \right]_{0}^{z} = \lambda_1 \lambda_2 e^{-\lambda_2 z} \frac{e^{(\lambda_2 - \lambda_1)z} - 1}{\lambda_2 - \lambda_1}$$
$$f_Z(z) = \frac{\lambda_1 \lambda_2}{\lambda_2 - \lambda_1} (e^{-\lambda_1 z} - e^{-\lambda_2 z})$$
This resulting distribution is known as a hypoexponential or generalized Erlang distribution.

#### General Transformations of Multiple Variables: The Jacobian Method

For general transformations of multiple [continuous random variables](@entry_id:166541), such as $(U, V) = g(X, Y)$, we use a multivariate version of the change-of-variables method. If we have a set of old variables $\mathbf{x} = (x_1, \ldots, x_n)$ and a set of new variables $\mathbf{y} = g(\mathbf{x})$, the method requires finding the inverse transformation $\mathbf{x} = h(\mathbf{y})$. The joint PDF of the new variables is given by:
$$f_{\mathbf{Y}}(\mathbf{y}) = f_{\mathbf{X}}(h(\mathbf{y})) |J|$$
where $|J|$ is the absolute value of the **Jacobian determinant** of the inverse transformation. The Jacobian matrix consists of all the partial derivatives of the old variables with respect to the new ones:
$$J = \det \begin{pmatrix} \frac{\partial x_1}{\partial y_1}  \cdots  \frac{\partial x_1}{\partial y_n} \\ \vdots  \ddots  \vdots \\ \frac{\partial x_n}{\partial y_1}  \cdots  \frac{\partial x_n}{\partial y_n} \end{pmatrix}$$

A straightforward example is finding the joint distribution of the sum $U=X+Y$ and difference $V=X-Y$ of two independent signals $X, Y \sim \text{Uniform}[0,1]$ [@problem_id:1408018]. The joint PDF of $(X,Y)$ is $f_{X,Y}(x,y) = 1$ on the unit square $[0,1] \times [0,1]$ and 0 otherwise.
The inverse transformation is $X = (U+V)/2$ and $Y = (U-V)/2$. The Jacobian determinant is:
$$J = \det \begin{pmatrix} \frac{\partial X}{\partial U}  \frac{\partial X}{\partial V} \\ \frac{\partial Y}{\partial U}  \frac{\partial Y}{\partial V} \end{pmatrix} = \det \begin{pmatrix} 1/2  1/2 \\ 1/2  -1/2 \end{pmatrix} = -\frac{1}{4} - \frac{1}{4} = -\frac{1}{2}$$
The absolute value is $|J|=1/2$. The new joint PDF is $f_{U,V}(u,v) = f_{X,Y}((u+v)/2, (u-v)/2) |J| = 1 \cdot \frac{1}{2} = \frac{1}{2}$, provided the point is within the transformed region. The constraints $0 \le x \le 1$ and $0 \le y \le 1$ map to a rhombus in the $(u,v)$-plane defined by $0 \le u+v \le 2$ and $0 \le u-v \le 2$.

A more profound application of this method is the **Box-Muller transform**, a cornerstone technique for generating normally distributed random numbers [@problem_id:1408014]. It transforms two independent uniform variables $U_1, U_2 \sim \text{Uniform}(0,1)$ into two independent standard normal variables $X, Y \sim \mathcal{N}(0,1)$ via:
$$X = \sqrt{-2 \ln U_1} \cos(2\pi U_2)$$
$$Y = \sqrt{-2 \ln U_1} \sin(2\pi U_2)$$
The logic here is to interpret $(X,Y)$ in [polar coordinates](@entry_id:159425). The squared radius is $R^2 = X^2+Y^2 = -2 \ln U_1$, and the angle is $\Theta = 2\pi U_2$. This suggests that $\Theta$ is uniform on $[0, 2\pi]$, and the distribution of $R^2$ is related to an exponential. The inverse transformation is found to be $U_1 = \exp(-(x^2+y^2)/2)$ and $U_2 = \frac{1}{2\pi} \arctan(y/x)$ (using an appropriate multi-valued arctan). The Jacobian determinant of this inverse transformation can be calculated as $J = -\frac{1}{2\pi}\exp(-(x^2+y^2)/2)$.
Since $f_{U_1,U_2}(u_1, u_2) = 1$ on the unit square, the joint PDF for $(X,Y)$ becomes:
$$f_{X,Y}(x,y) = 1 \cdot |J| = \frac{1}{2\pi} \exp\left(-\frac{x^2+y^2}{2}\right)$$
This can be factored into two separate standard normal PDFs, $f_X(x) = \frac{1}{\sqrt{2\pi}}e^{-x^2/2}$ and $f_Y(y) = \frac{1}{\sqrt{2\pi}}e^{-y^2/2}$, demonstrating that the Box-Muller transform indeed produces two independent standard normal random variables.

### Advanced and Specialized Techniques

#### Linear Functions of Correlated Normal Variables

A special but highly important case involves [linear combinations](@entry_id:154743) of **[jointly normal random variables](@entry_id:199620)**. A key property of the [multivariate normal distribution](@entry_id:267217) is that any linear combination of its components is also a normal random variable.
If $(X_1, X_2)$ are jointly normal, then $S = aX_1 + bX_2$ is normal. Its mean and variance are easily calculated using the [linearity of expectation](@entry_id:273513) and the [properties of variance](@entry_id:185416):
$$E[S] = aE[X_1] + bE[X_2]$$
$$Var(S) = a^2 Var(X_1) + b^2 Var(X_2) + 2ab \cdot Cov(X_1, X_2)$$
Note the crucial covariance term, $Cov(X_1, X_2) = \rho \sigma_1 \sigma_2$, where $\rho$ is the [correlation coefficient](@entry_id:147037). This formula is fundamental in fields like finance for calculating portfolio variance and in engineering for analyzing systems with [correlated noise](@entry_id:137358) sources.

For example, if two correlated sensor measurements $X_1$ and $X_2$ are averaged to produce an estimate $S = \frac{1}{2}(X_1+X_2)$, we can find the variance of this estimate as [@problem_id:1347063]:
$$Var(S) = \frac{1}{4}(Var(X_1) + Var(X_2) + 2Cov(X_1, X_2)) = \frac{1}{4}(\sigma_1^2 + \sigma_2^2 + 2\rho\sigma_1\sigma_2)$$
This principle can be used in reverse. If we can experimentally measure a probability related to $S$ (e.g., $P(S > c) = p$), we can standardize $S$ using the variance expression above. This allows us to solve for an unknown parameter, such as the correlation coefficient $\rho$, connecting theoretical models to observable data.

#### Mixture Models and Compounding

A different kind of transformation occurs in **hierarchical** or **mixture models**. Here, a random variable's distribution depends on a parameter that is itself a random variable. The resulting unconditional distribution is a "mixture" of all the possible conditional distributions, weighted by the distribution of the parameter. The primary tool for this analysis is the **Law of Total Probability**.

If $K$ is a [discrete random variable](@entry_id:263460) whose distribution depends on a parameter $N$, which is also a [discrete random variable](@entry_id:263460), then:
$$P(K=k) = \sum_{n} P(K=k | N=n) P(N=n)$$

A classic example is **Poisson thinning** [@problem_id:1347103]. Imagine packets arriving at a switch according to a Poisson process, so the total number of packets $N$ in an interval is $N \sim \text{Poisson}(\lambda)$. Each packet is independently corrupted with probability $p$. We want to find the distribution of $K$, the number of corrupted packets.
Given that $N=n$ packets have arrived, the number of corrupted packets $K$ follows a [binomial distribution](@entry_id:141181): $K|N=n \sim \text{Binomial}(n, p)$.
To find the unconditional PMF of $K$, we apply the law of total probability:
$$P(K=k) = \sum_{n=0}^{\infty} P(K=k | N=n) P(N=n)$$
The term $P(K=k | N=n)$ is zero if $n  k$, so the sum can start from $n=k$:
$$P(K=k) = \sum_{n=k}^{\infty} P(K=k | N=n) P(N=n) = \sum_{n=k}^{\infty} \binom{n}{k}p^k(1-p)^{n-k} \frac{e^{-\lambda}\lambda^n}{n!}$$
This sum can be simplified by rearranging terms and re-indexing:
$$P(K=k) = \frac{(\lambda p)^k e^{-\lambda}}{k!} \sum_{n=k}^{\infty} \frac{(\lambda(1-p))^{n-k}}{(n-k)!}$$
Letting $j = n-k$, the sum becomes $\sum_{j=0}^{\infty} \frac{(\lambda(1-p))^j}{j!}$, which is the Taylor series for $e^{\lambda(1-p)}$.
$$P(K=k) = \frac{(\lambda p)^k e^{-\lambda}}{k!} e^{\lambda(1-p)} = \frac{(\lambda p)^k e^{-\lambda p}}{k!}$$
This reveals that the number of corrupted packets, $K$, also follows a Poisson distribution, but with a new rate parameter $\lambda p$.