## Introduction
In the advanced study of stochastic processes, the ability to change the underlying probability measure is a transformative tool. This technique, formalized by Girsanov's theorem, is central to solving complex stochastic differential equations (SDEs) and is the foundation of modern [mathematical finance](@entry_id:187074). The validity of this [change of measure](@entry_id:157887) hinges on a specific stochastic process—the Doléans–Dade exponential—being a true, [uniformly integrable martingale](@entry_id:180573), allowing it to serve as a valid Radon-Nikodym density. However, this exponential is, by construction, only guaranteed to be a [local martingale](@entry_id:203733). This article addresses the fundamental problem of identifying the conditions under which this crucial step from local to true martingale is justified.

Over the following chapters, we will embark on a comprehensive exploration of this topic. In **Principles and Mechanisms**, we will dissect the core problem and introduce the celebrated Novikov and Kazamaki conditions, explaining their mechanics, limitations, and the unifying role of BMO martingales. Following this theoretical foundation, **Applications and Interdisciplinary Connections** will demonstrate the profound impact of these conditions in practice, validating drift removal in SDEs, enabling [option pricing](@entry_id:139980) in finance, and justifying transformations in [nonlinear filtering theory](@entry_id:198025). Finally, **Hands-On Practices** will offer a series of guided problems to build intuition and mastery of these essential concepts.

## Principles and Mechanisms

In the study of stochastic differential equations and their applications, particularly in [mathematical finance](@entry_id:187074) and [filtering theory](@entry_id:186966), the transformation of one probability measure to another equivalent measure is a fundamental tool. This transformation is typically achieved via the Girsanov theorem, which relies on a specific positive [local martingale](@entry_id:203733), the **Doléans–Dade exponential** (or [stochastic exponential](@entry_id:197698)), to serve as a Radon–Nikodym density. A critical requirement for this construction is that the [local martingale](@entry_id:203733) in question must be a true, [uniformly integrable martingale](@entry_id:180573). This chapter delves into the principal conditions that guarantee this essential property, exploring the mechanisms by which they function and the relationships between them.

### The Central Problem: From Local Martingale to True Martingale

Let $M = (M_t)_{t \in [0,T]}$ be a [continuous local martingale](@entry_id:188921) on a filtered probability space $(\Omega, \mathcal{F}, \{\mathcal{F}_t\}_{t \in [0,T]}, \mathbb{P})$, with $M_0=0$. The Doléans–Dade exponential of $M$, denoted $\mathcal{E}(M)$, is the unique strictly positive solution to the [stochastic differential equation](@entry_id:140379):
$$
dZ_t = Z_t dM_t, \quad Z_0=1
$$
where we write $Z_t = \mathcal{E}(M)_t$. By applying Itô's formula to the function $f(x,y) = \exp(x - y/2)$ with the [semimartingale](@entry_id:188438) $(M_t, \langle M \rangle_t)$, where $\langle M \rangle$ is the quadratic variation of $M$, we arrive at the explicit solution:
$$
\mathcal{E}(M)_t = \exp\left(M_t - \frac{1}{2}\langle M \rangle_t\right)
$$
The term $-\frac{1}{2}\langle M \rangle_t$ is a compensator that precisely cancels the quadratic variation term arising from the convexity of the exponential function, ensuring that $\mathcal{E}(M)$ is, by construction, a [local martingale](@entry_id:203733).

Since $\mathcal{E}(M)_t$ is strictly positive for all $t$, it is a non-negative [local martingale](@entry_id:203733). A foundational result in [martingale theory](@entry_id:266805) states that any non-negative [local martingale](@entry_id:203733) is a [supermartingale](@entry_id:271504). This implies that for any $0 \le s \le t \le T$, we have $\mathbb{E}[\mathcal{E}(M)_t | \mathcal{F}_s] \le \mathcal{E}(M)_s$. Taking expectations, we find $\mathbb{E}[\mathcal{E}(M)_t] \le \mathbb{E}[\mathcal{E}(M)_0] = 1$.

For $\mathcal{E}(M)_T$ to serve as a valid Radon–Nikodym density for a [change of measure](@entry_id:157887), its expectation must be exactly 1. The central problem, therefore, is to identify conditions under which $\mathcal{E}(M)$ is not merely a [supermartingale](@entry_id:271504), but a true martingale, for which $\mathbb{E}[\mathcal{E}(M)_t] = 1$ for all $t \in [0,T]$. For a non-negative [supermartingale](@entry_id:271504) on a finite interval, this is equivalent to the process being **[uniformly integrable](@entry_id:202893) (UI)**. The subsequent sections explore the most celebrated criteria for establishing this property.

### Novikov's Condition: A Direct Control on Quadratic Variation

The most direct and historically one of the first sufficient criteria is **Novikov's condition**. It imposes an [integrability](@entry_id:142415) constraint directly on the total [quadratic variation](@entry_id:140680) of the [local martingale](@entry_id:203733).

**Novikov's Condition:** Let $M$ be a [continuous local martingale](@entry_id:188921) on $[0,T]$ with $M_0=0$. If
$$
\mathbb{E}\left[\exp\left(\frac{1}{2}\langle M \rangle_T\right)\right]  \infty,
$$
then the process $\mathcal{E}(M)$ is a [uniformly integrable martingale](@entry_id:180573) on $[0,T]$. Consequently, $\mathbb{E}[\mathcal{E}(M)_T] = 1$, and $\mathcal{E}(M)_T$ can be used as a Radon–Nikodym density to define a new probability measure $\mathbb{Q}$ on $\mathcal{F}_T$ that is equivalent to $\mathbb{P}$ [@problem_id:2989035].

The power of Novikov's condition lies in its relative simplicity; it depends only on the expected value of a single random variable, $\langle M \rangle_T$. However, it is crucial to understand its limitations. First, it is a *sufficient* condition, not a necessary one. There are many instances where $\mathcal{E}(M)$ is a [uniformly integrable martingale](@entry_id:180573), yet Novikov's condition fails.

Second, the constant $\frac{1}{2}$ in the exponent is sharp [@problem_id:2989057]. This optimality can be understood in a two-fold sense:
1.  Any stronger condition, such as $\mathbb{E}[\exp(c\langle M \rangle_T)]  \infty$ for some constant $c > \frac{1}{2}$, is trivially also sufficient. This is because for non-negative $\langle M \rangle_T$, $\exp(\frac{1}{2}\langle M \rangle_T) \le \exp(c\langle M \rangle_T)$, so the stronger assumption implies Novikov's original condition holds.
2.  Any weaker condition is insufficient in general. That is, for any constant $c  \frac{1}{2}$, one can construct a [continuous local martingale](@entry_id:188921) $M$ for which $\mathbb{E}[\exp(c\langle M \rangle_T)]  \infty$, but $\mathcal{E}(M)$ is a strict [supermartingale](@entry_id:271504) (i.e., $\mathbb{E}[\mathcal{E}(M)_T]  1$). This demonstrates that the constant $\frac{1}{2}$ cannot be lowered without losing the general applicability of the theorem.

### Kazamaki's Condition: A Control on the Martingale Itself

An alternative and more general criterion was provided by Kazamaki. Instead of controlling the [quadratic variation](@entry_id:140680) $\langle M \rangle$, **Kazamaki's condition** imposes an [integrability](@entry_id:142415) constraint on the martingale $M$ itself.

**Kazamaki's Condition:** Let $M$ be a [continuous local martingale](@entry_id:188921) on $[0,T]$ with $M_0=0$. If the process $X_t = \exp(\frac{1}{2}M_t)$ is a [submartingale](@entry_id:263978) of class $\mathcal{D}$ (i.e., the family of random variables $\{X_\tau\}$, where $\tau$ is any bounded [stopping time](@entry_id:270297), is [uniformly integrable](@entry_id:202893)), then $\mathcal{E}(M)$ is a [uniformly integrable martingale](@entry_id:180573).

A more practical, verifiable form of this condition is often used: if
$$
\sup_{\tau} \mathbb{E}\left[\exp\left(\frac{1}{2}M_\tau\right)\right]  \infty,
$$
where the [supremum](@entry_id:140512) is taken over all bounded [stopping times](@entry_id:261799) $\tau \le T$, then $\mathcal{E}(M)$ is a [uniformly integrable martingale](@entry_id:180573) on $[0,T]$ [@problem_id:2989063].

Like Novikov's condition, Kazamaki's condition is sufficient but not necessary. The constant $\frac{1}{2}$ in the exponent is also sharp [@problem_id:2989062]. A stronger assumption with a constant $\alpha > \frac{1}{2}$ implies Kazamaki's condition holds, as can be shown via Jensen's inequality. Conversely, for any $c  \frac{1}{2}$, counterexamples exist where the condition $\sup_{\tau}\mathbb{E}[\exp(c M_\tau)]  \infty$ holds, but $\mathcal{E}(M)$ fails to be a true martingale. Thus, $c=\frac{1}{2}$ represents the smallest universal threshold for this type of exponential integrability test to be sufficient [@problem_id:2989062].

### A Hierarchy of Conditions and the Role of BMO

While both Novikov's and Kazamaki's conditions are sufficient for $\mathcal{E}(M)$ to be a [uniformly integrable martingale](@entry_id:180573), neither implies the other. This suggests the existence of a more fundamental property that unifies them. For [continuous local martingales](@entry_id:204638), this property is captured by the concept of **Bounded Mean Oscillation (BMO)**.

A [continuous local martingale](@entry_id:188921) $M$ on $[0,T]$ is said to be in the space BMO if its BMO-norm is finite:
$$
\|M\|_{\mathrm{BMO}} := \sup_{\tau} \left\| \mathbb{E}\left[ \langle M \rangle_T - \langle M \rangle_\tau \,|\, \mathcal{F}_\tau \right] \right\|_{\infty}^{1/2}  \infty
$$
where the [supremum](@entry_id:140512) is over all bounded [stopping times](@entry_id:261799) $\tau \le T$ and $\|\cdot\|_\infty$ is the [essential supremum](@entry_id:186689) norm. This condition means that the conditionally expected future increase in [quadratic variation](@entry_id:140680) is uniformly bounded, irrespective of the [stopping time](@entry_id:270297).

The BMO property provides a complete characterization for the [uniform integrability](@entry_id:199715) of the [stochastic exponential](@entry_id:197698). A landmark theorem states that for a [continuous local martingale](@entry_id:188921) $M$ with $M_0=0$:
$$
M \in \text{BMO} \quad \iff \quad \mathcal{E}(M) \text{ is a uniformly integrable martingale.}
$$
This establishes BMO as a necessary and sufficient condition [@problem_id:2989052]. This insight allows us to place the classical conditions in a clear hierarchy. Both Novikov's condition and Kazamaki's condition are [sufficient conditions](@entry_id:269617) for $M$ to be a BMO [martingale](@entry_id:146036). However, they are strictly stronger; there exist BMO martingales that satisfy neither Novikov's nor Kazamaki's condition [@problem_id:2989051].

The BMO property is deeply connected to other powerful analytical properties. For instance, $M \in \text{BMO}$ if and only if there exists some $\lambda > 0$ such that $\mathcal{E}(\lambda M)$ is a [uniformly integrable martingale](@entry_id:180573) [@problem_id:2989040]. This is further equivalent to the celebrated **John-Nirenberg inequality** for martingales, which states that the conditional exponential moments of the [martingale](@entry_id:146036)'s future increments are uniformly bounded [@problem_id:2989051]: for some $\alpha > 0$,
$$
\sup_{\tau} \left\| \mathbb{E}\left[ \exp\left( \alpha |M_T - M_\tau| \right) \,|\, \mathcal{F}_\tau \right] \right\|_{\infty}  \infty
$$
Another equivalent characterization is that $\mathcal{E}(M)$ satisfies a **reverse Hölder inequality** of some order $p>1$ [@problem_id:2989051]. These equivalences reveal that the BMO property encapsulates a fundamental geometric regularity of the martingale's paths, which is precisely what is needed to ensure the good behavior of its [stochastic exponential](@entry_id:197698).

### Generalizations and Extensions

The principles discussed thus far can be extended to more general settings, including [martingales](@entry_id:267779) in multiple dimensions and those with jump components.

#### The Multidimensional Case

Consider a $d$-dimensional standard Brownian motion $W = (W_t)_{t \ge 0}$ and a [continuous local martingale](@entry_id:188921) defined by the stochastic integral $M_t = \int_0^t \theta_s \cdot dW_s$, where $\theta_s$ is a [predictable process](@entry_id:274260) taking values in $\mathbb{R}^d$. The [quadratic variation](@entry_id:140680) of $M$ is given by:
$$
\langle M \rangle_t = \int_0^t \|\theta_s\|^2 ds
$$
where $\|\cdot\|$ denotes the standard Euclidean norm in $\mathbb{R}^d$. With this expression for the [quadratic variation](@entry_id:140680), both Novikov's and Kazamaki's conditions retain their original form without any explicit dependence on the dimension $d$ [@problem_id:2989034]:
- **Novikov:** $\mathbb{E}\left[\exp\left(\frac{1}{2} \int_0^T \|\theta_s\|^2 ds\right)\right]  \infty$.
- **Kazamaki:** $\sup_{\tau} \mathbb{E}\left[\exp\left(\frac{1}{2} M_\tau\right)\right]  \infty$.
The dimension is implicitly handled within the squared Euclidean norm of the integrand process $\theta$. The critical constant remains $\frac{1}{2}$ in all dimensions.

#### Martingales with Jumps

When the [local martingale](@entry_id:203733) $M$ has jump components, the structure of its [stochastic exponential](@entry_id:197698) and the corresponding [martingale](@entry_id:146036) criteria become more complex. Let $M$ be a general [semimartingale](@entry_id:188438). The solution to $dZ_t = Z_{t-}dM_t$ is given by **Yor's formula**:
$$
\mathcal{E}(M)_t = \exp\left( M_t^c - \frac{1}{2}\langle M^c \rangle_t \right) \prod_{0  s \le t} (1 + \Delta M_s) e^{-\Delta M_s}
$$
where $M^c$ is the continuous part of $M$ and $\Delta M_s = M_s - M_{s-}$ are the jumps. Assuming $1+\Delta M_s > 0$ for all $s$, this can be rewritten as:
$$
\mathcal{E}(M)_t = \exp\left( M_t - \frac{1}{2}\langle M^c \rangle_t - \sum_{0  s \le t} \left[\Delta M_s - \log(1+\Delta M_s)\right] \right)
$$
The criteria for $\mathcal{E}(M)$ to be a [uniformly integrable martingale](@entry_id:180573) must now account for the contribution from the jumps. The Lépingle–Mémin condition provides a powerful generalization. Let $M$ be driven by a Brownian motion and a compensated random measure $\mu-\nu$, such that the jumps are given by an integral of a function $\xi$ with respect to $\mu$. A sufficient condition for $\mathcal{E}(M)$ to be a UI martingale is [@problem_id:2989047]:
$$
\mathbb{E}\left[\exp\left(\frac{1}{2}\langle M^c \rangle_T + \int_0^T \int_E \big((1+\xi)\log(1+\xi) - \xi\big) \, \nu(ds,dz) \right)\right]  \infty
$$
The integral term involving the convex function $U(y) = (1+y)\log(1+y)-y$ is the predictable compensator of the sum of $U(\Delta M_s)$. This condition elegantly combines the Novikov control on the continuous part with an "entropy-like" control on the jumps.

#### An Illustrative Example: Failure of Classical Conditions

The necessity of such generalized criteria can be vividly illustrated with an example where both Novikov's and Kazamaki's conditions fail, yet $\mathcal{E}(M)$ is a true [martingale](@entry_id:146036). Consider a purely discontinuous [local martingale](@entry_id:203733) $M_t$ representing a compensated compound Poisson process, where the jump sizes are drawn from a heavy-tailed Pareto distribution with density $f(x) = p x^{-(p+1)}$ for $x \ge 1$ and a parameter $p>2$ [@problem_id:2989038].

For such a process, any exponential moment of the martingale itself or its [quadratic variation](@entry_id:140680) will diverge. For any constants $c > 0$ and $\alpha > 0$:
- $\mathbb{E}[\exp(c \sum_{s \le T} (\Delta M_s)^2)] = \infty$, because the exponential function $e^{cx^2}$ grows faster than the polynomial decay of the Pareto tail. Thus, any Novikov-type condition fails.
- $\mathbb{E}[\exp(\alpha M_T)] = \infty$, for the same reason. Thus, any Kazamaki-type condition fails.

However, the Lépingle–Mémin criterion requires us to check the [integrability](@entry_id:142415) of the function $U(x) = (1+x)\log(1+x)-x$ against the jump-size distribution. For large $x$, $U(x)$ grows approximately as $x\log x$. The corresponding expectation involves an integral of the form $\int_1^\infty (x\log x) \cdot p x^{-(p+1)} dx = p\int_1^\infty (\log x) x^{-p} dx$. This integral converges precisely when $p>1$. Since our assumption is $p>2$, the integral is finite.

Therefore, the predictable compensator associated with the jumps is finite. As the continuous part is zero, the Lépingle-Mémin condition holds. It can be verified directly that $\mathbb{E}[\mathcal{E}(M)_T] = 1$. This example powerfully demonstrates that for processes with heavy-tailed jumps, criteria based on exponential moments are too restrictive. Finer conditions that rely on transformations with slower growth, like the entropy-like function $U(y)$, are required to correctly capture the conditions for a [change of measure](@entry_id:157887).