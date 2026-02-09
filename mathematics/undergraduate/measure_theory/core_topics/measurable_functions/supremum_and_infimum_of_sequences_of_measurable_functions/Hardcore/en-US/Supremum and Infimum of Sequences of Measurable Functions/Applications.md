## Applications and Interdisciplinary Connections

The preceding chapters established that the class of measurable functions is remarkably robust, remaining closed under the fundamental operations of taking pointwise suprema, infima, limits superior, and limits inferior. While these results are cornerstones of measure theory in their own right, their true power is revealed when they are applied to construct new objects, prove foundational theorems, and forge connections between disparate fields of mathematics and science. This chapter explores a selection of these applications, demonstrating how the stability of measurability under limiting operations provides the essential framework for modern analysis, probability theory, and beyond. We will see that from the very definition of the Lebesgue integral to advanced problems in materials science and stochastic control, these principles are not mere technicalities but indispensable tools for both theory and practice.

### Foundational Applications in Analysis

The utility of suprema and infima of functions is first and most fundamentally apparent within the architecture of real and functional analysis itself. These operations are not simply tools to be applied to measurable functions; they are integral to the very definition of the core concepts of the field.

#### The Definition of the Lebesgue Integral

The construction of the Lebesgue integral begins with simple functions, for which the integral is an elementary sum. To extend this definition to a general non-negative measurable function $f$, one must approximate $f$ with these simpler objects. The Lebesgue integral of $f$ is defined as the supremum of the integrals of all simple functions $\phi$ that are bounded above by $f$. Formally, if $S(f)$ is the set of all non-negative simple functions $\phi$ such that $0 \le \phi(x) \le f(x)$ for all $x$, the Lebesgue integral is defined as:
$$
\int_X f \, d\mu = \sup_{\phi \in S(f)} \left\{ \int_X \phi \, d\mu \right\}
$$
This definition relies on taking a supremum over what is typically an uncountable set of function values. The foundational results on the measurability of suprema of *sequences* of functions are what allow us to connect this abstract definition to a more concrete computational tool. The Monotone Convergence Theorem, for instance, guarantees that this supremum can be realized as the limit of integrals of a specific, explicit, and monotonically increasing sequence of simple functions that converge pointwise to $f$. Thus, the concept of a supremum lies at the very heart of Lebesgue's theory of integration.

#### Characterizing Points of Continuity

A central question in analysis is to understand the structure of the set of points where a given function is continuous. The concept of the oscillation of a function provides a precise answer, and its definition relies on infima and suprema. For a function $f: X \to \mathbb{R}$ on a metric space $X$, the oscillation of $f$ at a point $x$ is defined as:
$$
\omega_f(x) = \inf_{\delta  0} \left( \sup_{y, z \in B(x, \delta)} |f(y) - f(z)| \right)
$$
where $B(x, \delta)$ is the open ball of radius $\delta$ around $x$. A function $f$ is continuous at $x$ if and only if $\omega_f(x) = 0$. The measurability of the oscillation function $\omega_f$ is a direct consequence of the stability properties we have studied. By considering a sequence of radii $\delta_n = 1/n$ tending to zero, the infimum can be expressed over a countable set:
$$
\omega_f(x) = \inf_{n \in \mathbb{N}} \left( \sup_{y, z \in B(x, 1/n)} |f(y) - f(z)| \right)
$$
For a measurable function $f$, one can show that each function in the sequence, $S_n(x) = \sup_{y, z \in B(x, 1/n)} |f(y) - f(z)|$, is measurable. Consequently, their infimum, $\omega_f(x)$, is also measurable. This has a profound implication: for any measurable function, the set of points where it is continuous, $\{x \in X \mid \omega_f(x) = 0\}$, is a measurable set. This result provides a powerful analytical tool, for instance, in showing that the characteristic function of a generalized Cantor set is continuous only on the complement of the set, a property that allows for the computation of the integral of its oscillation.

#### Generalizing the Derivative: Dini Derivatives

For functions that are not differentiable in the classical sense, it is often useful to consider weaker notions of derivatives. The Dini derivatives serve this purpose. For a function $F: \mathbb{R} \to \mathbb{R}$, the upper right Dini derivative, for example, is defined as:
$$
D^+F(x) = \limsup_{h \to 0^+} \frac{F(x+h) - F(x)}{h}
$$
The definition itself is a limit superior. To establish that $D^+F$ is a measurable function when $F$ is continuous, one expresses the limit superior as an infimum of suprema:
$$
D^+F(x) = \inf_{n \in \mathbb{N}} \left( \sup_{0  h  1/n} \frac{F(x+h) - F(x)}{h} \right)
$$
Because the inner function is continuous in $h$, the supremum over the interval $(0, 1/n)$ is the same as the supremum over the rational numbers in that interval. This reduces the uncountable supremum to a countable one. The function $x \mapsto \frac{F(x+h)-F(x)}{h}$ is continuous for fixed $h$. Thus, $D^+F$ is the infimum of a sequence of functions, each of which is the supremum of a countable collection of continuous (and thus measurable) functions. By the stability theorems, $D^+F$ is measurable. This measurability is not a mere curiosity; it is a prerequisite for foundational results in real analysis, such as the Denjoy-Young-Saks theorem, which provides a complete description of the behavior of Dini derivatives for arbitrary functions.

### Connections to Probability and Ergodic Theory

The language of measure theory provides the rigorous foundation for modern probability theory, where a probability space is a measure space of total measure one, and random variables are measurable functions. In this context, the stability of measurability under limiting operations is of paramount importance.

#### Limits of Random Variables

A sequence of random variables $\{X_n\}$ represents an evolving random process. A fundamental question is whether the limiting behavior of this sequence is itself a well-defined random variable. The answer is yes, and the proof relies directly on the principles of this section. For instance, the limit superior $Y = \limsup_{n \to \infty} X_n$ is a random variable if each $X_n$ is. To prove this, one must show that the set $\{Y \le a\}$ is a measurable event for any real number $a$. This is achieved by expressing the event using only countable set operations on the events associated with the individual $X_n$:
$$
\{Y \le a\} = \bigcap_{m=1}^{\infty} \bigcup_{n=1}^{\infty} \bigcap_{k=n}^{\infty} \{X_k \le a + \frac{1}{m}\}
$$
Since each set on the right-hand side is measurable by the definition of a random variable, and sigma-algebras are closed under countable unions and intersections, the set on the left-hand side is also measurable. This ensures that long-term behaviors of sequences of random variables, such as those described in the Borel-Cantelli lemmas, are themselves well-defined random quantities.

#### Hitting Times and Stopping Times

In the study of stochastic processes and dynamical systems, a key concept is the "first hitting time," which is the first time a process enters a specified target set. Given a sequence of measurable functions $\{f_n\}$ and a measurable set $A$, the first hitting time is defined as:
$$
\tau(x) = \inf\{n \ge 1 \mid f_n(x) \in A\}
$$
with the convention that $\inf(\emptyset) = \infty$. The function $\tau$ is measurable. This can be seen by observing that for any integer $k \ge 1$, the event $\{\tau(x) \le k\}$ is equivalent to the statement "there exists at least one $n \in \{1, \dots, k\}$ such that $f_n(x) \in A$." This allows us to write the level set as a finite union of measurable sets:
$$
\{\tau(x) \le k\} = \bigcup_{n=1}^k f_n^{-1}(A)
$$
Since finite unions of measurable sets are measurable, $\tau$ is a measurable function. This concept is central to the theory of stochastic processes, where it is known as a stopping time, a crucial ingredient for martingale theory and its applications in mathematical finance. The same principle applies in ergodic theory, where one might study the first passage time of a point's orbit into a certain region of the state space under a transformation. This idea of a first time something happens also appears in contexts like analyzing runs of digits in binary expansions, where the length of a run can be defined as an infimum, thereby guaranteeing its measurability.

#### Long-Term Behavior in Dynamical Systems

In ergodic theory, one is interested in the long-term statistical behavior of a dynamical system $(X, \mathcal{M}, \mu, T)$, where $T$ is a measure-preserving transformation. Given an observable (a measurable function) $g$, one can study the sequence of observations along an orbit, $f_n(p) = g(T^n p)$. The limit superior and limit inferior of this sequence, $L^+(p) = \limsup_n f_n(p)$ and $L^-(p) = \liminf_n f_n(p)$, describe the range of values the system revisits infinitely often. The measurability of $L^+$ and $L^-$ ensures they are valid observables of the system. For ergodic systems on compact spaces, a remarkable result emerges: for almost every starting point $p$, the orbit $\{T^n p\}$ is dense in the space $X$. If $g$ is continuous, this implies that the sequence of values $g(T^n p)$ will eventually get arbitrarily close to every value in the range of $g$. Consequently, for almost every $p$:
$$
L^+(p) = \sup_{q \in X} g(q) \quad \text{and} \quad L^-(p) = \inf_{q \in X} g(q)
$$
In this way, the pointwise limiting behavior of a sequence of functions reveals global, deterministic properties of the underlying function $g$. This powerful connection between dynamics and analysis is enabled by the robust measurability properties of limsup and liminf.

### Advanced Applications in Functional Analysis and PDEs

The principles of measurability for suprema and infima are indispensable in more advanced areas of analysis, where functions are themselves treated as points in an abstract space.

#### The Hardy-Littlewood Maximal Function

A central object in harmonic analysis is the Hardy-Littlewood maximal function. For a locally integrable function $f$ on $\mathbb{R}^d$, it is defined as:
$$
Mf(x) = \sup_{r  0} \frac{1}{\mu(B(x,r))} \int_{B(x,r)} |f(t)| \, d\mu(t)
$$
This function provides a pointwise upper bound on the averages of $|f|$ over balls centered at $x$. Its definition involves a supremum over an *uncountable* set of radii $r$. To prove that $Mf$ is measurable, a two-step argument is employed. First, one shows that for a fixed $x$, the map $r \mapsto A_r(x) = \frac{1}{\mu(B(x,r))} \int_{B(x,r)} |f(t)| \, d\mu(t)$ is continuous. This continuity allows the uncountable supremum over $r0$ to be replaced by a countable supremum over rational radii $r \in \mathbb{Q}_{0}$, without changing the value. Second, for a fixed rational radius $r$, the function $x \mapsto A_r(x)$ is continuous (and therefore measurable). Thus, $Mf$ is the supremum of a countable collection of measurable functions, making it measurable. The measurability of $Mf$ is the first step in proving the famous Hardy-Littlewood maximal inequality, a cornerstone result used to establish the Lebesgue differentiation theorem and other almost-everywhere convergence results.

#### Properties of Function Spaces ($L^p$)

The theory of $L^p$ spaces, which are fundamental in functional analysis and PDEs, relies heavily on consequences of the measurability of suprema. For instance, a powerful result states that if $\{f_n\}$ is a sequence of functions in $L^p(X, \mu)$ for $p \in 1, \infty)$ such that the series of their norms converges, $\sum_{n=1}^\infty \|f_n\|_p  \infty$, then the function defined by the [pointwise supremum, $g(x) = \sup_n |f_n(x)|$, also belongs to $L^p(X, \mu)$. The proof leverages the triangle inequality and the completeness of $L^p$ spaces to show that the function $h(x) = \sum_{n=1}^\infty |f_n(x)|$ is in $L^p$. Since $g(x) \le h(x)$ almost everywhere, it follows that $g$ must also be in $L^p$.

It is crucial, however, to distinguish this from the commutation of integrals and suprema. In general, $\int (\sup_n f_n) \, d\mu \neq \sup_n (\int f_n \, d\mu)$. Indeed, it is easy to construct sequences of functions for which the supremum of the integrals is a finite value, while the integral of the supremum is a different finite value, or even infinite. This non-commutativity is precisely what motivates Fatou's Lemma and the Monotone and Dominated Convergence Theorems, which provide conditions under which some form of commutation (or inequality) holds.

#### Viscosity Solutions of PDEs

In modern PDE theory, particularly for fully non-linear equations like the Hamilton-Jacobi-Bellman (HJB) equations arising in stochastic optimal control, solutions are often not smooth enough to be classical solutions. Instead, they are understood in a weak sense as "viscosity solutions." The value function of a control problem is typically defined as an infimum over a set of admissible controls. The theory of viscosity solutions includes a critical stability property: the supremum of a family of viscosity subsolutions is a viscosity subsolution, and dually for infima of supersolutions. This property is the theoretical engine behind powerful approximation and construction methods. For example, in the "vanishing viscosity" method, one regularizes the equation with a small parameter $\varepsilon$, finds a smooth solution $u^\varepsilon$, and then passes to the limit as $\varepsilon \to 0$. The stability theorem for viscosity solutions guarantees that the limit of the $u^\varepsilon$ is a viscosity solution to the original, non-regularized equation. These methods are fundamental to the existence and uniqueness theory for HJB equations and are indispensable in mathematical finance and control theory.

### Connections to Materials Science and Calculus of Variations

The formation of complex patterns and microstructures in materials like alloys, crystals, and composites can be modeled using the calculus of variations, where one seeks to minimize an energy functional. For an elastic material, this energy may take the form $I(u) = \int_\Omega W(\nabla u) \, dx$, where $u$ represents the deformation and $W$ is the stored energy density function.

If $W$ is not well-behaved (specifically, not "quasiconvex"), a minimizer may not exist. Instead, minimizing sequences develop progressively finer oscillations, forming a "microstructure." The physically observed macroscopic behavior corresponds to a relaxed energy, whose density is given by the quasiconvex envelope, $QW$. This envelope is defined as the greatest quasiconvex function that lies below $W$:
$$
QW(F) = \sup \{ g(F) \mid g \text{ is quasiconvex and } g \le W \}
$$
Equivalently, $QW$ can be computed via a "cell formula," which involves taking an infimum of the average energy over an infinite-dimensional space of admissible deformations. These definitions, built upon suprema and infima over entire classes of functions, are essential for predicting the effective properties of composite materials and the morphology of phase transformations. The mathematical framework for understanding these physical phenomena is thus deeply rooted in the analytical principles of taking suprema and infima of functions.

In conclusion, the measurability of suprema, infima, and their limiting counterparts is far more than a technical lemma. It is a generative principle that enables the construction and analysis of some of the most important objects in modern mathematics, with profound and far-reaching consequences in probability, dynamics, analysis, and the physical sciences.