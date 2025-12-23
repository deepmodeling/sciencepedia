## Introduction
The analysis and control of [nonlinear dynamical systems](@entry_id:267921) are central challenges across science and engineering. While traditional methods like linearization are effective near [equilibrium points](@entry_id:167503), they often fail to capture the global, complex behaviors inherent in systems ranging from fluid flows to biological networks. This creates a knowledge gap: how can we develop computationally tractable, yet globally accurate models directly from observational data?

This article introduces a powerful and modern approach to address this challenge: the Koopman operator framework. This paradigm shifts the focus from the nonlinear evolution of the system's state to the linear evolution of observable functions, allowing the full power of linear [spectral theory](@entry_id:275351) to be applied to [nonlinear dynamics](@entry_id:140844). We will explore how Dynamic Mode Decomposition (DMD), a versatile data-driven algorithm, provides a practical means to approximate the Koopman operator and extract meaningful insights from complex [time-series data](@entry_id:262935).

Through the following chapters, you will gain a comprehensive understanding of this transformative methodology.
*   **Principles and Mechanisms** delves into the mathematical foundations of the Koopman operator, its spectral properties, and how DMD and its variants like EDMD serve as finite-dimensional approximations.
*   **Applications and Interdisciplinary Connections** showcases the framework's real-world impact, from designing controllers for cyber-physical systems and discovering governing equations to analyzing fluid dynamics and network structures.
*   **Hands-On Practices** provides targeted exercises to solidify your theoretical and practical understanding of these concepts.

We begin by establishing the core principles, moving from high-level concepts to the rigorous mathematical formulation that underpins this entire field.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms underpinning Dynamic Mode Decomposition (DMD) and the Koopman operator framework. We will transition from the high-level concepts introduced previously to a rigorous mathematical formulation. Our objective is to construct a theoretical foundation that explains how a linear, operator-theoretic perspective can be used to analyze, predict, and control complex [nonlinear dynamical systems](@entry_id:267921). We will explore the spectral properties of the Koopman operator and demonstrate how data-driven methods like DMD and its variants serve as practical tools for approximating these properties from measurements.

### The Koopman Operator: A Linear Perspective on Nonlinear Dynamics

At the heart of modern [data-driven analysis](@entry_id:635929) of dynamical systems lies a powerful conceptual shift, first proposed by Bernard Koopman in the context of Hamiltonian mechanics. The central idea is to move the analysis from the finite-dimensional, and often nonlinear, evolution of the system's **state** to the infinite-dimensional, but always **linear**, evolution of **observables**—functions defined on the state space.

Consider a [discrete-time dynamical system](@entry_id:276520) governed by the state-transition map $x_{k+1} = f(x_k)$, where $x_k$ belongs to a state space $\mathcal{X} \subseteq \mathbb{R}^n$ and $f: \mathcal{X} \to \mathcal{X}$ is a potentially nonlinear function. While tracking the evolution of the state vector $x_k$ directly can be complex, let us instead consider the evolution of a scalar-valued function $g: \mathcal{X} \to \mathbb{C}$, which represents some measurement or quantity of interest derived from the state. We call such a function an **observable**.

The value of the observable at time step $k+1$ is $g(x_{k+1})$. By substituting the system's dynamics, we can express this value in terms of the state at time $k$:
$$
g(x_{k+1}) = g(f(x_k))
$$
This equation defines a new function, which is the composition of $g$ and $f$, denoted $g \circ f$. This composition tells us what the value of the observable will be at the next time step, based on the current state. This leads to the definition of the **Koopman operator**, $\mathcal{K}$. The Koopman operator is an operator that acts on the space of observable functions, advancing them one step forward in time. Its action is formally defined as:
$$
(\mathcal{K}g)(x) = g(f(x))
$$
Thus, the Koopman operator maps an observable function $g$ to a new observable function $\mathcal{K}g$.

A pivotal property of the Koopman operator is its linearity. This linearity holds regardless of whether the underlying state-transition map $f$ is linear or nonlinear. To verify this, let $g_1$ and $g_2$ be two [observables](@entry_id:267133) and let $\alpha, \beta \in \mathbb{C}$ be scalars. The action of $\mathcal{K}$ on the [linear combination](@entry_id:155091) $\alpha g_1 + \beta g_2$ is:
$$
(\mathcal{K}(\alpha g_1 + \beta g_2))(x) = (\alpha g_1 + \beta g_2)(f(x)) = \alpha g_1(f(x)) + \beta g_2(f(x)) = \alpha (\mathcal{K}g_1)(x) + \beta (\mathcal{K}g_2)(x)
$$
Since this holds for any state $x \in \mathcal{X}$, we have $\mathcal{K}(\alpha g_1 + \beta g_2) = \alpha \mathcal{K}g_1 + \beta \mathcal{K}g_2$. This demonstrates that the Koopman operator $\mathcal{K}$ is a [linear operator](@entry_id:136520) on the space of observables $\mathcal{G}$ .

This is a profound result: we have traded the study of a finite-dimensional nonlinear map $f: \mathcal{X} \to \mathcal{X}$ for the study of an infinite-dimensional [linear operator](@entry_id:136520) $\mathcal{K}: \mathcal{G} \to \mathcal{G}$. The power of this transformation lies in our ability to leverage the vast and mature toolkit of [linear operator theory](@entry_id:151141) and [spectral analysis](@entry_id:143718) to understand [nonlinear dynamics](@entry_id:140844).

For [continuous-time systems](@entry_id:276553) described by $\dot{x}(t) = f(x(t))$, the equivalent concept is the **Koopman [infinitesimal generator](@entry_id:270424)**, $\mathcal{L}$, defined by the Lie derivative:
$$
(\mathcal{L}g)(x) = \nabla g(x) \cdot f(x)
$$
The generator $\mathcal{L}$ governs the [time evolution](@entry_id:153943) of observables via the [linear differential equation](@entry_id:169062) $\frac{d}{dt}g(x(t)) = (\mathcal{L}g)(x(t))$.

### Spectral Decomposition of Dynamics

The linearity of the Koopman operator invites spectral analysis. The core idea is to find special [observables](@entry_id:267133)—**Koopman [eigenfunctions](@entry_id:154705)**—that transform in a particularly simple way under the action of $\mathcal{K}$. A non-zero observable $\phi: \mathcal{X} \to \mathbb{C}$ is a Koopman [eigenfunction](@entry_id:149030) of $\mathcal{K}$ with a corresponding **Koopman eigenvalue** $\lambda \in \mathbb{C}$ if it satisfies the equation:
$$
\mathcal{K}\phi = \lambda\phi
$$
This means that applying the Koopman operator to $\phi$ simply scales the function by the constant $\lambda$. In terms of the system's dynamics, this is equivalent to:
$$
\phi(x_{k+1}) = \phi(f(x_k)) = \lambda\phi(x_k)
$$
By induction, the value of the [eigenfunction](@entry_id:149030) along a trajectory evolves as $\phi(x_k) = \lambda^k \phi(x_0)$. The dynamics, when viewed through the lens of an [eigenfunction](@entry_id:149030), become purely linear and exponential.

The Koopman eigenvalues contain critical information about the system's temporal behavior:
- The **magnitude** $|\lambda|$ indicates growth or decay. If $|\lambda| \lt 1$, the [eigenfunction](@entry_id:149030) decays to zero, corresponding to stable dynamics. If $|\lambda| \gt 1$, it grows, indicating unstable dynamics. If $|\lambda| = 1$, the dynamics are oscillatory or neutral. This makes Koopman eigenvalues powerful tools for stability analysis, especially for nonhyperbolic fixed points where linearization fails .
- The **argument** $\arg(\lambda)$ determines the frequency of oscillation.

If we can decompose a general observable of interest, such as a sensor measurement $g(x)$, into a basis of Koopman eigenfunctions, we can represent its entire future evolution as a linear superposition of simple exponential behaviors. This is the essence of **Koopman [mode decomposition](@entry_id:1128062)**.

A crucial distinction must be made between Koopman [eigenfunctions](@entry_id:154705) and **Koopman modes** .
- A **Koopman [eigenfunction](@entry_id:149030)** $\phi_j(x)$ is a scalar-valued function on the state space $\mathcal{X}$. It is intrinsic to the system's dynamics $f$ and is independent of any specific measurement process.
- A **Koopman mode** $\mathbf{v}_j$ is a vector in the measurement space (e.g., $\mathbb{R}^m$ for $m$ sensors). It is determined by the specific measurement function $g: \mathcal{X} \to \mathbb{R}^m$ and represents the spatial structure or pattern associated with a particular temporal frequency.

If a vector-valued observable $g(x)$ can be expanded in terms of Koopman [eigenfunctions](@entry_id:154705) $\phi_j$, the expansion takes the form:
$$
g(x) = \sum_j \mathbf{v}_j \phi_j(x)
$$
The vector coefficients $\mathbf{v}_j$ are the Koopman modes. The evolution of the measurement $y_k = g(x_k)$ is then given by:
$$
y_k = g(x_k) = \sum_j \mathbf{v}_j \phi_j(x_k) = \sum_j \mathbf{v}_j \lambda_j^k \phi_j(x_0)
$$
This formula elegantly separates the dynamics into three components: the spatial patterns ($\mathbf{v}_j$), the temporal behaviors ($\lambda_j^k$), and the initial condition dependencies ($\phi_j(x_0)$).

For example, in a linear system $x_{k+1} = Ax$ with measurement $y_k=Cx$, where $A$ has right eigenvectors $w_j$ and left eigenvectors $z_j$, the linear functions $\phi_j(x) = z_j^\top x$ are Koopman eigenfunctions. The corresponding Koopman modes are given by $\mathbf{v}_j = Cw_j$ . This shows how the abstract concepts of Koopman analysis connect directly to familiar [linear systems theory](@entry_id:172825). More profoundly, under certain conditions, Koopman eigenfunctions can define a [coordinate transformation](@entry_id:138577) that locally linearizes a [nonlinear system](@entry_id:162704), providing a deep connection to classical results in [dynamical systems theory](@entry_id:202707) .

### Data-Driven Approximation: Dynamic Mode Decomposition (DMD)

The Koopman operator is a powerful theoretical construct, but its infinite-dimensional nature presents a practical challenge. We cannot compute it directly for most systems. Dynamic Mode Decomposition (DMD) is a pivotal algorithm that provides a finite-dimensional, data-driven approximation of the Koopman operator and its spectral properties.

The standard DMD algorithm begins with a sequence of state measurements, or "snapshots," sampled at uniform time intervals $\Delta t$. Let this sequence be $\{x_1, x_2, \dots, x_m\}$. We organize these snapshots into two matrices:
$$
X = \begin{pmatrix} |  |   | \\ x_1  x_2  \dots  x_{m-1} \\ |  |   | \end{pmatrix} \quad \text{and} \quad Y = \begin{pmatrix} |  |   | \\ x_2  x_3  \dots  x_m \\ |  |   | \end{pmatrix}
$$
The underlying (and potentially unknown) nonlinear dynamics dictate that $x_{k+1} = f(x_k)$. DMD seeks to find the best linear operator, represented by a matrix $A \in \mathbb{R}^{n \times n}$, that approximates this relationship across the entire dataset. That is, we seek an $A$ such that $x_{k+1} \approx A x_k$ for all $k$. In matrix form, this is expressed as $Y \approx AX$ .

The "best" matrix $A$ is found by solving a [least-squares problem](@entry_id:164198), which minimizes the Frobenius norm of the residual error $\|Y - AX\|_F$. The solution is given by:
$$
A = Y X^\dagger
$$
where $X^\dagger$ is the Moore-Penrose [pseudoinverse](@entry_id:140762) of $X$.

This matrix $A$ is the DMD operator. It is a finite-dimensional approximation of the Koopman operator $\mathcal{K}$. Specifically, it is the projection of $\mathcal{K}$ onto the subspace of linear observables spanned by the state coordinates themselves. The eigenvalues and eigenvectors of the matrix $A$ serve as approximations of the Koopman eigenvalues and Koopman modes, respectively. DMD thus provides a practical algorithm to extract the dominant temporal frequencies and spatial patterns directly from [time-series data](@entry_id:262935), without requiring an explicit model of the system's governing equations.

### Generalizations and Enhancements

Standard DMD approximates the Koopman operator on the limited subspace of linear observables. For highly [nonlinear systems](@entry_id:168347), this may be insufficient. The framework can be significantly enhanced through several key generalizations.

#### Extended Dynamic Mode Decomposition (EDMD)

Extended DMD (EDMD) generalizes DMD by replacing the linear state [observables](@entry_id:267133) with a user-defined dictionary of nonlinear [observables](@entry_id:267133) . Instead of working with the state $x$, we "lift" the state into a higher-dimensional space using a vector of observables $\Psi(x) = [\psi_1(x), \psi_2(x), \dots, \psi_N(x)]^\top$. The choice of this dictionary $\Psi$ is critical and can incorporate domain knowledge about the system. Common choices include polynomials, radial basis functions, or Fourier series.

The procedure is analogous to standard DMD. We form snapshot matrices in the lifted space:
$$
\mathbf{X}_\psi = [\Psi(x_1), \Psi(x_2), \dots, \Psi(x_{m-1})] \quad \text{and} \quad \mathbf{Y}_\psi = [\Psi(x_2), \Psi(x_3), \dots, \Psi(x_m)]
$$
We then find the best linear operator $K$ in this lifted space by solving the [least-squares problem](@entry_id:164198) $\mathbf{Y}_\psi \approx K \mathbf{X}_\psi$, which yields $K = \mathbf{Y}_\psi \mathbf{X}_\psi^\dagger$. The matrix $K$ is a finite-dimensional approximation of the Koopman operator projected onto the subspace spanned by the chosen dictionary functions $\{\psi_j\}$. EDMD provides a flexible and powerful framework for approximating the Koopman operator for a much wider range of nonlinear systems.

This data-driven approach is intimately related to the model-based technique of **Carleman linearization**. For a system with polynomial dynamics, Carleman linearization lifts the state into an infinite-dimensional space of monomials, resulting in an infinite-dimensional linear ODE. Truncating this system at a finite degree is equivalent to a Galerkin projection of the Koopman generator onto a finite polynomial basis. In the limit of infinite data and vanishingly small time steps, EDMD with a monomial dictionary recovers precisely this truncated Carleman model, bridging the gap between data-driven and model-based methods .

#### Dynamic Mode Decomposition with Control (DMDc)

To apply the Koopman framework to controlled systems of the form $x_{k+1} = f(x_k, u_k)$, we must account for the influence of the input $u_k$. Several strategies exist . One approach is to augment the state space to include the inputs, forming a larger [autonomous system](@entry_id:175329) if the input evolution is known. For instance, a system with input $u_k$ generated by $u_{k+1}=p(u_k)$ can be made autonomous by defining an augmented state $z_k = (x_k, u_k)$ that evolves as $z_{k+1} = (f(x_k, u_k), p(u_k))$.

A more flexible data-driven approach is Dynamic Mode Decomposition with Control (DMDc). DMDc seeks a model that separates the state dynamics from the input's influence. In the lifted space of observables, this corresponds to the bilinear model:
$$
\Psi(x_{k+1}) \approx A \Psi(x_k) + B \Phi(u_k)
$$
Here, $\Psi(x_k)$ is a vector of state observables, $\Phi(u_k)$ is a vector of input [observables](@entry_id:267133), and the matrices $A$ and $B$ represent the intrinsic dynamics and the control influence, respectively. These matrices are identified simultaneously from data. This structure approximates the evolution of state observables as a linear combination of the current state [observables](@entry_id:267133) and the current input [observables](@entry_id:267133), providing a powerful tool for [system identification](@entry_id:201290) and control design in a linear framework.

### Theoretical Foundations and Advanced Concepts

A deeper understanding of the Koopman framework requires appreciating some of its more subtle theoretical aspects.

#### The Koopman and Perron-Frobenius Operators

The Koopman operator describes the evolution of observables (functions). Its dual operator, the **Perron-Frobenius operator**, $P$, describes the evolution of probability densities (measures). While the Koopman operator pulls back functions ($\mathcal{K}g = g \circ f$), the Perron-Frobenius operator pushes forward densities. This means if a system's state has a probability density function $\rho_k(x)$ at time $k$, its density at time $k+1$ is $\rho_{k+1} = P\rho_k$. For systems with an [invariant measure](@entry_id:158370) $\mu$, the two operators are adjoints with respect to the $L^2(\mu)$ inner product: $\langle \mathcal{K}f, g \rangle_{L^2(\mu)} = \langle f, Pg \rangle_{L^2(\mu)}$ . This duality is crucial: the Koopman operator is used for predicting the values of quantities, while the Perron-Frobenius operator is used for propagating uncertainty and forecasting the distribution of future states. The same duality holds for [stochastic systems](@entry_id:187663), where the operators are defined in terms of a Markov transition kernel .

#### The Continuous Spectrum

While our discussion has focused on the [point spectrum](@entry_id:274057) ([eigenvalues and eigenfunctions](@entry_id:167697)), the spectrum of the Koopman operator for general systems can be more complex. For chaotic and mixing systems, the spectrum is often **continuous**. A mixing system is one where correlations between [observables](@entry_id:267133) decay over time. This decay property is incompatible with the non-decaying evolution of [eigenfunctions](@entry_id:154705) ($\phi(x_k) = \lambda^k \phi(x_0)$ with $|\lambda|=1$). Consequently, for mixing systems, the only eigenvalue is typically $\lambda=1$ (corresponding to constant functions), and the rest of the spectrum is continuous .

A [continuous spectrum](@entry_id:153573) means there is no [countable basis](@entry_id:155278) of [eigenfunctions](@entry_id:154705) that can be used for decomposition. Instead, the dynamics are composed of a continuum of frequencies. When a data-driven method like DMD is applied to such a system, it cannot find a few discrete "true" eigenvalues because they do not exist. Instead, the algorithm will produce a set of eigenvalues and modes that form a discrete approximation of the underlying continuous spectrum. As more data is used, these computed eigenvalues tend to become denser, "painting a picture" of the continuous spectral bands on the unit circle . This is a fundamental limitation and feature of applying finite-dimensional approximations to systems with infinite-dimensional complexity, and it highlights the importance of correctly interpreting the results of DMD and EDMD in the context of the underlying system's nature.