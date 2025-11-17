## Introduction
The analysis of feedback systems containing uncertain or hard-to-model nonlinear components is a persistent challenge in control engineering. While stability can often be verified for a single, well-defined nonlinearity, how can we guarantee stability when the nonlinear element is only known to belong to a certain class of functions? This is the fundamental question of [absolute stability](@entry_id:165194), a powerful concept that provides [robust stability](@entry_id:268091) guarantees for an entire family of nonlinearities, not just a single instance. Addressing this knowledge gap is crucial for designing reliable control systems that can withstand variations in components like saturating actuators or devices with dead-zones.

This article provides a comprehensive exploration of two of the most important tools in [absolute stability](@entry_id:165194) theory: the Circle Criterion and the Popov Criterion. We will move beyond simple graphical tests to uncover their deep theoretical underpinnings. The journey begins in **Principles and Mechanisms**, where we will formally define the [absolute stability](@entry_id:165194) problem and derive both criteria from a unified viewpoint of passivity and Lyapunov theory. Next, in **Applications and Interdisciplinary Connections**, we will translate this theory into practice, demonstrating how to model common engineering nonlinearities and apply the criteria in case studies, while also exploring connections to [robust control](@entry_id:260994) and the modern IQC framework. Finally, the **Hands-On Practices** section will provide opportunities to apply these concepts through guided problem-solving, solidifying your understanding of these essential analytical techniques.

## Principles and Mechanisms

The analysis of [feedback systems](@entry_id:268816) comprising a known linear time-invariant (LTI) element and a "difficult" or uncertain nonlinear element is a central theme in control theory. This chapter delves into the core principles of [absolute stability](@entry_id:165194), a powerful framework for guaranteeing [robust stability](@entry_id:268091) in the face of such nonlinear uncertainty. We will develop the two cornerstone results of this field—the Circle and Popov criteria—not merely as graphical tests, but as direct consequences of a unified theory based on passivity and Lyapunov stability.

### The Problem of Absolute Stability

Consider the canonical feedback system, often referred to as a **Lur'e system**, composed of a known LTI plant with transfer function $G(s)$ and a static, memoryless nonlinearity $\phi(\cdot)$ subject to a [negative feedback](@entry_id:138619) law $u = -\phi(y)$. The fundamental challenge arises when the [exact form](@entry_id:273346) of $\phi(\cdot)$ is unknown. We may only know that it belongs to a specific class of functions, for instance, those confined to a given sector.

The question of **[absolute stability](@entry_id:165194)** is then one of [robust stability](@entry_id:268091): is the equilibrium of the unforced system (typically the origin) globally asymptotically stable not just for one specific nonlinearity, but for *every* possible nonlinearity within the prescribed class? This is a substantially stronger requirement than verifying stability for a single, fixed nonlinear function. As such, [absolute stability](@entry_id:165194) is a guarantee of robustness against variations or uncertainties in the nonlinear component [@problem_id:2689020].

It is crucial to distinguish this concept from other forms of stability. **Internal stability**, as it is often termed, refers to the stability of the system's state for one fixed nonlinearity. Absolute stability demands this property hold for an entire family of nonlinearities. It is also distinct from **Bounded-Input Bounded-Output (BIBO) stability**, which is an input-output property concerning the system's response to external forcing signals. Absolute stability, in contrast, is fundamentally a property of the internal state dynamics of the autonomous (unforced) system, focusing on the convergence of all trajectories to the equilibrium.

### Characterizing the Nonlinearity: Sector and Slope Conditions

To make the problem tractable, we must mathematically define the class of admissible nonlinearities. The most common and useful characterization is the **[sector condition](@entry_id:175672)**. A nonlinearity $\phi(\cdot)$ is said to belong to the sector $[k_1, k_2]$ if, for all its inputs $y \neq 0$, the inequality
$$
k_1 \le \frac{\phi(y)}{y} \le k_2
$$
holds. This is equivalent to stating that the graph of the function $\phi(y)$ lies between the lines $y=k_1 x$ and $y=k_2 x$. Assuming $\phi(0)=0$, this can be written as a quadratic inequality:
$$
(\phi(y) - k_1 y)(k_2 y - \phi(y)) \ge 0 \quad \text{for all } y \in \mathbb{R}.
$$

A related, but stricter, condition is that of **slope restriction**. A differentiable nonlinearity is slope-restricted in $[k_1, k_2]$ if its derivative is bounded:
$$
k_1 \le \frac{d\phi}{dy}(y) \le k_2
$$
for almost every $y$. By the Mean Value Theorem (or, more generally, integrating the derivative for [absolutely continuous functions](@entry_id:158609)), slope restriction implies a bound on the secant slope between any two points $y_1$ and $y_2$:
$$
k_1 \le \frac{\phi(y_1) - \phi(y_2)}{y_1 - y_2} \le k_2
$$
If we add the common assumption that the nonlinearity passes through the origin, $\phi(0)=0$, and set $y_2=0$, the [secant condition](@entry_id:164914) immediately reduces to the [sector condition](@entry_id:175672). Therefore, a slope-restricted nonlinearity in $[k_1, k_2]$ with $\phi(0)=0$ is also sector-bounded in $[k_1, k_2]$.

However, the converse is not true: a function can be sector-bounded without being slope-restricted in the same interval [@problem_id:2689000]. A simple [piecewise linear function](@entry_id:634251) that oscillates within the sector but has segments with slopes outside $[k_1, k_2]$ serves as a [counterexample](@entry_id:148660). This distinction is important: the classical Circle and Popov criteria, which we will derive, only require the weaker [sector condition](@entry_id:175672).

### A Unified Viewpoint: Dissipativity and Lyapunov Stability

The seemingly distinct frequency-domain criteria for [absolute stability](@entry_id:165194) are elegantly unified by the theory of **[dissipativity](@entry_id:162959)**. The core idea is to analyze stability in terms of an energy-like quantity, described by a **storage function** $V(x)$, and the rate at which this quantity is supplied to or dissipated from the system, known as the **supply rate** $s(u, y)$. A system is dissipative if the rate of change of its storage, $\dot{V}(x)$, is no greater than the supply rate.

For the Lur'e system, we can partition the system into the LTI plant and the nonlinearity and analyze their dissipative properties separately. The [sector condition](@entry_id:175672) on the nonlinearity provides a key constraint. With the feedback law $u = -\phi(y)$, the inequality $(\phi(y) - k_1 y)(k_2 y - \phi(y)) \ge 0$ becomes an inequality on the plant's input $u$ and output $y$:
$$
(-u - k_1 y)(k_2 y - (-u)) \ge 0 \implies (u + k_1 y)(u + k_2 y) \le 0
$$
Expanding this gives:
$$
u^2 + (k_1 + k_2)uy + k_1 k_2 y^2 \le 0
$$
Multiplying by $-1$ reverses the inequality, and rearranging terms gives:
$$
-k_1 k_2 y^2 - (k_1 + k_2)uy - u^2 \ge 0
$$
This expression is a [quadratic form](@entry_id:153497) in $(y, u)$, which can be written as $\begin{bmatrix} y  u \end{bmatrix} \Pi \begin{bmatrix} y \\ u \end{bmatrix} \ge 0$, where $\Pi$ is a symmetric matrix. One such matrix is:
$$
\Pi = \begin{pmatrix} -k_1 k_2  -\frac{k_1+k_2}{2} \\ -\frac{k_1+k_2}{2}  -1 \end{pmatrix}
$$
This inequality means that the nonlinearity, as seen from the perspective of the LTI plant, has a supply rate $s_{\text{NL}}(u,y) = \begin{bmatrix} y  u \end{bmatrix} \Pi \begin{bmatrix} y \\ u \end{bmatrix}$ that is always non-negative [@problem_id:2730756].

For the entire closed-loop system to be stable, the LTI plant must "absorb" or dissipate this "energy". Specifically, if the LTI plant is dissipative with respect to the supply rate $-s_{\text{NL}}(u,y)$, then there exists a positive definite storage function $V(x)$ for the plant such that:
$$
\dot{V}(x) \le -s_{\text{NL}}(u,y) = - \begin{bmatrix} y  u \end{bmatrix} \Pi \begin{bmatrix} y \\ u \end{bmatrix}
$$
Since the right-hand side is guaranteed to be non-positive by the [sector condition](@entry_id:175672), we have $\dot{V}(x) \le 0$. This establishes that $V(x)$ is a **Lyapunov function** for the closed-loop system, proving its stability. With slightly stronger conditions (strict inequality and detectability), one can prove [global asymptotic stability](@entry_id:187629).

### The Circle Criterion: A Frequency-Domain Test from Passivity

The power of the [dissipativity](@entry_id:162959) framework is that it connects directly to the frequency domain via the celebrated **Kalman-Yakubovich-Popov (KYP) Lemma**. For a minimal, stable LTI system, the existence of a quadratic storage function $V(x) = x^T P x$ satisfying the [dissipation inequality](@entry_id:188634) is equivalent to a corresponding frequency-domain inequality (FDI).

For the LTI plant to be dissipative with supply rate $-\begin{bmatrix} y  u \end{bmatrix} \Pi \begin{bmatrix} y \\ u \end{bmatrix}$, the KYP lemma requires the following FDI to hold for all $\omega \in \mathbb{R}$:
$$
\begin{bmatrix} G(j\omega)^*  1 \end{bmatrix} (-\Pi) \begin{bmatrix} G(j\omega) \\ 1 \end{bmatrix} \ge 0
$$
Substituting our matrix $\Pi$ gives:
$$
\begin{bmatrix} G(j\omega)^*  1 \end{bmatrix} \begin{pmatrix} k_1 k_2  \frac{k_1+k_2}{2} \\ \frac{k_1+k_2}{2}  1 \end{pmatrix} \begin{bmatrix} G(j\omega) \\ 1 \end{bmatrix} \ge 0
$$
Expanding this expression yields the inequality:
$$
k_1 k_2 |G(j\omega)|^2 + (k_1+k_2)\Re\{G(j\omega)\} + 1 \ge 0
$$
This is the analytical form of the **Circle Criterion**. For stability, we typically require a strict inequality. The boundary of this condition, where the expression equals zero, defines a circle (or a line, in degenerate cases) in the complex plane. If the Nyquist plot of $G(j\omega)$ avoids this "forbidden" region, [absolute stability](@entry_id:165194) is guaranteed.

To see that this defines a circle, let $G(j\omega) = x + iy$. The boundary equation becomes:
$$
k_1 k_2 (x^2+y^2) + (k_1+k_2)x + 1 = 0
$$
Assuming $k_1 k_2 \ne 0$, we can complete the square to find the [equation of a circle](@entry_id:167379):
$$
\left(x + \frac{k_1+k_2}{2k_1 k_2}\right)^2 + y^2 = \left(\frac{k_2-k_1}{2k_1 k_2}\right)^2
$$
This circle is centered on the real axis at $c = -\frac{k_1+k_2}{2k_1 k_2}$ with radius $r = \frac{k_2-k_1}{2|k_1 k_2|}$ [@problem_id:2688998]. It is straightforward to verify that this circle passes through the critical points $-1/k_1$ and $-1/k_2$ on the real axis. For instance, if we have a sector $[0.2, 1.5]$, the criterion requires the Nyquist plot of $G(s)$ to avoid the interior of a circle with center $c = -17/6$ and radius $r = 13/6$ [@problem_id:2688998].

In the common special case of a sector $[0, k]$, where $k_1=0$, the inequality simplifies dramatically to $k\Re\{G(j\omega)\} + 1 > 0$, or:
$$
\Re\{G(j\omega)\} > -\frac{1}{k}
$$
This requires the Nyquist plot of $G(j\omega)$ to remain entirely to the right of the vertical line at $\Re\{z\} = -1/k$.

### The Popov Criterion: Reducing Conservatism

The Circle Criterion is a powerful tool, but it can be conservative. This conservatism stems from its origin in a simple quadratic Lyapunov function, $V(x) = x^T P x$. We can obtain a more powerful, less conservative criterion by employing a more sophisticated Lyapunov function.

The **Popov Criterion** arises from considering an augmented Lyapunov candidate, often called a **Lur'e-Popov function**, which includes an integral term related to the nonlinearity. For a sector $[0, k]$, a common form is:
$$
V(x) = x^T P x + 2q \int_0^y \phi(\sigma) d\sigma
$$
where $P=P^T \succ 0$ and $q \ge 0$ is a free scalar parameter to be chosen. The time derivative of this function along system trajectories introduces cross-terms involving $\dot{y}$, which, after applying the KYP lemma, leads to a frequency-dependent multiplier in the FDI. For a strictly proper $G(s)$ and a sector $[0, k]$, this procedure yields the **Popov inequality**: There must exist some $q \ge 0$ such that for all $\omega \ge 0$,
$$
\Re\{(1+j\omega q)G(j\omega)\} + \frac{1}{k} > 0
$$
This is the celebrated **Popov Criterion** [@problem_id:2689028]. The term $1+j\omega q$ is the **Popov multiplier**. Geometrically, this criterion requires that a modified frequency plot, the **Popov plot** of $G(j\omega)$ (where the real part is $\Re\{G(j\omega)\}$ and the imaginary part is $\omega \Im\{G(j\omega)\}$), lies to the right of a line whose slope is determined by $q$. The freedom to choose any non-negative $q$ provides an extra degree of freedom, allowing the test to "bend" the stability boundary in the frequency domain to better fit the shape of the system's Nyquist plot, thereby reducing conservatism. The Circle Criterion is simply the special case of the Popov Criterion where $q=0$.

### Comparing the Criteria: An Illustrative Example

The benefit of the Popov criterion is not merely theoretical; it can lead to dramatically less conservative results. Consider a plant with the transfer function $G(s) = \frac{1}{(s+1)^3}$ and a nonlinearity in the sector $[0, k]$ [@problem_id:2721617].

1.  **Circle Criterion ($q=0$)**: We must satisfy $\Re\{G(j\omega)\} > -1/k$. The real part is $\Re\{G(j\omega)\} = \frac{1-3\omega^2}{(1+\omega^2)^3}$. Finding its minimum value, which occurs at $\omega^2=1$, gives $\inf_{\omega} \Re\{G(j\omega)\} = -1/4$. The criterion thus requires $-1/4 > -1/k$, which implies $k  4$.

2.  **Popov Criterion ($q \ge 0$)**: We must satisfy $\Re\{(1+j\omega q)G(j\omega)\}  -1/k$. A careful optimization over the free parameter $q$ reveals that the optimal choice is $q=1$. For this choice, the [infimum](@entry_id:140118) of the Popov function $\Re\{(1+j\omega)G(j\omega)\}$ is found to be $-1/8$. The stability condition becomes $-1/8  -1/k$, which implies $k  8$.

In this example, the Popov criterion certifies stability for a sector twice as large as the Circle Criterion, demonstrating its power to reduce conservatism. In some cases, the improvement is even more dramatic. For the plant $G(s) = \frac{1}{(s+1)(s+2)}$, the Circle Criterion yields a finite stability bound of $k_{\max} = 9+6\sqrt{2}$. The Popov Criterion, however, by choosing $q \ge 1/3$, can show that the Popov function $\Re\{(1+j\omega q)G(j\omega)\}$ is non-negative for all frequencies. This means the criterion is satisfied for *any* $k  0$, giving an infinite stability bound [@problem_id:2689004].

### Scope, Limitations, and Extensions

The standard forms of the Circle and Popov criteria rely on several key assumptions, which define their scope of applicability.

*   **Strict Stability of $G(s)$**: The proofs via the KYP lemma are formulated for systems where the state matrix $A$ is Hurwitz (all eigenvalues in the open [left-half plane](@entry_id:270729)). This ensures a baseline of stability for the linear part.

*   **Relative Degree Constraint**: The Popov criterion is fundamentally a positive-realness test on the weighted transfer function $(1+qs)G(s)$. For a [rational function](@entry_id:270841) to be positive real, its [relative degree](@entry_id:171358) (degree of denominator minus degree of numerator) can be at most 1. Since the multiplier $(1+qs)$ reduces the [relative degree](@entry_id:171358) of $G(s)$ by one, the standard Popov criterion is only applicable to plants where the [relative degree](@entry_id:171358) of $G(s)$ is at most 2 [@problem_id:2689023].

These limitations can be overcome. For plants with [relative degree](@entry_id:171358) higher than 2, one can employ more general **dynamic multipliers** (often called Zames-Falb multipliers), such as $(1+q_1 s)(1+q_2 s)$, which can reduce the effective [relative degree](@entry_id:171358) of the weighted plant back to 1, allowing a positive-realness argument to proceed [@problem_id:2689023].

A particularly important extension addresses the "critical case" where the plant $G(s)$ has poles on the imaginary axis (e.g., an integrator $1/s$), violating the strict stability assumption. This breaks the standard KYP lemma and makes the [frequency response](@entry_id:183149) singular at the [pole frequency](@entry_id:262343). A rigorous way to handle this is through **regularization**. One can perturb the problematic pole slightly into the left-half plane (e.g., replace $1/s$ with $1/(s+\epsilon)$ for a small $\epsilon  0$). If the stability criterion holds for the perturbed system $G_\epsilon(s)$ with a margin that is uniform (independent of $\epsilon$) as $\epsilon \to 0^+$, then one can pass to the limit and prove stability for the original system. An alternative, equally rigorous approach from modern IQC theory involves using a specific dynamic multiplier that cancels the problematic pole in a principled manner (e.g., using a multiplier like $\frac{s}{s+a}$ for an integrator pole) [@problem_id:2689038]. Simply indenting the Nyquist contour, while necessary for visualization, is not sufficient for a rigorous proof without these deeper arguments.

By understanding the Lyapunov and passivity foundations of these criteria, we can appreciate not only their utility as graphical tests but also their profound connections to the fundamental principles of system stability, as well as the elegant ways in which their limitations can be rigorously extended. When faced with verifying stability for an uncertain system, it is crucial to employ these methods with a full awareness of both their power and their underlying assumptions, as exemplified by the need for robust verification procedures when dealing with finite or uncertain frequency-domain data [@problem_id:2689064].