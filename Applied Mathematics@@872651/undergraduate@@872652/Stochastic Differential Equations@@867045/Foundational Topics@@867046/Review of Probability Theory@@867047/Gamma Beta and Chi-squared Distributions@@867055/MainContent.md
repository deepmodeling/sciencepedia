## Introduction
In the study of [stochastic processes](@entry_id:141566), understanding long-term equilibrium behavior is paramount. While systems may evolve randomly, they often settle into a predictable statistical state. A key question is which probability distributions govern these states, especially for processes constrained to specific domains, such as positive interest rates or proportions bounded between zero and one. This article demystifies the fundamental roles of three interconnected distribution families: the Gamma, Beta, and Chi-squared. We bridge the gap between their abstract definitions and their concrete emergence as stationary solutions to important stochastic differential equations (SDEs), revealing them as essential descriptors of stochastic reality.

The following chapters will guide you through this exploration. First, **Principles and Mechanisms** will establish the core mathematical properties of each distribution, their defining parameters, and their crucial relationships, such as the link between the Gamma and Chi-squared families. Next, **Applications and Interdisciplinary Connections** will journey into the practical use of these distributions in financial modeling, [population genetics](@entry_id:146344), and Bayesian statistics, highlighting their role in describing processes like the Cox-Ingersoll-Ross model. Finally, **Hands-On Practices** will offer practical exercises to ground your theoretical knowledge and build confidence in applying these powerful tools.

## Principles and Mechanisms

In the study of stochastic differential equations, certain families of probability distributions emerge not as mere mathematical conveniences, but as fundamental building blocks that naturally describe the long-term behavior of [stochastic systems](@entry_id:187663). The state space of a process—the set of all possible values it can assume—profoundly dictates the type of distribution that can characterize its statistical equilibrium. For processes confined to be positive, such as models for variance or interest rates, we require distributions supported on the positive real line $(0, \infty)$. For processes representing proportions or frequencies, we need distributions supported on the unit interval $(0, 1)$. This chapter explores three interconnected families of distributions—the Gamma, Beta, and Chi-squared—that fulfill these roles with remarkable elegance. We will examine their defining properties, their relationships to one another, and their crucial appearance as [stationary distributions](@entry_id:194199) for canonical SDEs.

### The Gamma Distribution: Modeling Unbounded Positive Quantities

The **Gamma distribution** is a versatile two-parameter family of [continuous probability distributions](@entry_id:636595) defined on the positive real line. It is an ideal candidate for modeling quantities that are inherently positive but unbounded, and its structure arises directly from the equilibrium conditions of important mean-reverting processes.

#### Definition and Core Properties

A random variable $X$ is said to follow a Gamma distribution with **[shape parameter](@entry_id:141062)** $k > 0$ and **scale parameter** $\theta > 0$, denoted $X \sim \Gamma(k, \theta)$, if its probability density function (PDF) is given by:
$$
f(x; k, \theta) = \frac{1}{\Gamma(k)\theta^k} x^{k-1} \exp\left(-\frac{x}{\theta}\right), \quad \text{for } x > 0
$$
Here, $\Gamma(k) = \int_0^\infty z^{k-1} e^{-z} dz$ is the **Gamma function**, which serves as the normalization constant. The shape parameter $k$ governs the form of the distribution, particularly its behavior near the origin, which is proportional to $x^{k-1}$. The [scale parameter](@entry_id:268705) $\theta$ stretches or compresses the distribution along the x-axis.

An alternative and equally important parametrization uses a **[rate parameter](@entry_id:265473)** $\beta = 1/\theta$. Substituting $\theta = 1/\beta$ into the density gives the rate form [@problem_id:3056382]:
$$
f(x; k, \beta) = \frac{\beta^k}{\Gamma(k)} x^{k-1} \exp(-\beta x), \quad \text{for } x > 0
$$
This form is frequently encountered in Bayesian statistics and in the study of Poisson processes, where $\beta$ represents an event rate.

A critical feature of the Gamma distribution is its tail behavior. As $x \to \infty$, the exponential term $\exp(-x/\theta)$ dominates the polynomial term $x^{k-1}$, causing the density to decay to zero rapidly. This **exponentially decaying tail** is a key property, making the Gamma distribution suitable for modeling the stationary state of mean-reverting processes, where large excursions from the mean are possible but increasingly rare [@problem_id:3056389].

#### Moments and Generating Functions

The moments of the Gamma distribution can be systematically derived using its **[moment generating function](@entry_id:152148) (MGF)**, defined as $M_X(t) = \mathbb{E}[\exp(tX)]$. We can compute this directly from the PDF [@problem_id:3056383]:
$$
\begin{align}
M_X(t)  = \int_0^\infty \exp(tx) \frac{1}{\Gamma(k)\theta^k} x^{k-1} \exp\left(-\frac{x}{\theta}\right) dx \\
 = \frac{1}{\Gamma(k)\theta^k} \int_0^\infty x^{k-1} \exp\left( -x \left( \frac{1}{\theta} - t \right) \right) dx
\end{align}
$$
For this integral to converge, we require $\frac{1}{\theta} - t > 0$, which implies $t  1/\theta$. This defines the domain where the MGF is finite. By performing a change of variables $u = x(1/\theta - t)$, the integral becomes $\Gamma(k) / (1/\theta - t)^k$. Substituting this back yields the remarkably simple form for the MGF:
$$
M_X(t) = \frac{1}{\Gamma(k)\theta^k} \frac{\Gamma(k)}{(1/\theta - t)^k} = \frac{1}{(1-\theta t)^k}, \quad \text{for } t  1/\theta
$$
From the MGF, we can also find the **[cumulant generating function](@entry_id:149336) (CGF)**, $K_X(t) = \ln M_X(t)$, which is often simpler for calculating moments [@problem_id:3056383]:
$$
K_X(t) = \ln\left((1-\theta t)^{-k}\right) = -k \ln(1 - \theta t)
$$
The mean and variance are the first and second [cumulants](@entry_id:152982), which can be found by differentiating the CGF. Alternatively, we can differentiate the MGF [@problem_id:3056426]. The first moment (mean) is $\mathbb{E}[X] = M'_X(0)$:
$$
M'_X(t) = \frac{d}{dt}(1-\theta t)^{-k} = (-k)(1-\theta t)^{-k-1}(-\theta) = k\theta(1-\theta t)^{-k-1}
$$
$$
\mathbb{E}[X] = M'_X(0) = k\theta
$$
The second moment is $\mathbb{E}[X^2] = M''_X(0)$:
$$
M''_X(t) = k\theta(-k-1)(1-\theta t)^{-k-2}(-\theta) = k(k+1)\theta^2(1-\theta t)^{-k-2}
$$
$$
\mathbb{E}[X^2] = M''_X(0) = k(k+1)\theta^2
$$
The variance is then easily calculated:
$$
\mathrm{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2 = k(k+1)\theta^2 - (k\theta)^2 = k^2\theta^2 + k\theta^2 - k^2\theta^2 = k\theta^2
$$
Thus, for $X \sim \Gamma(k, \theta)$, the mean is $k\theta$ and the variance is $k\theta^2$.

#### The Chi-squared Distribution as a Special Case

The **Chi-squared distribution** is of paramount importance in statistics and is deeply connected to Gaussian processes like Brownian motion. A random variable with a chi-squared distribution with $\nu$ degrees of freedom, denoted $\chi^2_\nu$, is defined as the sum of the squares of $\nu$ independent standard normal random variables. For instance, the scaled quadratic variation of a standard Brownian motion $W_t$ over $n$ steps, $S_n = \sum_{i=1}^n \frac{(W_{i\Delta t} - W_{(i-1)\Delta t})^2}{\Delta t}$, follows a $\chi^2_n$ distribution [@problem_id:3056434].

The $\chi^2_\nu$ distribution is a special case of the Gamma distribution. Specifically, a random variable $X \sim \chi^2_\nu$ is identically distributed to a Gamma random variable with shape $k = \nu/2$ and scale $\theta=2$ [@problem_id:3056434].
$$
X \sim \chi^2_\nu \iff X \sim \Gamma\left(k = \frac{\nu}{2}, \theta = 2\right)
$$
By substituting these parameters into the Gamma PDF, we obtain the PDF for the $\chi^2_\nu$ distribution:
$$
f(x; \nu) = \frac{1}{\Gamma(\nu/2)2^{\nu/2}} x^{\nu/2 - 1} \exp(-x/2), \quad \text{for } x > 0
$$
From this relationship, we can immediately find its MGF, mean, and variance by substituting $k=\nu/2$ and $\theta=2$ into the general Gamma formulas [@problem_id:3056442]:
- **MGF**: $M_X(t) = (1 - 2t)^{-\nu/2}$ for $t  1/2$.
- **Mean**: $\mathbb{E}[X] = k\theta = (\nu/2) \cdot 2 = \nu$.
- **Variance**: $\mathrm{Var}(X) = k\theta^2 = (\nu/2) \cdot 2^2 = 2\nu$.
These results are cornerstones of [statistical hypothesis testing](@entry_id:274987).

#### Application: Stationary Distribution of the CIR Process

The theoretical importance of the Gamma distribution is powerfully illustrated by its emergence as the [stationary distribution](@entry_id:142542) of the **Cox-Ingersoll-Ross (CIR) process**. This process is a cornerstone of [financial mathematics](@entry_id:143286), often used to model interest rates, and is defined by the SDE [@problem_id:3056382]:
$$
dX_t = \kappa(\mu - X_t)dt + \sigma \sqrt{X_t} dW_t
$$
where $\kappa$ is the speed of [mean reversion](@entry_id:146598), $\mu$ is the long-term mean, and $\sigma$ is the volatility. The drift coefficient is $A(x) = \kappa(\mu - x)$ and the squared diffusion coefficient is $B(x)^2 = \sigma^2 x$.

To find the stationary density $p(x)$, we use the steady-state Fokker-Planck equation, which reduces to the [zero-flux condition](@entry_id:182067):
$$
A(x) p(x) - \frac{1}{2}\frac{d}{dx}[B(x)^2 p(x)] = 0
$$
Substituting the CIR coefficients:
$$
\kappa(\mu - x)p(x) = \frac{1}{2}\frac{d}{dx}[\sigma^2 x p(x)]
$$
This is a first-order ordinary differential equation for $p(x)$. Solving it by [separation of variables](@entry_id:148716) leads to the solution:
$$
p(x) \propto x^{\frac{2\kappa\mu}{\sigma^2} - 1} \exp\left(-\frac{2\kappa}{\sigma^2} x\right)
$$
We immediately recognize this as the kernel of a Gamma distribution. By comparing this form to the rate-parameterized Gamma PDF, $f(x; k, \beta) \propto x^{k-1}\exp(-\beta x)$, we can identify the parameters of the [stationary distribution](@entry_id:142542):
- **Shape parameter**: $k = \frac{2\kappa\mu}{\sigma^2}$
- **Rate parameter**: $\beta = \frac{2\kappa}{\sigma^2}$
This corresponds to a [scale parameter](@entry_id:268705) of $\theta = 1/\beta = \frac{\sigma^2}{2\kappa}$. Thus, the CIR process has a [stationary distribution](@entry_id:142542) $\Gamma\left(\frac{2\kappa\mu}{\sigma^2}, \frac{\sigma^2}{2\kappa}\right)$. This profound result connects the microscopic dynamics of the SDE to a macroscopic, time-invariant statistical law.

### The Beta Distribution: Modeling Proportions and Frequencies

Just as the Gamma distribution is the natural choice for unbounded positive quantities, the **Beta distribution** is the canonical distribution for quantities constrained to lie within the unit interval $(0, 1)$, such as probabilities, proportions, or frequencies.

#### Definition and Core Properties

A random variable $X$ follows a Beta distribution with [shape parameters](@entry_id:270600) $\alpha > 0$ and $\beta > 0$, denoted $X \sim \mathrm{Beta}(\alpha, \beta)$, if its PDF is:
$$
f(x; \alpha, \beta) = \frac{1}{B(\alpha, \beta)} x^{\alpha-1} (1-x)^{\beta-1}, \quad \text{for } 0  x  1
$$
The normalization constant is the **Beta function**, $B(\alpha, \beta) = \int_0^1 u^{\alpha-1}(1-u)^{\beta-1}du$, which has a direct relationship with the Gamma function: $B(\alpha, \beta) = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$.

The support of the Beta distribution is strictly $(0, 1)$. The behavior at the boundaries is governed by the [shape parameters](@entry_id:270600) [@problem_id:3056389]:
- Near $x=0$, the density behaves like $x^{\alpha-1}$.
- Near $x=1$, the density behaves like $(1-x)^{\beta-1}$.
By varying $\alpha$ and $\beta$, the Beta distribution can assume a wide variety of shapes—U-shaped, J-shaped, uniform, or bell-shaped—making it extremely flexible for modeling phenomena on a bounded interval.

#### Moments of the Beta Distribution

The moments of the Beta distribution are most elegantly calculated by exploiting the integral form of the Beta function itself [@problem_id:3056406]. The $k$-th raw moment $\mathbb{E}[X^k]$ is given by:
$$
\mathbb{E}[X^k] = \int_0^1 x^k \frac{1}{B(\alpha, \beta)} x^{\alpha-1} (1-x)^{\beta-1} dx = \frac{1}{B(\alpha, \beta)} \int_0^1 x^{\alpha+k-1} (1-x)^{\beta-1} dx
$$
The integral is simply the Beta function $B(\alpha+k, \beta)$. Therefore,
$$
\mathbb{E}[X^k] = \frac{B(\alpha+k, \beta)}{B(\alpha, \beta)}
$$
Using the Gamma function representation, we can derive the mean ($\mathbb{E}[X]$) and variance. For the mean ($k=1$):
$$
\mathbb{E}[X] = \frac{B(\alpha+1, \beta)}{B(\alpha, \beta)} = \frac{\Gamma(\alpha+1)\Gamma(\beta)}{\Gamma(\alpha+\beta+1)} \cdot \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} = \frac{\alpha\Gamma(\alpha)}{\Gamma(\alpha)} \cdot \frac{\Gamma(\alpha+\beta)}{(\alpha+\beta)\Gamma(\alpha+\beta)} = \frac{\alpha}{\alpha+\beta}
$$
A similar calculation for $\mathbb{E}[X^2]$ yields $\frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)}$. The variance is then:
$$
\mathrm{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2 = \frac{\alpha(\alpha+1)}{(\alpha+\beta)(\alpha+\beta+1)} - \left(\frac{\alpha}{\alpha+\beta}\right)^2 = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}
$$

#### Application: Stationary Distribution of Wright-Fisher Type Diffusions

The Beta distribution naturally appears as the stationary law for SDEs modeling frequencies on $(0, 1)$, such as the **Wright-Fisher diffusion** used in [population genetics](@entry_id:146344) or the related **Jacobi diffusion** [@problem_id:3056445]. Consider a diffusion on $(0, 1)$ given by:
$$
dX_t = \kappa(\theta - X_t)dt + \sqrt{2c X_t(1-X_t)} dW_t
$$
Here, $\theta \in (0, 1)$ is a mean frequency, $\kappa$ is a mean-reversion speed, and the diffusion term $\sqrt{X_t(1-X_t)}$ ensures the process remains within $(0, 1)$ by vanishing at the boundaries. The drift is $A(x) = \kappa(\theta-x)$ and the squared diffusion is $B(x)^2 = 2cx(1-x)$.

Applying the stationary Fokker-Planck equation, $A(x)\pi(x) = \frac{1}{2}\frac{d}{dx}[B(x)^2\pi(x)]$, gives:
$$
\kappa(\theta-x)\pi(x) = \frac{1}{2}\frac{d}{dx}[2cx(1-x)\pi(x)] = c\frac{d}{dx}[x(1-x)\pi(x)]
$$
Solving this differential equation for the stationary density $\pi(x)$ yields:
$$
\pi(x) \propto x^{\frac{\kappa\theta}{c}-1} (1-x)^{\frac{\kappa(1-\theta)}{c}-1}
$$
This is precisely the kernel of a Beta distribution. By comparing exponents, we identify its parameters as [@problem_id:3056445]:
- $\alpha = \frac{\kappa\theta}{c}$
- $\beta = \frac{\kappa(1-\theta)}{c}$
This demonstrates that the [equilibrium distribution](@entry_id:263943) of frequencies in such models is a Beta distribution, with parameters determined by the balance of drift and diffusion in the SDE.

### Interconnections and Further Applications

The Gamma and Beta distributions are not merely analogues for different state spaces; they are deeply mathematically intertwined.

#### The Gamma-Beta Relationship

A fundamental result connects the two families: the ratio of two independent Gamma-distributed random variables with the same [scale parameter](@entry_id:268705) follows a Beta distribution. Specifically, let $X \sim \Gamma(\alpha, \theta)$ and $Y \sim \Gamma(\beta, \theta)$ be independent. We want to find the distribution of $U = X/(X+Y)$ [@problem_id:3056390].

We use the change-of-variables method with the auxiliary variable $V = X+Y$. The inverse transformation is $X = UV$ and $Y = V(1-U)$. The Jacobian of this transformation is $|J|=v$. The joint PDF of $(X,Y)$ is
$$
f_{X,Y}(x,y) = \frac{1}{\Gamma(\alpha)\Gamma(\beta)\theta^{\alpha+\beta}} x^{\alpha-1}y^{\beta-1} \exp\left(-\frac{x+y}{\theta}\right)
$$
The joint PDF of $(U,V)$ is therefore:
$$
\begin{align}
f_{U,V}(u,v) = f_{X,Y}(uv, v(1-u)) \cdot v \\
= \frac{1}{\Gamma(\alpha)\Gamma(\beta)\theta^{\alpha+\beta}} (uv)^{\alpha-1}(v(1-u))^{\beta-1} \exp\left(-\frac{v}{\theta}\right) \cdot v \\
= \frac{u^{\alpha-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)} \cdot \frac{v^{\alpha+\beta-1}\exp(-v/\theta)}{\theta^{\alpha+\beta}}
\end{align}
$$
To find the [marginal density](@entry_id:276750) of $U$, we integrate over $v$ from $0$ to $\infty$:
$$
f_U(u) = \frac{u^{\alpha-1}(1-u)^{\beta-1}}{\Gamma(\alpha)\Gamma(\beta)\theta^{\alpha+\beta}} \int_0^\infty v^{\alpha+\beta-1}\exp(-v/\theta) dv
$$
The integral is the unnormalized kernel of a $\Gamma(\alpha+\beta, \theta)$ distribution, and it evaluates to $\Gamma(\alpha+\beta)\theta^{\alpha+\beta}$. The $\theta^{\alpha+\beta}$ terms cancel perfectly, yielding:
$$
f_U(u) = \frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)} u^{\alpha-1}(1-u)^{\beta-1}
$$
This is the PDF of a $\mathrm{Beta}(\alpha, \beta)$ distribution. Remarkably, the distribution of the ratio $U$ is independent of the common scale parameter $\theta$.

Furthermore, the factorized form of the joint density $f_{U,V}(u,v)$ reveals another profound result: $U$ and $V=X+Y$ are independent random variables [@problem_id:3056388]. We have $U \sim \mathrm{Beta}(\alpha, \beta)$ and $V \sim \Gamma(\alpha+\beta, \theta)$. This powerful property is a cornerstone of many [hierarchical models](@entry_id:274952) in Bayesian statistics.

#### Conjugate Priors in Bayesian Inference

The structure of the Beta distribution makes it a **[conjugate prior](@entry_id:176312)** for the Bernoulli (and Binomial) likelihood. Conjugacy means that the [posterior distribution](@entry_id:145605) belongs to the same family as the prior distribution, which greatly simplifies Bayesian updating.

Suppose we model a series of binary events (e.g., threshold crossings of an SDE's solution in [discrete time](@entry_id:637509) windows) with a Bernoulli process. The probability of success is $p$. We observe $x$ successes in $n$ trials. The likelihood of this data is Binomial: $L(p|x,n) \propto p^x(1-p)^{n-x}$. If we place a $\mathrm{Beta}(\alpha, \beta)$ prior on the unknown probability $p$, its density is $f(p) \propto p^{\alpha-1}(1-p)^{\beta-1}$.

By Bayes' theorem, the posterior density is proportional to the product of the prior and the likelihood [@problem_id:3056440]:
$$
f(p|x,n) \propto f(p) \cdot L(p|x,n) \propto \left( p^{\alpha-1}(1-p)^{\beta-1} \right) \cdot \left( p^x(1-p)^{n-x} \right)
$$
$$
f(p|x,n) \propto p^{\alpha+x-1}(1-p)^{\beta+n-x-1}
$$
This is immediately recognizable as the kernel of another Beta distribution. The [posterior distribution](@entry_id:145605) is therefore $\mathrm{Beta}(\alpha+x, \beta+n-x)$. The hyperparameters are updated in a simple, intuitive way: the new [shape parameter](@entry_id:141062) $\alpha'$ is the prior's $\alpha$ plus the number of successes, and the new $\beta'$ is the prior's $\beta$ plus the number of failures. This elegant property makes the Beta distribution indispensable in the Bayesian modeling of proportions.