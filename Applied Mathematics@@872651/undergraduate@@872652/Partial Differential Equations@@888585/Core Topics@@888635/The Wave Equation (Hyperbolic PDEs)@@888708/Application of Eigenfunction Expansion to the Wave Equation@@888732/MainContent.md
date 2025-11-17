## Introduction
The wave equation is a cornerstone of mathematical physics, describing a vast array of phenomena from the vibrations of a guitar string to the [propagation of sound](@entry_id:194493) and light. While the equation itself is elegant, solving it for realistic scenarios with specific initial states and boundary constraints presents a significant challenge. This is where the powerful technique of [eigenfunction expansion](@entry_id:151460) comes into play. It provides a systematic method to deconstruct seemingly complex wave motions into a superposition of simpler, fundamental building blocks known as normal modes.

This article addresses the knowledge gap between knowing the wave equation and being able to apply a robust method to solve it. By mastering [eigenfunction expansion](@entry_id:151460), you will gain the ability to analyze and predict the behavior of a wide range of vibrating systems. Across the following sections, you will embark on a journey from fundamental principles to advanced applications. In "Principles and Mechanisms," you will learn the core mechanics of the method, from [separation of variables](@entry_id:148716) to handling initial conditions and [forced vibrations](@entry_id:167019). Following this, "Applications and Interdisciplinary Connections" will broaden your perspective, showcasing how this single idea unifies concepts in [acoustics](@entry_id:265335), structural engineering, and even quantum mechanics. Finally, "Hands-On Practices" will allow you to solidify your understanding by tackling concrete problems that highlight key physical insights derived from the method.

## Principles and Mechanisms

The analysis of wave phenomena, as described by [partial differential equations](@entry_id:143134) like the wave equation, is profoundly simplified by a powerful mathematical technique known as [eigenfunction expansion](@entry_id:151460). This method is predicated on the principle of superposition and involves decomposing a complex wave motion into a sum of simpler, fundamental patterns of vibration called **[normal modes](@entry_id:139640)**. Each normal mode oscillates at a specific, characteristic frequency. By understanding these fundamental building blocks, we can construct solutions for a wide variety of physical scenarios, from the vibrations of a guitar string to the longitudinal oscillations of an elastic bar. This chapter will systematically develop the principles of this method and explore its mechanisms through a series of illustrative applications.

### The Superposition Principle and Normal Modes

Let us consider the canonical example of a flexible string of length $L$, fixed at both ends. Its small transverse displacement, $u(x,t)$, is governed by the [one-dimensional wave equation](@entry_id:164824):
$$
\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2}
$$
Here, $c$ is the constant wave propagation speed, determined by the string's tension and mass density. The fixed endpoints impose the boundary conditions $u(0,t) = 0$ and $u(L,t) = 0$.

We seek solutions using the method of **[separation of variables](@entry_id:148716)**, assuming the displacement can be written as a product of a function of position $x$ only and a function of time $t$ only: $u(x,t) = X(x)T(t)$. Substituting this into the wave equation and rearranging terms allows us to separate the variables:
$$
\frac{1}{c^2 T(t)} \frac{d^2 T}{dt^2} = \frac{1}{X(x)} \frac{d^2 X}{dx^2}
$$
Since the left side depends only on $t$ and the right side depends only on $x$, they must both be equal to a constant, which we denote as $-\lambda$. This yields two [ordinary differential equations](@entry_id:147024):

1.  The spatial equation: $\frac{d^2 X}{dx^2} + \lambda X(x) = 0$, with boundary conditions $X(0) = 0$ and $X(L) = 0$.
2.  The temporal equation: $\frac{d^2 T}{dt^2} + \lambda c^2 T(t) = 0$.

The spatial equation, along with its boundary conditions, constitutes an **[eigenvalue problem](@entry_id:143898)**. Non-trivial solutions for $X(x)$ exist only for specific values of $\lambda$, known as **eigenvalues**. For the fixed-end string, these are:
$$
\lambda_n = \left(\frac{n\pi}{L}\right)^2, \quad \text{for } n = 1, 2, 3, \ldots
$$
The corresponding solutions, $X_n(x)$, are the **[eigenfunctions](@entry_id:154705)** or **[normal modes](@entry_id:139640)** of the system:
$$
X_n(x) = \sin\left(\frac{n\pi x}{L}\right)
$$
Each eigenfunction represents a fundamental standing wave pattern the string can form. The integer $n$ corresponds to the number of antinodes (loops) in the pattern.

For each eigenvalue $\lambda_n$, the temporal equation becomes a [simple harmonic oscillator equation](@entry_id:196017):
$$
\frac{d^2 T_n}{dt^2} + \omega_n^2 T_n(t) = 0
$$
where $\omega_n = c\sqrt{\lambda_n} = \frac{n\pi c}{L}$ are the **natural frequencies** or **eigenfrequencies** of the system. The solution for $T_n(t)$ is a sinusoidal oscillation:
$$
T_n(t) = A_n \cos(\omega_n t) + B_n \sin(\omega_n t)
$$
The full solution $u(x,t)$ is a linear superposition of all possible modes, a principle that holds because the wave equation is linear. This results in the **[eigenfunction expansion](@entry_id:151460)**:
$$
u(x,t) = \sum_{n=1}^{\infty} u_n(x,t) = \sum_{n=1}^{\infty} \sin\left(\frac{n\pi x}{L}\right) \left[ A_n \cos\left(\frac{n\pi c t}{L}\right) + B_n \sin\left(\frac{n\pi c t}{L}\right) \right]
$$
This series represents any possible motion of the string as a sum of its fundamental vibrations.

### Determining Modal Amplitudes from Initial Conditions

The specific motion of the string is determined by its state at $t=0$: its initial displacement $u(x,0) = f(x)$ and [initial velocity](@entry_id:171759) $u_t(x,0) = g(x)$. The coefficients $A_n$ and $B_n$ in the expansion are found by matching this series to the [initial conditions](@entry_id:152863).

At $t=0$, the general solution gives:
$$
u(x,0) = f(x) = \sum_{n=1}^{\infty} A_n \sin\left(\frac{n\pi x}{L}\right)
$$
$$
u_t(x,0) = g(x) = \sum_{n=1}^{\infty} B_n \omega_n \sin\left(\frac{n\pi x}{L}\right)
$$
These are the **Fourier sine series** for the functions $f(x)$ and $g(x)$. The coefficients are determined by exploiting the **orthogonality** of the sine eigenfunctions over the interval $[0, L]$:
$$
\int_0^L \sin\left(\frac{n\pi x}{L}\right) \sin\left(\frac{m\pi x}{L}\right) dx = \begin{cases} L/2  \text{if } n=m \\ 0  \text{if } n \neq m \end{cases}
$$
Multiplying the series for $f(x)$ by $\sin(m\pi x/L)$ and integrating from $0$ to $L$ isolates the coefficient $A_m$. This procedure yields:
$$
A_n = \frac{2}{L} \int_0^L f(x) \sin\left(\frac{n\pi x}{L}\right) dx
$$
$$
B_n = \frac{2}{L\omega_n} \int_0^L g(x) \sin\left(\frac{n\pi x}{L}\right) dx = \frac{2}{n\pi c} \int_0^L g(x) \sin\left(\frac{n\pi x}{L}\right) dx
$$

A powerful illustration arises when the initial condition itself is a single normal mode [@problem_id:2089339]. Suppose a string is released from rest ($g(x)=0$) with an initial shape $u(x,0) = A \sin(\pi x/L)$. This shape corresponds precisely to the first [eigenfunction](@entry_id:149030) ($n=1$). The [orthogonality property](@entry_id:268007) immediately tells us that all coefficients $A_n$ are zero for $n \ne 1$, and $A_1 = A$. Since $g(x)=0$, all $B_n$ are zero. The [infinite series](@entry_id:143366) collapses to a single term:
$$
u(x,t) = A \cos\left(\frac{\pi c t}{L}\right) \sin\left(\frac{\pi x}{L}\right)
$$
The string oscillates purely in its [fundamental mode](@entry_id:165201). The velocity at any point is $u_t(x,t) = -A \frac{\pi c}{L} \sin(\frac{\pi c t}{L}) \sin(\frac{\pi x}{L})$. At the midpoint ($x=L/2$), $\sin(\pi x/L)=1$, and the maximum speed is reached when $\sin(\pi c t/L) = \pm 1$, yielding a maximum speed of $A \pi c / L$.

Similarly, initial displacement and initial velocity can excite different modes independently. Consider a string with initial shape $u(x,0) = A \sin(\pi x/L)$ and [initial velocity](@entry_id:171759) $u_t(x,0) = V \sin(3\pi x/L)$ [@problem_id:2089321]. The initial shape only excites the $n=1$ mode, yielding $A_1=A$ and all other $A_n=0$. The [initial velocity](@entry_id:171759) profile corresponds to the $n=3$ mode, so only $B_3$ is non-zero, with $B_3 \omega_3 = V$, or $B_3 = V / \omega_3 = VL/(3\pi c)$. The resulting motion is a simple superposition of two independently oscillating modes:
$$
u(x,t) = A\cos\left(\frac{\pi c t}{L}\right)\sin\left(\frac{\pi x}{L}\right)+\frac{V L}{3\pi c}\sin\left(\frac{3\pi c t}{L}\right)\sin\left(\frac{3\pi x}{L}\right)
$$

### Analysis of Complex Vibrations

More realistic scenarios involve initial shapes that are not simple sine functions. For instance, a string plucked at its midpoint has a triangular initial shape [@problem_id:2089349]. A string struck by a narrow hammer has a localized initial velocity profile [@problem_id:2089330]. In these cases, the [eigenfunction expansion](@entry_id:151460) will contain an infinite number of modes. The coefficients $A_n$ and $B_n$ represent the "spectral content" of the initial conditions, indicating how much each normal mode contributes to the overall motion. Typically, the magnitude of the coefficients $|A_n|$ and $|B_n|$ decreases for higher $n$, meaning that the low-frequency, long-wavelength modes dominate the motion.

The symmetry of the initial conditions can provide profound insight into which modes will be present in the subsequent motion. Consider an initial displacement $f(x)$ that is symmetric about the string's midpoint, i.e., $f(x) = f(L-x)$ [@problem_id:2089358]. The normal modes $\sin(n\pi x/L)$ are themselves either symmetric (for odd $n$) or antisymmetric (for even $n$) about the midpoint. The integral for the coefficient $A_n$ is $\frac{2}{L} \int_0^L f(x) \sin(n\pi x/L) dx$. When $n$ is even, we are integrating the product of a symmetric function ($f(x)$) and an antisymmetric function ($\sin(n\pi x/L)$), which results in zero. Thus, for any symmetric initial displacement, all even-numbered modes are guaranteed to be absent ($A_n=0$ for $n=2, 4, 6, \dots$). This has a direct impact on the timbre, or sound quality, of a plucked string. Plucking a string exactly at its center tends to suppress the second harmonic and all other even harmonics.

A fascinating consequence of this modal structure appears in the [time evolution](@entry_id:153943). For a string released from rest from a triangular shape $f(x)$, the solution at time $t=L/c$ is found to be $u(x, L/c) = -f(x)$ [@problem_id:2089349]. The string's shape is perfectly inverted. This is because the time-evolution term for each mode is $\cos(n\pi c t/L)$. At $t=L/c$, this becomes $\cos(n\pi) = (-1)^n$. The solution becomes $\sum A_n (-1)^n \sin(n\pi x/L)$. For a symmetric pluck, only odd $n$ are present, so $(-1)^n = -1$ for all excited modes, and the entire shape inverts.

### Energy in Vibrating Systems

The [eigenfunction expansion](@entry_id:151460) is also a powerful tool for analyzing the energy of a vibrating system. The total mechanical energy $E(t)$ of the string is the sum of its kinetic energy (due to motion) and potential energy (due to stretching). For a string with [linear mass density](@entry_id:276685) $\rho$ and tension $T$:
$$
E(t) = \text{Kinetic Energy} + \text{Potential Energy} = \frac{1}{2} \int_0^L \left[ \rho (u_t)^2 + T (u_x)^2 \right] dx
$$
By substituting the full [eigenfunction expansions](@entry_id:177104) for $u_t$ and $u_x$ into this integral and leveraging the orthogonality of both [sine and cosine functions](@entry_id:172140), a remarkable result emerges. The cross-terms between different modes ($n \ne m$) integrate to zero, meaning the total energy is simply the sum of the energies contained in each individual mode [@problem_id:2089332].
$$
E(t) = \sum_{n=1}^{\infty} E_n(t)
$$
Furthermore, when calculating the energy $E_n(t)$ for a single mode, the time-dependent terms involving $\sin^2(\omega_n t)$ and $\cos^2(\omega_n t)$ combine in such a way that the time dependence vanishes completely. This is a manifestation of the **[conservation of energy](@entry_id:140514)**. The energy of each mode is constant, and therefore the total energy of the ideal, unforced system is constant. The total energy can be expressed directly in terms of the Fourier coefficients of the initial conditions, $f_n$ and $g_n$:
$$
E = \frac{L}{4} \sum_{n=1}^{\infty} \left( T \lambda_{n} f_{n}^{2} + \rho g_{n}^{2} \right)
$$
This elegant formula shows that the total energy is locked in at $t=0$ and is partitioned among the modes according to the spectral content of the initial displacement and velocity.

### Forced Vibrations and Resonance

The [eigenfunction expansion](@entry_id:151460) method extends naturally to the **[forced wave equation](@entry_id:174142)**, which models a system subjected to an external force $F(x,t)$:
$$
\frac{\partial^2 u}{\partial t^2} = c^2 \frac{\partial^2 u}{\partial x^2} + \frac{F(x,t)}{\rho}
$$
We expand both the solution $u(x,t)$ and the normalized [forcing term](@entry_id:165986) $F(x,t)/\rho$ in the basis of the system's [eigenfunctions](@entry_id:154705). For a fixed string, this means:
$$
u(x,t) = \sum_{n=1}^{\infty} q_n(t) \sin\left(\frac{n\pi x}{L}\right) \quad \text{and} \quad \frac{F(x,t)}{\rho} = \sum_{n=1}^{\infty} \phi_n(t) \sin\left(\frac{n\pi x}{L}\right)
$$
where $q_n(t)$ are the unknown modal coordinates and $\phi_n(t)$ are the known modal forces, found by the usual Fourier coefficient formula. Substituting these into the PDE transforms the complex partial differential equation into a set of independent ordinary differential equations, one for each mode:
$$
\frac{d^2 q_n}{dt^2} + \omega_n^2 q_n(t) = \phi_n(t)
$$
Each mode behaves as an independent harmonic oscillator driven by its corresponding modal force.

A critical phenomenon in forced systems is **resonance**. This occurs when the driving frequency of the external force matches one of the natural frequencies of the system. Consider a [forcing term](@entry_id:165986) $F(x,t) = K \sin(\pi x/L) \sin(\omega t)$, where the spatial part matches the first mode [@problem_id:2089338]. Orthogonality ensures that only the first modal force, $\phi_1(t)$, is non-zero. If the driving frequency $\omega$ is set to the [fundamental frequency](@entry_id:268182) $\omega_1 = \pi c/L$, the equation for the first mode becomes:
$$
\frac{d^2 q_1}{dt^2} + \omega_1^2 q_1(t) = (\text{const}) \times \sin(\omega_1 t)
$$
The solution to this ODE for an initially resting string contains a term that grows linearly with time: $t \cos(\omega_1 t)$. This **secular growth** leads to an amplitude that increases without bound (in an idealized, undamped system), a defining characteristic of resonance.

In the case of a time-independent (static) force $F(x)$, the modal forces $\phi_n$ are constants. The modal equation $a_n'' + \omega_n^2 a_n = \phi_n$ for a system starting from rest has the solution $a_n(t) = \frac{\phi_n}{\omega_n^2}(1-\cos(\omega_n t))$ [@problem_id:2089302]. The displacement for each mode oscillates about a new non-zero [equilibrium position](@entry_id:272392) $\phi_n/\omega_n^2$. The full solution is an oscillation around a new static shape determined by the external force.

### Generalizations and Sturm-Liouville Theory

The power of the [eigenfunction](@entry_id:149030) method is not limited to strings with fixed ends. The method applies to a vast class of problems with different boundary conditions and even variable coefficients.

For example, the [longitudinal vibrations](@entry_id:176640) of an elastic bar with **free ends** are governed by the same wave equation but with **Neumann boundary conditions**: $u_x(0,t) = 0$ and $u_x(L,t) = 0$ [@problem_id:2089361]. Solving the spatial [eigenvalue problem](@entry_id:143898) with these conditions yields a different set of eigenfunctions:
$$
X_n(x) = \cos\left(\frac{n\pi x}{L}\right), \quad \text{for } n = 0, 1, 2, \ldots
$$
The solution is now a Fourier cosine series. A notable difference is the presence of the $n=0$ mode, $X_0(x) = \text{constant}$. This mode, with a frequency $\omega_0=0$, corresponds to a rigid-body translation of the entire bar, a motion that is physically possible for a free-ended object.

More generally, many one-dimensional wave problems lead to a spatial equation of the form:
$$
\frac{d}{dx}\left(p(x)\frac{dX}{dx}\right) - q(x)X + \lambda w(x)X = 0
$$
This is known as a **Sturm-Liouville equation**. For a string with variable tension $T(x)$ and constant density $\rho$, the equation for the [normal modes](@entry_id:139640) takes this form with $p(x)=T(x)$, $q(x)=0$, and $w(x)=\rho$ [@problem_id:2089360]. **Sturm-Liouville theory** guarantees that for a wide range of functions $p(x)$, $q(x)$, and $w(x)$ and appropriate boundary conditions, there exists an infinite set of real eigenvalues $\lambda_n$ and a corresponding complete set of eigenfunctions $X_n(x)$. These eigenfunctions are orthogonal, but with respect to the weight function $w(x)$. This means the principle of [eigenfunction expansion](@entry_id:151460) is a robust and general method, allowing us to analyze vibrations in complex, non-uniform media by decomposing the motion into a sum of its characteristic, orthogonal normal modes.