## Introduction
In the study of dynamical systems, a central challenge lies not in deriving exact analytical solutions, which are often intractable, but in understanding the qualitative nature of their long-term behavior. How does a system evolve over time? Does it settle into a state of rest, engage in perpetual oscillation, or exhibit more complex dynamics? The answers to these fundamental questions are rooted in the concepts of [equilibrium solutions](@entry_id:174651) and their stability. These ideas form the bedrock of [qualitative analysis](@entry_id:137250), providing a powerful framework for predicting the ultimate fate of systems ranging from [planetary orbits](@entry_id:179004) and chemical reactions to population dynamics and [gene regulatory networks](@entry_id:150976). This article addresses the core problem of classifying long-term system behavior without needing to solve the governing differential equations explicitly.

Over the following sections, you will embark on a structured journey through this essential topic. The first section, **Principles and Mechanisms**, will establish the mathematical foundation, defining [equilibrium solutions](@entry_id:174651) and introducing the primary analytical tools for determining their stability, including [phase line](@entry_id:269561) analysis, the [linearization](@entry_id:267670) principle, the Jacobian matrix, and Lyapunov's direct method. The second section, **Applications and Interdisciplinary Connections**, will demonstrate the profound utility of these concepts by exploring their application across a wide array of fields, from engineering and ecology to biology and economics, showing how the same mathematical structures provide insight into disparate real-world phenomena. Finally, the **Hands-On Practices** section will provide a set of targeted problems designed to solidify your command of these techniques, bridging the gap between theory and practical application.

## Principles and Mechanisms

In the study of dynamical systems, described by ordinary differential equations, our primary goal is often not to find an explicit formula for the solution $y(t)$ for all time. Instead, we seek to understand the qualitative behavior of solutions. We are particularly interested in the long-term behavior: where do solutions go as time $t \to \infty$? Do they settle down to a constant value, oscillate periodically, or grow without bound? The concepts of [equilibrium solutions](@entry_id:174651) and their stability form the bedrock of this [qualitative analysis](@entry_id:137250).

### Equilibrium Solutions: The Steady States of Dynamical Systems

An **equilibrium solution**, also known as a fixed point or critical point, represents a state of a system that does not change over time. For a system described by the autonomous differential equation $\frac{d\vec{y}}{dt} = \vec{f}(\vec{y})$, an equilibrium solution $\vec{y}^*$ is a constant vector that satisfies the algebraic equation:
$$ \vec{f}(\vec{y}^*) = \vec{0} $$
Physically, this means that at the point $\vec{y}^*$, all forces and rates of change are perfectly balanced, resulting in a static state. Finding these points is the first step in analyzing any dynamical system. It reduces a problem in differential equations to a problem of solving a system of algebraic equations.

For example, in a one-dimensional system $\frac{dy}{dt} = f(y)$, the equilibria are simply the roots of the function $f(y)$. Consider the equation $\frac{dy}{dt} = y^3(y-2)^2(y+1)$ [@problem_id:2201290]. To find the [equilibrium solutions](@entry_id:174651), we set the right-hand side to zero:
$$ y^3(y-2)^2(y+1) = 0 $$
This yields the constant solutions $y = -1$, $y = 0$, and $y = 2$. If the system starts in any of these states, it will remain there for all time.

Similarly, for a two-dimensional system such as a model for a chemical reactor with concentrations $x$ and $y$ [@problem_id:2201261]:
$$ \frac{dx}{dt} = 1 - x^2 $$
$$ \frac{dy}{dt} = x - y $$
Equilibrium points $(x_e, y_e)$ must simultaneously satisfy $\frac{dx}{dt} = 0$ and $\frac{dy}{dt} = 0$. The first equation, $1 - x^2 = 0$, gives $x = \pm 1$. The second equation, $x - y = 0$, implies $y = x$. Combining these conditions, we find two [equilibrium points](@entry_id:167503): $(1, 1)$ and $(-1, -1)$.

Finding the equilibria is only part of the story. The crucial question is: what happens if the system starts *near* an [equilibrium point](@entry_id:272705)? Will it return to the equilibrium, or will it move away? This leads us to the fundamental concept of stability.

### Stability in One-Dimensional Systems

For a one-dimensional system $\frac{dy}{dt} = f(y)$, the behavior of solutions near an equilibrium point $y^*$ is determined by the sign of $f(y)$ in the vicinity of $y^*$.

- If $f(y) > 0$, then $\frac{dy}{dt} > 0$, and the value of $y$ increases over time.
- If $f(y)  0$, then $\frac{dy}{dt}  0$, and the value of $y$ decreases over time.

This simple observation allows for a complete graphical analysis of stability using a **[phase line](@entry_id:269561)**.

#### Graphical Analysis and Classification of Equilibria

By examining the sign of $f(y)$ in the intervals between the [equilibrium points](@entry_id:167503), we can determine the direction of flow. This leads to three fundamental types of stability:

1.  **Asymptotically Stable**: An equilibrium $y^*$ is asymptotically stable if all solutions starting sufficiently close to $y^*$ not only stay close but also converge to $y^*$ as $t \to \infty$. On a [phase line](@entry_id:269561), this corresponds to arrows on both sides of $y^*$ pointing toward it. Such a point is often called an **attractor**.

2.  **Unstable**: An equilibrium $y^*$ is unstable if solutions starting arbitrarily close to it eventually move away. On a [phase line](@entry_id:269561), this corresponds to arrows on both sides of $y^*$ pointing away from it. Such a point is often called a **repeller**.

3.  **Semi-stable**: An equilibrium $y^*$ is semi-stable if solutions on one side of $y^*$ are attracted to it, while solutions on the other side are repelled.

Let's return to the system $\frac{dy}{dt} = f(y) = y^3(y-2)^2(y+1)$ [@problem_id:2201290]. The equilibria are $y = -1, 0, 2$. We analyze the sign of $f(y)$:
- For $y  -1$ (e.g., $y=-2$), $f(y) = (-)^3(-)^2(-) = (+)$. Solutions move right, toward $-1$.
- For $-1  y  0$ (e.g., $y=-0.5$), $f(y) = (-)^3(-)^2(+) = (-)$. Solutions move left, toward $-1$.
Since trajectories on both sides of $y=-1$ approach it, **$y=-1$ is asymptotically stable**.

- For $0  y  2$ (e.g., $y=1$), $f(y) = (+)^3(-)^2(+) = (+)$. Solutions move right, away from $0$.
Trajectories to the left of $y=0$ move left (away), and trajectories to the right move right (away). Therefore, **$y=0$ is unstable**.

- For $y > 2$ (e.g., $y=3$), $f(y) = (+)^3(+)^2(+) = (+)$. Solutions move right, away from $2$.
Trajectories to the left of $y=2$ move right (toward $2$), while trajectories to the right also move right (away from $2$). This makes **$y=2$ semi-stable**.

Notice that the sign of $f(y)$ changes at roots with odd multiplicity ($y=-1$ and $y=0$) but not at the root with even [multiplicity](@entry_id:136466) ($y=2$). This is a general principle: equilibria corresponding to roots of even [multiplicity](@entry_id:136466) are typically semi-stable.

#### Linearization Principle

While graphical analysis is powerful, an analytical approach is often more efficient. The **linearization principle** states that the stability of an equilibrium point $y^*$ of a nonlinear system $\frac{dy}{dt} = f(y)$ can usually be determined by the stability of its linearization, $\frac{du}{dt} = f'(y^*) u$, where $u = y - y^*$ is a small perturbation from equilibrium.

- If **$f'(y^*)  0$**, the perturbation $u(t) = u_0 \exp(f'(y^*)t)$ decays to zero. The equilibrium $y^*$ is **asymptotically stable**.
- If **$f'(y^*) > 0$**, the perturbation grows exponentially. The equilibrium $y^*$ is **unstable**.
- If **$f'(y^*) = 0$**, the linear test is inconclusive. The stability depends on the higher-order terms of $f(y)$, and we must resort to other methods like graphical analysis.

A classic case where linearization fails is the equation $\frac{dy}{dt} = y|y|$ [@problem_id:2201265]. Here, $f(y)=y|y|$ and the only equilibrium is $y=0$. The derivative $f'(y)$ is not formally defined at $y=0$. However, if we approximate it, we find $f'(0)=0$. The linearization test is inconclusive. But a simple sign analysis shows that for $y > 0$, $\frac{dy}{dt} = y^2 > 0$, and for $y  0$, $\frac{dy}{dt} = -y^2  0$. In both cases, solutions move away from the origin, so $y=0$ is an unstable equilibrium.

#### Gradient Systems and Potential Energy

A particularly important class of one-dimensional systems are **[gradient systems](@entry_id:275982)**, which can be written in the form:
$$ \frac{dx}{dt} = -\frac{dU}{dx} $$
Here, $U(x)$ is a **potential energy function**. This formulation provides a profound physical intuition: the system evolves in a way that always seeks to decrease its potential energy, like a ball rolling down a hill.

The equilibrium points $x^*$ satisfy $\frac{dU}{dx}(x^*) = 0$, meaning they are the critical points of the [potential energy function](@entry_id:166231). To determine their stability, we use the linearization criterion. Let $f(x) = -\frac{dU}{dx}$. Then $f'(x) = -\frac{d^2U}{dx^2}$.
- An equilibrium $x^*$ is stable if $f'(x^*) = -U''(x^*)  0$, which implies $U''(x^*) > 0$. This is the condition for a **local minimum** of the potential energy $U(x)$.
- An equilibrium $x^*$ is unstable if $f'(x^*) = -U''(x^*) > 0$, which implies $U''(x^*)  0$. This is the condition for a **local maximum** of the potential energy $U(x)$.

Consider a particle whose potential energy is given by $U(x) = \frac{1}{4}x^4 - \frac{2}{3}x^3 - \frac{3}{2}x^2 + 7$ [@problem_id:2201266]. The dynamics are $\frac{dx}{dt} = -U'(x)$.
First, find the equilibria by setting $U'(x) = 0$:
$$ U'(x) = x^3 - 2x^2 - 3x = x(x-3)(x+1) = 0 $$
The equilibria are $x=-1$, $x=0$, and $x=3$. To classify them, we examine the sign of the second derivative, $U''(x) = 3x^2 - 4x - 3$:
- At $x=-1$: $U''(-1) = 3(1) - 4(-1) - 3 = 4 > 0$. This is a local minimum of $U(x)$, so the equilibrium is **stable**.
- At $x=0$: $U''(0) = -3  0$. This is a local maximum of $U(x)$, so the equilibrium is **unstable**.
- At $x=3$: $U''(3) = 3(9) - 4(3) - 3 = 12 > 0$. This is another local minimum, so this equilibrium is also **stable**.
The stability of the system is directly visualized by the shape of the potential energy landscape.

### Stability in Higher-Dimensional Systems

For systems in two or more dimensions, $\frac{d\vec{y}}{dt} = \vec{f}(\vec{y})$, the concept of stability remains the same, but the dynamics become much richer. Instead of just moving left or right, trajectories can spiral, orbit, or follow complex paths in a phase space.

#### Linearization and the Jacobian Matrix

The [linearization](@entry_id:267670) principle generalizes beautifully to higher dimensions. Near an [equilibrium point](@entry_id:272705) $\vec{y}^*$, the behavior of the nonlinear system is, under most circumstances, faithfully captured by its linearization:
$$ \frac{d\vec{u}}{dt} = J(\vec{y}^*) \vec{u} $$
where $\vec{u} = \vec{y} - \vec{y}^*$ is the perturbation vector and $J(\vec{y}^*)$ is the **Jacobian matrix** of $\vec{f}$ evaluated at the equilibrium. The Jacobian matrix is the matrix of all first-order partial derivatives:
$$ J_{ij} = \frac{\partial f_i}{\partial y_j} $$
The stability of the linear system, and thus the [local stability](@entry_id:751408) of the [nonlinear system](@entry_id:162704), is determined entirely by the **eigenvalues** of the Jacobian matrix $J(\vec{y}^*)$. An equilibrium is called **hyperbolic** if none of the eigenvalues of its Jacobian have a zero real part. The Hartman-Grobman theorem guarantees that for hyperbolic equilibria, the flow of the nonlinear system is topologically equivalent to the flow of its linearization in a neighborhood of the equilibrium.

For a 2D system, as in the [chemical reactor](@entry_id:204463) model from before [@problem_id:2201261], the vector function is $\vec{f}(x,y) = \begin{pmatrix} 1-x^2 \\ x-y \end{pmatrix}$. The Jacobian matrix is:
$$ J(x,y) = \begin{pmatrix} \frac{\partial}{\partial x}(1-x^2)  \frac{\partial}{\partial y}(1-x^2) \\ \frac{\partial}{\partial x}(x-y)  \frac{\partial}{\partial y}(x-y) \end{pmatrix} = \begin{pmatrix} -2x  0 \\ 1  -1 \end{pmatrix} $$
We evaluate this matrix at each [equilibrium point](@entry_id:272705):
- At $(1,1)$: $J(1,1) = \begin{pmatrix} -2  0 \\ 1  -1 \end{pmatrix}$. The eigenvalues are the diagonal entries, $\lambda_1 = -2$ and $\lambda_2 = -1$. Since both are real and negative, trajectories are strongly attracted to the origin. This equilibrium is a **[stable node](@entry_id:261492)**.
- At $(-1,-1)$: $J(-1,-1) = \begin{pmatrix} 2  0 \\ 1  -1 \end{pmatrix}$. The eigenvalues are $\lambda_1 = 2$ and $\lambda_2 = -1$. Since one eigenvalue is positive and one is negative, trajectories are attracted along one direction (the eigenvector for $\lambda_2$) but repelled along another (the eigenvector for $\lambda_1$). This type of [unstable equilibrium](@entry_id:174306) is called a **saddle point**.

#### Classification of 2D Linear Systems

The eigenvalues $\lambda_1, \lambda_2$ of the $2 \times 2$ Jacobian matrix $J$ determine the geometry of the [phase portrait](@entry_id:144015) near an equilibrium.
- **Real, Distinct Eigenvalues**:
    - $\lambda_1, \lambda_2  0$: **Stable Node**. All trajectories approach the origin.
    - $\lambda_1, \lambda_2 > 0$: **Unstable Node**. All trajectories (except the origin itself) move away.
    - $\lambda_1 \lambda_2  0$: **Saddle Point**. Trajectories approach along the stable eigenvector and move away along the unstable eigenvector. Saddles are always unstable.
- **Complex Conjugate Eigenvalues** $\lambda = \alpha \pm i\beta$ ($\beta \neq 0$):
    - $\alpha  0$: **Stable Spiral (or Focus)**. Trajectories spiral inwards towards the equilibrium.
    - $\alpha > 0$: **Unstable Spiral (or Focus)**. Trajectories spiral outwards, away from the equilibrium.
    - $\alpha = 0$: **Center**. Trajectories are [closed orbits](@entry_id:273635) (ellipses) around the equilibrium.

An example of an unstable spiral is found in the system $\frac{dx}{dt} = -2x + 2y, \frac{dy}{dt} = -5x + 4y$ [@problem_id:2201271]. The [system matrix](@entry_id:172230) is $A = \begin{pmatrix} -2  2 \\ -5  4 \end{pmatrix}$. Its [characteristic equation](@entry_id:149057) is $\lambda^2 - 2\lambda + 2 = 0$, with eigenvalues $\lambda = 1 \pm i$. The positive real part ($\alpha = 1$) indicates that the origin is an **unstable spiral**.

#### The Trace-Determinant Plane

A powerful tool for classifying 2D linear systems is the **[trace-determinant plane](@entry_id:163457)**. For any $2 \times 2$ matrix $A$, its eigenvalues $\lambda_{1,2}$ are related to its trace $\text{tr}(A)$ and determinant $\det(A)$ by:
$$ \lambda_1 + \lambda_2 = \text{tr}(A) \quad \text{and} \quad \lambda_1 \lambda_2 = \det(A) $$
The [characteristic equation](@entry_id:149057) is $\lambda^2 - \text{tr}(A)\lambda + \det(A) = 0$. The condition for [asymptotic stability](@entry_id:149743) (both eigenvalues having negative real parts) can be elegantly stated using the **Routh-Hurwitz criteria** for a second-order polynomial:
$$ \text{tr}(A)  0 \quad \text{and} \quad \det(A) > 0 $$
The type of equilibrium (node, spiral, or saddle) is determined by the discriminant of the characteristic equation, $\Delta = (\text{tr}(A))^2 - 4\det(A)$.
- If $\Delta > 0$, the eigenvalues are real (Node or Saddle).
- If $\Delta  0$, the eigenvalues are complex (Spiral or Center).
- If $\Delta = 0$, the eigenvalues are repeated (Degenerate or Star Node).

This framework is exceptionally useful when analyzing systems with parameters. Consider the system $\vec{x}' = A \vec{x}$ with $A = \begin{pmatrix} -1  \alpha \\ 1  -1 \end{pmatrix}$ [@problem_id:2201281]. We have $\text{tr}(A) = -2$ and $\det(A) = 1-\alpha$. For [asymptotic stability](@entry_id:149743), we need $\text{tr}(A)  0$ (which is always true) and $\det(A) > 0$. This second condition requires $1-\alpha > 0$, or $\alpha  1$. Thus, the origin is asymptotically stable if and only if $\alpha  1$.

#### Non-Hyperbolic Equilibria and Structural Stability

Equilibria where the Jacobian has at least one eigenvalue with a zero real part are called **non-hyperbolic**. The Hartman-Grobman theorem does not apply, and the behavior of the [nonlinear system](@entry_id:162704) may differ from its linearization.

A key example is a **center**, which occurs when eigenvalues are purely imaginary, $\lambda = \pm i\omega$. The linear system consists of nested periodic orbits. This equilibrium is **stable** (in the sense of Lyapunov: nearby trajectories stay nearby) but **not asymptotically stable** (they do not converge to the equilibrium). A classic example is the frictionless [harmonic oscillator](@entry_id:155622), $\ddot{x} + \omega^2 x = 0$, which in system form is $\vec{z}' = \begin{pmatrix} 0  1 \\ -\omega^2  0 \end{pmatrix} \vec{z}$ [@problem_id:2201287]. The eigenvalues are $\pm i\omega$, indicating a center. Trajectories are ellipses in the [phase plane](@entry_id:168387), representing bounded oscillations that neither decay nor grow.

Centers are also a prime example of a **structurally unstable** system. This means that an arbitrarily small perturbation to the system can qualitatively change the nature of the equilibrium. For instance, a center can easily be turned into a stable or unstable spiral. Consider the center from the previous example with $\omega^2=9$, given by $A_0 = \begin{pmatrix} 0  3 \\ -3  0 \end{pmatrix}$. If we add a small perturbation $\epsilon P$, where $P=\begin{pmatrix} -1  2 \\ 1  -1 \end{pmatrix}$ [@problem_id:2201255], the new matrix is $A_\epsilon = \begin{pmatrix} -\epsilon  3+2\epsilon \\ -3+\epsilon  -\epsilon \end{pmatrix}$. The trace is now $\text{tr}(A_\epsilon) = -2\epsilon$. If $\epsilon$ is a small positive number, the trace becomes negative. This is enough to shift the purely imaginary eigenvalues into the left half-plane, turning the center into a [stable spiral](@entry_id:269578). Such sensitivity is a hallmark of [non-hyperbolic systems](@entry_id:268227).

### Bifurcation Theory: The Birth and Death of Equilibria

When a system's parameters change, its equilibrium points can move, change their stability, or even be created or destroyed. A **bifurcation** is a qualitative change in the long-term behavior of a system that occurs at a specific parameter value.

#### Saddle-Node Bifurcation
This is the fundamental mechanism for the creation and [annihilation](@entry_id:159364) of equilibria. The canonical example is $\frac{dx}{dt} = r + x^2$ [@problem_id:2197590].
- For $r > 0$, $r+x^2$ is always positive, so there are no equilibria.
- For $r = 0$, we have a single, semi-stable equilibrium at $x=0$.
- For $r  0$, there are two equilibria at $x = \pm\sqrt{-r}$. By linearizing $f(x)=r+x^2$, we find $f'(x)=2x$. The equilibrium at $x_1^* = -\sqrt{-r}$ has $f'(x_1^*)  0$ and is stable. The equilibrium at $x_2^* = \sqrt{-r}$ has $f'(x_2^*) > 0$ and is unstable.
As $r$ increases through 0, a [stable equilibrium](@entry_id:269479) (the "node") and an unstable one (the "saddle," by analogy to higher dimensions) approach each other, collide, and annihilate. This is why it is called a **saddle-node bifurcation**.

#### Transcritical Bifurcation
In a [transcritical bifurcation](@entry_id:272453), two equilibria collide and exchange their stability. The canonical form is $\frac{dx}{dt} = rx - x^2$. This models phenomena like the concentration of a chemical species [@problem_id:1675846]. The equilibria are $x^*=0$ and $x^*=r$.
Let's analyze their stability with $f(x)=rx-x^2$, so $f'(x)=r-2x$.
- At $x^*=0$: $f'(0)=r$. This equilibrium is stable for $r0$ and unstable for $r>0$.
- At $x^*=r$: $f'(r)=r-2r=-r$. This equilibrium is stable for $r>0$ and unstable for $r0$.
As the parameter $r$ passes through 0, the two equilibria meet at $x=0$. The stable equilibrium at $x=0$ (for $r0$) becomes unstable, and it "passes on" its stability to the other equilibrium, $x=r$, which emerges into the physical domain $x>0$ and is stable for $r>0$.

#### Pitchfork Bifurcation
This bifurcation is common in systems with symmetry. In a supercritical [pitchfork bifurcation](@entry_id:143645), a [stable equilibrium](@entry_id:269479) becomes unstable and gives rise to a pair of new stable equilibria. The laser model equation $\frac{dy}{dt} = (gP-l)y - ky^3$ provides an excellent physical example [@problem_id:2201244]. Let the [bifurcation parameter](@entry_id:264730) be $\mu = gP-l$. The equation is $\frac{dy}{dt} = \mu y - ky^3$.
- For $\mu  0$ (low [pump power](@entry_id:190414) $P$), the only non-negative equilibrium is $y=0$. The derivative of the right-hand side is $f'(y) = \mu - 3ky^2$, so $f'(0)=\mu  0$. The zero-amplitude state is stable (laser is "off").
- For $\mu > 0$ (high [pump power](@entry_id:190414) $P$), the equilibrium at $y=0$ becomes unstable since $f'(0)=\mu>0$. Two new equilibria appear at $y^* = \pm\sqrt{\mu/k}$. For the physical amplitude $y \ge 0$, we consider $y^*=\sqrt{\mu/k}$. The derivative at this point is $f'(\sqrt{\mu/k}) = \mu - 3k(\mu/k) = -2\mu  0$. This new non-zero amplitude is stable (laser is "on").
This transition, where one stable path splits into two, is the defining feature of a **pitchfork bifurcation**.

### Advanced Stability Analysis: Lyapunov's Direct Method

What happens when [linearization](@entry_id:267670) fails (non-hyperbolic case) or when we want to prove stability over a large region, not just locally? **Lyapunov's direct method** provides a powerful alternative inspired by the concept of energy.

The idea is to find a scalar function $V(\vec{y})$, called a **Lyapunov function**, which is positive everywhere except at the equilibrium (where $V(\vec{0})=0$), and whose value decreases along all system trajectories. If such a function exists, it acts like a generalized energy that the system is always dissipating, forcing trajectories to fall towards the state of minimum "energy," which is the equilibrium.

More formally, for an equilibrium at the origin $\vec{y}=\vec{0}$:
- **Lyapunov's Stability Theorem**: If there exists a continuously differentiable, **positive definite** function $V(\vec{y})$ (i.e., $V(\vec{0})=0$ and $V(\vec{y})>0$ for $\vec{y}\neq\vec{0}$) in a neighborhood of the origin, whose time derivative along trajectories, $\dot{V} = \frac{dV}{dt}$, is **negative semi-definite** (i.e., $\dot{V}(\vec{y}) \le 0$), then the origin is **stable**.
- **Asymptotic Stability Theorem**: If, in addition, $\dot{V}$ is **[negative definite](@entry_id:154306)** (i.e., $\dot{V}(\vec{y})  0$ for $\vec{y}\neq\vec{0}$), then the origin is **asymptotically stable**.

The time derivative is computed using the chain rule: $\dot{V}(\vec{y}) = \nabla V \cdot \frac{d\vec{y}}{dt} = \nabla V(\vec{y}) \cdot \vec{f}(\vec{y})$.

For the harmonic oscillator [@problem_id:2201287], the physical energy $V(x,v) = \frac{1}{2}(\omega^2x^2+v^2)$ is a natural Lyapunov function candidate. It is clearly [positive definite](@entry_id:149459). Its time derivative is $\dot{V} = \omega^2x\dot{x} + v\dot{v} = \omega^2x(v) + v(-\omega^2x) = 0$. Since $\dot{V}$ is negative semi-definite (as $0 \le 0$), the origin is stable. Since it is not [negative definite](@entry_id:154306), we cannot conclude [asymptotic stability](@entry_id:149743), which is indeed the correct result.

Finding a Lyapunov function can be an art, but for many systems near an equilibrium, a [quadratic form](@entry_id:153497) $V(x,y) = ax^2 + by^2$ is a good starting point. Consider the system [@problem_id:2201268]:
$$ \frac{dx}{dt} = -2x - 2y + xy^2 $$
$$ \frac{dy}{dt} = 7x - 3y - x^2y $$
Let's try $V(x,y) = ax^2 + by^2$ with $a,b > 0$.
$$ \dot{V} = \frac{\partial V}{\partial x}\dot{x} + \frac{\partial V}{\partial y}\dot{y} = (2ax)(-2x - 2y + ...) + (2by)(7x - 3y - ...) $$
$$ \dot{V} = -4ax^2 - 4axy - 6by^2 + 14bxy + \text{higher order terms} $$
$$ \dot{V} = -4ax^2 - 6by^2 + (-4a + 14b)xy + ... $$
To make $\dot{V}$ easier to analyze, we can choose $a$ and $b$ to eliminate the cross-term $xy$. Setting its coefficient to zero gives $-4a + 14b = 0$, which implies a ratio $\frac{a}{b} = \frac{14}{4} = 3.5$. Choosing, for instance, $a=7, b=2$, our time derivative becomes:
$$ \dot{V} = -28x^2 - 12y^2 + 10x^2y^2 $$
Near the origin, the quadratic terms $-28x^2 - 12y^2$ dominate the quartic term $10x^2y^2$. Therefore, in a sufficiently small neighborhood of the origin, $\dot{V}$ is [negative definite](@entry_id:154306). Since $V$ is positive definite, this proves that the origin is an asymptotically stable equilibrium for the [nonlinear system](@entry_id:162704). This conclusion would be difficult to reach with linearization alone due to the complexity of the higher-order terms.