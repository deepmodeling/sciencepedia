## Introduction
In the study of stochastic processes, we are frequently faced with the need to compare different, yet related, probabilistic models. For instance, how does a standard Brownian motion differ from one with an added drift, and how can we translate calculations from one model to the other? The key to formalizing this comparison lies in the theory of measure change, a powerful framework built upon the Radon-Nikodým derivative, which in this context is known as the [likelihood ratio](@entry_id:170863). This article provides a comprehensive guide to understanding and applying this essential concept in the world of stochastic differential equations.

This article is structured to build your understanding from the ground up. The first chapter, **Principles and Mechanisms**, delves into the measure-theoretic foundations of [absolute continuity](@entry_id:144513) and the Radon-Nikodým theorem, leading to the development of Girsanov's theorem for changing the law of a [stochastic process](@entry_id:159502). The second chapter, **Applications and Interdisciplinary Connections**, explores the profound impact of this theory, showcasing its role in solving concrete problems in statistics, [mathematical finance](@entry_id:187074), and signal processing. Finally, the **Hands-On Practices** section provides an opportunity to solidify your knowledge by working through key calculations for diffusion and [counting processes](@entry_id:260664). By the end, you will have a robust understanding of how to use likelihood ratios to navigate between different probabilistic worlds.

## Principles and Mechanisms

In the study of [stochastic differential equations](@entry_id:146618), we are often concerned not with a single model, but with a family of related models. A common scenario involves comparing a process under a simple, canonical measure (like the Wiener measure for standard Brownian motion) with the same process under a more [complex measure](@entry_id:187234), perhaps one that includes a drift. The mathematical toolkit for making these comparisons precise is founded upon the measure-theoretic concepts of [absolute continuity](@entry_id:144513) and the Radon-Nikodým derivative. This derivative, when used to relate two probability measures, is termed the **likelihood ratio**. It functions as a re-weighting factor, allowing us to translate expectations and probabilities from one probabilistic world to another. This chapter elucidates the core principles of this framework, from its measure-theoretic roots to its application in changing the law of [stochastic processes](@entry_id:141566) via Girsanov's theorem.

### The Radon-Nikodým Derivative as a Relative Density

The ability to relate one measure to another begins with the concept of **[absolute continuity](@entry_id:144513)**. Let $(\Omega, \mathcal{F})$ be a [measurable space](@entry_id:147379), and let $\mathbb{P}$ and $\mathbb{Q}$ be two probability measures defined on it. We say that $\mathbb{Q}$ is **absolutely continuous** with respect to $\mathbb{P}$, denoted $\mathbb{Q} \ll \mathbb{P}$, if every event that is impossible under $\mathbb{P}$ is also impossible under $\mathbb{Q}$. Formally, for any event $A \in \mathcal{F}$, if $\mathbb{P}(A) = 0$, then $\mathbb{Q}(A) = 0$. In essence, the measure $\mathbb{Q}$ does not assign positive probability to any event that $\mathbb{P}$ considers a [null set](@entry_id:145219) [@problem_id:3071897].

If the relationship is symmetric—that is, if both $\mathbb{Q} \ll \mathbb{P}$ and $\mathbb{P} \ll \mathbb{Q}$ hold—we say the measures are **mutually absolutely continuous** or **equivalent**, denoted $\mathbb{Q} \sim \mathbb{P}$. This is equivalent to stating that $\mathbb{P}$ and $\mathbb{Q}$ have the exact same collection of [null sets](@entry_id:203073).

The significance of [absolute continuity](@entry_id:144513) is captured by the **Radon-Nikodým theorem**. The theorem states that if $\mathbb{Q} \ll \mathbb{P}$, there exists a non-negative, $\mathcal{F}$-measurable random variable, which we will denote $L$, such that for any event $A \in \mathcal{F}$, the probability of $A$ under $\mathbb{Q}$ can be calculated by integrating $L$ over the set $A$ with respect to the measure $\mathbb{P}$:
$$
\mathbb{Q}(A) = \int_A L(\omega) \, d\mathbb{P}(\omega)
$$
This random variable $L$ is called the **Radon-Nikodým derivative** of $\mathbb{Q}$ with respect to $\mathbb{P}$ and is denoted $L = \frac{d\mathbb{Q}}{d\mathbb{P}}$. It is unique up to a $\mathbb{P}$-[null set](@entry_id:145219).

For $L$ to successfully define a new *probability* measure $\mathbb{Q}$, it must satisfy two fundamental properties that stem directly from the [axioms of probability](@entry_id:173939) [@problem_id:3071911]. First, since the probability of any event must be non-negative, we must have $\mathbb{Q}(A) \ge 0$ for all $A \in \mathcal{F}$. This necessitates that the density $L$ be non-negative, $L \ge 0$, [almost surely](@entry_id:262518) with respect to $\mathbb{P}$. If $L$ were negative on some set of positive $\mathbb{P}$-measure, we could compute the $\mathbb{Q}$-measure of that very set and obtain a negative "probability," a contradiction. Second, the total probability of the entire sample space $\Omega$ must be one. Applying the Radon-Nikodým formula to the event $A=\Omega$:
$$
1 = \mathbb{Q}(\Omega) = \int_\Omega L(\omega) \, d\mathbb{P}(\omega) = \mathbb{E}_{\mathbb{P}}[L]
$$
Thus, the Radon-Nikodým derivative must have an expectation of exactly one under the original measure $\mathbb{P}$.

The derivative $L$ is often called a **[likelihood ratio](@entry_id:170863)** because it provides a point-wise comparison of the "plausibility" of outcomes under the two measures. The defining relation $\mathbb{Q}(A) = \mathbb{E}_{\mathbb{P}}[L \mathbf{1}_A]$ can be rearranged for an event $A$ with $\mathbb{P}(A) > 0$ to give:
$$
\frac{\mathbb{Q}(A)}{\mathbb{P}(A)} = \frac{\mathbb{E}_{\mathbb{P}}[L \mathbf{1}_A]}{\mathbb{P}(A)} = \mathbb{E}_{\mathbb{P}}[L | A]
$$
This shows that the ratio of probabilities for an event is the average value of the likelihood ratio $L$ over that event. Heuristically, for a small region around an outcome $\omega$, the value $L(\omega)$ represents the factor by which the local probability density is scaled when moving from $\mathbb{P}$ to $\mathbb{Q}$. Outcomes $\omega$ for which $L(\omega) > 1$ are more likely under $\mathbb{Q}$ than under $\mathbb{P}$, while outcomes for which $L(\omega)  1$ are less likely [@problem_id:3071903].

It is important to recognize that [absolute continuity](@entry_id:144513) is not always symmetric. Consider the Wiener space $\Omega = C([0,T], \mathbb{R})$ with the Wiener measure $\mathbb{P}$. Let $A$ be the event that a path's maximum value exceeds 1, i.e., $A = \{\omega \in \Omega : \sup_{t \in [0,T]} \omega(t) \ge 1\}$. This event has a probability strictly between 0 and 1. We can define a new probability measure $\mathbb{Q}$ by conditioning on this event: $\mathbb{Q}(B) = \frac{\mathbb{P}(B \cap A)}{\mathbb{P}(A)}$. By this construction, if $\mathbb{P}(B)=0$, then $\mathbb{P}(B \cap A)=0$, so $\mathbb{Q}(B)=0$. Thus, $\mathbb{Q} \ll \mathbb{P}$. The Radon-Nikodým derivative is simply $L = \frac{\mathbf{1}_A}{\mathbb{P}(A)}$. However, the reverse does not hold. Consider the [complementary event](@entry_id:275984) $A^c$. Under the new measure, $\mathbb{Q}(A^c) = \frac{\mathbb{P}(A^c \cap A)}{\mathbb{P}(A)} = 0$. But under the original measure, $\mathbb{P}(A^c) = 1 - \mathbb{P}(A)  0$. We have found a set that is null under $\mathbb{Q}$ but not under $\mathbb{P}$, proving that $\mathbb{P} \not\ll \mathbb{Q}$ [@problem_id:3071897].

### The Likelihood Ratio Process and its Martingale Property

In the context of [stochastic processes](@entry_id:141566), which evolve over time, we are interested in how measures relate on the filtration $(\mathcal{F}_t)_{t \ge 0}$. We can define a **likelihood ratio process** (or density process) $(L_t)_{t \ge 0}$ by setting $L_t = \frac{d\mathbb{Q}}{d\mathbb{P}}|_{\mathcal{F}_t}$, where the derivative is taken with respect to the measures restricted to the [sigma-algebra](@entry_id:137915) $\mathcal{F}_t$.

A crucial property of this process is that, under natural [consistency conditions](@entry_id:637057), it forms a [martingale](@entry_id:146036). Assume the family of measures $(\mathbb{Q}_t)$ is consistent, meaning that for any $s \le t$, the restriction of $\mathbb{Q}_t$ to the smaller sigma-algebra $\mathcal{F}_s$ is just $\mathbb{Q}_s$. This is a natural requirement, stating that the probabilities of past events do not change as we reveal more information. This consistency directly implies that the density process $(L_t)$ is a martingale with respect to the filtration $(\mathcal{F}_t)$ and the measure $\mathbb{P}$.

To prove this, we must show that $L_s = \mathbb{E}_{\mathbb{P}}[L_t | \mathcal{F}_s]$ for $s \le t$. By the definition of [conditional expectation](@entry_id:159140), this is equivalent to showing that for any event $A \in \mathcal{F}_s$, the equality $\mathbb{E}_{\mathbb{P}}[L_s \mathbf{1}_A] = \mathbb{E}_{\mathbb{P}}[L_t \mathbf{1}_A]$ holds. Using the definition of the Radon-Nikodým derivatives $L_s$ and $L_t$, and the consistency of the $\mathbb{Q}$ measures, we have:
$$
\mathbb{E}_{\mathbb{P}}[L_s \mathbf{1}_A] = \mathbb{Q}_s(A) \quad \text{and} \quad \mathbb{E}_{\mathbb{P}}[L_t \mathbf{1}_A] = \mathbb{Q}_t(A)
$$
Since $A \in \mathcal{F}_s$ and the measures are consistent, $\mathbb{Q}_s(A) = \mathbb{Q}_t(A)$. This establishes the required equality of integrals, proving the [martingale property](@entry_id:261270) of $(L_t)$ [@problem_id:3071883].

To build intuition for the Radon-Nikodým derivative in this infinite-dimensional setting, it is instructive to consider its finite-dimensional analogue: the Jacobian factor in the change of variables formula for integrals [@problem_id:3071917]. If we have a transformation $y=T(x)$ and a measure defined by the Lebesgue measure $\lambda$ in the $x$-space, the [pushforward measure](@entry_id:201640) $\nu$ in the $y$-space is related to $\lambda$ by a density. The density of $\nu$ with respect to $\lambda$ at a point $y$ is given by $\frac{d\nu}{d\lambda}(y) = \frac{1}{|T'(T^{-1}(y))|}$, the reciprocal of the Jacobian of the transformation. This factor locally scales the measure to account for how the transformation stretches or compresses space. The likelihood ratio process $(L_t)$ plays exactly this role for paths of [stochastic processes](@entry_id:141566), providing the random, path-dependent "Jacobian" for the transformation between measures.

### Girsanov's Theorem and the Change of Drift

The premier application of this framework in the study of SDEs is **Girsanov's theorem**, which provides an explicit formula for the [likelihood ratio](@entry_id:170863) process that corresponds to adding a drift to a standard Brownian motion.

Let $W_t$ be a standard Brownian motion under a measure $\mathbb{P}$. Suppose we wish to find a new measure $\mathbb{Q}$ under which the process $X_t = W_t - \int_0^t \theta_s ds$ is a standard Brownian motion, for some suitable [adapted process](@entry_id:196563) $\theta_t$. This is equivalent to finding a measure $\mathbb{Q}$ under which $W_t$ behaves like a process with drift $\theta_t$.

The key to constructing the required likelihood ratio process $L_t = \frac{d\mathbb{Q}}{d\mathbb{P}}|_{\mathcal{F}_t}$ is the **Doléans-Dade exponential** (also known as the [stochastic exponential](@entry_id:197698)). For a [continuous local martingale](@entry_id:188921) $M_t$, its [stochastic exponential](@entry_id:197698) $\mathcal{E}(M)_t$ is the unique solution to the SDE:
$$
dZ_t = Z_t dM_t, \quad Z_0 = 1
$$
By applying Itô's formula, one can show that the explicit solution is given by:
$$
\mathcal{E}(M)_t = \exp\left(M_t - \frac{1}{2}\langle M \rangle_t\right)
$$
where $\langle M \rangle_t$ is the [quadratic variation](@entry_id:140680) of $M_t$ [@problem_id:3071922]. The structure of this SDE reveals a critical property: since the solution $Z_t$ is given by a [stochastic integral](@entry_id:195087) $Z_t = 1 + \int_0^t Z_s dM_s$, and the integral of a [predictable process](@entry_id:274260) against a [local martingale](@entry_id:203733) is a [local martingale](@entry_id:203733), $\mathcal{E}(M)_t$ is always a **[local martingale](@entry_id:203733)**.

Girsanov's theorem states that the specific [change of measure](@entry_id:157887) we seek is achieved by defining the [likelihood ratio](@entry_id:170863) process as the [stochastic exponential](@entry_id:197698) of the [martingale](@entry_id:146036) part of the drift. Let $M_t = \int_0^t \theta_s dW_s$. Then we define:
$$
L_t = \mathcal{E}(M)_t = \exp\left(\int_0^t \theta_s dW_s - \frac{1}{2} \int_0^t \theta_s^2 ds\right)
$$
The theorem asserts that if we define a new measure $\mathbb{Q}$ on $\mathcal{F}_T$ via the Radon-Nikodým derivative $\frac{d\mathbb{Q}}{d\mathbb{P}}|_{\mathcal{F}_T} = L_T$, then the process $W_t^\theta = W_t - \int_0^t \theta_s ds$ is a standard Brownian motion under $\mathbb{Q}$ on the interval $[0,T]$ [@problem_id:3071919].

### A Technical Interlude: When is a Local Martingale a True Martingale?

There is a crucial subtlety in the application of Girsanov's theorem. As we established, for $L_T$ to define a valid probability measure, we must have $\mathbb{E}_{\mathbb{P}}[L_T] = 1$. However, the Doléans-Dade exponential $\mathcal{E}(M)_T$ is only guaranteed to be a [local martingale](@entry_id:203733). A non-negative [local martingale](@entry_id:203733) is always a [supermartingale](@entry_id:271504), which means $\mathbb{E}_{\mathbb{P}}[\mathcal{E}(M)_T] \le \mathcal{E}(M)_0 = 1$. If this inequality is strict, then $\mathbb{Q}(\Omega) = \mathbb{E}_{\mathbb{P}}[L_T]  1$, and $\mathbb{Q}$ is not a probability measure, but a sub-probability measure. The [change of measure](@entry_id:157887) fails. A [local martingale](@entry_id:203733) that is not a true [martingale](@entry_id:146036) is called a **[strict local martingale](@entry_id:636161)**.

A widely used sufficient condition to ensure that the [local martingale](@entry_id:203733) $\mathcal{E}(M)_t$ is a true (and [uniformly integrable](@entry_id:202893)) [martingale](@entry_id:146036) on $[0,T]$ is **Novikov's condition**. For the martingale $M_t = \int_0^t \theta_s dW_s$, whose quadratic variation is $\langle M \rangle_t = \int_0^t \theta_s^2 ds$, Novikov's condition is:
$$
\mathbb{E}_{\mathbb{P}}\left[\exp\left(\frac{1}{2}\int_0^T \theta_s^2 ds\right)\right]  \infty
$$
If this condition holds, the [change of measure](@entry_id:157887) is valid [@problem_id:3071914].

A classic example where this condition fails and the measure change breaks down involves the 3-dimensional Bessel process, $R_t$, which solves $dR_t = dW_t + \frac{1}{R_t} dt$ and almost surely never hits zero. Let's attempt to define a measure $\mathbb{Q}$ under which $R_t$ becomes a standard Brownian motion. This would require removing the drift term $\frac{1}{R_t} dt$. Following Girsanov's theorem, we would choose $\theta_t = -1/R_t$. The [likelihood ratio](@entry_id:170863) would be $L_t = \mathcal{E}(-\int_0^\cdot \frac{1}{R_s} dW_s)_t$. If this were a valid [change of measure](@entry_id:157887), $R_t$ would be a $\mathbb{Q}$-Brownian motion. However, a standard Brownian motion starting at $R_0 > 0$ hits the origin with probability 1, whereas the 3D Bessel process does not. This is a contradiction. The only way to resolve it is to conclude that the proposed [change of measure](@entry_id:157887) was invalid. The process $L_t$ must be a [strict local martingale](@entry_id:636161) with $\mathbb{E}_{\mathbb{P}}[L_T]  1$. Novikov's condition fails in this case because the process $R_t$ can get arbitrarily close to zero, causing the integral $\int_0^T \frac{1}{R_s^2} ds$ to become large with enough probability to make the expectation infinite [@problem_id:3071890].

This example highlights that while the local [martingale property](@entry_id:261270) of the [stochastic exponential](@entry_id:197698) is automatic, its status as a true [martingale](@entry_id:146036) is not, and this distinction is precisely what determines the validity of a Girsanov-style measure change. This issue can often be managed through a **localization** procedure. For the Bessel process example, if we stop the process at $\tau_n = \inf\{t : R_t \le 1/n\}$, the drift term's magnitude is bounded on the stopped interval. On this localized interval, Novikov's condition holds, the stopped density process is a true [martingale](@entry_id:146036), and a valid [change of measure](@entry_id:157887) can be performed on the stopped sigma-algebra $\mathcal{F}_{T \wedge \tau_n}$ [@problem_id:3071890].

### Beyond Brownian Motion: Changing the Intensity of Jump Processes

The principles of changing measure via a [likelihood ratio](@entry_id:170863) built from a [stochastic exponential](@entry_id:197698) are not limited to continuous processes. They form a general framework applicable to any [semimartingale](@entry_id:188438). A prominent example is the change of intensity for a counting process.

Let $N_t$ be a simple counting process with a predictable intensity $\lambda_t > 0$ under measure $\mathbb{P}$. The corresponding compensated [martingale](@entry_id:146036) is $M_t = N_t - \int_0^t \lambda_s ds$. Suppose we wish to find a measure $\mathbb{Q}$ under which $N_t$ has a new predictable intensity $\tilde{\lambda}_t > 0$.

Analogous to the continuous case, Girsanov's theorem for [jump processes](@entry_id:180953) states that the [likelihood ratio](@entry_id:170863) process is given by the Doléans-Dade exponential $Z_t = \mathcal{E}(L)_t$, where the generating martingale $L_t$ is constructed to cancel the old drift and add the new one. The correct form is:
$$
L_t = \int_0^t \left(\frac{\tilde{\lambda}_s}{\lambda_s} - 1\right) dM_s
$$
The explicit solution for the Doléans-Dade exponential of a purely discontinuous martingale is different from the continuous case. Instead of the quadratic variation correction term, it involves a product over the jumps. This leads to the following explicit formula for the likelihood ratio [@problem_id:3071913]:
$$
Z_t = \exp\left(\int_0^t \log\left(\frac{\tilde{\lambda}_s}{\lambda_s}\right) dN_s - \int_0^t (\tilde{\lambda}_s - \lambda_s) ds\right)
$$
The first term in the exponent is a sum of log-ratios of intensities evaluated at the jump times of $N_t$, and the second term is a compensator that ensures $Z_t$ is a $\mathbb{P}$-[martingale](@entry_id:146036) (under suitable [boundedness](@entry_id:746948) conditions on the intensities). This powerful result demonstrates the unifying nature of [martingale theory](@entry_id:266805) in constructing likelihood ratios for transforming the laws of diverse stochastic processes.