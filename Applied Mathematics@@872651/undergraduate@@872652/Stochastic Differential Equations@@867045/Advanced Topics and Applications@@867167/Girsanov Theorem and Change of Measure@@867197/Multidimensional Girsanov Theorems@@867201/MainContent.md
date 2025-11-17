## Introduction
The Multidimensional Girsanov Theorem is one of the most powerful and elegant results in modern [stochastic calculus](@entry_id:143864). It provides a rigorous mathematical framework for changing the probability measure—or, more intuitively, the "world"—under which a [stochastic process](@entry_id:159502) evolves. This transformation's primary effect is to alter the process's drift, or average tendency, while leaving its fundamental random character, or diffusion, intact. Its significance lies in its ability to transform complex problems into simpler, more tractable forms, making it an indispensable tool for quantitative analysis.

This article addresses the fundamental question of how one can formally and controllably alter the dynamics of a [stochastic differential equation](@entry_id:140379) (SDE). By mastering this technique, we can simplify valuation problems in finance, decouple signals from noise in engineering, and gain deeper insight into the structure of [stochastic systems](@entry_id:187663).

The following chapters will guide you through this theory and its applications. In "Principles and Mechanisms," we will build the theorem from the ground up, starting with the Radon-Nikodym theorem from [measure theory](@entry_id:139744) and progressing through the concepts of density processes, [martingale representation](@entry_id:182858), and the [stochastic exponential](@entry_id:197698). Next, "Applications and Interdisciplinary Connections" will demonstrate the theorem's immense practical utility in the fields of mathematical finance for [risk-neutral pricing](@entry_id:144172) and in [nonlinear filtering](@entry_id:201008) for signal estimation. Finally, "Hands-On Practices" will provide a set of guided problems to solidify your understanding and develop your ability to apply the theorem to concrete scenarios.

## Principles and Mechanisms

The Girsanov theorem provides a powerful and elegant framework for changing the probability measure under which a stochastic process is observed. This [change of measure](@entry_id:157887), or "change of world," fundamentally alters the statistical properties of the process, most notably its drift, while preserving its diffusion characteristics. In this chapter, we will construct the Girsanov theorem from first principles, examining the necessary components, the underlying mechanisms, and the profound consequences for the analysis of [stochastic differential equations](@entry_id:146618).

### The Radon-Nikodym Framework for Changing Measures

At its core, the Girsanov theorem is an application of the Radon-Nikodym theorem from [measure theory](@entry_id:139744) to the dynamic setting of [stochastic processes](@entry_id:141566). To understand the mechanism, we must first revisit the static case.

Let $(\Omega, \mathcal{F})$ be a [measurable space](@entry_id:147379), and let $\mathbb{P}$ and $\mathbb{Q}$ be two probability measures defined on this space. We say that $\mathbb{Q}$ is **absolutely continuous** with respect to $\mathbb{P}$, denoted $\mathbb{Q} \ll \mathbb{P}$, if every event with zero probability under $\mathbb{P}$ also has zero probability under $\mathbb{Q}$. Formally, for any event $A \in \mathcal{F}$, if $\mathbb{P}(A) = 0$, then $\mathbb{Q}(A) = 0$. This condition ensures that the "impossible" events are the same under both measures.

The **Radon-Nikodym theorem** states that $\mathbb{Q} \ll \mathbb{P}$ if and only if there exists a non-negative, $\mathcal{F}$-measurable random variable, which we will denote by $Z$, such that for any event $A \in \mathcal{F}$, the probability $\mathbb{Q}(A)$ can be computed by integrating $Z$ over the set $A$ with respect to the measure $\mathbb{P}$ [@problem_id:3067543]:
$$
\mathbb{Q}(A) = \int_A Z \, d\mathbb{P}.
$$
This relationship is often expressed in terms of expectation:
$$
\mathbb{Q}(A) = \mathbb{E}_{\mathbb{P}}[\mathbf{1}_A Z],
$$
where $\mathbf{1}_A$ is the [indicator function](@entry_id:154167) for the event $A$. The random variable $Z$ is called the **Radon-Nikodym derivative** of $\mathbb{Q}$ with respect to $\mathbb{P}$, written as $Z = \frac{d\mathbb{Q}}{d\mathbb{P}}$. This derivative is unique up to $\mathbb{P}$-almost sure equality.

Since $\mathbb{Q}$ is a probability measure, we must have $\mathbb{Q}(\Omega) = 1$. Applying the formula above to the entire sample space $\Omega$ (i.e., setting $A=\Omega$), we find a crucial property of the Radon-Nikodym derivative:
$$
1 = \mathbb{Q}(\Omega) = \mathbb{E}_{\mathbb{P}}[\mathbf{1}_\Omega Z] = \mathbb{E}_{\mathbb{P}}[Z].
$$
This means that any valid Radon-Nikodym derivative connecting two probability measures must have an expectation of 1 under the original measure $\mathbb{P}$ [@problem_id:3067543] [@problem_id:3067586].

Furthermore, this framework provides a powerful tool for converting expectations under $\mathbb{Q}$ into expectations under $\mathbb{P}$. For any bounded, $\mathcal{F}$-measurable random variable $X$, the [change of measure](@entry_id:157887) formula for expectations holds [@problem_id:3067543]:
$$
\mathbb{E}_{\mathbb{Q}}[X] = \mathbb{E}_{\mathbb{P}}[XZ].
$$
This formula is the engine that drives many applications of the Girsanov theorem, particularly in [mathematical finance](@entry_id:187074) for pricing derivatives under a [risk-neutral measure](@entry_id:147013).

### The Density Process and Martingale Representation

To apply these ideas to a [continuous-time stochastic process](@entry_id:188424) evolving on an interval $[0, T]$, we work with a filtered probability space $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \in [0,T]}, \mathbb{P})$. Here, the [change of measure](@entry_id:157887) is defined on the terminal [sigma-algebra](@entry_id:137915) $\mathcal{F}_T$ via a Radon-Nikodym derivative $Z_T = \frac{d\mathbb{Q}}{d\mathbb{P}} \big|_{\mathcal{F}_T}$.

A crucial requirement for consistency is that the [change of measure](@entry_id:157887) must be well-behaved at all intermediate times $t \le T$. The restriction of $\mathbb{Q}$ to the sigma-algebra $\mathcal{F}_t$ should also be absolutely continuous with respect to the restriction of $\mathbb{P}$ to $\mathcal{F}_t$. The Radon-Nikodym derivative for this restricted measure, denoted $Z_t = \frac{d\mathbb{Q}}{d\mathbb{P}} \big|_{\mathcal{F}_t}$, forms a **density process** $(Z_t)_{t \in [0,T]}$.

From the [tower property of conditional expectation](@entry_id:181314), these random variables are related by a fundamental consistency condition. For any $s \le t$, we must have $Z_s = \mathbb{E}_{\mathbb{P}}[Z_t | \mathcal{F}_s]$. This is precisely the definition of a **[martingale](@entry_id:146036)**. Therefore, any valid density process $(Z_t)_{t \in [0,T]}$ must be a $\mathbb{P}$-[martingale](@entry_id:146036) with respect to the filtration $(\mathcal{F}_t)_{t \in [0,T]}$ [@problem_id:3067586]. Since $Z_0$ must be constant (as $\mathcal{F}_0$ is typically trivial), and $\mathbb{E}_{\mathbb{P}}[Z_T]=1$, we must have $Z_0=1$.

This raises a natural question: how can we construct such a martingale? The answer lies in another cornerstone of stochastic calculus, the **Predictable Representation Property (PRP)**, also known as the Martingale Representation Theorem. For a filtration generated by a $d$-dimensional standard Brownian motion $W$, this theorem asserts that any square-integrable $\mathbb{P}$-martingale $(M_t)_{t \in [0,T]}$ can be uniquely represented as a [stochastic integral](@entry_id:195087) with respect to $W$ [@problem_id:3067587]:
$$
M_t = M_0 + \int_0^t H_s \cdot dW_s, \quad t \in [0,T].
$$
Here, $H_s$ is a $d$-dimensional, **predictable** process satisfying the square-[integrability condition](@entry_id:160334) $\mathbb{E}_{\mathbb{P}}[\int_0^T \|H_s\|^2 ds]  \infty$. This theorem is profound: it tells us that the Brownian motion $W$ is the *only* source of randomness in its own filtration. Any [martingale](@entry_id:146036)-driven uncertainty must ultimately arise from $W$. This gives us a concrete way to build our density martingale $Z_t$.

### The Stochastic Exponential and its Properties

Following the insight from the Predictable Representation Property, we construct our density process $Z_t$ as the result of a stochastic integral involving the underlying Brownian motion $W_t$. The specific form that yields the desired properties is the **Doléans-Dade [stochastic exponential](@entry_id:197698)** (or simply [stochastic exponential](@entry_id:197698)).

Let $\theta = (\theta_t)_{t \in [0,T]}$ be a $d$-dimensional [predictable process](@entry_id:274260). Predictability is a technical condition of non-anticipation, ensuring that the value of $\theta_t$ is known "just before" time $t$. This is a crucial requirement for the mathematical consistency of the Itô integral [@problem_id:3067555]. If $\theta_t$ were allowed to depend on future information (e.g., the value of $W_T$), the resulting integral would not be an Itô integral, and the process we are about to construct would lose its essential [martingale property](@entry_id:261270) under $\mathbb{P}$, invalidating the entire framework [@problem_id:3067555].

Assuming $\theta_t$ is predictable and satisfies the appropriate square-[integrability condition](@entry_id:160334), $\mathbb{E}_{\mathbb{P}}[\int_0^T \|\theta_s\|^2 ds]  \infty$, the vector Itô integral $M_t = \int_0^t \theta_s \cdot dW_s = \sum_{i=1}^d \int_0^t \theta_s^i dW_s^i$ is well-defined. This integral represents a continuous, square-integrable $\mathbb{P}$-[martingale](@entry_id:146036) [@problem_id:3067605].

The [stochastic exponential](@entry_id:197698) of $M_t$, denoted $\mathcal{E}(M)_t$, is defined as:
$$
Z_t = \mathcal{E}(M)_t = \exp\left( M_t - \frac{1}{2}\langle M \rangle_t \right) = \exp\left( \int_0^t \theta_s \cdot dW_s - \frac{1}{2}\int_0^t \|\theta_s\|^2 ds \right).
$$
The term $\langle M \rangle_t = \int_0^t \|\theta_s\|^2 ds$ is the quadratic variation of the [martingale](@entry_id:146036) $M_t$. Its presence is a correction term, derived from Itô's formula, that precisely cancels the drift that would otherwise arise from applying the [exponential function](@entry_id:161417) to a [stochastic integral](@entry_id:195087). As a result, the process $(Z_t)_{t \in [0,T]}$ is a **[local martingale](@entry_id:203733)** with $Z_0 = 1$.

However, for $Z_t$ to serve as a valid density process, it must be a true [martingale](@entry_id:146036), not just a local one. A [local martingale](@entry_id:203733) is not guaranteed to have a constant expectation. In fact, being non-negative, $Z_t$ is always a [supermartingale](@entry_id:271504), meaning $\mathbb{E}_{\mathbb{P}}[Z_t] \le Z_0 = 1$. To ensure equality, we need a stronger condition that guarantees the [uniform integrability](@entry_id:199715) of the [martingale](@entry_id:146036) $Z_t$ [@problem_id:3067613].

The most celebrated sufficient condition for this is **Novikov's condition** [@problem_id:3067573]:
$$
\mathbb{E}_{\mathbb{P}}\left[ \exp\left( \frac{1}{2}\int_0^T \|\theta_s\|^2 ds \right) \right]  \infty.
$$
If this condition holds, it guarantees that $(Z_t)_{t \in [0,T]}$ is a [uniformly integrable martingale](@entry_id:180573), and thus $\mathbb{E}_{\mathbb{P}}[Z_T]=1$ [@problem_id:3067565]. Other, stronger conditions also suffice, such as the quadratic variation being almost surely bounded by a constant, i.e., $\int_0^T \|\theta_s\|^2 ds \le K$ for some constant $K$ [@problem_id:3067613]. It is important to note that Novikov's condition is sufficient, but not necessary; other criteria, such as the Kazamaki criterion, can also establish the [martingale property](@entry_id:261270) [@problem_id:3067613].

### The Multidimensional Girsanov Theorem

With all the necessary machinery in place, we can now state the main theorem.

**Theorem (Girsanov, Multidimensional Version):** Let $W_t$ be a $d$-dimensional standard Brownian motion on a filtered probability space $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \in [0,T]}, \mathbb{P})$. Let $\theta_t$ be a $d$-dimensional [predictable process](@entry_id:274260) satisfying Novikov's condition. Define a new probability measure $\mathbb{Q}$ on $\mathcal{F}_T$ via the Radon-Nikodym derivative:
$$
\frac{d\mathbb{Q}}{d\mathbb{P}}\bigg|_{\mathcal{F}_T} = Z_T = \exp\left( \int_0^T \theta_s \cdot dW_s - \frac{1}{2}\int_0^T \|\theta_s\|^2 ds \right).
$$
Then, the process $W_t^{\mathbb{Q}}$ defined by
$$
W_t^{\mathbb{Q}} = W_t - \int_0^t \theta_s ds
$$
is a $d$-dimensional standard Brownian motion under the new probability measure $\mathbb{Q}$ [@problem_id:3067591] [@problem_id:3067565].

This theorem is remarkable. It provides an explicit method to transform a standard Brownian motion into a process with a specific drift. By rearranging the final equation, we see the dynamics of the original process $W_t$ under the new measure $\mathbb{Q}$:
$$
W_t = W_t^{\mathbb{Q}} + \int_0^t \theta_s ds.
$$
This reveals that under $\mathbb{Q}$, the process $W_t$ is a sum of a $\mathbb{Q}$-Brownian motion and a drift term. The process $\theta_t$ is therefore the **drift** of $W_t$ in the new world defined by $\mathbb{Q}$ [@problem_id:3067565].

A key insight is that the Girsanov transformation changes the drift but preserves the quadratic variation. The quadratic variation of $W_t^{\mathbb{Q}}$ is identical to that of $W_t$. This means the "volatility" or "diffusion" structure of the process remains unchanged. An equivalent [change of measure](@entry_id:157887) only affects the predictable, finite-variation part of a [semimartingale](@entry_id:188438), not its martingale part's diffusion coefficient. For instance, an [orthogonal transformation](@entry_id:155650) $AW_t$ of a $\mathbb{P}$-Brownian motion $W_t$ is also a $\mathbb{P}$-Brownian motion. However, under $\mathbb{Q}$, the process $AW_t$ becomes $AW_t^{\mathbb{Q}} + \int_0^t A\theta_s ds$, which is not a $\mathbb{Q}$-Brownian motion unless $A\theta_s=0$ [@problem_id:3067565].

### Generalizations and Applications

The true power of Girsanov's theorem is realized when applied to general Itô processes. Consider an $n$-dimensional process $X_t$ governed by the [stochastic differential equation](@entry_id:140379) (SDE) under $\mathbb{P}$:
$$
dX_t = b_t dt + \sigma_t dW_t,
$$
where $b_t \in \mathbb{R}^n$ is the drift vector and $\sigma_t \in \mathbb{R}^{n \times d}$ is the [diffusion matrix](@entry_id:182965). What are the dynamics of $X_t$ under the measure $\mathbb{Q}$ generated by the process $\theta_t \in \mathbb{R}^d$?

We substitute $dW_t = dW_t^{\mathbb{Q}} + \theta_t dt$ into the SDE:
$$
dX_t = b_t dt + \sigma_t (dW_t^{\mathbb{Q}} + \theta_t dt) = (b_t + \sigma_t \theta_t) dt + \sigma_t dW_t^{\mathbb{Q}}.
$$
This is the SDE for $X_t$ under the measure $\mathbb{Q}$. The new drift is $\tilde{b}_t = b_t + \sigma_t \theta_t$. The drift adjustment, $\sigma_t \theta_t$, has a profound geometric interpretation. The matrix-vector product $\sigma_t \theta_t$ is a linear combination of the columns of the [diffusion matrix](@entry_id:182965) $\sigma_t$, with the components of $\theta_t$ acting as weights. This means the change in drift can only occur in directions where the process already has diffusion or randomness. The Girsanov transformation cannot introduce drift in a direction in which the process is purely deterministic [@problem_id:3067585].

The theorem can be generalized even further. Let $M_t$ be a general $d$-dimensional continuous local $\mathbb{P}$-martingale with a quadratic variation matrix process given by $[M]_t = \int_0^t a_s ds$, where $a_s$ is a [predictable process](@entry_id:274260) of [symmetric positive semidefinite matrices](@entry_id:163376). If we perform a [change of measure](@entry_id:157887) using the density process $Z_t = \mathcal{E}(\int \theta_s^T dM_s)_t$, the process that becomes a $\mathbb{Q}$-[local martingale](@entry_id:203733) is [@problem_id:3067570]:
$$
M_t^{\mathbb{Q}} = M_t - \langle M, \int \theta^T dM \rangle_t = M_t - \int_0^t a_s \theta_s ds.
$$
The drift adjustment is now $a_s \theta_s$, incorporating the covariance structure $a_s$ of the underlying martingale. The standard Girsanov theorem for Brownian motion is simply the special case where $M_t = W_t$ and $a_s = I_d$, the identity matrix. This general form highlights the fundamental mechanism: the [change of measure](@entry_id:157887) induces a drift in the direction of the underlying martingale's covariance structure, as specified by the process $\theta$.