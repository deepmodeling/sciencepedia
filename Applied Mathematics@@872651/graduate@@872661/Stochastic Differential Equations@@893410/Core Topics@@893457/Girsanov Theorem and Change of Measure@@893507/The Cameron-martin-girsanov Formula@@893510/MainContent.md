## Introduction
The Cameron-Martin-Girsanov theorem is a cornerstone of modern [stochastic calculus](@entry_id:143864), offering a powerful framework for changing the probability measure governing a stochastic process. Its significance lies in its ability to solve a fundamental problem: how to controllably alter the dynamics of a [stochastic system](@entry_id:177599), particularly by transforming a process with a complex drift into a simpler one, like a [martingale](@entry_id:146036), without changing its fundamental "noisiness" or diffusion structure. This article provides a comprehensive, graduate-level exploration of this vital theorem.

The journey begins in **Principles and Mechanisms**, where we will dissect the probabilistic foundations of the theorem, from [equivalent measures](@entry_id:634447) to the Doléans-Dade exponential, and explore the critical conditions like Novikov's that ensure a valid transformation. Next, **Applications and Interdisciplinary Connections** will showcase the theorem's immense utility, demonstrating its central role in the [risk-neutral pricing](@entry_id:144172) of [financial derivatives](@entry_id:637037), statistical inference for [diffusion processes](@entry_id:170696), and foundational proofs in probability theory. Finally, **Hands-On Practices** will solidify your understanding by guiding you through concrete problems, from verifying [martingale](@entry_id:146036) properties to applying the theorem to solve complex expectation calculations.

## Principles and Mechanisms

The Cameron-Martin-Girsanov theorem is a cornerstone of modern [stochastic calculus](@entry_id:143864), providing a powerful tool for changing the probability measure under which a [stochastic process](@entry_id:159502) is considered. This [change of measure](@entry_id:157887), or "change of numéraire" in financial applications, allows us to transform a process with a complicated drift into a simpler one, typically a [martingale](@entry_id:146036), without altering its diffusion structure. This chapter elucidates the core principles and mechanisms of this theorem, starting from the foundational setting, exploring its consequences, delving into the necessary technical conditions, and finally discussing its generalizations and limitations.

### The Probabilistic Setting: Equivalent Measures and Density Processes

The theory of measure change for continuous-time processes requires a rigorous probabilistic framework. We work on a filtered probability space $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \in [0,T]}, \mathbb{P})$ for some fixed time horizon $T > 0$. The [filtration](@entry_id:162013) $(\mathcal{F}_t)_{t \in [0,T]}$ represents the flow of information over time and is assumed to satisfy the **usual conditions**. This standard technical assumption means two things:
1.  The filtration is **complete**: the initial $\sigma$-algebra $\mathcal{F}_0$ contains all subsets of $\mathbb{P}$-[null sets](@entry_id:203073) (sets of probability zero). This ensures that if an event has probability zero, we know this from the start, and this knowledge persists.
2.  The filtration is **right-continuous**: for all $t \in [0,T)$, we have $\mathcal{F}_t = \mathcal{F}_{t+} \equiv \bigcap_{u>t} \mathcal{F}_u$. This condition prevents information from arriving in an unanticipated "[big bang](@entry_id:159819)" and is essential for the powerful results of [martingale theory](@entry_id:266805).

When we consider the canonical space of continuous functions $C_0[0,T]$ for constructing a standard Brownian motion $W$, the [natural filtration](@entry_id:200612) $\sigma(W_s : s \le t)$ does not satisfy these conditions. Therefore, we work with its **usual augmentation**, which is the smallest filtration containing the natural one that satisfies the usual conditions. This augmented space provides the proper setting for theorems like Cameron-Martin-Girsanov [@problem_id:3000282].

The central idea is to define a new probability measure $\mathbb{Q}$ on the terminal $\sigma$-algebra $\mathcal{F}_T$ that is **equivalent** to the original measure $\mathbb{P}$. Equivalence means that $\mathbb{P}$ and $\mathbb{Q}$ have the same [null sets](@entry_id:203073): $\mathbb{Q}(A) = 0$ if and only if $\mathbb{P}(A)=0$. This relationship is established via a **Radon-Nikodým derivative**, a non-negative random variable $Z_T$ such that for any event $A \in \mathcal{F}_T$:
$$
\mathbb{Q}(A) = \int_A Z_T(\omega) \,d\mathbb{P}(\omega) = \mathbb{E}_{\mathbb{P}}[Z_T \mathbf{1}_A]
$$
This is often written in shorthand as $\frac{d\mathbb{Q}}{d\mathbb{P}} = Z_T$. For $\mathbb{Q}$ to be a valid probability measure, we must have $\mathbb{Q}(\Omega)=1$, which implies the crucial condition $\mathbb{E}_{\mathbb{P}}[Z_T] = 1$.

The Radon-Nikodým derivative $Z_T$ is the terminal value of a **density process** $(Z_t)_{t \in [0,T]}$, defined by $Z_t := \mathbb{E}_{\mathbb{P}}[Z_T | \mathcal{F}_t]$. By the [tower property of conditional expectation](@entry_id:181314), this process is a $\mathbb{P}$-[martingale](@entry_id:146036). The condition $\mathbb{E}_{\mathbb{P}}[Z_T] = 1$ ensures that this martingale has a constant expectation of 1, as $Z_0 = \mathbb{E}_{\mathbb{P}}[Z_T|\mathcal{F}_0] = \mathbb{E}_{\mathbb{P}}[Z_T] = 1$. Girsanov's theorem provides a systematic way to construct such a density process.

### The Girsanov Theorem for Brownian Motion

The most celebrated version of Girsanov's theorem describes how to change the drift of a standard Brownian motion. Let $W = (W_t)_{t \in [0,T]}$ be a $d$-dimensional standard Brownian motion under $\mathbb{P}$. We wish to find a measure $\mathbb{Q}$ under which $W_t$ behaves like a Brownian motion with an added drift.

The key is to introduce a process that will become this new drift. Let $\theta = (\theta_t)_{t \in [0,T]}$ be an $\mathbb{R}^d$-valued [stochastic process](@entry_id:159502). For the subsequent constructions to be valid, $\theta$ must be a **[predictable process](@entry_id:274260)**. This technical condition is fundamental. The Itô integral $\int_0^t \theta_s \cdot dW_s$ is constructed as a limit of sums over partitions of the time interval. For the resulting integral to be a (local) martingale, the value of the integrand $\theta_s$ over an interval $(t_i, t_{i+1}]$ must be "known" at the start of the interval, i.e., measurable with respect to $\mathcal{F}_{t_i}$. Predictability is the precise formulation of this non-anticipating property, and it is the bedrock upon which the [martingale](@entry_id:146036) properties of stochastic integrals are built [@problem_id:2978186].

Given a [predictable process](@entry_id:274260) $\theta$ satisfying $\int_0^T \|\theta_s\|^2 ds  \infty$ [almost surely](@entry_id:262518), we define the density process $Z_t$ via the **Doléans-Dade exponential** (or [stochastic exponential](@entry_id:197698)):
$$
Z_t = \mathcal{E}\left(\int_0^\cdot \theta_s^\top dW_s\right)_t := \exp\left(\int_0^t \theta_s^\top dW_s - \frac{1}{2}\int_0^t \|\theta_s\|^2 ds\right)
$$
This process is the unique solution to the linear SDE $dZ_t = Z_t \theta_t^\top dW_t$ with $Z_0=1$. As this SDE has no $dt$ term, $Z_t$ is a [continuous local martingale](@entry_id:188921) under $\mathbb{P}$ [@problem_id:3000294]. Assuming for now that $(Z_t)$ is a true [martingale](@entry_id:146036) on $[0,T]$ with $\mathbb{E}_{\mathbb{P}}[Z_T] = 1$, we can state the theorem.

**Girsanov's Theorem:** Let $W_t$ be a $d$-dimensional $\mathbb{P}$-Brownian motion and let $\theta_t$ be a [predictable process](@entry_id:274260) satisfying the conditions above. Let $\mathbb{Q}$ be the probability measure on $\mathcal{F}_T$ defined by the Radon-Nikodým derivative $\frac{d\mathbb{Q}}{d\mathbb{P}} = Z_T$. Then the process $\widetilde{W}_t$ defined by
$$
\widetilde{W}_t := W_t - \int_0^t \theta_s ds
$$
is a $d$-dimensional standard Brownian motion under the measure $\mathbb{Q}$ [@problem_id:3000265] [@problem_id:3000333].

### Core Mechanisms and Consequences

To understand the theorem's power, we must examine its key mechanisms.

#### Invariance of Quadratic Variation

A central tenet of the theory is that an equivalent [change of measure](@entry_id:157887) does not alter the [sample paths](@entry_id:184367) of a process, only their probability. Consequently, any property defined pathwise remains unchanged. The **[quadratic variation](@entry_id:140680)** of a continuous [semimartingale](@entry_id:188438) is such a property. It is determined by the "roughness" of the path.
The process $\widetilde{W}_t = W_t - \int_0^t \theta_s ds$ is the sum of a $\mathbb{P}$-Brownian motion and a [finite variation process](@entry_id:635841) (the drift integral). Its quadratic variation is therefore identical to that of its [martingale](@entry_id:146036) part:
$$
\langle \widetilde{W} \rangle_t = \langle W \rangle_t = t \cdot I_d
$$
where $I_d$ is the $d \times d$ identity matrix. Girsanov's theorem shows that under the measure $\mathbb{Q}$, the process $\widetilde{W}_t$ is not only a [continuous local martingale](@entry_id:188921) with this [quadratic variation](@entry_id:140680), but that it also has the independent, normally distributed increments characteristic of a Brownian motion. The fact that the [quadratic variation](@entry_id:140680) is invariant is essential; if it were altered by the measure change, $\widetilde{W}_t$ could not be a standard Brownian motion [@problem_id:3000265] [@problem_id:3000333].

#### Transformation of Drifts in SDEs

The primary application of Girsanov's theorem is to transform the drift of a general Itô process. Consider a process $X_t$ that solves the SDE under $\mathbb{P}$:
$$
dX_t = b_t(X_t) dt + \sigma_t(X_t) dW_t
$$
To find the dynamics of $X_t$ under $\mathbb{Q}$, we simply rearrange the relation from Girsanov's theorem: $dW_t = d\widetilde{W}_t + \theta_t dt$. Substituting this into the SDE for $X_t$ gives:
$$
dX_t = b_t(X_t) dt + \sigma_t(X_t) (d\widetilde{W}_t + \theta_t dt) = \left(b_t(X_t) + \sigma_t(X_t) \theta_t \right) dt + \sigma_t(X_t) d\widetilde{W}_t
$$
Under the measure $\mathbb{Q}$, $\widetilde{W}_t$ is the new Brownian motion. The SDE reveals that the drift of $X_t$ has been transformed from $b_t$ to $b_t + \sigma_t \theta_t$, while the diffusion coefficient $\sigma_t$ remains unchanged [@problem_id:3000294] [@problem_id:3000333]. This simple algebraic manipulation is the source of the theorem's immense utility in finance (for pricing derivatives) and control theory.

#### The Cameron-Martin Theorem: A Deterministic Shift

The simplest and historically first version of the theorem considers a deterministic drift. This is known as the **Cameron-Martin Theorem**. Let $h(t)$ be a deterministic function in the **Cameron-Martin space** $H$, meaning $h(0)=0$, $h$ is absolutely continuous, and its derivative $\dot{h}$ is square-integrable on $[0,T]$. We can set $\theta_t = \dot{h}(t)$. Because $\theta_t$ is deterministic, the conditions for Girsanov's theorem are easily met. The theorem then states that under the measure $\mathbb{Q}$ with density $\mathcal{E}(\int \dot{h} dW)_T$, the process $\widetilde{W}_t = W_t - h(t)$ is a standard Brownian motion. This means the law of the original Brownian motion $W_t$ under $\mathbb{Q}$ is the same as the law of a shifted process, $B_t + h(t)$, where $B_t$ is a standard Brownian motion under $\mathbb{P}$. The Cameron-Martin formula provides an explicit Radon-Nikodým derivative for translating a Brownian motion by a deterministic function [@problem_id:3000327].

### Conditions for a Valid Change of Measure

As noted, for $Z_T$ to define a new probability measure $\mathbb{Q}$, we must have $\mathbb{E}_{\mathbb{P}}[Z_T]=1$. The process $Z_t = \mathcal{E}(\int \theta dW)_t$ is always a non-negative [continuous local martingale](@entry_id:188921), which implies it is a [supermartingale](@entry_id:271504), so $\mathbb{E}_{\mathbb{P}}[Z_t] \le Z_0=1$. The critical step is to find conditions that prevent the expectation from being strictly less than 1, which would mean $Z_t$ is a **[strict local martingale](@entry_id:636161)**.

#### Sufficient Conditions: Novikov and Kazamaki

A widely used sufficient condition for $(Z_t)_{t \in [0,T]}$ to be a [uniformly integrable martingale](@entry_id:180573) (which ensures $\mathbb{E}_{\mathbb{P}}[Z_T]=1$) is **Novikov's condition**:
$$
\mathbb{E}_{\mathbb{P}}\left[\exp\left(\frac{1}{2}\int_0^T \|\theta_s\|^2 ds\right)\right]  \infty
$$
This condition essentially requires that the drift process $\theta$ does not grow too quickly. Note that the integral inside the exponential is half the [quadratic variation](@entry_id:140680) of the [stochastic integral](@entry_id:195087) $\int \theta^\top dW$. When $\theta$ is deterministic, as in the Cameron-Martin theorem, this condition is always satisfied, as the expression inside the expectation is a constant [@problem_id:3000327].

Another important sufficient condition is **Kazamaki's condition**, which requires that the process $\exp(\frac{1}{2} M_t)$ is a [submartingale](@entry_id:263978), where $M_t = \int_0^t \theta_s dW_s$. A detailed analysis shows that Novikov's condition implies Kazamaki's condition. However, the converse is not true; Kazamaki's condition is strictly weaker. There exist processes $\theta$ for which Kazamaki's condition holds (and thus $\mathcal{E}(\int\theta dW)$ is a true [martingale](@entry_id:146036)) while Novikov's condition fails. This makes Kazamaki's condition a more general criterion [@problem_id:3000256].

#### When the Conditions Fail: A Counterexample

The importance of these conditions is best illustrated by a counterexample. Consider a Brownian motion $W_t$ starting at $W_0=1$ and let $\tau_0$ be the first time it hits zero. If we define the Girsanov kernel as $\theta_t = - \frac{1}{W_t}$ for $t  \tau_0$ and $\theta_t=0$ otherwise, one can explicitly compute the density process $Z_t$. A careful calculation shows that on the event that the Brownian motion hits zero before time $T=1$ (i.e., $\tau_0 \le 1$), the density $Z_1$ becomes zero. On the event that it does not hit zero, the density is positive.
The total mass of the new "measure" is $\mathbb{E}_{\mathbb{P}}[Z_1]$. This can be shown to be equal to the [survival probability](@entry_id:137919) $\mathbb{P}(\tau_0 > 1)$, which by the reflection principle is $2\Phi(1)-1 \approx 0.6826$, where $\Phi$ is the standard normal CDF. Since $\mathbb{E}_{\mathbb{P}}[Z_1]  1$, the process $Z_t$ is a [strict local martingale](@entry_id:636161), and the resulting measure $\mathbb{Q}$ is not a probability measure as its total mass is less than one [@problem_id:3000325]. This example powerfully demonstrates that not every [local martingale](@entry_id:203733) exponential can serve as a valid probability density.

### Generalizations and Advanced Perspectives

The Girsanov theorem can be stated in a much more general form, extending beyond Brownian motion.

#### General Girsanov Theorem for Continuous Local Martingales

Let $M$ be any continuous local $\mathbb{P}$-martingale. Let $\theta$ be a [predictable process](@entry_id:274260), and define the density process via the [stochastic integral](@entry_id:195087) with respect to $M$:
$$
Z_t = \mathcal{E}\left(\int_0^\cdot \theta_s dM_s\right)_t = \exp\left(\int_0^t \theta_s dM_s - \frac{1}{2}\int_0^t \theta_s^2 d\langle M \rangle_s\right)
$$
where $\langle M \rangle_t$ is the quadratic variation process of $M$. If $(Z_t)$ is a true [martingale](@entry_id:146036), defining a new measure $\mathbb{Q}$, then the process
$$
N_t = M_t - \int_0^t \theta_s d\langle M \rangle_s = M_t - \langle M, \int \theta dM \rangle_t
$$
is a [continuous local martingale](@entry_id:188921) under $\mathbb{Q}$ [@problem_id:3000293]. This general form reveals the fundamental structure: the new [martingale](@entry_id:146036) is the old one minus the [quadratic covariation](@entry_id:180155) with the logarithm of the density process. A crucial consequence, again, is the invariance of quadratic (co)variation under this equivalent [change of measure](@entry_id:157887). For any two continuous local $\mathbb{P}$-martingales $M$ and $K$, we have $\langle M, K \rangle_t = \langle N, J \rangle_t$, where $N$ and $J$ are the corresponding $\mathbb{Q}$-[martingales](@entry_id:267779) [@problem_id:3000339].

#### The Inverse Problem and the Martingale Representation Theorem

Girsanov's theorem shows how to construct a density from a kernel $\theta$. What about the inverse problem? Given a target density $Z_T > 0$ with $\mathbb{E}_{\mathbb{P}}[Z_T]=1$, can we find the corresponding kernel $\theta$? The answer lies in the **Martingale Representation Theorem (MRT)**.
In a Brownian filtration, the MRT states that any square-integrable [martingale](@entry_id:146036) $Z_t = \mathbb{E}_{\mathbb{P}}[Z_T | \mathcal{F}_t]$ can be written as a stochastic integral with respect to the underlying Brownian motion $W$:
$$
dZ_t = \xi_t^\top dW_t
$$
for some unique [predictable process](@entry_id:274260) $\xi_t$. On the other hand, the Girsanov density process must satisfy the SDE $dZ_t = Z_t \theta_t^\top dW_t$. By comparing these two SDEs and using the uniqueness of the MRT integrand, we must have $\xi_t = Z_t \theta_t$. Since $Z_t = \mathbb{E}[Z_T|\mathcal{F}_t] > 0$, we can solve for the kernel:
$$
\theta_t = \frac{\xi_t}{Z_t}
$$
The integrand $\xi_t$ can also be identified via the [quadratic covariation](@entry_id:180155): $\xi^i_t = \frac{d\langle Z, W^i \rangle_t}{dt}$. Thus, the MRT provides the constructive link from a given density back to the Girsanov kernel that generates it [@problem_id:3000272].

### Scope and Limitations: Why Diffusion Coefficients Matter

The Girsanov framework allows for a change in the drift of an SDE, but it fundamentally cannot change the diffusion coefficient. This is a critical limitation for applications in statistical inference.
Consider two SDE models for a process $X_t$:
$$
\begin{align*}
\text{Model 0: }  dX_t = b_0(X_t) dt + \sigma_0(X_t) dW_t \\
\text{Model 1: }  dX_t = b_1(X_t) dt + \sigma_1(X_t) dW_t
\end{align*}
$$
Let $\mathbb{P}_0$ and $\mathbb{P}_1$ be the respective laws on the space of [continuous paths](@entry_id:187361). The [quadratic variation](@entry_id:140680) of the path $X_t$ is a pathwise property, and for any path generated under Model $k$, it must satisfy $\langle X \rangle_T = \int_0^T \sigma_k^2(X_s) ds$.

If the diffusion coefficients differ, $\sigma_0 \not\equiv \sigma_1$, then the set of paths satisfying the quadratic variation condition for Model 0 is disjoint from the set of paths satisfying it for Model 1. Since $\mathbb{P}_0$ assigns full probability to the first set and $\mathbb{P}_1$ assigns full probability to the second, the measures are **mutually singular** ($\mathbb{P}_0 \perp \mathbb{P}_1$).
This means that, in principle, by observing a single continuous path and calculating its quadratic variation, one could determine with certainty which model generated it.
Because the measures are singular, they are not equivalent, and no Radon-Nikodým derivative exists between them. Consequently, Girsanov's theorem cannot be used to find a likelihood ratio for comparing models with different diffusion coefficients based on continuous observations. Statistical inference in this setting must rely on discrete-time observations, for which the measures are not singular, and one can construct approximate likelihoods (quasi-likelihoods) [@problem_id:2989893]. This limitation underscores that the Girsanov transformation is fundamentally about altering the "signal" (drift) while preserving the "noise" structure (diffusion).