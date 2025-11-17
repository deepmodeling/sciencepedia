## Introduction
The study of dynamical systems, which describe how systems evolve over time, has traditionally focused on the geometric paths of states in a state space. However, many systems of interest, from fluid flows to economic models, are governed by complex nonlinear rules that make analysis and prediction exceptionally difficult. Koopman [operator theory](@entry_id:139990) offers a revolutionary change in perspective. Instead of tracking the nonlinear evolution of states, it focuses on the linear evolution of observable functions of those states. This elegant approach transforms the intractable problem of nonlinear dynamics into the well-understood realm of [linear operator theory](@entry_id:151141).

This article addresses the fundamental challenge of analyzing and modeling nonlinear systems by introducing the Koopman operator as a powerful linearization tool. You will learn how this shift from state space to a function space provides a unified framework for understanding complex behaviors. The first chapter, "Principles and Mechanisms," will lay the theoretical groundwork, defining the Koopman operator, establishing its crucial property of linearity, and introducing the concepts of its spectrum, eigenfunctions, and [invariant subspaces](@entry_id:152829). The second chapter, "Applications and Interdisciplinary Connections," will demonstrate the practical power of this theory, exploring its use in [data-driven modeling](@entry_id:184110) with Dynamic Mode Decomposition (DMD), the design of [control systems](@entry_id:155291), and its surprising connections to fields like quantum computing. Finally, the "Hands-On Practices" section will provide concrete exercises to solidify your understanding of these core concepts.

## Principles and Mechanisms

The analysis of dynamical systems traditionally focuses on the geometric structure of trajectories in the state space, a perspective established by Poincaré. Koopman [operator theory](@entry_id:139990) offers a complementary and powerful viewpoint. Instead of tracking the evolution of individual states, we track the evolution of functions defined on the state space. These functions, known as **observables**, can represent any measurable quantity of the system. This shift in perspective transforms the study of a potentially complex, nonlinear system into the study of a linear operator acting on a function space. While this space of functions is typically infinite-dimensional, the linearity of the operator grants us access to the powerful tools of [functional analysis](@entry_id:146220) and spectral theory.

### The Koopman Operator: A Functional-Analytic View of Dynamics

Let us consider a dynamical system whose state at a given time is represented by a point $x$ in a state space $M$. The evolution of the system is described by a map that takes the current state to a future state.

For a **discrete-time system**, this evolution is governed by a map $f: M \to M$, such that if the state at step $k$ is $x_k$, the state at the next step is $x_{k+1} = f(x_k)$. An observable is any scalar-valued function $g: M \to \mathbb{C}$. The **Koopman operator**, denoted by $K$, describes how the value of this observable changes in a single time step. Its action is defined by composition with the dynamics map $f$:

$$
(K g)(x) = g(f(x))
$$

This equation states that the new function, $Kg$, evaluated at the old state $x$, gives the same value as the original function, $g$, evaluated at the new state, $f(x)$. For example, if we have a simple population model where the population size evolves according to $p_{n+1} = f(p_n) = a p_n - b p_n^2$, and we are interested in an "environmental stress" observable given by $g(p) = k p^2$, the Koopman operator allows us to find the stress function for the next year. Applying the definition gives $(Kg)(p) = g(f(p)) = k(a p - b p^2)^2$. This expands to a fourth-degree polynomial, illustrating how the operator maps simple functions to more complex ones while retaining a clear structure [@problem_id:1688982].

For a **continuous-time system**, the dynamics are described by an [ordinary differential equation](@entry_id:168621) $\dot{x} = F(x)$, which generates a **[flow map](@entry_id:276199)** $\Phi_t: M \to M$. The [flow map](@entry_id:276199) $\Phi_t(x_0)$ gives the state of the system at time $t$ given it started at state $x_0$. The Koopman operator here is a one-parameter family of operators, $K_t$, defined as:

$$
(K_t g)(x_0) = g(\Phi_t(x_0))
$$

This definition has a direct physical interpretation. Imagine a satellite component whose temperature $T$ cools according to $\dot{T} = -\alpha T$. If a sensor measures a voltage proportional to the temperature squared, $g(T) = cT^2$, then $(K_t g)(T_0)$ is precisely the voltage reading at time $t$ given an initial temperature $T_0$. To calculate this, one first solves for the state at time $t$, which is $T(t) = T_0 \exp(-\alpha t)$, and then evaluates the observable: $(K_t g)(T_0) = g(T_0 \exp(-\alpha t)) = c(T_0 \exp(-\alpha t))^2 = c T_0^2 \exp(-2\alpha t)$ [@problem_id:1689025]. In both discrete and continuous time, the Koopman operator provides a rule for evolving functions forward in time, consistent with the underlying [system dynamics](@entry_id:136288).

### The Cornerstone of Linearity

The most significant feature of the Koopman operator is its **linearity**. This property holds regardless of whether the underlying dynamical system $f$ or $\Phi_t$ is linear or nonlinear. The operator acts on a vector space of observable functions, and its linearity means that for any two observables $g_1$ and $g_2$ and any two scalar constants $c_1$ and $c_2$:

$$
K(c_1 g_1 + c_2 g_2) = c_1 (K g_1) + c_2 (K g_2)
$$

The proof follows directly from the definition. In the discrete-time case:
$$
(K(c_1 g_1 + c_2 g_2))(x) = (c_1 g_1 + c_2 g_2)(f(x)) = c_1 g_1(f(x)) + c_2 g_2(f(x)) = c_1 (K g_1)(x) + c_2 (K g_2)(x)
$$
A similar proof holds for the continuous-time operator $K_t$.

This linearity allows us to transfer the challenges of [nonlinear dynamics](@entry_id:140844) into the realm of linear analysis. Consider the famously complex [logistic map](@entry_id:137514), $x_{k+1} = T(x) = rx(1-x)$. While the [state evolution](@entry_id:755365) is nonlinear, the associated Koopman operator $K$ is linear. If we take two simple observables, such as the [population density](@entry_id:138897) $g_1(x) = x$ and the interaction rate $g_2(x) = x^2$, we can analyze their evolution. The Koopman operator maps them as follows:
$(K g_1)(x) = T(x) = rx - rx^2$
$(K g_2)(x) = (T(x))^2 = (rx(1-x))^2 = r^2x^2 - 2r^2x^3 + r^2x^4$

Due to linearity, the evolution of any linear combination of these observables, such as $H(x) = c_1 g_1(x) + c_2 g_2(x)$, is simply $KH(x) = c_1(Kg_1)(x) + c_2(Kg_2)(x)$. We can compute this directly, resulting in a predictable polynomial expression, even though the underlying dynamics can exhibit chaotic behavior [@problem_id:1689002]. This principle is foundational: by understanding how the Koopman operator acts on a basis of functions, we can predict the evolution of any function that can be expressed in that basis.

### Spectral Decomposition: Eigenfunctions and Eigenvalues

Since the Koopman operator is linear, we can study its structure using spectral theory. The most important components of this [spectral analysis](@entry_id:143718) are the **[eigenfunctions](@entry_id:154705)** and **eigenvalues** of the operator.

An observable $\phi(x)$ is an [eigenfunction](@entry_id:149030) of the discrete-time Koopman operator $K$ if it satisfies:
$$
K\phi = \mu\phi \quad \Leftrightarrow \quad \phi(f(x)) = \mu\phi(x)
$$
where $\mu \in \mathbb{C}$ is the corresponding eigenvalue.

For a continuous-time system, the [eigenfunction](@entry_id:149030) equation is:
$$
K_t\phi = \lambda_t\phi \quad \Leftrightarrow \quad \phi(\Phi_t(x)) = \lambda_t\phi(x)
$$
For consistency, the eigenvalues $\lambda_t$ must form a group, $\lambda_{t+s} = \lambda_t \lambda_s$, which implies they have an exponential form $\lambda_t = \exp(\omega t)$ for some complex constant $\omega$, often called the continuous-time eigenvalue or frequency.

A particularly useful tool for finding these eigenvalues in [continuous-time systems](@entry_id:276553) is the **infinitesimal generator** of the Koopman semigroup, defined as:
$$
Lg = \lim_{t \to 0} \frac{K_t g - g}{t}
$$
For an eigenfunction $\phi$, this definition simplifies to $L\phi = \omega\phi$. The generator can also be expressed as a directional derivative along the vector field $F(x)$ of the dynamics:
$$
Lg(x) = F(x) \cdot \nabla g(x)
$$
This transforms the search for eigenfunctions into solving the partial differential equation $F(x) \cdot \nabla \phi(x) = \omega \phi(x)$. For example, in a 2D linear system describing spiral motion, $\dot{x} = \alpha x - \beta y$ and $\dot{y} = \beta x + \alpha y$, the complex observable $\psi(x, y) = x+iy$ is an [eigenfunction](@entry_id:149030). By applying the generator, we find $L\psi = (\alpha x - \beta y)(1) + (\beta x + \alpha y)(i) = (\alpha + i\beta)(x+iy) = (\alpha+i\beta)\psi$. Comparing this to $L\psi = \omega\psi$, we identify the continuous-time eigenvalue as $\omega = \alpha + i\beta$. The corresponding eigenvalue for the operator $K_t$ is $\exp(\omega t) = \exp((\alpha+i\beta)t)$ [@problem_id:1689036]. The real part $\alpha$ governs the growth or decay, while the imaginary part $\beta$ governs the rotation.

### Applications of Koopman Eigenfunctions

The power of finding eigenfunctions lies in their ability to simplify prediction and analysis.

#### Linear Prediction of Observables
Once an [eigenfunction](@entry_id:149030) $\phi$ and its corresponding eigenvalue ($\mu$ or $\omega$) are known, predicting the future value of the observable $\phi$ becomes trivial. For an initial state $x_0$, the value of the observable at a future time $t$ (or step $k$) is given by:
$$
\phi(x_k) = \mu^k \phi(x_0) \quad \text{(discrete time)}
$$
$$
\phi(x(t)) = \exp(\omega t) \phi(x_0) \quad \text{(continuous time)}
$$
This provides a linear, closed-form prediction for the evolution of the observable $\phi$, completely bypassing the need to solve the original nonlinear equations of motion for the state $x(t)$. For instance, in a nonlinear system like $\dot{x} = -ax + bx^3$, one can verify that the function $\phi(x) = x^{-2} - b/a$ is an [eigenfunction](@entry_id:149030) with continuous-time eigenvalue $\omega = 2a$. Therefore, without solving the nonlinear ODE for $x(t)$, we can immediately state that the value of this observable evolves as $\phi(x(t)) = \phi(x_0) \exp(2at) = (x_0^{-2} - b/a)\exp(2at)$ [@problem_id:1688981].

Furthermore, because of linearity, if we can decompose an arbitrary observable $\psi$ into a [linear combination](@entry_id:155091) of eigenfunctions, $\psi(x) = \sum_i c_i \phi_i(x)$, its [time evolution](@entry_id:153943) is simply the weighted sum of the individual exponential evolutions:
$$
\psi(x(t)) = \sum_i c_i \phi_i(x(t)) = \sum_i c_i \phi_i(x_0) \exp(\omega_i t)
$$
This "Koopman [spectral decomposition](@entry_id:148809)" provides a complete linear model for the evolution of any observable that lies in the span of the discovered [eigenfunctions](@entry_id:154705) [@problem_id:1689024].

#### Physical Interpretation and Stability Analysis
Koopman eigenfunctions often have clear physical interpretations. A foundational example is a **conserved quantity**, or an integral of motion, which is a function $g(x)$ whose value remains constant along any trajectory: $g(\Phi_t(x)) = g(x)$. Comparing this to the eigenfunction definition, $g(\Phi_t(x)) = \exp(\omega t) g(x)$, we see that a conserved quantity is simply an eigenfunction with continuous-time eigenvalue $\omega = 0$ (or discrete-time eigenvalue $\mu=1$) [@problem_id:1689005].

The eigenvalues are also intimately linked to the stability of the system's fixed points and [limit cycles](@entry_id:274544). For a simple discrete-time linear system $x_{k+1} = \lambda x_k$, the state variable itself, $g(x)=x$, is a Koopman [eigenfunction](@entry_id:149030) with eigenvalue $\mu = \lambda$. The fixed point $x^*=0$ is asymptotically stable if and only if $|\lambda|  1$. This directly translates to the Koopman perspective: the fixed point is stable if the magnitude of the corresponding Koopman eigenvalue is less than 1 [@problem_id:1689007]. This principle generalizes: Koopman eigenvalues with magnitude less than one (or with negative real part in continuous time) correspond to observables that decay towards zero, indicating convergence towards a stable structure.

### Koopman-Invariant Subspaces and Finite-Dimensional Models

The primary theoretical challenge of Koopman [operator theory](@entry_id:139990) is that the operator acts on an [infinite-dimensional space](@entry_id:138791) of functions. However, for many systems of practical interest, we can find finite-dimensional subspaces of functions that are **invariant** under the action of the Koopman operator. A subspace $\mathcal{G}$ is Koopman-invariant if for any function $g \in \mathcal{G}$, the function $Kg$ (or $K_t g$) is also in $\mathcal{G}$.

If we can identify a basis of $N$ functions $\{g_1, ..., g_N\}$ that spans such an invariant subspace, then the action of the Koopman operator on any of these basis functions can be written as a [linear combination](@entry_id:155091) of the basis functions themselves. This means the Koopman operator, when restricted to this subspace, can be represented by a finite-dimensional $N \times N$ matrix.

Consider a nonlinear economic model $\dot{x} = \alpha x$, $\dot{y} = \beta y + \gamma x^2$. The state space is two-dimensional, but the dynamics are nonlinear due to the $x^2$ term. Let's examine the vector of [observables](@entry_id:267133) $\mathbf{g}(x,y) = (x, y, x^2)^T$. We find the time derivatives of these observables along the system's trajectories:
- $\frac{d}{dt} g_1 = \dot{x} = \alpha x = \alpha g_1$
- $\frac{d}{dt} g_2 = \dot{y} = \beta y + \gamma x^2 = \beta g_2 + \gamma g_3$
- $\frac{d}{dt} g_3 = \frac{d}{dt}(x^2) = 2x \dot{x} = 2x(\alpha x) = 2\alpha x^2 = 2\alpha g_3$

The time derivative of each observable is a linear combination of the observables in the set $\{g_1, g_2, g_3\}$. This confirms that the space spanned by these three functions is a Koopman-invariant subspace. The evolution of the vector of observables $\mathbf{g}$ is governed by a linear system $\dot{\mathbf{g}} = \mathbf{A} \mathbf{g}$, where $\mathbf{A}$ is a $3 \times 3$ matrix. This linear system can be solved to find a matrix [propagator](@entry_id:139558) $\mathbf{K}_t = \exp(\mathbf{A}t)$ such that $\mathbf{g}(t) = \mathbf{K}_t \mathbf{g}(0)$. This procedure effectively "linearizes" the nonlinear dynamics by embedding it in a higher-dimensional, but linear, space of [observables](@entry_id:267133) [@problem_id:1689045]. This is the central idea behind data-driven methods like Dynamic Mode Decomposition (DMD), which seek to find such finite-dimensional approximations from measurement data.

### The Koopman Spectrum and Qualitative Dynamics

The complete set of eigenvalues forms the **Koopman spectrum**. The nature of this spectrum reveals profound information about the qualitative long-term behavior of the dynamical system. The spectrum can be decomposed into two main types: discrete and continuous.

A **[discrete spectrum](@entry_id:150970)** (or pure [point spectrum](@entry_id:274057)) consists of isolated eigenvalues. Systems with a [discrete spectrum](@entry_id:150970) are typically associated with regular, recurrent behavior like periodic or [quasi-periodic motion](@entry_id:273617). For example, a simple rotation on a circle by an angle $\theta$ where $\theta/(2\pi)$ is irrational is quasi-periodic. Its Koopman operator has a [discrete spectrum](@entry_id:150970) of eigenvalues lying on the unit circle. For such a system, the temporal autocorrelation of an observable, which measures how the observable's value at one time relates to its value at a later time, will oscillate indefinitely without decaying to zero. This reflects the system's persistent "memory" and regular, non-mixing nature [@problem_id:1689016].

In contrast, a **[continuous spectrum](@entry_id:153573)** is associated with chaotic and mixing dynamics. In these systems, trajectories that start close together diverge exponentially, and the system appears to evolve randomly. An example is the map $x \to 2x \pmod{1}$ on the unit interval. For such systems, correlations between the state at different times decay to zero as the time separation grows. This is reflected in the autocorrelation function of a typical observable, which, according to the Riemann-Lebesgue lemma, will decay to zero for a system with a continuous Koopman spectrum. This decay signifies a loss of memory and the irreversible mixing of states [@problem_id:1689016].

By analyzing the spectrum of the Koopman operator, we can thus classify the dynamics of a system, distinguishing between regular, predictable motions and complex, chaotic ones, all within a unified linear framework.