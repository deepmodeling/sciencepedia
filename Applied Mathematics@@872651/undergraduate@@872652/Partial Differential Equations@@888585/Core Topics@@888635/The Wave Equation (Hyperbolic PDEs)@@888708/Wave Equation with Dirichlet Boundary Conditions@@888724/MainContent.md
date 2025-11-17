## Introduction
The [one-dimensional wave equation](@entry_id:164824), $\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2}$, stands as a cornerstone of [mathematical physics](@entry_id:265403), describing a multitude of phenomena from the vibrations of a guitar string to the propagation of electromagnetic signals. While simple in form, its behavior is profoundly shaped by the constraints imposed at its boundaries. This article addresses the fundamental problem of [solving the wave equation](@entry_id:171826) on a finite interval with its ends held in a fixed position, a scenario encapsulated by Dirichlet boundary conditions. This common physical setup presents a rich mathematical structure that serves as a gateway to understanding more complex wave phenomena.

This article provides a systematic exploration of this canonical problem. In **"Principles and Mechanisms"**, you will learn the powerful [method of separation of variables](@entry_id:197320), discovering how it decomposes the problem into simpler [ordinary differential equations](@entry_id:147024) and reveals the concepts of eigenvalues, eigenfunctions, and [normal modes](@entry_id:139640). We will assemble these building blocks into a general solution using Fourier series and explore alternative perspectives through d'Alembert's method and the principle of [energy conservation](@entry_id:146975). The subsequent chapter, **"Applications and Interdisciplinary Connections"**, demonstrates the remarkable versatility of these ideas, showing how they apply to [acoustics](@entry_id:265335), engineering design, computational methods, and even the esoteric realms of quantum [field theory](@entry_id:155241). Finally, **"Hands-On Practices"** will allow you to solidify your understanding by tackling concrete problems that connect the mathematical theory to [physical quantities](@entry_id:177395) and conceptual insights.

## Principles and Mechanisms

The [one-dimensional wave equation](@entry_id:164824), $\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2}$, provides a fundamental model for a vast range of physical phenomena, from the vibrations of a guitar string to the propagation of signals in a [transmission line](@entry_id:266330). In this chapter, we will conduct a systematic analysis of this equation within a specific, yet widely applicable, physical context: a [finite domain](@entry_id:176950) with fixed endpoints. This scenario is mathematically described by **Dirichlet boundary conditions**.

### Physical Interpretation of Dirichlet Boundary Conditions

Consider a flexible, elastic string of length $L$ stretched along the x-axis. Its transverse displacement from the [equilibrium position](@entry_id:272392) is given by the function $u(x,t)$. To obtain a unique solution that describes the string's motion, the partial differential equation must be supplemented with conditions that specify the state of the string's boundaries.

For a string whose ends are held in a fixed position, such as a violin or guitar string, the displacement at the endpoints must be zero for all time. Mathematically, this is expressed as:
$$
u(0,t) = 0 \quad \text{and} \quad u(L,t) = 0 \quad \text{for all } t \ge 0
$$
These are known as homogeneous **Dirichlet boundary conditions**. The condition $u(0,t)=0$ states that the end of the string at $x=0$ is permanently fixed at the [equilibrium position](@entry_id:272392), and similarly for the end at $x=L$. This constraint is fundamental to the behavior of the system, as it dictates that any wave propagating along the string will be reflected at the boundaries, leading to the formation of standing waves. It is crucial to distinguish these boundary conditions, which constrain the system in space for all time, from [initial conditions](@entry_id:152863), which specify the state of the entire string (e.g., its shape $u(x,0)$ and velocity $\frac{\partial u}{\partial t}(x,0)$) at a single moment in time, $t=0$ [@problem_id:2155993].

### Solving with Separation of Variables

A powerful and systematic method for solving [linear partial differential equations](@entry_id:171085) like the wave equation is the **[method of separation of variables](@entry_id:197320)**. This technique seeks special solutions, known as **[normal modes](@entry_id:139640)**, that have a product form.

#### The Separation Ansatz

We begin by assuming a solution of the form $u(x,t) = X(x)T(t)$, where $X(x)$ is a function only of position and $T(t)$ is a function only of time. Substituting this *ansatz* into the wave equation gives:
$$
X(x) \frac{d^2T}{dt^2} = c^2 \frac{d^2X}{dx^2} T(t)
$$
To separate the variables, we divide both sides by $c^2 X(x)T(t)$ (assuming non-trivial solutions where these factors are not zero):
$$
\frac{1}{c^2 T(t)} \frac{d^2T}{dt^2} = \frac{1}{X(x)} \frac{d^2X}{dx^2}
$$
The left side of this equation depends only on time $t$, while the right side depends only on position $x$. The only way for a function of $t$ to equal a function of $x$ for all $x$ and $t$ is if both are equal to the same constant. We call this the **[separation constant](@entry_id:175270)**, which we denote by $-\lambda$.

This separation yields two ordinary differential equations (ODEs) [@problem_id:2156022]:
$$
\frac{d^2X}{dx^2} + \lambda X(x) = 0
$$
$$
\frac{d^2T}{dt^2} + c^2 \lambda T(t) = 0
$$

#### The Spatial Boundary Value Problem

The Dirichlet boundary conditions $u(0,t) = X(0)T(t) = 0$ and $u(L,t) = X(L)T(t) = 0$ must hold for all time $t$. For a non-trivial (i.e., moving) string, $T(t)$ cannot be identically zero. Therefore, the spatial function $X(x)$ must satisfy the boundary conditions:
$$
X(0) = 0 \quad \text{and} \quad X(L) = 0
$$
The problem for $X(x)$ is now a **boundary value problem**. To obtain physically meaningful, non-trivial solutions (i.e., $X(x)$ is not identically zero), we must analyze the sign of the [separation constant](@entry_id:175270) $\lambda$ [@problem_id:2155988].

*   **Case 1: $\lambda  0$**. Let $\lambda = -\mu^2$ for some real $\mu > 0$. The ODE becomes $X'' - \mu^2 X = 0$, with the general solution $X(x) = A\cosh(\mu x) + B\sinh(\mu x)$. Applying $X(0)=0$ gives $A\cosh(0) + B\sinh(0) = A = 0$. The solution simplifies to $X(x) = B\sinh(\mu x)$. The second condition, $X(L)=0$, requires $B\sinh(\mu L) = 0$. Since $\mu > 0$ and $L > 0$, $\sinh(\mu L) \neq 0$. Thus, we must have $B=0$. This leads to $X(x)=0$ for all $x$, the trivial solution, which corresponds to no vibration.

*   **Case 2: $\lambda = 0$**. The ODE becomes $X'' = 0$, with the general solution $X(x) = A + Bx$. Applying $X(0)=0$ gives $A=0$. The solution is $X(x)=Bx$. The second condition, $X(L)=0$, implies $BL=0$, which means $B=0$. Again, this leads only to the [trivial solution](@entry_id:155162) $X(x)=0$.

*   **Case 3: $\lambda > 0$**. Let $\lambda = k^2$ for some real $k > 0$. The ODE becomes $X'' + k^2 X = 0$, with the general solution $X(x) = A\cos(kx) + B\sin(kx)$. Applying the first boundary condition, $X(0)=0$, gives $A\cos(0) + B\sin(0) = A = 0$. The solution reduces to $X(x) = B\sin(kx)$. Now, applying the second boundary condition, $X(L)=0$, we get $B\sin(kL) = 0$. To avoid the trivial solution, we must have $B \neq 0$. This forces the condition $\sin(kL) = 0$.

The sine function is zero at integer multiples of $\pi$. Therefore, we must have $kL = n\pi$ for $n = 1, 2, 3, \ldots$. (We exclude $n=0$ as it leads to $k=0$ and the trivial solution, and negative integers for $n$ only produce a sign change in the solution, which can be absorbed into the constant $B$).

This analysis reveals a profound result: non-trivial solutions exist only for a [discrete set](@entry_id:146023) of positive values for the [separation constant](@entry_id:175270). These allowed values are the **eigenvalues** of the [boundary value problem](@entry_id:138753) [@problem_id:2155982]:
$$
\lambda_n = k_n^2 = \left(\frac{n\pi}{L}\right)^2, \quad n = 1, 2, 3, \ldots
$$
For each eigenvalue $\lambda_n$, there is a corresponding non-[trivial solution](@entry_id:155162) for $X(x)$, known as an **eigenfunction**:
$$
X_n(x) = \sin\left(\frac{n\pi x}{L}\right)
$$
These [eigenfunctions](@entry_id:154705) represent the fundamental spatial shapes, or **[normal modes](@entry_id:139640)**, of the [vibrating string](@entry_id:138456). The integer $n$ corresponds to the number of antinodes (humps) in the standing wave shape.

#### The Temporal Solution and Normal Frequencies

Having found the discrete eigenvalues $\lambda_n$, we now solve the temporal ODE for each mode $n$:
$$
\frac{d^2T_n}{dt^2} + c^2 \lambda_n T_n(t) = 0 \quad \implies \quad \frac{d^2T_n}{dt^2} + \left(\frac{n\pi c}{L}\right)^2 T_n(t) = 0
$$
This is the equation for a simple harmonic oscillator. Its general solution is:
$$
T_n(t) = A_n \cos(\omega_n t) + B_n \sin(\omega_n t)
$$
where $\omega_n$ is the **[angular frequency](@entry_id:274516)** (or natural frequency) of the $n$-th mode:
$$
\omega_n = \frac{n\pi c}{L}
$$
The frequencies are integer multiples of the [fundamental frequency](@entry_id:268182) $\omega_1 = \pi c/L$. This harmonic relationship is the physical basis for the pleasing sound of many musical instruments.

Combining the spatial and temporal parts, we obtain the set of normal mode solutions for the wave equation with Dirichlet boundary conditions:
$$
u_n(x,t) = X_n(x)T_n(t) = \sin\left(\frac{n\pi x}{L}\right) \left( A_n \cos(\omega_n t) + B_n \sin(\omega_n t) \right)
$$

### The General Solution and Fourier's Method

Each normal mode $u_n(x,t)$ is a valid solution to the wave equation and its boundary conditions. Since the wave equation is linear, any sum of these solutions is also a solution. This is the **[principle of superposition](@entry_id:148082)**. The most general solution is an infinite series superposition of all possible [normal modes](@entry_id:139640):
$$
u(x,t) = \sum_{n=1}^{\infty} u_n(x,t) = \sum_{n=1}^{\infty} \sin\left(\frac{n\pi x}{L}\right) \left( A_n \cos(\omega_n t) + B_n \sin(\omega_n t) \right)
$$
The final step is to determine the coefficients $A_n$ and $B_n$ using the initial conditions of the string:
$$
u(x,0) = f(x) \quad \text{(initial position)}
$$
$$
\frac{\partial u}{\partial t}(x,0) = g(x) \quad \text{(initial velocity)}
$$
At $t=0$, the general solution becomes:
$$
f(x) = u(x,0) = \sum_{n=1}^{\infty} A_n \sin\left(\frac{n\pi x}{L}\right)
$$
$$
g(x) = \frac{\partial u}{\partial t}(x,0) = \sum_{n=1}^{\infty} (B_n \omega_n) \sin\left(\frac{n\pi x}{L}\right)
$$
These are **Fourier sine series** expansions for the functions $f(x)$ and $g(x)$. To find the coefficients, we exploit the **orthogonality** of the sine eigenfunctions on the interval $[0, L]$:
$$
\int_0^L \sin\left(\frac{n\pi x}{L}\right) \sin\left(\frac{m\pi x}{L}\right) dx = \begin{cases} L/2  \text{if } n=m \\ 0  \text{if } n \neq m \end{cases}
$$
By multiplying the series for $f(x)$ by $\sin(m\pi x/L)$ and integrating from $0$ to $L$, all terms in the sum vanish except for the one where $n=m$. This isolates the coefficient $A_m$:
$$
A_n = \frac{2}{L} \int_0^L f(x) \sin\left(\frac{n\pi x}{L}\right) dx
$$
Similarly, for the velocity coefficients:
$$
B_n \omega_n = \frac{2}{L} \int_0^L g(x) \sin\left(\frac{n\pi x}{L}\right) dx \quad \implies \quad B_n = \frac{2}{n\pi c} \int_0^L g(x) \sin\left(\frac{n\pi x}{L}\right) dx
$$
For instance, if the [initial conditions](@entry_id:152863) are already given in terms of sine functions, the coefficients can be found by simple inspection. If a string has an initial shape $u(x,0) = A_1 \sin(\frac{\pi x}{L}) + A_2 \sin(\frac{4\pi x}{L})$ and [initial velocity](@entry_id:171759) $\frac{\partial u}{\partial t}(x,0) = B_1 \sin(\frac{2\pi x}{L})$, by matching terms we can immediately identify $A_1$, $A_2$, and $B_2 \omega_2 = B_1$ as the only non-zero coefficients, leading to a simple, finite-term solution [@problem_id:2156010].

More generally, for any reasonably well-behaved initial shape, such as a string plucked into a triangular shape, these integrals can be computed to find the complete set of Fourier coefficients that define the subsequent motion [@problem_id:2156024]. For a string plucked at $x=d$ to a height $h$, the coefficients are found to be $A_n = \frac{2hL^2}{n^2\pi^2 d(L-d)} \sin(\frac{n\pi d}{L})$, illustrating how the pluck position and height influence the harmonic content of the vibration.

### Alternative Perspectives and Deeper Principles

#### Standing Waves as Superposed Traveling Waves

The normal mode solutions are called **standing waves** because the nodes (points of zero displacement) and antinodes (points of maximum displacement) remain at fixed positions. It is physically illuminating to see that every standing wave is, in fact, the superposition of two identical traveling waves moving in opposite directions. Using the product-to-sum trigonometric identity, $\sin(a)\cos(b) = \frac{1}{2}[\sin(a-b) + \sin(a+b)]$, we can rewrite a simple standing wave solution:
$$
u_n(x,t) = A \sin(k_n x) \cos(\omega_n t) = \frac{A}{2} \left[ \sin(k_n x - \omega_n t) + \sin(k_n x + \omega_n t) \right]
$$
Recalling that $\omega_n = c k_n$, this becomes:
$$
u_n(x,t) = \underbrace{\frac{A}{2} \sin\left(k_n(x - ct)\right)}_{\text{Right-traveling wave}} + \underbrace{\frac{A}{2} \sin\left(k_n(x + ct)\right)}_{\text{Left-traveling wave}}
$$
This decomposition shows that a [standing wave](@entry_id:261209) on a fixed string can be interpreted as a wave continuously traveling to the right, reflecting off the boundary at $x=L$, becoming a left-traveling wave, which then reflects at $x=0$, and so on. The interference of these perpetually reflecting waves creates the stable standing wave pattern [@problem_id:2156005].

#### D'Alembert's Solution and the Method of Images

An entirely different approach to [solving the wave equation](@entry_id:171826) is due to d'Alembert. For an [infinite string](@entry_id:168476) with [initial conditions](@entry_id:152863) $u(x,0)=f(x)$ and $u_t(x,0)=g(x)$, the solution is given by:
$$
u(x,t) = \frac{1}{2}[f(x-ct) + f(x+ct)] + \frac{1}{2c}\int_{x-ct}^{x+ct} g(s) ds
$$
This formula elegantly expresses the solution as a sum of a right-traveling and a left-traveling wave whose shapes are determined by the initial conditions. To apply this to a finite string on $[0, L]$ with fixed ends, we use the **[method of images](@entry_id:136235)**. The key is to extend the initial condition functions $f(x)$ and $g(x)$ from the interval $[0, L]$ to the entire real line in a way that automatically satisfies the boundary conditions. The correct extension for Dirichlet conditions is an **odd [periodic extension](@entry_id:176490)**. Specifically, we define an extended function $\tilde{f}(x)$ such that:
1.  $\tilde{f}(x) = f(x)$ for $x \in [0, L]$.
2.  $\tilde{f}(x) = -f(-x)$ for $x \in [-L, 0]$ (odd extension around $x=0$).
3.  $\tilde{f}(x)$ is periodic with period $2L$, i.e., $\tilde{f}(x+2L) = \tilde{f}(x)$.

The solution on the finite string is then given by d'Alembert's formula using these extended [initial conditions](@entry_id:152863). This method is particularly powerful for finding the solution at a specific point $(x,t)$ without having to compute an entire Fourier series [@problem_id:2155987]. For example, to find the displacement at $x=3/2, t=3$ for a string of length $L=4$ released from rest with a specific initial pulse shape $f(x)$, we can directly compute $u(3/2, 3) = \frac{1}{2}[\tilde{f}(3/2 - 3) + \tilde{f}(3/2 + 3)] = \frac{1}{2}[\tilde{f}(-3/2) + \tilde{f}(9/2)]$. The values of the extended function are found by applying the oddness and periodicity rules, providing a direct numerical answer.

#### Energy Conservation and Uniqueness

The total mechanical energy of the string is the sum of its kinetic energy (due to motion) and potential energy (due to stretching). For a string with [linear mass density](@entry_id:276685) $\rho$ and tension $T$, the energy is given by the integral:
$$
E(t) = \frac{1}{2} \int_0^L \left( \rho \left[\frac{\partial u}{\partial t}\right]^2 + T \left[\frac{\partial u}{\partial x}\right]^2 \right) dx
$$
For the wave equation with Dirichlet boundary conditions, this total energy is a **conserved quantity**, meaning $E(t)$ is constant for all time. We can therefore calculate the energy of the system by evaluating this integral at $t=0$ using the initial conditions [@problem_id:2155964].

The principle of [energy conservation](@entry_id:146975) also provides a rigorous way to prove the **uniqueness** of the solution. If we have two solutions, $u_A$ and $u_B$, corresponding to the same [initial conditions](@entry_id:152863), their difference $w = u_B - u_A$ must satisfy the wave equation with zero initial conditions ($w(x,0)=0$ and $w_t(x,0)=0$). The energy of this difference wave, $E_w$, must be zero at $t=0$. Since energy is conserved, $E_w$ must be zero for all time. An energy of zero implies that both the kinetic and potential energy densities are zero everywhere, meaning $w_t \equiv 0$ and $w_x \equiv 0$. This forces $w(x,t)$ to be a constant, and since $w(x,0)=0$, that constant must be zero. Therefore, $w(x,t)=0$ for all $x$ and $t$, which means $u_A = u_B$. This confirms that specifying both initial position and [initial velocity](@entry_id:171759) is essential for a unique physical outcome [@problem_id:2155984].

Furthermore, due to the orthogonality of the normal modes, the total energy of a complex vibration is simply the sum of the energies of its constituent modes. For a solution composed of several modes, the total energy is constant and can be calculated as the sum of the initial kinetic and potential energies contributed by each mode [@problem_id:2155964].