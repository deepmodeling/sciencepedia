## Introduction
In the study of probability, many real-world phenomena—from the lifetime of a component to the price of a stock—are best modeled not by discrete values but by quantities that can vary continuously over a range. These are known as continuous random variables, and understanding them is a cornerstone of modern statistics. Unlike their discrete counterparts, the probability of a [continuous random variable](@entry_id:261218) taking any single, specific value is zero. This fundamental difference requires a new conceptual framework for defining and calculating probabilities. How do we describe the likelihood of events when individual outcomes have zero probability?

This article bridges that gap by systematically introducing the essential tools for working with continuous random variables. The **Principles and Mechanisms** section lays the theoretical groundwork, defining the Probability Density Function (PDF), the Cumulative Distribution Function (CDF), and key statistical measures like mean and variance. The subsequent **Applications** section demonstrates how these principles are applied to solve real-world problems in engineering, physics, and finance. Finally, the **Hands-On Practices** in the appendices provide opportunities to solidify your understanding through practical exercises. By progressing through these sections, you will move from foundational theory to practical application, gaining a robust understanding of how to model and analyze continuous phenomena.

## Principles and Mechanisms

In our study of probability, we distinguish between [discrete random variables](@entry_id:163471), which take on a countable number of values, and continuous random variables, which can take any value within a given range. While a discrete variable's behavior is described by a probability [mass function](@entry_id:158970) (PMF) that assigns a specific probability to each possible outcome, the situation for a continuous variable is fundamentally different. The probability that a [continuous random variable](@entry_id:261218) $X$ takes on any single specific value is zero. Instead, we focus on the probability that $X$ falls within a particular interval. This chapter explores the foundational tools for describing and analyzing continuous random variables: the probability density function and the [cumulative distribution function](@entry_id:143135).

### The Probability Density Function (PDF)

The primary tool for defining the probability distribution of a [continuous random variable](@entry_id:261218) is the **probability density function (PDF)**, denoted by $f(x)$. The PDF does not give probability directly; rather, the value of $f(x)$ at a point $x$ can be thought of as a measure of the relative likelihood that the random variable will be near $x$. The probability of the variable falling within an interval is found by integrating the PDF over that interval.

For a function $f(x)$ to be a valid PDF, it must satisfy two fundamental properties:

1.  **Non-negativity:** The function must be non-negative for all real numbers $x$.
    $f(x) \ge 0$ for all $x \in (-\infty, \infty)$.
    Probability cannot be negative, so the density that underpins it must also be non-negative.

2.  **Normalization:** The total area under the curve of the PDF must be equal to 1.
    $\int_{-\infty}^{\infty} f(x) \, dx = 1$.
    This ensures that the total probability of all possible outcomes is 1, a certainty.

A common task is to determine a constant within a proposed functional form of a PDF that ensures it is properly normalized [@problem_id:1909907]. Consider a random variable $X$ whose PDF is given by $f(x) = a|x-1|$ for $x \in [0, 3]$ and $f(x)=0$ otherwise. To find the constant $a$ that makes this a valid PDF, we first note that the non-negativity condition $f(x) \ge 0$ implies $a \ge 0$, since the absolute value term $|x-1|$ is always non-negative. The core task is to apply the [normalization condition](@entry_id:156486):

$$ \int_{0}^{3} a|x-1| \, dx = 1 $$

The presence of the absolute value function requires us to split the integral at the point where the argument of the absolute value changes sign, which is at $x=1$.

$$ a \left( \int_{0}^{1} (1-x) \, dx + \int_{1}^{3} (x-1) \, dx \right) = 1 $$

Evaluating these elementary integrals gives:

$$ \int_{0}^{1} (1-x) \, dx = \left[x - \frac{x^2}{2}\right]_{0}^{1} = \frac{1}{2} $$
$$ \int_{1}^{3} (x-1) \, dx = \left[\frac{x^2}{2} - x\right]_{1}^{3} = \left(\frac{9}{2}-3\right) - \left(\frac{1}{2}-1\right) = 2 $$

Substituting these results back into the normalization equation yields:

$$ a \left( \frac{1}{2} + 2 \right) = a \left( \frac{5}{2} \right) = 1 $$

Solving for $a$, we find $a = \frac{2}{5}$. This positive value ensures both non-negativity and normalization are satisfied.

Once a valid PDF is established, its primary use is to calculate the probability that the random variable falls within a specific range $[c, d]$. This probability is simply the area under the PDF curve between $c$ and $d$:

$$ P(c \le X \le d) = \int_{c}^{d} f(x) \, dx $$

For example, imagine modeling the location of a manufacturing defect along a wire of length $L$. Suppose the PDF is found to be $f(x) = kx(L-x)$ for $x \in [0, L]$, where $k$ is a normalization constant [@problem_id:1909917]. First, we find $k$ by normalization:

$$ \int_{0}^{L} kx(L-x) \, dx = k \left[ \frac{Lx^2}{2} - \frac{x^3}{3} \right]_{0}^{L} = k \left( \frac{L^3}{2} - \frac{L^3}{3} \right) = k \frac{L^3}{6} = 1 \implies k = \frac{6}{L^3} $$

Now, with the complete PDF $f(x) = \frac{6}{L^3}x(L-x)$, we can find the probability of the defect being in, for instance, the first quarter of the wire, i.e., $X \in [0, L/4]$.

$$ P\left(0 \le X \le \frac{L}{4}\right) = \int_{0}^{L/4} \frac{6}{L^3}x(L-x) \, dx = \frac{6}{L^3} \left[ \frac{Lx^2}{2} - \frac{x^3}{3} \right]_{0}^{L/4} $$

$$ = \frac{6}{L^3} \left( \frac{L(L/4)^2}{2} - \frac{(L/4)^3}{3} \right) = \frac{6}{L^3} \left( \frac{L^3}{32} - \frac{L^3}{192} \right) = 6 \left( \frac{6-1}{192} \right) = \frac{30}{192} = \frac{5}{32} $$

### The Cumulative Distribution Function (CDF)

While the PDF is fundamental, it is often more convenient to work with the **cumulative distribution function (CDF)**, denoted by $F(x)$. The CDF is defined as the probability that the random variable $X$ takes on a value less than or equal to $x$:

$$ F(x) = P(X \le x) = \int_{-\infty}^{x} f(t) \, dt $$

The CDF "accumulates" probability starting from $-\infty$. It has several key properties that follow directly from its definition:

1.  **Limits:** $F(x) \to 0$ as $x \to -\infty$, and $F(x) \to 1$ as $x \to \infty$.
2.  **Non-decreasing:** $F(x)$ is a [non-decreasing function](@entry_id:202520). That is, if $x_1 \lt x_2$, then $F(x_1) \le F(x_2)$.

The relationship between the PDF and CDF is central to the theory of continuous random variables. As seen from the definition, the CDF is the integral of the PDF. By the Fundamental Theorem of Calculus, the PDF is therefore the derivative of the CDF:

$$ f(x) = \frac{d}{dx} F(x) = F'(x) $$

This provides a direct path between the two descriptions of the random variable. For instance, if a physical process is described by a CDF $F(x) = \frac{1}{\pi}\arctan(x) + \frac{1}{2}$, a model associated with the Cauchy distribution, we can find the corresponding PDF by differentiation [@problem_id:1909909]:

$$ f(x) = \frac{d}{dx} \left( \frac{1}{\pi}\arctan(x) + \frac{1}{2} \right) = \frac{1}{\pi} \cdot \frac{1}{1+x^2} + 0 = \frac{1}{\pi(1+x^2)} $$

A significant advantage of the CDF is its ability to directly provide the probability of an interval. The probability that $X$ lies in the interval $(c, d]$ is:

$$ P(c \lt X \le d) = P(X \le d) - P(X \le c) = F(d) - F(c) $$

Since the probability of $X$ being exactly equal to any single point is zero for a continuous variable, $P(c \lt X \le d) = P(c \le X \le d) = P(c \lt X \lt d) = P(c \le X \lt d)$. Consider an electronic component whose lifetime $T$ (in thousands of hours) has a CDF $F(t) = \frac{t^2 - 100}{125}$ for $t \in [10, 15]$ [@problem_id:1909900]. The probability that a component's lifetime is between 11,000 and 14,000 hours ($11 \le T \le 14$) can be computed directly without integration:

$$ P(11 \le T \le 14) = F(14) - F(11) $$
$$ = \frac{14^2 - 100}{125} - \frac{11^2 - 100}{125} = \frac{196 - 100}{125} - \frac{121 - 100}{125} = \frac{96}{125} - \frac{21}{125} = \frac{75}{125} = 0.6 $$

This demonstrates the [computational efficiency](@entry_id:270255) offered by the CDF once it is known.

### Measures of Central Tendency

To summarize a distribution, we often use numerical measures that describe its center and shape.

#### The Expected Value (Mean)

The **expected value** or **mean** of a [continuous random variable](@entry_id:261218) $X$, denoted $E[X]$ or $\mu$, represents the long-run average value of the variable. It is calculated by integrating the product of each possible value $x$ and its corresponding probability density $f(x)$:

$$ E[X] = \mu = \int_{-\infty}^{\infty} x f(x) \, dx $$

Conceptually, the expected value is the "center of mass" of the distribution. This analogy leads to an important insight regarding symmetric distributions. If a PDF is symmetric about a point $c$, meaning $f(c+u) = f(c-u)$ for all $u$, then the expected value is $E[X] = c$. A formal proof confirms this intuition [@problem_id:6674]. For a distribution with PDF $f(x) = k(w^2 - (x-c)^2)$ on $[c-w, c+w]$, the expectation is:

$$ E[X] = \int_{c-w}^{c+w} x f(x) \, dx $$

By substituting $u = x-c$, we have $x = u+c$ and $dx=du$. The integral becomes:
$$ E[X] = \int_{-w}^{w} (u+c) k(w^2-u^2) \, du = k \int_{-w}^{w} u(w^2-u^2) \, du + ck \int_{-w}^{w} (w^2-u^2) \, du $$

The [first integral](@entry_id:274642) is of an [odd function](@entry_id:175940), $u(w^2-u^2)$, over a symmetric interval $[-w, w]$, so it evaluates to zero. The second integral is $ck \int_{-w}^{w} (w^2-u^2) \, du$, which is equal to $c$ times the integral of the PDF, which must be 1. Thus, $E[X] = c$.

For non-symmetric distributions, direct calculation is required. For a random variable with CDF $F(x) = \sin(\frac{\pi x}{2})$ on $[0,1]$, we first find the PDF $f(x) = F'(x) = \frac{\pi}{2}\cos(\frac{\pi x}{2})$ [@problem_id:1909896]. The expectation is then:

$$ E[X] = \int_{0}^{1} x \left( \frac{\pi}{2}\cos\left(\frac{\pi x}{2}\right) \right) \, dx $$

This integral requires [integration by parts](@entry_id:136350), yielding the result $E[X] = 1 - \frac{2}{\pi}$.

#### The Median and Mode

Besides the mean, two other important [measures of central tendency](@entry_id:168414) are the median and the mode.

The **median**, denoted $m$, is the value that divides the distribution into two halves of equal probability. It is the 50th percentile, satisfying the condition:

$$ F(m) = P(X \le m) = \int_{-\infty}^{m} f(x) \, dx = 0.5 $$

The **mode** is the value of $x$ at which the PDF $f(x)$ attains its maximum value. It represents the most likely outcome of the random variable. For a differentiable PDF on a closed interval, the mode can be found by finding the [critical points](@entry_id:144653) (where $f'(x)=0$) and checking them along with the interval endpoints [@problem_id:1909903]. For example, if $f(x) = 12x^2(1-x)$ for $x \in [0,1]$, we find the maximum by taking the derivative:

$$ f'(x) = \frac{d}{dx} (12x^2 - 12x^3) = 24x - 36x^2 = 12x(2-3x) $$

Setting $f'(x)=0$ gives [critical points](@entry_id:144653) at $x=0$ and $x=2/3$. By evaluating the PDF at these points and the endpoints ($f(0)=0, f(1)=0, f(2/3) = 16/9$), we find the mode is $x=2/3$.

The relationship between the mean, median, and mode gives an indication of the **[skewness](@entry_id:178163)** of a distribution. For a unimodal, symmetric distribution, all three are identical. If the distribution has a long tail to the right (right-skewed), we typically find that mode  median  mean. For a distribution modeling component lifetime as $f(x) = 3(1-x)^2$ on $[0,1]$ [@problem_id:190862], the mean is $E[X]=1/4$. The median $m$ is found by solving $F(m) = \int_0^m 3(1-t)^2 dt = 0.5$, which yields $m = 1-2^{-1/3} \approx 0.2063$. The difference $E[X]-m \approx 0.25 - 0.2063 = 0.0437$ is positive, indicating a right skew.

### Measures of Dispersion: Variance

While central tendency tells us about the "typical" value, [measures of dispersion](@entry_id:172010) describe how spread out the distribution is. The most important of these is the **variance**.

The **variance** of a random variable $X$, denoted $\text{Var}(X)$ or $\sigma^2$, is the expected value of the squared deviation from the mean:

$$ \text{Var}(X) = \sigma^2 = E[(X - \mu)^2] = \int_{-\infty}^{\infty} (x-\mu)^2 f(x) \, dx $$

A more convenient computational formula is derived from this definition:

$$ \text{Var}(X) = E[X^2] - (E[X])^2 $$

Here, $E[X^2]$ is the **second moment** of $X$, calculated as $E[X^2] = \int_{-\infty}^{\infty} x^2 f(x) \, dx$. To calculate the variance, one typically calculates the mean $E[X]$ and the second moment $E[X^2]$ separately.

As an example, let's find the [variance of a random variable](@entry_id:266284) with PDF $f(x) = \frac{1}{2}(x+1)$ on $[-1, 1]$ [@problem_id:1909898].
First, we compute the mean:
$$ E[X] = \int_{-1}^{1} x \cdot \frac{1}{2}(x+1) \, dx = \frac{1}{2} \int_{-1}^{1} (x^2+x) \, dx = \frac{1}{2} \left[\frac{x^3}{3} + \frac{x^2}{2}\right]_{-1}^{1} = \frac{1}{3} $$

Next, we compute the second moment:
$$ E[X^2] = \int_{-1}^{1} x^2 \cdot \frac{1}{2}(x+1) \, dx = \frac{1}{2} \int_{-1}^{1} (x^3+x^2) \, dx = \frac{1}{2} \left[\frac{x^4}{4} + \frac{x^3}{3}\right]_{-1}^{1} = \frac{1}{3} $$

Finally, we apply the [computational formula for variance](@entry_id:200764):
$$ \text{Var}(X) = E[X^2] - (E[X])^2 = \frac{1}{3} - \left(\frac{1}{3}\right)^2 = \frac{1}{3} - \frac{1}{9} = \frac{2}{9} $$

The square root of the variance, $\sigma = \sqrt{\text{Var}(X)}$, is the **standard deviation**. It is often preferred for interpretation as it has the same units as the random variable $X$.

### Conditional and Truncated Distributions

Sometimes we are interested in the behavior of a random variable given that some event has occurred. This leads to the concept of conditional distributions. A common case is when we know that the value of $X$ falls within a specific interval $[a, b]$. This is known as a **truncated distribution**.

If $X$ is a random variable with PDF $f(x)$, and we are given that $a \le X \le b$, the new conditional PDF, $f_{X|[a,b]}(x)$, is zero outside of $[a,b]$. Inside the interval, the shape of the density remains the same, but it must be rescaled so that the total probability integrates to 1 over the new, smaller domain. The scaling factor is the probability of the event itself, $P(a \le X \le b)$.

$$ f_{X|[a,b]}(x) = \frac{f(x)}{P(a \le X \le b)} = \frac{f(x)}{\int_a^b f(t) \, dt}, \quad \text{for } a \le x \le b $$

This concept is powerful. Consider a sensor whose lifetime $T$ follows an [exponential distribution](@entry_id:273894), $f_T(t) = \lambda \exp(-\lambda t)$ for $t \ge 0$. Suppose we only observe failures that occur within a time window $[a, b]$ [@problem_id:1909904]. Let $X$ be the failure time, conditioned on it being in $[a,b]$.

First, we find the probability of the conditioning event:
$$ P(a \le T \le b) = \int_a^b \lambda \exp(-\lambda t) \, dt = [-\exp(-\lambda t)]_a^b = \exp(-\lambda a) - \exp(-\lambda b) $$

The conditional PDF for $X$ is then:
$$ f_X(x) = \frac{\lambda \exp(-\lambda x)}{\exp(-\lambda a) - \exp(-\lambda b)}, \quad \text{for } a \le x \le b $$

We can now find the expected value of this truncated distribution, $E[X]$, by applying the standard expectation formula to the new conditional PDF:

$$ E[X] = \int_a^b x f_X(x) \, dx = \frac{1}{\exp(-\lambda a) - \exp(-\lambda b)} \int_a^b x \lambda \exp(-\lambda x) \, dx $$

Evaluating the integral (using integration by parts) leads to the expression for the [expected lifetime](@entry_id:274924), given that the sensor fails within the observation window:

$$ E[X] = \frac{a\exp(-\lambda a) - b\exp(-\lambda b)}{\exp(-\lambda a) - \exp(-\lambda b)} + \frac{1}{\lambda} $$

This result, which can be rearranged to the form $a + \frac{1}{\lambda} - \frac{b-a}{\exp(\lambda(b-a))-1}$, shows how conditioning modifies the expected outcome, blending the properties of the original exponential distribution with the constraints of the observation interval. Such analyses are crucial in fields like [reliability engineering](@entry_id:271311) and [survival analysis](@entry_id:264012), where data are often incomplete or subject to observational limits.