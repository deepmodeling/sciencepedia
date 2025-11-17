## Introduction
Lévy processes provide a powerful framework for modeling phenomena that evolve randomly over time, accommodating both continuous, diffusive behavior and sudden, discontinuous jumps. While Brownian motion captures purely continuous fluctuations, many real-world systems—from stock prices and insurance claims to particle physics—exhibit abrupt shocks that defy a continuous description. This raises a fundamental question: is there a universal structure underlying all such processes with stationary and [independent increments](@entry_id:262163)?

This article addresses this question by exploring the **Lévy-Itô decomposition**, a cornerstone theorem of modern probability theory. It reveals that any Lévy process, no matter how complex, can be constructed from just three elementary and independent building blocks: a deterministic drift, a continuous Brownian motion, and a pure [jump process](@entry_id:201473). This decomposition provides the definitive "genetic blueprint" for these processes, making them analytically and computationally tractable.

Across the following chapters, you will gain a comprehensive understanding of this powerful result. The first chapter, **Principles and Mechanisms**, will formally state the decomposition theorem, explore the roles of the Lévy measure and the [characteristic triplet](@entry_id:635937), and analyze the properties of each component. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the decomposition's utility in analyzing process characteristics, extending [stochastic calculus](@entry_id:143864), and building models across finance, insurance, and physics. Finally, **Hands-On Practices** will offer guided problems to solidify your understanding. Our exploration begins with the fundamental principles and mechanisms that form the bedrock of the decomposition.

## Principles and Mechanisms

Having established the foundational properties of Lévy processes in the preceding chapter, we now turn to their structural core. A central question in the theory of stochastic processes is the pathwise characterization of its members. While the continuity of Brownian paths offers a certain simplicity, many phenomena modeled by processes with stationary and [independent increments](@entry_id:262163) exhibit discontinuous, jump-like behavior. The fundamental insight, and the main subject of this chapter, is that every Lévy process, no matter how complex its behavior, can be deconstructed into a [universal set](@entry_id:264200) of elementary and mutually independent components. This [canonical representation](@entry_id:146693) is known as the **Lévy-Itô decomposition**. It provides an explicit pathwise construction of any Lévy process from three fundamental building blocks: a deterministic drift, a continuous Gaussian [martingale](@entry_id:146036) (a Brownian motion), and a pure-[jump process](@entry_id:201473).

### The Anatomy of Jumps: The Lévy Measure

The defining feature of a general Lévy process, distinguishing it from Brownian motion, is the presence of jumps. To construct a path, we must first have a complete description of these jumps. This is the role of the **Lévy measure**.

Let $X = (X_t)_{t \ge 0}$ be a Lévy process in $\mathbb{R}^d$. The jump of the process at time $s$ is denoted by $\Delta X_s = X_s - X_{s-}$. The jumps of a Lévy process can be described by a **Poisson random measure (PRM)**, denoted $N$, on the space $\mathbb{R}_+ \times (\mathbb{R}^d \setminus \{0\})$. For any time $t > 0$ and any Borel set $A \subset \mathbb{R}^d \setminus \{0\}$, the random variable $N(t, A)$ counts the number of jumps occurring up to time $t$ whose size falls into the set $A$:
$$ N(t, A) = \sum_{0  s \le t} \mathbf{1}_{\{\Delta X_s \in A\}} $$
A fundamental property of Lévy processes is that the intensity of this random measure is deterministic and time-homogeneous. It takes the form $dt \otimes \nu(dx)$, where $\nu$ is a measure on $\mathbb{R}^d \setminus \{0\}$ known as the **Lévy measure**. The expected number of jumps with sizes in $A$ up to time $t$ is therefore given by:
$$ \mathbb{E}[N(t, A)] = t \nu(A) $$
The Lévy measure $\nu$ thus governs the frequency and size distribution of the jumps. It is not an arbitrary measure; for a measure $\nu$ to be a valid Lévy measure, it must satisfy the following crucial [integrability condition](@entry_id:160334):
$$ \int_{\mathbb{R}^d \setminus \{0\}} (|x|^2 \wedge 1) \nu(dx)  \infty $$
This single condition has profound implications for the structure of the [jump process](@entry_id:201473). We can analyze its meaning by splitting the domain of integration into "large" and "small" jumps, separated by a sphere of radius $1$.

*   For **large jumps** (i.e., $|x| > 1$), the condition implies $\int_{|x|>1} 1 \cdot \nu(dx) = \nu(\{x: |x|>1\})  \infty$. This means the total rate of jumps with a magnitude greater than one is finite. Consequently, on any finite time interval, a Lévy process can only have a finite number of such large jumps. [@problem_id:3002100]

*   For **small jumps** (i.e., $|x| \le 1$), the condition implies $\int_{|x|\le 1} |x|^2 \nu(dx)  \infty$. This ensures that the variance of the small jumps is finite. However, it places no restriction on the total rate of small jumps, $\nu(\{x: |x|\le 1\})$, which can be infinite.

A process is said to have **finite jump activity** if the total number of jumps on any compact time interval is almost surely finite. This occurs if and only if the total mass of the Lévy measure is finite, i.e., $\nu(\mathbb{R}^d \setminus \{0\})  \infty$. A classic example is the **compound Poisson process**, whose Lévy measure $\nu(dx) = \lambda \mu(dx)$, where $\lambda$ is the jump rate and $\mu$ is a probability measure for the jump sizes, has total mass $\lambda$. Conversely, a process has **infinite jump activity** if $\nu(\mathbb{R}^d \setminus \{0\}) = \infty$. This is characteristic of processes like the **[gamma process](@entry_id:637312)** or **[stable processes](@entry_id:269810)**, where an infinite number of small jumps occur in any finite time interval. [@problem_id:3002100]

It is a standard convention to define the Lévy measure on $\mathbb{R}^d \setminus \{0\}$, which implicitly requires $\nu(\{0\}) = 0$. This is not a consequence of the [integrability condition](@entry_id:160334), but rather a canonical choice to ensure a unique correspondence between a Lévy process and its [characteristic triplet](@entry_id:635937). If one were to allow $\nu(\{0\}) > 0$, it would correspond to jumps of size zero, which are unobservable and do not affect the process path. Including them would lead to a non-unique representation, as different measures differing only by their mass at the origin would describe the same process. Setting $\nu(\{0\}) = 0$ eliminates this redundancy. [@problem_id:2984424]

### The Decomposition Theorem

The Lévy-Itô decomposition theorem provides the definitive pathwise construction of a Lévy process from its constituent parts. It states that any Lévy process $X_t$ with [characteristic triplet](@entry_id:635937) $(b, Q, \nu)$ can be represented as the sum of three independent components: a drift, a Brownian motion, and a [jump process](@entry_id:201473). The [exact form](@entry_id:273346) of the decomposition depends on a choice of **truncation function** $h(x)$, which is a bounded function that equals $x$ in a neighborhood of the origin. For clarity, we will adopt the most common choice, $h(x) = x \mathbf{1}_{\{|x| \le 1\}}$.

**Theorem (Lévy-Itô Decomposition):** Let $X_t$ be a Lévy process in $\mathbb{R}^d$ with [characteristic triplet](@entry_id:635937) $(b, Q, \nu)$ relative to the truncation $h(x) = x \mathbf{1}_{\{|x| \le 1\}}$. Then $X_t$ has the representation:
$$ X_t = b t + W_t^Q + \int_0^t \int_{|x|>1} x N(ds, dx) + \int_0^t \int_{|x|\le 1} x \tilde{N}(ds, dx) $$
The terms in this decomposition are:
1.  A deterministic linear drift, $b t$.
2.  A $d$-dimensional Brownian motion $W_t^Q$ with covariance matrix $Q$, i.e., $\text{Cov}(W_t^Q) = tQ$.
3.  A compound Poisson process of large jumps.
4.  A square-integrable pure-jump [martingale](@entry_id:146036) of compensated small jumps, where $\tilde{N}(ds, dx) = N(ds, dx) - \nu(dx)ds$ is the **compensated Poisson random measure**.

The drift, the Brownian motion, and the Poisson random measure $N$ (which generates both jump components) are mutually independent.

Let us examine each component in detail [@problem_id:3002093].

*   **Drift ($b t$):** This is the deterministic, continuous, and predictable component of the process. The vector $b \in \mathbb{R}^d$ is the drift parameter from the [characteristic triplet](@entry_id:635937).

*   **Gaussian Part ($W_t^Q$):** This process is the [continuous martingale](@entry_id:185466) component of $X_t$. The fact that it must be a Brownian motion follows from the requirement of stationary and [independent increments](@entry_id:262163). The symmetric, non-[negative definite](@entry_id:154306) matrix $Q$ is the covariance matrix of this Brownian motion. If $Q=0$, the process has no continuous Gaussian part.

*   **Large Jumps ($\int_0^t \int_{|x|>1} x N(ds, dx)$):** As we established, the rate of jumps with magnitude $|x|>1$ is finite. This integral therefore represents the sum of a finite number of jumps on any compact time interval, which defines a **compound Poisson process**. This process is of finite variation.

*   **Small Jumps ($\int_0^t \int_{|x|\le 1} x \tilde{N}(ds, dx)$):** This is the most intricate component. The Lévy measure may have infinite mass on the set $\{x: |x|\le 1\}$, implying an infinite number of small jumps. The simple sum of these jumps, $\int \int_{|x|\le 1} x N(ds, dx)$, may not converge. The solution is **compensation**: we subtract the expected value of the [jump process](@entry_id:201473) to center it. The resulting process, an integral with respect to the compensated measure $\tilde{N}$, is a well-defined zero-mean, square-integrable martingale. The condition $\int_{|x|\le 1} |x|^2 \nu(dx)  \infty$ is precisely what guarantees that this [compensated integral](@entry_id:181695) is square-integrable.

The construction of the stochastic integrals with respect to $W_t^Q$ and $\tilde{N}$ is a cornerstone of stochastic calculus. These are not standard Riemann-Stieltjes integrals, as the integrator paths are of infinite variation. They are defined through an $L^2$ theory, starting with simple, predictable integrands and then extending to a wider class of [predictable processes](@entry_id:262945) via an isometry. For a [predictable process](@entry_id:274260) $H_s$, the integrals are square-integrable [martingales](@entry_id:267779) provided $\mathbb{E}\int_0^t |H_s|^2 ds  \infty$ for the Brownian integral and $\mathbb{E}\int_0^t\int_E |h(s,x)|^2 \nu(dx)ds  \infty$ for the compensated Poisson integral. [@problem_id:3002079]

### Properties of the Decomposition

The power of the Lévy-Itô decomposition lies not only in its existence but also in its structural properties, which we now explore.

#### Uniqueness and the Role of the Truncation Function

For a fixed process $X_t$ and a fixed truncation function $h$, the decomposition is unique. This means the [characteristic triplet](@entry_id:635937) $(b, Q, \nu)$ is uniquely determined, and the four component processes are unique up to indistinguishability. This uniqueness is a consequence of the uniqueness of the [canonical decomposition](@entry_id:634116) of a [semimartingale](@entry_id:188438). [@problem_id:3002108]

The covariance matrix $Q$ (describing the continuous part) and the Lévy measure $\nu$ (describing all jumps) are intrinsic properties of the process $X_t$ itself and do not depend on the choice of the truncation function $h$. However, the drift parameter $b$ does depend on $h$. If we change the truncation function from $h$ to another valid choice $h'$, the drift $b$ must be adjusted to account for the different way jumps are being separated and compensated. The new drift $b'$ is given by:
$$ b' = b + \int_{\mathbb{R}^d} (h'(x) - h(x)) \nu(dx) $$
This adjustment ensures that the sum of all components remains unchanged. The change in drift precisely cancels the change in the compensator of the jump part. [@problem_id:3002108]

#### Path Variation and the Blumenthal-Getoor Index

The Lévy measure encodes not only the frequency of jumps but also subtle geometric properties of the [sample paths](@entry_id:184367). A key property is the **path variation**. A process has finite variation on compacts if the total distance traveled by its path is finite. The Brownian component $\sigma W_t$ always has infinite variation if $\sigma \neq 0$. The large-jump component, being a compound Poisson process, always has finite variation.

The variation of the small-jump martingale, $M_t = \int_0^t\int_{|x|\le 1} x \tilde{N}(ds,dx)$, depends critically on the behavior of $\nu$ near the origin. The process $M_t$ has paths of **finite variation** on compact intervals if and only if the first absolute moment of small jumps is integrable:
$$ \int_{|x|\le 1} |x| \nu(dx)  \infty $$
If this integral diverges, the paths of $M_t$ have **infinite variation**. [@problem_id:3002083]

This condition can be made more concrete for an important class of Lévy processes, including stable and stable-like processes, whose Lévy measures behave near the origin like $\nu(dx) \asymp |x|^{-1-\beta} dx$ for some $\beta \in (0,2)$. The parameter $\beta$ is known as the **Blumenthal-Getoor index**, which quantifies the intensity of small jumps. For such processes, the finite variation condition $\int_{|x|\le 1} |x| \nu(dx)  \infty$ is equivalent to $\int_0^1 x \cdot x^{-1-\beta} dx = \int_0^1 x^{-\beta} dx  \infty$, which holds if and only if $\beta  1$. Thus, for this class, the small-jump component has finite variation if its Blumenthal-Getoor index is less than 1, and infinite variation if the index is between 1 and 2. [@problem_id:3002083]

### Analytical Consequences: Generator and Characteristic Function

The pathwise decomposition has profound consequences for the analytical tools used to study Lévy processes. The characteristic function and the [infinitesimal generator](@entry_id:270424) of the process can be directly derived from its four independent components.

#### The Lévy-Khintchine Formula

The characteristic [function of a random variable](@entry_id:269391) is the Fourier transform of its probability distribution. For a Lévy process $X_t$, due to the stationary and [independent increments](@entry_id:262163) property, its [characteristic function](@entry_id:141714) takes the exponential form $\mathbb{E}[\exp(i\langle u, X_t \rangle)] = \exp(t \psi(u))$, where $\psi(u)$ is the [characteristic exponent](@entry_id:188977).

Because the three core components in the Lévy-Itô decomposition are independent, the [characteristic function](@entry_id:141714) of $X_t$ is the product of the characteristic functions of its parts. By calculating the [characteristic function](@entry_id:141714) for each component (drift, Brownian, and the total [jump process](@entry_id:201473)) and summing their exponents, we arrive directly at the celebrated **Lévy-Khintchine formula**. [@problem_id:3002103] With the convention $\mathbb{E}[e^{i\langle u, X_t\rangle}] = \exp(t\psi(u))$, the [characteristic exponent](@entry_id:188977) is:
$$ \psi(u) = i\langle u, b \rangle - \frac{1}{2}\langle u, Qu \rangle + \int_{\mathbb{R}^d} \left( e^{i\langle u, x\rangle} - 1 - i\langle u, x\rangle\mathbf{1}_{|x|\le 1} \right) \nu(dx) $$
Each term in the formula corresponds directly to a component in the pathwise decomposition: the imaginary linear term to the drift $b$, the negative quadratic term to the Brownian motion with covariance $Q$, and the integral term to the jumps, with the compensation for small jumps explicitly visible. [@problem_id:3002104]

#### The Infinitesimal Generator

The [infinitesimal generator](@entry_id:270424) $\mathcal{L}$ of a Markov process describes the expected rate of change of functions of the process. For a function $f \in C_b^2(\mathbb{R}^d)$ (twice continuously differentiable with bounded derivatives), it is defined as:
$$ \mathcal{L} f(x) = \lim_{t \downarrow 0} \frac{\mathbb{E}[f(x+X_t)] - f(x)}{t} $$
Just as with the [characteristic function](@entry_id:141714), the generator of the Lévy process is the sum of the generators of its independent components. Summing the generators for the drift (a first-order derivative), the Brownian motion (a second-order differential operator), and the jump parts ([integral operators](@entry_id:187690)) yields the general form of the generator for a Lévy process:
$$ \mathcal{L}f(x) = \langle b, \nabla f(x) \rangle + \frac{1}{2} \text{Tr}(Q \nabla^2 f(x)) + \int_{\mathbb{R}^d} \left( f(x+y) - f(x) - \langle \nabla f(x), y \rangle \mathbf{1}_{|y|\le 1} \right) \nu(dy) $$
This integro-differential operator transparently displays the influence of the [characteristic triplet](@entry_id:635937) $(b, Q, \nu)$ on the dynamics of the process. [@problem_id:3002085]

### Lévy Processes as Semimartingales

The Lévy-Itô decomposition also provides the key to situating Lévy processes within the broader universe of **[semimartingales](@entry_id:184490)**, which are the most general class of processes for which a robust theory of [stochastic integration](@entry_id:198356) can be built. A process is a [semimartingale](@entry_id:188438) if it can be decomposed into the sum of a [local martingale](@entry_id:203733) and a process of finite variation.

The Lévy-Itô representation $X_t = b t + W_t^Q + M_t + J_t$ is already close to this form. The Brownian part $W_t^Q$ and the compensated small-jump part $M_t$ are [local martingales](@entry_id:186755). The drift $bt$ and the large-jump part $J_t$ (a compound Poisson process) are of finite variation. Their sum is therefore a process of finite variation. Thus, every Lévy process can be written as the sum of a [local martingale](@entry_id:203733) and a [finite variation process](@entry_id:635841), which proves that **every Lévy process is a [semimartingale](@entry_id:188438)**. [@problem_id:3002088]

A more refined result concerns the **[canonical decomposition](@entry_id:634116)** of a special [semimartingale](@entry_id:188438), which is a unique decomposition into a [local martingale](@entry_id:203733) and a *predictable* [finite variation process](@entry_id:635841). A Lévy process admits such a decomposition, i.e., is a **special [semimartingale](@entry_id:188438)**, if and only if the expected value of its large jumps is finite. This corresponds to the condition:
$$ \int_{|x|>1} |x| \nu(dx)  \infty $$
When this condition holds, the large jumps can also be compensated, moving their random part into the martingale component and leaving a predictable drift in the finite variation component. The [canonical decomposition](@entry_id:634116) then becomes $X_t = M_t^* + A_t$, where the [local martingale](@entry_id:203733) part is $M_t^* = W_t^Q + \int_0^t\int_{\mathbb{R}^d} x \tilde{N}(ds,dx)$ and the predictable, finite-variation part is $A_t = \left(b + \int_{|x|>1} x \nu(dx)\right)t$. [@problem_id:3002088]

In summary, the Lévy-Itô decomposition provides a complete and explicit "genetic blueprint" for any Lévy process, revealing its universal structure as a combination of drift, diffusion, and jumps. This decomposition is the gateway to understanding the process's path properties, its analytical description, and its place within the general theory of [stochastic integration](@entry_id:198356).