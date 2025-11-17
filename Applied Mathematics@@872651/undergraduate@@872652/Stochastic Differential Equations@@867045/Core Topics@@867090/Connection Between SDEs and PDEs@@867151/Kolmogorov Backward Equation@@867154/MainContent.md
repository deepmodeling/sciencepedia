## Introduction
The relationship between [stochastic differential equations](@entry_id:146618) (SDEs) and [partial differential equations](@entry_id:143134) (PDEs) represents one of the most powerful synergies in modern applied mathematics. This connection allows us to tackle complex probabilistic questions about random processes using the robust analytical toolkit of PDEs, and conversely, to find solutions to intricate PDEs through the simulation of stochastic paths. However, bridging these two worlds requires a formal mathematical framework. How can we precisely relate the dynamics of a random process, governed by drift and diffusion, to a deterministic equation?

This article explores the cornerstone of this connection: the Kolmogorov backward equation (KBE). It provides a direct and elegant method for calculating the expected value of a function of a stochastic process's future state. The **Principles and Mechanisms** section derives the equation from first principles, introducing the crucial concept of the infinitesimal generator via Itô's formula. The **Applications and Interdisciplinary Connections** section showcases the equation's immense utility by solving real-world problems in finance, [population genetics](@entry_id:146344), and [chemical physics](@entry_id:199585). Finally, the **Hands-On Practices** section will challenge you to apply your newfound knowledge to concrete computational exercises, solidifying the link between theory and practice.

## Principles and Mechanisms

The relationship between [stochastic differential equations](@entry_id:146618) (SDEs) and partial differential equations (PDEs) is one of the most profound and useful connections in modern mathematics. It allows us to analyze probabilistic questions about the behavior of [random processes](@entry_id:268487) using the powerful analytical tools of PDEs, and conversely, to solve complex PDEs by simulating the random paths of an associated SDE. The Kolmogorov backward equation is a cornerstone of this theory, providing a direct link between the expected value of a function of a stochastic process and the solution to a particular parabolic PDE. This chapter will derive this equation from first principles and explore its fundamental properties and implications.

### The Infinitesimal Generator: The Heart of the Dynamics

To understand how the dynamics of a stochastic process translate into a deterministic PDE, we must first introduce the concept of the **infinitesimal generator**. Consider a time-homogeneous Itô [diffusion process](@entry_id:268015) $X_t$ in $\mathbb{R}^d$ governed by the SDE:
$$
\mathrm{d}X_t = b(X_t)\,\mathrm{d}t + \sigma(X_t)\,\mathrm{d}W_t
$$
where $b(X_t)$ is the drift vector, $\sigma(X_t)$ is the [diffusion matrix](@entry_id:182965), and $W_t$ is a standard Brownian motion. Let $f: \mathbb{R}^d \to \mathbb{R}$ be a sufficiently [smooth function](@entry_id:158037). We are interested in how the value of $f(X_t)$ changes on average over an infinitesimally small time step.

The infinitesimal generator, denoted by $\mathcal{L}$, is an operator that captures this expected [instantaneous rate of change](@entry_id:141382). For a process starting at $X_0 = x$, it is defined by the [pointwise limit](@entry_id:193549):
$$
\mathcal{L}f(x) = \lim_{h \to 0^+} \frac{\mathbb{E}_x[f(X_h)] - f(x)}{h}
$$
where $\mathbb{E}_x[\cdot]$ denotes the expectation conditional on $X_0=x$. This operator is not defined for any arbitrary function $f$. For $\mathcal{L}f$ to be a [well-defined function](@entry_id:146846) itself within a given function space (such as the space of bounded, measurable functions $B_b(\mathbb{R}^d)$), its **domain**, $D(\mathcal{L})$, must consist of functions $f$ for which this limit exists for all $x$ and the resulting function $\mathcal{L}f(x)$ also belongs to that space [@problem_id:3062746].

While this limit definition is conceptually crucial, a more practical form of the generator can be derived using Itô's formula. Applying Itô's formula to $f(X_t)$ gives:
$$
\mathrm{d}f(X_t) = \nabla f(X_t) \cdot \mathrm{d}X_t + \frac{1}{2} \mathrm{Tr}\left( (\mathrm{d}X_t)(\mathrm{d}X_t)^\top \nabla^2 f(X_t) \right)
$$
where $\nabla f$ is the gradient and $\nabla^2 f$ is the Hessian matrix of $f$. The [quadratic variation](@entry_id:140680) term $(\mathrm{d}X_t)(\mathrm{d}X_t)^\top$ is calculated using the Itô multiplication rules: $(\mathrm{d}t)^2=0$, $\mathrm{d}t \cdot \mathrm{d}W_t=0$, and $\mathrm{d}W_t \mathrm{d}W_t^\top = I\,\mathrm{d}t$. This yields:
$$
(\mathrm{d}X_t)(\mathrm{d}X_t)^\top = (\sigma(X_t)\,\mathrm{d}W_t)(\sigma(X_t)\,\mathrm{d}W_t)^\top = \sigma(X_t) (\mathrm{d}W_t \mathrm{d}W_t^\top) \sigma(X_t)^\top = \sigma(X_t)\sigma(X_t)^\top \mathrm{d}t = a(X_t)\,\mathrm{d}t
$$
where we define the **diffusion covariance matrix** $a(x) = \sigma(x)\sigma(x)^\top$. Substituting this and the SDE for $\mathrm{d}X_t$ into Itô's formula, we get:
$$
\mathrm{d}f(X_t) = \nabla f(X_t) \cdot (b(X_t)\,\mathrm{d}t + \sigma(X_t)\,\mathrm{d}W_t) + \frac{1}{2} \mathrm{Tr}\left( a(X_t) \nabla^2 f(X_t) \right)\,\mathrm{d}t
$$
Grouping terms, we find the differential for $f(X_t)$ is:
$$
\mathrm{d}f(X_t) = \left( b(X_t) \cdot \nabla f(X_t) + \frac{1}{2} \mathrm{Tr}\left( a(X_t) \nabla^2 f(X_t) \right) \right) \mathrm{d}t + \nabla f(X_t)^\top \sigma(X_t) \mathrm{d}W_t
$$
The term multiplying $\mathrm{d}t$ is precisely the operator $\mathcal{L}$ applied to $f$. Thus, for a function $f$ in its domain, the [infinitesimal generator](@entry_id:270424) of the Itô process is the second-order partial differential operator:
$$
\mathcal{L}f(x) = \sum_{i=1}^d b_i(x) \frac{\partial f}{\partial x_i}(x) + \frac{1}{2} \sum_{i,j=1}^d a_{ij}(x) \frac{\partial^2 f}{\partial x_i \partial x_j}(x)
$$
This remarkable result connects the drift $b$ and diffusion $\sigma$ coefficients of the SDE directly to the first and second-order terms of a PDE operator.

For instance, consider the one-dimensional Geometric Brownian Motion, often used in finance, described by $dX_t = \mu X_t \,dt + \sigma X_t \,dW_t$. Here, the drift is $b(x) = \mu x$ and the diffusion is $\sigma(x) = \sigma x$. The diffusion covariance is $a(x) = (\sigma x)^2 = \sigma^2 x^2$. For a function $f(x)$, the generator is found by substituting these into the general form [@problem_id:3062765]:
$$
\mathcal{L}f(x) = (\mu x) f'(x) + \frac{1}{2} (\sigma^2 x^2) f''(x)
$$

### The Evolution of Expectations: Dynkin's Formula and the Initial Value Problem

With the generator defined, we can now address how the expected value of a function of the state evolves over time. Let $u(t,x) = \mathbb{E}_x[f(X_t)]$. How does $u(t,x)$ change with $t$? The answer is given by **Dynkin's formula**.

To derive it, we return to the integrated form of Itô's formula for $f(X_t)$:
$$
f(X_t) - f(X_0) = \int_0^t \mathcal{L}f(X_s)\,\mathrm{d}s + \int_0^t \nabla f(X_s)^\top \sigma(X_s)\,\mathrm{d}W_s
$$
Taking the [conditional expectation](@entry_id:159140) $\mathbb{E}_x[\cdot]$ (where $X_0=x$) on both sides:
$$
\mathbb{E}_x[f(X_t)] - f(x) = \mathbb{E}_x\left[\int_0^t \mathcal{L}f(X_s)\,\mathrm{d}s\right] + \mathbb{E}_x\left[\int_0^t \nabla f(X_s)^\top \sigma(X_s)\,\mathrm{d}W_s\right]
$$
A key property of the Itô integral is that, under suitable conditions on the integrand, it forms a martingale with an expectation of zero. While these conditions are not always met globally, a localization argument using [stopping times](@entry_id:261799) ensures that the expectation of the [stochastic integral](@entry_id:195087) vanishes [@problem_id:3062722]. This simplifies the equation to:
$$
\mathbb{E}_x[f(X_t)] = f(x) + \mathbb{E}_x\left[\int_0^t \mathcal{L}f(X_s)\,\mathrm{d}s\right]
$$
This is **Dynkin's formula**. It provides an explicit relationship between the expected value of the function at time $t$ and an integral involving the generator acting on the process over the interval $[0,t]$.

By differentiating Dynkin's formula with respect to $t$, we obtain its differential form:
$$
\frac{\mathrm{d}}{\mathrm{d}t}\mathbb{E}_x[f(X_t)] = \mathbb{E}_x[\mathcal{L}f(X_t)]
$$
Now, let us define $u(t,x) = \mathbb{E}_x[\varphi(X_t)]$ for some given function $\varphi$. Using the time-homogeneous property of the process, we can write $u(t,x) = (P_t \varphi)(x)$, where $P_t$ is the [transition semigroup](@entry_id:193053). The evolution of the [semigroup](@entry_id:153860) is given by $\frac{\mathrm{d}}{\mathrm{d}t} P_t \varphi = \mathcal{L}(P_t \varphi)$. Applying this to our function $u(t,x)$ yields:
$$
\frac{\partial u}{\partial t}(t,x) = \mathcal{L}u(t, \cdot)(x)
$$
where the operator $\mathcal{L}$ acts on the spatial variable $x$ of the function $u(t,\cdot)$. The initial condition is found by setting $t=0$: $u(0,x) = \mathbb{E}_x[\varphi(X_0)] = \varphi(x)$. Therefore, the function $u(t,x) = \mathbb{E}_x[\varphi(X_t)]$ is the solution to the [initial value problem](@entry_id:142753) [@problem_id:3062742]:
$$
\begin{cases}
\frac{\partial u}{\partial t}(t,x) = \mathcal{L}u(t,x),  (t,x) \in (0, \infty) \times \mathbb{R}^d \\
u(0,x) = \varphi(x),  x \in \mathbb{R}^d
\end{cases}
$$
This is a form of the Kolmogorov backward equation, structured as an [initial value problem](@entry_id:142753). It describes how the expectation of a function of the process state propagates forward in time from an initial state.

### The Terminal Value Problem: The Classic Kolmogorov Backward Equation

While the [initial value formulation](@entry_id:161941) is instructive, many practical applications, particularly in [mathematical finance](@entry_id:187074) and engineering, involve a different question: what is the expected value *now* of some payoff or state that will be realized at a fixed *future* time?

Let us define a function $u(t,x)$ for $t \in [0, T]$ as the expected value of a terminal payoff $\varphi(X_T)$, given that the process is at state $x$ at time $t$:
$$
u(t,x) = \mathbb{E}[\varphi(X_T) | X_t = x]
$$
The most direct way to find the PDE for $u(t,x)$ is to use a [martingale](@entry_id:146036) argument [@problem_id:3062759]. Consider the process $Y_s = u(s, X_s)$ for $s \in [t, T]$. By the [tower property of conditional expectation](@entry_id:181314) and the Markov property of $X_s$, for any $s' \in [s, T]$, we have $\mathbb{E}[Y_{s'} | \mathcal{F}_s] = \mathbb{E}[\mathbb{E}[\varphi(X_T) | X_{s'}] | \mathcal{F}_s] = \mathbb{E}[\varphi(X_T) | \mathcal{F}_s] = u(s, X_s) = Y_s$. This demonstrates that $Y_s$ is a martingale.

An Itô process is a martingale if and only if its drift ($\mathrm{d}t$) term is zero. Applying Itô's formula to $Y_s = u(s, X_s)$ (assuming $u$ is sufficiently smooth) gives:
$$
\mathrm{d}Y_s = \left(\frac{\partial u}{\partial s} + \mathcal{L}_s u \right)(s,X_s)\,\mathrm{d}s + (\dots)\,\mathrm{d}W_s
$$
For $Y_s$ to be a martingale, its drift must vanish. This implies that $u$ must satisfy the PDE:
$$
\frac{\partial u}{\partial t}(t,x) + \mathcal{L}_t u(t,x) = 0
$$
where $\mathcal{L}_t$ is the generator, which may now depend on time if the SDE coefficients $b$ and $\sigma$ are time-dependent. The boundary condition is determined by evaluating $u(t,x)$ at the terminal time $t=T$:
$$
u(T,x) = \mathbb{E}[\varphi(X_T) | X_T=x] = \varphi(x)
$$
This gives us the classic **Kolmogorov backward equation**, which is a **terminal value problem** [@problem_id:3062764]:
$$
\begin{cases}
\frac{\partial u}{\partial t}(t,x) + \mathcal{L}_t u(t,x) = 0,  (t,x) \in [0,T) \times \mathbb{R}^d \\
u(T,x) = \varphi(x),  x \in \mathbb{R}^d
\end{cases}
$$
The equation is called "backward" because it is solved backward in time, from the known terminal condition at $t=T$ to find the solution at earlier times $t  T$. The sign convention $\partial_t u + \mathcal{L}_t u = 0$ is a direct consequence of the problem's structure. The term $\partial_t u$ reflects the change in value due to the passage of time, while $\mathcal{L}_t u$ reflects the change due to the random movement of the state. For the total value to remain constant on average (the [martingale property](@entry_id:261270)), these two effects must cancel each other out [@problem_id:3062718].

A helpful way to understand the sign convention is to change variables to the "time-to-go," $\tau = T - t$. If we define $v(\tau, x) = u(T-\tau, x)$, then $\partial_\tau v = -\partial_t u$. Substituting this into the backward equation gives $\partial_\tau v = \mathcal{L}_{T-\tau}v$, which is a standard forward parabolic equation with an initial condition $v(0,x) = \varphi(x)$ [@problem_id:3062718]. This transformation confirms that the structure of the backward equation is mathematically sound and directly reflects its backward-in-time nature.

### Generalizations and Connections: Feynman-Kac and the Forward Equation

The framework of the Kolmogorov backward equation can be extended to handle more complex scenarios. A particularly powerful generalization is given by the **Feynman-Kac formula**, which addresses problems where the process may be "killed" or where a running cost or reward is accumulated.

Consider the PDE with an additional zeroth-order term:
$$
\frac{\partial u}{\partial t}(t,x) + \mathcal{L}_t u(t,x) - c(t,x)u(t,x) = 0, \quad u(T,x) = \varphi(x)
$$
Here, $c(t,x)$ can be interpreted as a killing rate or a [discount rate](@entry_id:145874). The Feynman-Kac formula states that the solution to this PDE has the probabilistic representation [@problem_id:3062737]:
$$
u(t,x) = \mathbb{E}_{t,x}\left[ \exp\left(-\int_t^T c(s, X_s)\,\mathrm{d}s\right) \varphi(X_T) \right]
$$
where $\mathbb{E}_{t,x}[\cdot]$ denotes expectation conditional on $X_t=x$. The exponential term acts as a discount factor that depends on the path taken by the process $X_s$. This formula is fundamental in many areas, from [option pricing](@entry_id:139980) in finance (where $c$ is the risk-free interest rate) to quantum mechanics. The proof follows a similar [martingale](@entry_id:146036) argument as before, but applied to the process $Y_s = \exp(-\int_t^s c(r, X_r)\,\mathrm{d}r) u(s, X_s)$.

It is crucial to distinguish the Kolmogorov backward equation, which describes the evolution of expected values, from the **Kolmogorov forward equation** (also known as the **Fokker-Planck equation**), which describes the evolution of the probability density function $p(t,x)$ of the process $X_t$ itself. The forward equation is an initial value problem, evolving forward from a given initial distribution $p(0,x)$, and is given by [@problem_id:3062776]:
$$
\frac{\partial p}{\partial t}(t,x) = \mathcal{L}^* p(t,x)
$$
Here, $\mathcal{L}^*$ is the formal adjoint of the generator $\mathcal{L}$. It can be derived via integration by parts from the condition $\langle \mathcal{L}f, g \rangle = \langle f, \mathcal{L}^* g \rangle$. For the generator $\mathcal{L}f = \sum_i b_i \partial_i f + \frac{1}{2}\sum_{ij} a_{ij} \partial_{ij} f$, its adjoint is:
$$
\mathcal{L}^*g(x) = -\sum_i \frac{\partial}{\partial x_i} (b_i(x)g(x)) + \frac{1}{2} \sum_{ij} \frac{\partial^2}{\partial x_i \partial x_j} (a_{ij}(x)g(x))
$$
The backward equation governs how expectations of functions of the state evolve backward from a terminal condition, while the forward equation governs how the probability density of the state itself evolves forward from an initial condition [@problem_id:3062764].

### A Note on Rigor: Conditions for Classical Solutions

Throughout this chapter, we have assumed that the solution $u(t,x)$ to the Kolmogorov backward equation is sufficiently smooth—specifically, once continuously differentiable in time and twice in space ($u \in C^{1,2}$). Such a solution is called a **classical solution**. The existence of a classical solution, and thus the validity of the SDE-PDE connection, is not automatic. It depends critically on the regularity of the SDE coefficients and the terminal data.

Standard results from the theory of parabolic PDEs, such as Schauder estimates, provide [sufficient conditions](@entry_id:269617). A key requirement is that the operator $\mathcal{L}_t$ must be **uniformly parabolic**, which means the diffusion covariance matrix $a(t,x)$ must be uniformly [positive definite](@entry_id:149459). This is often termed **[uniform ellipticity](@entry_id:194714)**. Furthermore, for the solution $u$ to possess the required smoothness up to the boundary, the coefficients $b$ and $\sigma$ (and therefore $a$) and the terminal function $\varphi$ must themselves be sufficiently smooth. For example, if the coefficients are Hölder continuous in both space and time, and the terminal data $\varphi$ is in a corresponding higher-order Hölder space (e.g., $C_b^{2+\alpha}$), then a unique classical solution is guaranteed to exist [@problem_id:3062750].

If these regularity conditions are not met—for instance, if the diffusion is degenerate ($\sigma$ is not invertible) or the coefficients are not smooth—the PDE may not have a classical solution. In such cases, the SDE-PDE connection still holds, but the solution must be interpreted in a weaker sense, such as a **[viscosity solution](@entry_id:198358)**. This more advanced theory is beyond the scope of this chapter but underpins much of modern research in [stochastic control](@entry_id:170804) and nonlinear PDEs.