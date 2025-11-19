## Introduction
One-dimensional [diffusion processes](@entry_id:170696), described by stochastic differential equations (SDEs), are fundamental models for random phenomena across science and finance. While the SDE coefficients—drift and volatility—define the process's infinitesimal movements, a deeper understanding of its global behavior, from [long-term stability](@entry_id:146123) to its interaction with boundaries, requires a more powerful framework. The challenge lies in translating the local SDE dynamics into a comprehensive picture of the process's entire lifecycle.

This article introduces the [canonical representation](@entry_id:146693) of [one-dimensional diffusions](@entry_id:198610) through the lens of the **scale function** and the **speed measure**. This elegant framework, developed by pioneers like Feller and Itô, provides a complete characterization of the process's law. By mastering these concepts, you will gain a profound intuition for why a process lingers in certain regions, how it behaves at the edges of its domain, and what determines its ultimate equilibrium state.

The journey begins in **Principles and Mechanisms**, where we will formally define the [scale function and speed measure](@entry_id:186111), explore their relationship to the diffusion's generator, and uncover their physical interpretations related to [occupation time](@entry_id:199380) and stationary behavior. Next, **Applications and Interdisciplinary Connections** will demonstrate the power of this framework in practical contexts, from classifying the behavior of stock price models in finance to calculating expected [exit times](@entry_id:193122) in physics. Finally, **Hands-On Practices** will provide you with opportunities to solidify your understanding by applying these theoretical tools to concrete problems, bridging the gap between mathematical theory and computational application.

## Principles and Mechanisms

A [one-dimensional diffusion](@entry_id:181320) process, described by the stochastic differential equation (SDE) $dX_t = b(X_t)dt + \sigma(X_t)dW_t$, possesses a rich structure that can be fully characterized by a pair of mathematical objects: a **scale function** $s$ and a **speed measure** $m$. This [canonical representation](@entry_id:146693), developed by pioneers such as William Feller, Kiyosi Itô, and Henry P. McKean, Jr., provides a powerful framework for analyzing the process's behavior, from its local dynamics to its long-term stationary properties and its interaction with boundaries. This chapter elucidates the principles and mechanisms underlying this representation, with a particular focus on the role and interpretation of the speed measure.

### The Canonical Representation: Scale Function and Speed Measure

The [infinitesimal generator](@entry_id:270424) of the diffusion, which describes the expected rate of change of a [smooth function](@entry_id:158037) of the process, is given by the [differential operator](@entry_id:202628) $L$:
$$
L f(x) = \frac{1}{2} \sigma^2(x) f''(x) + b(x) f'(x)
$$
While this form is directly tied to the SDE's coefficients, a more profound understanding emerges from decomposing the generator's action into two fundamental steps, governed by the scale function and the speed measure.

#### The Scale Function

The first step in simplifying the diffusion is to find a change of spatial coordinates that eliminates the drift term. We seek a strictly increasing, twice continuously differentiable function $s(x)$ such that the transformed process $Y_t = s(X_t)$ becomes driftless, meaning it behaves locally like a time-changed Brownian motion. Applying Itô's formula to $Y_t = s(X_t)$ yields:
$$
dY_t = s'(X_t)dX_t + \frac{1}{2}s''(X_t)d\langle X \rangle_t = \left( \frac{1}{2}\sigma^2(X_t)s''(X_t) + b(X_t)s'(X_t) \right)dt + s'(X_t)\sigma(X_t)dW_t
$$
For the drift term (the term multiplying $dt$) to vanish, the function $s(x)$ must satisfy the ordinary differential equation $L s(x) = 0$. Such a function is called a **scale function** of the diffusion. Solving this ODE for $s'(x)$ reveals its structure [@problem_id:3074962]:
$$
\frac{s''(x)}{s'(x)} = -\frac{2b(x)}{\sigma^2(x)} \implies s'(x) = C \exp\left(-\int^x \frac{2b(z)}{\sigma^2(z)} dz\right)
$$
where $C$ is a positive constant. Since any positive affine transformation of a scale function, $c_1 s(x) + c_2$ with $c_1 > 0$, also satisfies $Ls=0$ and remains strictly increasing, the scale function is unique only up to such transformations. A specific choice of $s(x)$ is referred to as "a scale" for the process.

With this choice of $s$, the transformed process $Y_t = s(X_t)$ becomes a [continuous local martingale](@entry_id:188921) with dynamics $dY_t = s'(X_t)\sigma(X_t)dW_t$. This means that on its own scale, the process has no directional preference. The scale function thus encodes the "local odds" of the process, governing probabilities of hitting one point before another.

#### The Speed Measure

The process $Y_t$ is not a standard Brownian motion because its quadratic variation, $d\langle Y \rangle_t = (s'(X_t)\sigma(X_t))^2 dt$, is not constant. Instead, $Y_t$ is a Brownian motion run on a different clock. This new "intrinsic" clock is related to the speed measure.

The second canonical object, the **speed measure** $m$, is a positive measure on the state space that quantifies the "speed" at which the process moves. It is defined such that the generator $L$ can be written in the generalized Sturm-Liouville form [@problem_id:3074973]:
$$
L f = \frac{d}{dm}\left(\frac{df}{ds}\right)
$$
where $\frac{d}{ds}$ and $\frac{d}{dm}$ are [generalized derivative](@entry_id:265109) operators. If $s$ is $C^1$ and $m$ has a density $m'(x)$ with respect to Lebesgue measure, these operators are $\frac{d}{ds}f(x) = \frac{f'(x)}{s'(x)}$ and $\frac{d}{dm}g(x) = \frac{g'(x)}{m'(x)}$. Expanding this form gives:
$$
L f(x) = \frac{1}{m'(x)s'(x)} f''(x) - \frac{s''(x)}{m'(x)(s'(x))^2} f'(x)
$$
By comparing the coefficients of $f''(x)$ in this expression with the original form of $L$, we find the density of the speed measure [@problem_id:3074962]:
$$
m'(x) = \frac{2}{\sigma^2(x)s'(x)}
$$
The speed measure is unique up to a positive multiplicative constant. However, this constant is linked to the choice of scale function. If the scale is changed from $s$ to $\tilde{s} = c_1 s + c_2$, the generator is preserved if the speed measure is changed from $m$ to $\tilde{m} = m/c_1$. This interdependence is crucial.

This [canonical representation](@entry_id:146693) is remarkably powerful. The pair $(s, m)$, combined with a specification of behavior at the boundaries of the state space, uniquely determines the law of the [one-dimensional diffusion](@entry_id:181320) process [@problem_id:3074973].

### The Physical Interpretation of the Speed Measure

The definition of the speed measure via the generator's [canonical form](@entry_id:140237) may seem abstract. Its physical meaning becomes clearer when we consider its role in governing the time a process spends in different regions.

#### Diffusions in Natural Scale

A particularly insightful case is a diffusion in its **natural scale**, where the scale function can be chosen as $s(x)=x$. This occurs if and only if the drift coefficient $b(x)$ is identically zero. The SDE is $dX_t = \sigma(X_t)dW_t$, and the generator simplifies to $L f(x) = \frac{1}{2}\sigma^2(x)f''(x)$. In this case, since $s'(x)=1$, the speed measure density is simply [@problem_id:3074965]:
$$
m'(x) = \frac{2}{\sigma^2(x)}
$$
This formula provides a direct intuition: the speed measure density is large where the diffusion coefficient $\sigma(x)$ is small, and small where $\sigma(x)$ is large. A small diffusion coefficient means the process moves sluggishly and its random fluctuations are small, causing it to "spend more time" in that region. Conversely, a large diffusion coefficient implies rapid, wide fluctuations, allowing the process to quickly move away. The speed measure quantifies this inverse relationship between the local "speed" of the process and the magnitude of its random movements.

#### Occupation Time and Local Time

The most precise interpretation of the speed measure comes from the **occupation times formula**. This formula relates the total time the process $X_t$ spends in various parts of its state space, weighted by a function $g(x)$, to its local time. The **local time**, denoted $L_t^y$, is a random process that measures the amount of time $X_t$ has spent "at" the level $y$ up to time $t$. The occupation times formula states that for any suitable function $g$ [@problem_id:3074937]:
$$
\int_0^t g(X_s) ds = \int_I g(y) L_t^y m(dy)
$$
where $m(dy) = m'(y)dy$ is the speed measure.

This identity is profound. It shows that the speed measure density $m'(y)$ is precisely the factor that converts the measure of "wiggling" at point $y$ ([local time](@entry_id:194383)) into "clock time" ([occupation time](@entry_id:199380)). If the speed measure density $m'(y)$ is large at a point $y$, it means that each unit of [local time](@entry_id:194383) accumulated at $y$ contributes a large amount to the total [occupation time](@entry_id:199380). In colloquial terms, a large speed measure density signifies that the process moves slowly.

The factor of 2 in the conventional definition of the speed measure arises from the relationship between the generator-based diffusion local time $L_t^y$ and the symmetric [local time](@entry_id:194383) $\ell_t^y$ from [semimartingale](@entry_id:188438) theory. Specifically, for a diffusion in natural scale, one can show that $L_t^y = \frac{1}{2}\ell_t^y$, and this factor of $\frac{1}{2}$ is absorbed into the definition of $m'(x)$ to maintain the elegance of the occupation times formula [@problem_id:3074934].

### Speed Measure and Long-Term Behavior

The speed measure is not just a descriptor of transient dynamics; it is fundamental to the long-term, or stationary, behavior of the process.

#### Reflecting Boundaries and Stationary Distributions

Consider a diffusion on a finite interval $[a,b]$ with **[reflecting boundaries](@entry_id:199812)**. This means the process is pushed back into the interior whenever it hits an endpoint, ensuring that no probability mass is lost. Such a process can reach an equilibrium, described by a **stationary probability measure** $\pi$. This is a probability distribution that does not change over time. A measure $\pi$ is stationary if and only if $\int Lf d\pi = 0$ for all functions $f$ in the generator's domain, which for [reflecting boundaries](@entry_id:199812) includes the Neumann conditions $f'(a)=f'(b)=0$ [@problem_id:3074933].

This condition is equivalent to the stationary Fokker-Planck equation, which states that the probability flux $J(x) = b(x)p(x) - \frac{1}{2}\frac{d}{dx}(\sigma^2(x)p(x))$ must be constant, where $p(x)$ is the density of $\pi$. Reflecting boundaries imply this flux is zero everywhere. Setting $J(x)=0$ and solving for $p(x)$ reveals a remarkable result [@problem_id:3074938]:
$$
p(x) \propto \frac{1}{\sigma^2(x)} \exp\left(\int^x \frac{2b(z)}{\sigma^2(z)} dz\right)
$$
Recalling the formulas for $s'(x)$ and $m'(x)$, we see that this is precisely proportional to the speed measure density:
$$
p(x) \propto \frac{1}{\sigma^2(x) s'(x)} = \frac{1}{2} m'(x)
$$
This establishes a central principle: **for a diffusion with [reflecting boundaries](@entry_id:199812), the stationary probability density is proportional to the speed measure density.** The process spends most of its time in regions where the speed measure is largest. For a stationary *probability* measure to exist, the total speed measure of the interval, $\int_a^b m'(x)dx$, must be finite, allowing for normalization [@problem_id:3074938].

#### Absorbing Boundaries and Quasi-Stationary Distributions

When the boundaries are **absorbing**, the process is killed upon hitting them. In this case, probability mass continuously leaks out of the system, and no non-trivial stationary probability measure can exist [@problem_id:3074926].

However, one can study the long-term behavior of the population of *survivors*. The distribution of the process at time $t$, conditioned on not having been absorbed by time $t$, often converges to a **[quasi-stationary distribution](@entry_id:753961) (QSD)**, $\nu$. Even though no true [stationary state](@entry_id:264752) exists, the speed measure remains centrally important. The QSD is not proportional to the speed measure itself, but is given by a density with respect to the speed measure. Specifically, if $\eta(x)$ is the principal eigenfunction of the generator $L$ with Dirichlet (absorbing) boundary conditions, the QSD is given by [@problem_id:3074926]:
$$
d\nu(x) = C \cdot \eta(x) m(dx)
$$
where $C$ is a [normalization constant](@entry_id:190182). The speed measure acts as the underlying "reference" measure that determines the shape of the limiting [conditional distribution](@entry_id:138367).

### Speed Measure and Boundary Behavior

The influence of the [scale function and speed measure](@entry_id:186111) extends all the way to the boundaries of the state space, determining their very nature.

#### Feller's Boundary Classification

Feller's celebrated boundary classification categorizes a boundary point (say, $l$) as **regular, exit, entrance, or natural**. This classification depends on whether the boundary is accessible from the interior and whether the process can escape from the boundary into the interior. These properties are determined by the finiteness of two integrals that involve both the scale function and the speed measure [@problem_id:3074936]:
*   $I_l = \int_{l}^{x_0} (s(x_0) - s(y)) m(dy)$
*   $J_l = \int_{l}^{x_0} (s(y) - s(l)) m(dy)$

A boundary is regular (accessible and escapable) if both integrals are finite. It is natural (inaccessible and inescapable) if both are infinite. The mixed cases correspond to exit and entrance boundaries. This classification demonstrates that the pair $(s,m)$ is a complete characterization of the diffusion's local and global properties.

#### Sticky Boundaries

The speed measure framework is flexible enough to model more exotic behaviors, such as **sticky boundaries**. A sticky boundary is a point where the process can arrive and remain for a positive amount of time before continuing its motion. This is modeled by allowing the speed measure to have an atom (a [point mass](@entry_id:186768)) at the boundary. For a boundary at $0$, the speed measure might take the form [@problem_id:3074947]:
$$
m(dx) = \rho(x)dx + \theta \delta_0(dx)
$$
where $\rho(x)$ is the continuous density in the interior and $\theta > 0$ is the mass of the atom at $0$. This atomic mass leads to a modified boundary condition for functions in the generator's domain, known as a Wentzell boundary condition:
$$
f'(0+) = \theta Lf(0)
$$
The magnitude of $\theta$ is proportional to the "stickiness" of the boundary. In the limit $\theta \to 0$, the atom vanishes, and we recover the standard reflecting (Neumann) boundary condition $f'(0+) = 0$. This illustrates how the speed measure provides a unified and powerful language for describing a wide spectrum of boundary behaviors.