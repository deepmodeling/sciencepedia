## Introduction
Stochastic processes are the mathematical language of systems that evolve randomly over time. While the [continuous paths](@entry_id:187361) of Brownian motion provide a powerful model for many phenomena, they fall short when describing systems subject to sudden, unpredictable shocks or jumps. Lévy processes extend this framework by incorporating such discontinuities, providing a vastly more flexible and realistic class of models. They represent a cornerstone of modern probability theory, essential for capturing the [complex dynamics](@entry_id:171192) observed in fields ranging from financial markets to physical systems. This article addresses the fundamental question: what is the universal structure underlying these complex [jump processes](@entry_id:180953)?

Over the following chapters, you will build a comprehensive understanding of Lévy processes from the ground up. The journey begins in "Principles and Mechanisms," where we will dissect the formal axiomatic definition, unveil the powerful Lévy-Khintchine formula that characterizes their distribution, and explore the intuitive pathwise structure given by the Lévy-Itô decomposition. Next, "Applications and Interdisciplinary Connections" will demonstrate how this abstract theory is put into practice, showcasing how different types of Lévy processes model phenomena in finance, physics, and engineering. Finally, "Hands-On Practices" will challenge you to apply these concepts, solidifying your grasp of the core material. We begin by establishing the formal definition and foundational properties that make Lévy processes a unique and powerful tool.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and mechanisms that govern Lévy processes. We transition from the abstract axiomatic definition to a concrete, pathwise decomposition that reveals the structure of these processes. This structural understanding will allow us to explore their key properties, including their moments, [path regularity](@entry_id:203771), and connections to the broader theory of [semimartingales](@entry_id:184490).

### Formal Definition and Foundational Properties

A [stochastic process](@entry_id:159502) is a mathematical model for a system that evolves randomly over time. While many processes exhibit complex dependencies, the class of Lévy processes is defined by a powerful and simplifying structure: their evolution over disjoint time intervals is independent and statistically identical.

Formally, a [stochastic process](@entry_id:159502) $X = (X_t)_{t \ge 0}$ taking values in $\mathbb{R}^d$ is a **Lévy process** if it satisfies the following set of axioms [@problem_id:2984419]:

1.  **Initial Condition:** $X_0 = 0$ almost surely. The process starts at the origin.

2.  **Independent Increments:** For any sequence of times $0 \le t_0 \lt t_1 \lt \dots \lt t_n$, the increments $X_{t_1} - X_{t_0}, X_{t_2} - X_{t_1}, \dots, X_{t_n} - X_{t_{n-1}}$ are mutually independent random variables. The future evolution of the process depends only on its current state, not on its past trajectory.

3.  **Stationary Increments:** The distribution of an increment $X_{s+t} - X_s$ depends only on the length of the time interval, $t$, and not on its starting time, $s$. That is, for any $s, t \ge 0$, the random variable $X_{s+t} - X_s$ has the same probability distribution as $X_t$.

4.  **Stochastic Continuity:** The process does not exhibit fixed, deterministic jumps. Formally, for any $s \ge 0$ and any $\epsilon > 0$, the probability of a significant jump away from $X_s$ in a small time interval tends to zero: $\mathbb{P}(\|X_t - X_s\| > \epsilon) \to 0$ as $t \to s$.

An essential consequence of these axioms is a regularity property of the [sample paths](@entry_id:184367). It can be shown that any process satisfying the above conditions has a modification whose [sample paths](@entry_id:184367) are **càdlàg**, a French acronym for *continue à droite, limites à gauche*. This means the paths are right-continuous everywhere and have well-defined left-limits at every point. This regularity ensures that the process does not "explode" in finite time and that jumps are well-defined events occurring at specific instants. Many authors include the càdlàg property directly in the definition.

### The Lévy-Khintchine Formula and The Characteristic Triplet

The properties of stationary and [independent increments](@entry_id:262163) imply that the probability distribution of $X_t$ is **infinitely divisible** for any $t > 0$. A distribution is infinitely divisible if its characteristic random variable can be written as the sum of $n$ [independent and identically distributed](@entry_id:169067) (i.i.d.) random variables for any integer $n$. For a Lévy process, $X_t$ can be expressed as the sum of $n$ i.i.d. increments: $X_t = \sum_{k=1}^n (X_{kt/n} - X_{(k-1)t/n})$.

This property of [infinite divisibility](@entry_id:637199) is the key to characterizing all possible Lévy processes. The celebrated **Lévy-Khintchine theorem** states that a function $\phi(u)$ is the [characteristic function](@entry_id:141714) of an infinitely divisible distribution if and only if its logarithm has a specific [canonical form](@entry_id:140237). For a Lévy process $X_t$, this translates to a characterization of its characteristic function, $\mathbb{E}\left[e^{i \langle u, X_t \rangle}\right]$, where $u \in \mathbb{R}^d$. Due to [stationarity](@entry_id:143776), this function must be of the form $e^{t\Psi(u)}$, where $\Psi(u)$ is the **[characteristic exponent](@entry_id:188977)**. The Lévy-Khintchine formula gives the general representation of this exponent:
$$
\Psi(u) = i\langle b, u \rangle - \frac{1}{2}\langle u, Q u \rangle + \int_{\mathbb{R}^d \setminus \{0\}} \left( e^{i \langle u, x \rangle} - 1 - i \langle u, x \rangle \mathbf{1}_{\|x\| \le 1}(x) \right) \nu(dx)
$$
This formula reveals that every Lévy process is uniquely determined by a set of three parameters, known as the **Lévy triplet** $(b, Q, \nu)$, where the components have distinct structural interpretations [@problem_id:2984429]:

*   **The Drift Vector ($b$):** The vector $b \in \mathbb{R}^d$ is related to the deterministic, linear drift of the process. Note that its value depends on the choice of truncation function (here, $\mathbf{1}_{\|x\| \le 1}(x)$) used to ensure the convergence of the integral.

*   **The Gaussian Covariance Matrix ($Q$):** The matrix $Q$ is a $d \times d$ **symmetric positive semidefinite** matrix. It governs the continuous, diffusive part of the process, which behaves like a $d$-dimensional Brownian motion. Symmetry and [positive semidefiniteness](@entry_id:147720) are essential for $e^{-\frac{t}{2}\langle u, Qu \rangle}$ to be a valid [characteristic function](@entry_id:141714).

*   **The Lévy Measure ($\nu$):** The measure $\nu$ on $\mathbb{R}^d \setminus \{0\}$ is the most distinctive element, as it governs the jump behavior of the process. For any Borel set $A \subset \mathbb{R}^d \setminus \{0\}$, $t \nu(A)$ can be interpreted as the expected number of jumps in the time interval $[0, t]$ whose size falls within the set $A$. For $\nu$ to be a valid Lévy measure, it must satisfy two conditions:
    1.  **Exclusion of the Origin:** $\nu(\{0\}) = 0$. This is a crucial convention. The integrand in the Lévy-Khintchine formula evaluates to zero at $x=0$, meaning any mass at the origin would not affect the process's law. Allowing $\nu(\{0\}) > 0$ would lead to a non-unique triplet for the same process. From a pathwise perspective, a positive mass at zero would imply jumps of size zero occurring with positive intensity—events that are unobservable and redundant. By convention, we set $\nu(\{0\}) = 0$ to ensure a unique representation and eliminate this redundancy [@problem_id:2984424].
    2.  **Integrability Condition:** $\displaystyle \int_{\mathbb{R}^d} (\|x\|^2 \wedge 1) \nu(dx)  \infty$. This condition is subtle but fundamental. It can be broken into two parts:
        *   $\int_{\|x\|  1} 1 \cdot \nu(dx) = \nu(\{x: \|x\|  1\})  \infty$. This implies that the total expected rate of "large" jumps (those with size greater than 1) is finite.
        *   $\int_{\|x\| \le 1} \|x\|^2 \nu(dx)  \infty$. This condition restricts the intensity of "small" jumps. The rate of small jumps, $\int_{\|x\| \le 1} \nu(dx)$, can be infinite (a property known as infinite activity), but their "energy", weighted by the square of their size, must be finite.

### The Lévy-Itô Decomposition: A Pathwise Perspective

The Lévy-Khintchine formula provides a complete description of the *law* of a Lévy process. The **Lévy-Itô decomposition theorem** provides an even more intuitive picture by giving a pathwise construction of the process itself. It states that any Lévy process $X_t$ can be decomposed into a sum of four independent components, each corresponding to a term in its [characteristic triplet](@entry_id:635937) [@problem_id:2984420]:

$$
X_t = b t + W_t^{\!Q} + \int_{0}^{t}\int_{\{\|x\| \le 1\}} x \tilde{N}(ds, dx) + \int_{0}^{t}\int_{\{\|x\|  1\}} x N(ds, dx)
$$

Let's dissect each component of this powerful decomposition:

1.  **Linear Drift ($b t$):** This is a deterministic, continuous path representing the underlying drift. The drift parameter $b$ here is precisely the one appearing in the Lévy-Khintchine formula when the canonical truncation function $h(x) = x \mathbf{1}_{\|x\| \le 1}$ is used.

2.  **Brownian Motion ($W_t^{\!Q}$):** This is a $d$-dimensional Brownian motion with covariance matrix $Q$. That is, $\mathbb{E}[W_t^{\!Q}(W_t^{\!Q})^\top] = tQ$. This component represents the continuous, random fluctuations of the process. If $Q=0$, the process is a pure-[jump process](@entry_id:201473).

3.  **Compensated Small Jumps:** The term $M_t = \int_0^t \int_{\{\|x\| \le 1\}} x \tilde{N}(ds, dx)$ represents the contribution from small jumps. Here, $N(ds, dx)$ is the **Poisson random measure** that counts the jumps of the process; $N((0,t] \times A)$ is a Poisson random variable with mean $t\nu(A)$. If the process has infinite activity, the [direct sum](@entry_id:156782) of small jumps $\sum \Delta X_s$ may not converge. The solution is to use the **compensated measure** $\tilde{N}(ds, dx) = N(ds, dx) - ds\,\nu(dx)$, where we subtract the expected number of jumps. The resulting [stochastic integral](@entry_id:195087) is a well-defined **[martingale](@entry_id:146036)** (a process whose future expectation is its current value). It captures the random fluctuations from the potentially infinite stream of small jumps.

4.  **Large Jumps:** The term $J_t = \int_0^t \int_{\{\|x\|  1\}} x N(ds, dx)$ represents the contribution from large jumps. Since the rate of large jumps is finite, this process is a **compound Poisson process**—a sum of a finite number of jumps arriving at random times. No compensation is necessary for this integral to converge.

This decomposition is profound: it reveals that any Lévy process, no matter how complex its behavior, can be constructed from three simple, independent building blocks: a deterministic line, a Brownian motion, and a [jump process](@entry_id:201473) which itself is a combination of a [martingale](@entry_id:146036) of small jumps and a compound Poisson process of large jumps.

### Finer Structure and Properties

The Lévy-Itô decomposition is the master key to unlocking a deeper understanding of the properties of a Lévy process.

#### Moments and Martingale Properties

The integrability of a Lévy process depends on the properties of its jump measure. A general result states that for $p \in (0, 2]$, the $p$-th absolute moment $\mathbb{E}[|X_t|^p]$ is finite if and only if the Lévy measure's tail is sufficiently light [@problem_id:2984413]:
$$
\mathbb{E}[|X_t|^p]  \infty \quad \iff \quad \int_{|x|1} |x|^p \nu(dx)  \infty
$$
This is because the Brownian and compensated small-jump components are known to have finite moments up to order 2, so the existence of moments is dictated entirely by the behavior of the large jumps.

For the special case of the first moment ($p=1$), if $\int_{|x|1} |x| \nu(dx)  \infty$, we can compute the expectation of $X_t$ by taking the expectation of each term in the Lévy-Itô decomposition:
$$
\mathbb{E}[X_t] = \mathbb{E}[bt] + \mathbb{E}[W_t^{\!Q}] + \mathbb{E}\left[\int_{0}^{t}\int_{\{|x| \le 1\}} x \tilde{N}(ds, dx)\right] + \mathbb{E}\left[\int_{0}^{t}\int_{\{|x|  1\}} x N(ds, dx)\right]
$$
The expectations of the Brownian motion and the compensated small-jump [martingale](@entry_id:146036) are zero. The expectation of the compound Poisson process of large jumps is $t \int_{|x|1} x \nu(dx)$. This yields the formula for the mean:
$$
\mathbb{E}[X_t] = t \left( b + \int_{|x|1} x \nu(dx) \right)
$$
As an example, consider a process whose large jumps are exponentially distributed, with Lévy measure density $\nu(dx) = \lambda e^{-\beta x} \mathbf{1}_{\{x0\}}dx$ for $\beta  0$. The mean is found by calculating the integral $\int_1^\infty x (\lambda e^{-\beta x}) dx$, which yields $\mathbb{E}[X_t] = t \left(b + \frac{\lambda(\beta+1)}{\beta^2}e^{-\beta}\right)$ [@problem_id:2984413].

This formula for the mean directly leads to conditions for the [martingale property](@entry_id:261270) [@problem_id:3002115]. A Lévy process $X_t$ (with finite first moment) is a **[martingale](@entry_id:146036)** if and only if its expectation is zero for all $t$, which requires:
$$
b + \int_{|x|1} x \nu(dx) = 0
$$
Similarly, it is a **[submartingale](@entry_id:263978)** (i.e., $\mathbb{E}[X_t|\mathcal{F}_s] \ge X_s$) if and only if its expected value is a [non-decreasing function](@entry_id:202520) of time, which requires:
$$
b + \int_{|x|1} x \nu(dx) \ge 0
$$
In the special case where the Lévy measure $\nu$ is symmetric (i.e., $\nu(A) = \nu(-A)$), the integral $\int_{|x|1} x \nu(dx)$ is zero. Then, the process is a martingale if and only if its drift parameter $b$ is zero.

#### Path Regularity and the Blumenthal-Getoor Index

The [sample paths](@entry_id:184367) of a Lévy process can be smooth or extremely irregular. The degree of irregularity is largely determined by the intensity of small jumps. A powerful tool for quantifying this is the **Blumenthal-Getoor index**, defined as [@problem_id:2984414]:
$$
\beta = \inf\left\{ \gamma  0 : \int_{|x| \le 1} |x|^\gamma \nu(dx)  \infty \right\}
$$
By definition of a Lévy measure, this integral is always finite for $\gamma=2$, so we always have $\beta \in [0, 2]$. This index measures how fast the Lévy measure concentrates mass near the origin. A smaller $\beta$ implies fewer or smaller small jumps and thus smoother paths.

The main importance of the Blumenthal-Getoor index lies in its connection to the **$p$-variation** of the [sample paths](@entry_id:184367). For a pure-jump Lévy process (with $Q=0$), it is a fundamental theorem that its [sample paths](@entry_id:184367) on any compact interval have finite $p$-variation if $p  \beta$, and infinite $p$-variation if $p  \beta$ [@problem_id:2984414].

A key case is **bounded variation** (or finite 1-variation). A pure-[jump process](@entry_id:201473) has paths of bounded variation if and only if $\int_{|x| \le 1} |x| \nu(dx)  \infty$. If the Blumenthal-Getoor index $\beta  1$, this condition is automatically satisfied, implying the process has bounded variation paths [@problem_id:2984414].

For example, a symmetric **$\alpha$-[stable process](@entry_id:183611)** with $\alpha \in (0, 2)$ has a Lévy measure with density proportional to $|x|^{-1-\alpha}$. A direct calculation shows that its Blumenthal-Getoor index is exactly $\beta = \alpha$. Consequently, its paths have finite $p$-variation if and only if $p  \alpha$ [@problem_id:2984414].

#### Lévy Processes as Semimartingales

The Lévy-Itô decomposition provides a natural bridge to the general theory of stochastic calculus. A process is a **[semimartingale](@entry_id:188438)** if it can be decomposed into the sum of a [local martingale](@entry_id:203733) and a process of finite variation. Looking at the decomposition:
$$
X_t = \underbrace{\left(W_t^{\!Q} + \int_{0}^{t}\int_{\{\|x\| \le 1\}} x \tilde{N}(ds, dx)\right)}_{\text{Local Martingale}} + \underbrace{\left(b t + \int_{0}^{t}\int_{\{\|x\|  1\}} x N(ds, dx)\right)}_{\text{Finite Variation Process}}
$$
The Brownian part and the compensated small-jump integral are [local martingales](@entry_id:186755). The drift and the large-jump compound Poisson process are both of finite variation. Their sum is therefore a process of finite variation. This proves that **every Lévy process is a [semimartingale](@entry_id:188438)** [@problem_id:3002088].

A more refined result concerns the **[canonical decomposition](@entry_id:634116)** of a *special [semimartingale](@entry_id:188438)*, where the finite variation part is required to be predictable. The process of large jumps, $J_t = \int_0^t \int_{\{|x|1\}} x N(ds,dx)$, is not predictable. However, we can compensate it as well, provided its first moment exists. This is possible if and only if $\int_{|x|1} |x|\nu(dx)  \infty$. Under this condition, the process is a special [semimartingale](@entry_id:188438), and we can rearrange its components to obtain the [canonical decomposition](@entry_id:634116) $X_t = M_t + A_t$, where $M_t$ is the [local martingale](@entry_id:203733) part and $A_t$ is the predictable finite variation part [@problem_id:3002088]:
$$
M_t = W_t^{\!Q} + \int_{0}^{t}\int_{\mathbb{R}^d\setminus\{0\}} x \tilde{N}(ds, dx) \quad \text{and} \quad A_t = t \left(b + \int_{|x|1} x \nu(dx)\right)
$$

### Important Classes of Lévy Processes

#### Subordinators

A particularly important class of one-dimensional Lévy processes is that of **subordinators**. A subordinator is a Lévy process $X_t$ whose [sample paths](@entry_id:184367) are almost surely non-decreasing. Since $X_0=0$, this implies $X_t \ge 0$ for all $t$. Subordinators are often used to model a random notion of time.

The condition of non-decreasing paths imposes strong constraints on the Lévy triplet $(b, Q, \nu)$ [@problem_id:2984427]:
1.  **No Gaussian Part:** The oscillatory nature of Brownian motion is incompatible with monotonic paths, so we must have $Q=0$.
2.  **No Negative Jumps:** The process cannot jump downwards, so the Lévy measure $\nu$ must be supported on the positive half-line, $(0, \infty)$.
3.  **Non-negative Drift:** The underlying drift must be non-negative. For a subordinator, the process has paths of finite variation, so its representation simplifies. The effective drift coefficient must be non-negative.

For non-negative random variables, the Laplace transform is often more convenient than the characteristic function. For a subordinator $X_t$, we define the **Laplace exponent** $\Phi(\theta)$ for $\theta \ge 0$ by the relation $\mathbb{E}[e^{-\theta X_t}] = e^{-t\Phi(\theta)}$. By relating this to the [characteristic exponent](@entry_id:188977) ($\Phi(\theta) = -\Psi(i\theta)$), one can derive its canonical form, known as the Lévy-Khintchine formula for subordinators:
$$
\Phi(\theta) = a \theta + \int_{(0, \infty)} (1 - e^{-\theta x}) \nu(dx)
$$
Here, $a \ge 0$ is the drift coefficient, and the Lévy measure $\nu$ on $(0, \infty)$ must satisfy the [integrability condition](@entry_id:160334) $\int_{(0, \infty)} (x \wedge 1) \nu(dx)  \infty$.