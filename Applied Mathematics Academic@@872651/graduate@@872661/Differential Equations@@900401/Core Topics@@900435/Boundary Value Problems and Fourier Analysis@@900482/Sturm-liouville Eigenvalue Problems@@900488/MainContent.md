## Introduction
Sturm-Liouville theory provides a powerful and elegant framework for analyzing a broad class of [second-order linear differential equations](@entry_id:261043). Its principles are fundamental to numerous areas of science and engineering, offering a unified method for understanding oscillatory and decay phenomena, from the vibrations of a string to the energy levels of an atom. The central problem it addresses is why certain physical systems exhibit [discrete spectra](@entry_id:153575)—quantized values like frequencies or energies—and why their corresponding modes of behavior (eigenfunctions) are mutually orthogonal. This article demystifies the theory, providing a comprehensive guide to its core concepts and applications.

In the chapters that follow, you will gain a deep understanding of this essential topic. We will begin in **Principles and Mechanisms** by dissecting the canonical Sturm-Liouville equation, exploring the profound consequences of self-adjointness—such as real eigenvalues and [orthogonal eigenfunctions](@entry_id:167480)—and examining analytical tools like the Rayleigh quotient. Next, in **Applications and Interdisciplinary Connections**, we will see the theory in action, exploring how it emerges from [solving partial differential equations](@entry_id:136409), forms the mathematical bedrock of quantum mechanics, and provides critical tools for stability analysis in advanced [mathematical physics](@entry_id:265403). Finally, the **Hands-On Practices** section will offer a chance to apply this knowledge to solve concrete problems, solidifying your grasp of the material.

## Principles and Mechanisms

Having introduced the general context of Sturm-Liouville theory, we now delve into the foundational principles and mathematical mechanisms that grant it such predictive power. This chapter will dissect the structure of the Sturm-Liouville equation, establish the core properties of its solutions, and explore the advanced analytical tools used to characterize its spectrum.

### The Canonical Sturm-Liouville Form

While many second-order [linear ordinary differential equations](@entry_id:276013) (ODEs) arise in physics and engineering, a particular structure, known as the **canonical Sturm-Liouville form**, is exceptionally well-suited for analysis. This form is given by:
$$
\frac{d}{dx}\left[p(x)\frac{dy}{dx}\right] + [q(x) + \lambda w(x)]y = 0
$$
Here, $\lambda$ is a parameter, typically an eigenvalue. The functions $p(x)$, $q(x)$, and $w(x)$ define the specific problem. The function $p(x)$ is often called the Sturm-Liouville coefficient, $q(x)$ is the [potential function](@entry_id:268662), and $w(x)$ is the weight or density function. The structure $(p(x)y')'$ is key, as it leads to the property of formal self-adjointness, which we will explore shortly.

Many physically derived equations do not immediately appear in this [canonical form](@entry_id:140237). Consider a general second-order linear homogeneous ODE:
$$
a_2(x) y'' + a_1(x) y' + a_0(x) y = 0
$$
To transform this into the Sturm-Liouville form, we seek an **integrating factor**, $\mu(x)$, such that when the equation is multiplied by $\mu(x)$, the first two terms become the derivative of a product. That is, we require:
$$
\mu(x) a_2(x) y'' + \mu(x) a_1(x) y' = \frac{d}{dx} \left[ P(x) y' \right] = P'(x) y' + P(x) y''
$$
Comparing coefficients of $y''$ and $y'$, we see that $P(x) = \mu(x) a_2(x)$ and $P'(x) = \mu(x) a_1(x)$. Differentiating the first relation gives $P'(x) = (\mu a_2)' = \mu' a_2 + \mu a_2'$. Equating the two expressions for $P'(x)$ yields a first-order ODE for the integrating factor $\mu(x)$:
$$
\mu' a_2 + \mu a_2' = \mu a_1 \quad \implies \quad \mu' a_2 = \mu (a_1 - a_2') \quad \implies \quad \frac{\mu'}{\mu} = \frac{a_1(x) - a_2'(x)}{a_2(x)}
$$
Solving for $\mu(x)$ gives:
$$
\mu(x) = \frac{1}{a_2(x)} \exp\left( \int \frac{a_1(x)}{a_2(x)} dx \right)
$$
Once this [integrating factor](@entry_id:273154) is found, multiplying the original ODE by it puts the equation into [canonical form](@entry_id:140237), allowing for the identification of $p(x)$, $q(x)$, and $w(x)$.

For instance, consider the equation describing a physical system given by $y'' + \frac{2}{x}y' + (\lambda - V_0)y = 0$ for $x > 0$ [@problem_id:1151004]. Comparing this to the general form, we have $a_2(x)=1$ and $a_1(x) = 2/x$. The [integrating factor](@entry_id:273154) is:
$$
\mu(x) = \frac{1}{1} \exp\left( \int \frac{2}{x} dx \right) = \exp(2 \ln x) = x^2
$$
Multiplying the equation by $x^2$ yields:
$$
x^2 y'' + 2x y' + x^2(\lambda - V_0) y = 0
$$
The first two terms can be combined using the [product rule](@entry_id:144424): $x^2 y'' + 2x y' = \frac{d}{dx}(x^2 y')$. The equation becomes:
$$
\frac{d}{dx}\left[x^2 \frac{dy}{dx}\right] + x^2(\lambda - V_0) y = 0
$$
To match the standard form where the eigenvalue $\lambda$ multiplies the weight function, we write:
$$
\frac{d}{dx}\left[x^2 \frac{dy}{dx}\right] + (-V_0 x^2 + \lambda x^2) y = 0
$$
By comparing this to the canonical form, we can identify $p(x) = x^2$, $q(x) = -V_0 x^2$, and the weight function $w(x) = x^2$.

Conversely, one can ask what weight function $w(x)$ is required to make a given differential operator, such as $L[y] = -y'' - \frac{4}{x}y'$, formally self-adjoint [@problem_id:1150997]. This means we seek a $w(x)$ such that $w(x)L[y]$ can be written in Sturm-Liouville form, $(p(x)y')' + q(x)y$. In this example, $q(x)=0$. We need to find $w(x)$ such that:
$$
-w(x)y'' - \frac{4w(x)}{x}y' = \frac{d}{dx}\left[p(x)y'\right] = p'(x)y' + p(x)y''
$$
Comparing the coefficients of $y''$ gives $p(x) = -w(x)$. Comparing the coefficients of $y'$ gives $p'(x) = -4w(x)/x$. Since $p(x)=-w(x)$, we have $p'(x)=-w'(x)$. Equating the two expressions for $p'(x)$ yields a differential equation for the weight function:
$$
-w'(x) = -\frac{4w(x)}{x} \quad \implies \quad \frac{dw}{w} = \frac{4}{x}dx
$$
Integrating gives $\ln w = 4 \ln x + C_0$, or $w(x) = C x^4$. If a [normalization condition](@entry_id:156486) such as $w(1)=1$ is imposed, the constant is uniquely determined ($C=1$), yielding $w(x)=x^4$. This exercise highlights that the structure of a Sturm-Liouville problem is an intrinsic property that can be revealed by choosing the appropriate "measure" or weight for the underlying space of functions.

### The Sturm-Liouville Eigenvalue Problem

The Sturm-Liouville equation becomes an eigenvalue problem when paired with a set of [homogeneous boundary conditions](@entry_id:750371) on an interval $[a, b]$. A **regular Sturm-Liouville problem** is one where the interval $[a, b]$ is finite, the functions $p(x), p'(x), q(x), w(x)$ are continuous, and importantly, $p(x) > 0$ and $w(x) > 0$ for all $x \in [a, b]$. Problems violating these conditions (e.g., on an infinite interval or with coefficients that are zero or singular at an endpoint) are termed **singular**. For now, we focus on regular problems.

The power of the Sturm-Liouville formulation stems from the self-adjointness of the associated [differential operator](@entry_id:202628). Let the operator be $L[y] = (p(x)y')' + q(x)y$. The eigenvalue equation is $L[y] = -\lambda w(x) y$. The operator is said to be self-adjoint (or more precisely, Hermitian) with respect to an inner product weighted by $w(x)$ if it satisfies certain conditions. The defining feature is Lagrange's identity, which can be derived through [integration by parts](@entry_id:136350):
$$
\int_a^b \left( u L[v] - v L[u] \right) dx = \left[ p(x) (u v' - v u') \right]_a^b
$$
For the operator to be self-adjoint, the boundary term on the right-hand side, known as the **boundary form**, must vanish for all functions $u, v$ in the operator's domain (i.e., functions that satisfy the given boundary conditions). Common boundary conditions that ensure this are:
1.  **Separated Boundary Conditions**: Conditions of the form $\alpha_1 y(a) + \alpha_2 y'(a) = 0$ and $\beta_1 y(b) + \beta_2 y'(b) = 0$.
2.  **Periodic Boundary Conditions**: $y(a)=y(b)$ and $p(a)y'(a)=p(b)y'(b)$.

When the operator is self-adjoint, it guarantees several profound properties for its [eigenvalues and eigenfunctions](@entry_id:167697).

#### Reality of Eigenvalues

For any regular Sturm-Liouville problem (real $p,q,w$) with self-adjoint boundary conditions, all eigenvalues $\lambda$ are real. To prove this, let $\lambda$ be a possibly complex eigenvalue with a corresponding non-trivial complex-valued [eigenfunction](@entry_id:149030) $y(x)$. The eigenvalue equation is $L[y] = -\lambda w y$. Taking the [complex conjugate](@entry_id:174888) of this equation gives $\overline{L[y]} = -\overline{\lambda} \overline{w} \overline{y}$. Since the operator $L$ and the weight $w(x)$ are real, $\overline{L[y]} = L[\overline{y}]$ and $\overline{w}=w$. Thus, $L[\overline{y}] = -\overline{\lambda} w \overline{y}$.

Now, we use Lagrange's identity with $u = \overline{y}$ and $v = y$:
$$
\int_a^b \left( \overline{y} L[y] - y L[\overline{y}] \right) dx = \left[ p(x) (\overline{y} y' - y \overline{y}') \right]_a^b = 0
$$
The boundary form vanishes because both $y$ and its conjugate $\overline{y}$ satisfy the real-valued self-adjoint boundary conditions. Substituting the eigenvalue relations into the integral gives:
$$
\int_a^b \left( \overline{y} (-\lambda w y) - y (-\overline{\lambda} w \overline{y}) \right) dx = (\overline{\lambda} - \lambda) \int_a^b w(x) |y(x)|^2 dx = 0
$$
Since $w(x) > 0$ and $y(x)$ is a non-trivial [eigenfunction](@entry_id:149030), the integral $\int_a^b w(x) |y(x)|^2 dx$ is strictly positive. Therefore, we must have $\overline{\lambda} - \lambda = 0$, which implies $\overline{\lambda} = \lambda$, proving that the eigenvalue is real.

This proof hinges on the assumption that the coefficients and weight function are real. If we relax this, the conclusion may change. For instance, if the weight function $w(x)$ is complex-valued, the derivation leads to $L[\overline{y}] = \overline{\lambda} \overline{w(x)} \overline{y}$ [@problem_id:2129568]. This shows that $\overline{\lambda}$ is an eigenvalue not for the original problem, but for a new problem with a conjugated weight function $\overline{w(x)}$. Unless $w(x)$ is real, $\overline{\lambda}$ is generally not an eigenvalue of the original system.

#### Orthogonality of Eigenfunctions

Another cornerstone property is that [eigenfunctions](@entry_id:154705) corresponding to distinct eigenvalues are orthogonal with respect to the weight function $w(x)$. Let $y_n$ and $y_m$ be two [eigenfunctions](@entry_id:154705) corresponding to distinct real eigenvalues $\lambda_n \neq \lambda_m$. They satisfy:
$$
L[y_n] = -\lambda_n w y_n
$$
$$
L[y_m] = -\lambda_m w y_m
$$
Using Lagrange's identity again, with $u=y_m$ and $v=y_n$, and knowing the boundary form vanishes for the self-[adjoint problem](@entry_id:746299):
$$
\int_a^b (y_m L[y_n] - y_n L[y_m]) dx = 0
$$
Substituting the eigenvalue relations:
$$
\int_a^b (y_m (-\lambda_n w y_n) - y_n (-\lambda_m w y_m)) dx = (\lambda_m - \lambda_n) \int_a^b w(x) y_m(x) y_n(x) dx = 0
$$
Since we assumed $\lambda_m \neq \lambda_n$, the integral itself must be zero:
$$
\int_a^b w(x) y_m(x) y_n(x) dx = 0
$$
This is the **orthogonality relation**. It is fundamental to the expansion of arbitrary functions in series of [eigenfunctions](@entry_id:154705), such as Fourier series, which are a special case of Sturm-Liouville [eigenfunction expansions](@entry_id:177104).

The importance of the boundary conditions in ensuring self-adjointness and thus orthogonality cannot be overstated. Consider the simple problem $u''+\lambda u = 0$ on $[0,\pi]$. With standard separated boundary conditions like $u(0)=u(\pi)=0$, the eigenfunctions are orthogonal. However, if we impose non-standard boundary conditions such as $u(\pi) = 2u(0)$ and $u'(\pi)=0$, the self-adjointness is lost because the boundary term in Lagrange's identity no longer vanishes for arbitrary functions satisfying these conditions. As a consequence, [eigenfunctions](@entry_id:154705) corresponding to distinct eigenvalues are not guaranteed to be orthogonal. For example, for this specific problem, the functions $u_1(x) = \cos(x/3) + \sqrt{3}\sin(x/3)$ and $u_2(x) = \cos(5x/3) - \sqrt{3}\sin(5x/3)$ can be shown to be [eigenfunctions](@entry_id:154705) for distinct eigenvalues, yet a direct calculation shows that their integral $\int_0^\pi u_1(x) u_2(x) dx$ is non-zero [@problem_id:1151002].

#### The Spectrum of Regular Problems

The collection of all eigenvalues is known as the spectrum of the problem. For any regular Sturm-Liouville problem, the spectrum has a remarkably clean and predictable structure. The key properties of the eigenvalues are as follows [@problem_id:2203116]:
*   The eigenvalues are all real.
*   There are a countably infinite number of eigenvalues.
*   They can be ordered to form a strictly increasing sequence: $\lambda_0  \lambda_1  \lambda_2  \dots$.
*   There is no upper bound to the eigenvalues; that is, $\lim_{n \to \infty} \lambda_n = \infty$.
*   For each eigenvalue, there is a unique (up to a constant factor) corresponding eigenfunction. This means the eigenvalues are **simple**.

These properties ensure that the eigenfunctions form a complete orthogonal basis for the space of square-[integrable functions](@entry_id:191199) with weight $w(x)$, which is the theoretical underpinning for using [eigenfunction](@entry_id:149030) series to solve a wide variety of partial differential equations and other problems in mathematical physics.

### Variational Characterization: The Rayleigh Quotient

While eigenvalues are defined via a differential equation, they can also be characterized using an integral formulation known as the **Rayleigh quotient**. For an eigenpair $(\lambda, y)$, we start with the equation $-(py')' - qy = \lambda w y$. Multiplying by $y$ and integrating from $a$ to $b$:
$$
\int_a^b (- (py')' y - q y^2) dx = \lambda \int_a^b w y^2 dx
$$
Integrating the first term by parts:
$$
\int_a^b p (y')^2 dx - [p y y']_a^b - \int_a^b q y^2 dx = \lambda \int_a^b w y^2 dx
$$
For standard boundary conditions (like Dirichlet, $y(a)=y(b)=0$, or Neumann, $y'(a)=y'(b)=0$), the boundary term $[p y y']_a^b$ vanishes. This leads to an expression for the eigenvalue:
$$
\lambda = \frac{\int_a^b (p(x) [y'(x)]^2 - q(x) [y(x)]^2) dx}{\int_a^b w(x) [y(x)]^2 dx}
$$
This ratio is the Rayleigh quotient, denoted $R[y]$. The remarkable fact, known as the **Rayleigh-Ritz principle**, is that the lowest eigenvalue $\lambda_0$ is the minimum value of the Rayleigh quotient over the set of all admissible functions (i.e., sufficiently [smooth functions](@entry_id:138942) satisfying the boundary conditions):
$$
\lambda_0 = \min_{y \neq 0} R[y]
$$
The higher eigenvalues can also be found via a [minimax principle](@entry_id:170647).

This variational characterization is extremely powerful. It allows us to estimate eigenvalues without solving the differential equation. More importantly, it provides a way to study how eigenvalues change when the problem's parameters ($p, q, w$, or the interval) are modified.

For example, consider the problem $-y'' + q(x)y = \lambda y$ on $[0, L]$ with Dirichlet conditions $y(0)=y(L)=0$, where the potential $q(x)$ is continuous and non-negative, $q(x) \ge 0$ [@problem_id:1151020]. The Rayleigh quotient is:
$$
\lambda = \frac{\int_0^L ([y']^2 + q y^2) dx}{\int_0^L y^2 dx}
$$
Since $q(x) \ge 0$ and $y^2 \ge 0$, the integral $\int_0^L q y^2 dx$ is non-negative. Therefore:
$$
\lambda_1(q) = \min_y \frac{\int_0^L ([y']^2 + q y^2) dx}{\int_0^L y^2 dx} \ge \min_y \frac{\int_0^L [y']^2 dx}{\int_0^L y^2 dx}
$$
The expression on the right is the lowest eigenvalue for the case where the potential is identically zero, $q(x) \equiv 0$. The problem $-y'' = \lambda y$ with Dirichlet conditions has its lowest eigenvalue $\lambda_1(0) = (\pi/L)^2$. This means that for any non-negative potential $q(x)$, the lowest eigenvalue must be at least $(\pi/L)^2$. The [greatest lower bound](@entry_id:142178) (infimum) of $\lambda_1(q)$ over all such potentials is achieved when $q(x)=0$, so the [infimum](@entry_id:140118) is exactly $(\pi/L)^2$.

The Rayleigh quotient can also help determine when an operator ceases to be positive-definite (i.e., when its lowest eigenvalue transitions from positive to zero or negative). Consider the operator $L[y] = -y'' - 6 \operatorname{sech}^2(x) y$ on an interval $[-a, a]$ with Dirichlet conditions [@problem_id:1150982]. The lowest eigenvalue $\lambda_0$ depends on the interval half-length $a$. The operator is positive-definite as long as $\lambda_0 > 0$. The critical length $a_{cr}$ at which it ceases to be positive-definite corresponds to $\lambda_0 = 0$. This occurs when there is a non-trivial solution to the zero-energy equation $L[y]=0$, i.e., $-y'' - 6 \operatorname{sech}^2(x) y = 0$, that satisfies the boundary conditions $y(\pm a) = 0$. This particular equation can be transformed into the Legendre differential equation and solved exactly. The lowest-energy (even) solution is found to be $y(x) \propto 3\tanh^2(x) - 1$. Setting $y(a)=0$ allows one to solve for the critical half-length $a_{cr}$.

### Advanced Spectral Analysis

For more detailed information about the spectrum, especially for large eigenvalues or in singular cases, more advanced techniques are required.

#### Asymptotic Behavior of Eigenvalues

For regular Sturm-Liouville problems, the eigenvalues grow without bound, $\lambda_n \to \infty$. A natural question is to determine the rate of this growth. The leading-order [asymptotic behavior](@entry_id:160836) can be found using the **Liouville-Green approximation** (also related to the WKB method). This involves a [change of variables](@entry_id:141386), known as the **Liouville transformation**, that converts the Sturm-Liouville equation into a simpler, [canonical form](@entry_id:140237). For the equation $(py')' + qy + \lambda w y = 0$, the transformation is given by:
$$
z(x) = \int_a^x \sqrt{\frac{w(t)}{p(t)}} dt, \quad u(z) = (p(x)w(x))^{1/4} y(x)
$$
This transforms the original equation into the **Liouville [normal form](@entry_id:161181)**:
$$
\frac{d^2u}{dz^2} + (\lambda - Q(z))u(z) = 0
$$
where the new interval is $[0, L]$ with $L = \int_a^b \sqrt{w(t)/p(t)} dt$. For very large $\lambda$, the term $Q(z)$ becomes negligible compared to $\lambda$, and the equation simplifies to $u'' + \lambda u \approx 0$.

By solving this approximate equation with the appropriately transformed boundary conditions, we can find the [asymptotic distribution](@entry_id:272575) of eigenvalues. For example, for Dirichlet conditions ($y(a)=y(b)=0$, which approximately correspond to $u(0)=u(L)=0$), the solutions are $u(z) \propto \sin(\sqrt{\lambda}z)$, leading to $\sqrt{\lambda_n} \approx \frac{(n+1)\pi}{L}$. For Neumann conditions ($y'(a)=y'(b)=0$, approximately $u'(0)=u'(L)=0$), the solutions are $u(z) \propto \cos(\sqrt{\lambda}z)$, giving $\sqrt{\mu_n} \approx \frac{n\pi}{L}$.

Using these asymptotic formulas, we can analyze the fine structure of the spectrum. For instance, the difference between the $n$-th Dirichlet and Neumann eigenvalues for large $n$ behaves as [@problem_id:1151105]:
$$
\lambda_n - \mu_n \sim \frac{(n+1)^2 \pi^2}{L^2} - \frac{n^2 \pi^2}{L^2} = \frac{(2n+1)\pi^2}{L^2} \sim \frac{2n\pi^2}{L^2}
$$
Substituting the definition of $L$ gives the leading term:
$$
\lambda_n - \mu_n \sim \frac{2n\pi^2}{\left(\int_a^b \sqrt{\frac{w(x)}{p(x)}} dx\right)^2}
$$
This shows that while both sets of eigenvalues grow quadratically, their separation grows linearly with $n$.

#### Eigenvalue Interlacing

The eigenvalues corresponding to different boundary conditions are not independent. A classic result is that the eigenvalues for Dirichlet boundary conditions ($y(a)=y(b)=0$) and Neumann conditions ($y'(a)=y'(b)=0$) interlace: $\mu_0  \lambda_0  \mu_1  \lambda_1  \dots$. A more refined version shows the interlacing between eigenvalues for problems with a Dirichlet condition at one end ($y(a)=0$) and either a Dirichlet or Neumann condition at the other.

This can be elegantly proven by studying the behavior of solutions as a function of the parameter $\lambda$. Let $y(x, \lambda)$ be the unique solution satisfying [initial conditions](@entry_id:152863) $y(a, \lambda) = 0$ and $y'(a, \lambda) = 1$. The eigenvalues for the Dirichlet problem on $[a,b]$ are the values of $\lambda$ for which $y(b, \lambda) = 0$. The eigenvalues for the mixed problem with a Neumann condition at $b$ are the values of $\lambda$ for which $y'(b, \lambda) = 0$.

Consider the characteristic function $F(\lambda) = p(b) \frac{y'(b, \lambda)}{y(b, \lambda)}$ [@problem_id:1151055]. The zeros of $F(\lambda)$ are the Neumann eigenvalues, and its poles are the Dirichlet eigenvalues. By differentiating this function with respect to $\lambda$ and using Lagrange's identity on $y(x,\lambda)$ and its derivative with respect to $\lambda$, one can rigorously show that:
$$
\frac{dF}{d\lambda} = -\frac{\int_a^b w(x) [y(x, \lambda)]^2 dx}{[y(b, \lambda)]^2}
$$
Since $w(x)>0$, the derivative $\frac{dF}{d\lambda}$ is strictly negative wherever it is defined. This means that the function $F(\lambda)$ is strictly decreasing between its poles. As it goes from $+\infty$ just after one pole to $-\infty$ just before the next, it must cross the axis exactly once. This proves that between any two consecutive Dirichlet eigenvalues, there is exactly one Neumann eigenvalue, establishing the interlacing property.

#### Singular Sturm-Liouville Problems: Weyl's Alternative

When the conditions for a regular problem are not met, we have a **singular Sturm-Liouville problem**. A common singularity occurs at an endpoint of the interval, say $x=0$, where $p(0)=0$ or the interval extends to $0$ from the right. In such cases, the behavior of solutions near the [singular point](@entry_id:171198) dictates the nature of the problem.

According to **Weyl's alternative**, a singular endpoint falls into one of two categories:
1.  **Limit-Circle Case**: All solutions to the Sturm-Liouville equation $L[y]=\lambda y$ are square-integrable with respect to the weight $w(x)$ near the singular endpoint (i.e., $\int_0^c w(x)|y(x)|^2 dx  \infty$). In this case, a boundary condition *must* be specified at the [singular point](@entry_id:171198) to ensure a self-adjoint operator.
2.  **Limit-Point Case**: At least one solution is not square-integrable near the singular endpoint. In this case, the requirement of square-integrability acts as a boundary condition itself, and no additional condition is needed at that endpoint for self-adjointness.

The classification depends on the behavior of the coefficient functions $p(x), q(x), w(x)$ near the [singular point](@entry_id:171198). Consider an operator on $(0,1]$ with coefficients that behave as [power laws](@entry_id:160162) near $x=0$: $p(x) \sim x^\beta$, $q(x) \sim C x^{-\alpha}$, and $w(x) \sim x^\gamma$ [@problem_id:1151120]. The transition between the limit-circle and limit-point regimes often occurs at a critical value of the exponents. By analyzing the asymptotic behavior of solutions to the differential equation $- (x^\beta y')' + C x^{-\alpha} y = 0$ as $x \to 0^+$, one can determine this critical value. The analysis reveals a fundamental change in the character of the equation when the influence of the potential term $q(x)y$ begins to dominate the kinetic term $-(p(x)y')'$. This transition happens at a [critical exponent](@entry_id:748054) $\alpha_c$ that depends on $\beta$. This critical value is found to be $\alpha_c = 2 - \beta$. If $\alpha > \alpha_c$, the potential is "too singular," forcing the problem into the limit-point case. If $\alpha  \alpha_c$, the problem is typically in the limit-circle case (though the final classification also depends on $\gamma$). This analysis is crucial for correctly setting up quantum mechanical problems with [singular potentials](@entry_id:754921), such as the Coulomb potential in the hydrogen atom.