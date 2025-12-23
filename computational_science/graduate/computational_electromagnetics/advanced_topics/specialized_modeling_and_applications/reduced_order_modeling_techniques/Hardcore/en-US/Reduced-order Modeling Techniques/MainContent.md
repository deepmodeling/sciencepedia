## Introduction
In the field of [computational electromagnetics](@entry_id:269494), the quest for higher fidelity and accuracy often leads to extremely large-scale numerical models. These full-order models (FOMs), resulting from the [discretization](@entry_id:145012) of Maxwell's equations, can have millions of degrees of freedom, making transient simulations, design optimization, and [uncertainty quantification](@entry_id:138597) computationally prohibitive. Reduced-order modeling (ROM) offers a powerful solution to this challenge by creating highly compact, yet accurate, [surrogate models](@entry_id:145436) that can be simulated orders of magnitude faster. The central problem, however, is not merely to reduce the model's size but to do so while preserving crucial physical properties like energy conservation and passivity, and while effectively handling complexities such as nonlinearities and parameter dependencies.

This article provides a comprehensive exploration of modern [reduced-order modeling](@entry_id:177038) techniques tailored for electromagnetic systems. Over the next three chapters, you will gain a deep, practical understanding of this transformative methodology. We will begin our journey in **"Principles and Mechanisms"** by dissecting the core idea of projection, exploring systematic methods for constructing effective bases like Proper Orthogonal Decomposition (POD) and Krylov subspace methods. Building on this foundation, **"Applications and Interdisciplinary Connections"** will demonstrate how these principles are extended to solve real-world problems, from ensuring physical structure is preserved to tackling nonlinearities with [hyperreduction](@entry_id:750481) and drawing powerful connections to control theory and machine learning. Finally, **"Hands-On Practices"** will solidify your understanding through practical exercises, guiding you to implement ROMs for [data compression](@entry_id:137700) and design optimization.

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms that underpin [reduced-order modeling](@entry_id:177038) (ROM) in [computational electromagnetics](@entry_id:269494). We will begin by formalizing the large-scale, full-order models (FOMs) that arise from the discretization of Maxwell's equations. Subsequently, we will explore the central paradigm of projection-based reduction, investigating systematic methods for constructing the necessary projection bases. Our exploration will cover both data-driven approaches, such as Proper Orthogonal Decomposition (POD), and system-theoretic methods based on [moment matching](@entry_id:144382). A crucial aspect of any reliable ROM is the preservation of fundamental physical properties; thus, we will dedicate a section to understanding and enforcing passivity and stability. We will then advance to optimal reduction strategies, such as the Iterative Rational Krylov Algorithm (IRKA), and extend our framework to handle systems with parametric dependencies. Finally, we will examine an alternative, data-centric approach to modeling based on [rational function](@entry_id:270841) fitting in the frequency domain.

### The Full-Order Model: Our Starting Point

The journey into [reduced-order modeling](@entry_id:177038) begins with a comprehensive understanding of the object we wish to simplify: the **[full-order model](@entry_id:171001) (FOM)**. In [computational electromagnetics](@entry_id:269494), the FOM is typically a large-scale system of differential or algebraic equations that results from the [spatial discretization](@entry_id:172158) of Maxwell's partial differential equations.

Consider an electromagnetic problem within a bounded domain $\Omega$, characterized by material properties such as permittivity $\varepsilon(\mathbf{x})$, permeability $\mu(\mathbf{x})$, and conductivity $\sigma(\mathbf{x})$. Applying a numerical technique like the Finite Element Method (FEM) with curl-conforming basis functions (e.g., Nédélec elements) allows us to approximate the continuous electric field $\mathbf{E}(\mathbf{x},t)$ and magnetic field $\mathbf{H}(\mathbf{x},t)$ as finite linear combinations of basis functions. For instance, we may write $\mathbf{E}(\mathbf{x},t) \approx \sum_{i=1}^{n_e} e_i(t) \mathbf{N}_i^E(\mathbf{x})$, where $e_i(t)$ are time-varying coefficients.

By applying a Galerkin projection—a process where the governing PDEs are tested against the same basis functions used for the field expansion—we can transform Maxwell's equations from the realm of infinite-dimensional function spaces into a system of coupled, [first-order ordinary differential equations](@entry_id:264241) (ODEs) in time . This semi-discrete system is the FOM and typically takes the form of a **descriptor state-space model**:

$$
E \dot{x}(t) = A x(t) + B u(t)
$$
$$
y(t) = C x(t) + D u(t)
$$

Here, $x(t) \in \mathbb{R}^n$ is the state vector containing the unknown coefficients of the discretized electric and magnetic fields, with $n$ being the number of degrees of freedom—often in the millions for realistic problems. The vector $u(t)$ represents the inputs (e.g., source currents or port voltages), and $y(t)$ represents the outputs of interest (e.g., measured fields or [scattering parameters](@entry_id:754557)).

The system matrices are defined by integrals over the problem domain. For instance, a common structure resulting from a mixed discretization of the electric and magnetic fields is :
-   **Descriptor Matrix** $E$: Often block-diagonal, containing mass matrices related to [permittivity and permeability](@entry_id:275026), e.g., $(M_\varepsilon)_{ij} = \int_\Omega \varepsilon \mathbf{N}_i^E \cdot \mathbf{N}_j^E dV$. It represents energy storage capacity. In some formulations, $E$ can be singular, leading to a differential-algebraic equation (DAE).
-   **State Matrix** $A$: Encapsulates the internal dynamics, including curl operators and dissipative losses from conductivity, e.g., terms like $(M_\sigma)_{ij} = \int_\Omega \sigma \mathbf{N}_i^E \cdot \mathbf{N}_j^E dV$ and $(K)_{ij} = \int_\Omega (\nabla \times \mathbf{N}_i^E) \cdot \mathbf{N}_j^H dV$.
-   **Input and Output Matrices** $B$ and $C$: Relate the internal states to the external inputs and desired outputs, respectively.

While different [discretization schemes](@entry_id:153074) like the Finite-Difference Time-Domain (FDTD) method may produce matrices with slightly different properties (e.g., diagonal or "lumped" mass matrices), they often result in a similar sparse, large-scale state-space structure . The immense size $n$ of this system is the fundamental bottleneck that motivates [model reduction](@entry_id:171175).

### The Core Principle of Projection

The most prevalent strategy for reducing the complexity of FOMs is **projection**. The central idea is to approximate the high-dimensional state vector $x(t) \in \mathbb{R}^n$ by a trajectory that evolves within a much lower-dimensional subspace. We postulate the approximation, or **ansatz**:

$$
x(t) \approx V z(t)
$$

Here, $z(t) \in \mathbb{R}^r$ is the state vector of the **[reduced-order model](@entry_id:634428) (ROM)**, with $r \ll n$. The matrix $V \in \mathbb{R}^{n \times r}$ is the **trial basis** or [projection matrix](@entry_id:154479), whose columns span the low-dimensional subspace where the solution is presumed to lie.

To derive the dynamics for the reduced state $z(t)$, we substitute the ansatz into the FOM descriptor equation, which yields a residual $R(t)$:

$$
R(t) = E V \dot{z}(t) - A V z(t) - B u(t)
$$

Since the approximation $V z(t)$ does not, in general, satisfy the original equation exactly, the residual will be non-zero. The goal is to determine the evolution of $z(t)$ by forcing this residual to be zero in some sense. The **Petrov-Galerkin framework** achieves this by introducing a second basis, the **test basis** $W \in \mathbb{R}^{n \times r}$, and enforcing that the residual is orthogonal to the subspace spanned by the columns of $W$. This [orthogonality condition](@entry_id:168905) is expressed as:

$$
W^T R(t) = 0
$$

Substituting the expression for the residual gives the governing equation for the ROM:

$$
(W^T E V) \dot{z}(t) = (W^T A V) z(t) + (W^T B) u(t)
$$

This is a new, much smaller descriptor system, $E_r \dot{z}(t) = A_r z(t) + B_r u(t)$, with the reduced system matrices defined as:

$$
E_r = W^T E V, \quad A_r = W^T A V, \quad B_r = W^T B
$$

The reduced output is given by $y_r(t) = C_r z(t)$, where $C_r = C V$. This reduced system, with only $r$ states, can be simulated orders of magnitude faster than the FOM. When the test basis is chosen to be the same as the trial basis ($W=V$), the approach is known as a **Galerkin projection**.

This framework immediately raises two fundamental questions that drive the field of [model order reduction](@entry_id:167302):
1.  How do we construct an effective trial basis $V$ that can accurately represent the system's dynamics?
2.  Given $V$, what is the optimal choice for the test basis $W$?

The following sections will explore various systematic answers to these questions.

### Data-Driven Basis Generation: Proper Orthogonal Decomposition

A highly intuitive and powerful method for constructing the trial basis $V$ is to extract the most dominant spatial patterns directly from simulation data. This is the essence of **Proper Orthogonal Decomposition (POD)**, also known as Principal Component Analysis (PCA) in other fields. The procedure begins by collecting a set of representative solutions, or **snapshots**, of the FOM [state vector](@entry_id:154607), $\{x(t_1), x(t_2), \dots, x(t_m)\}$, which are assembled as columns into a **snapshot matrix** $S = [x(t_1) | \dots | x(t_m)] \in \mathbb{R}^{n \times m}$.

The goal of POD is to find an orthonormal basis that is optimal for representing the snapshot data, in the sense that it minimizes the average projection error. To make this notion of optimality physically meaningful in electromagnetics, we measure error not in the standard Euclidean norm but in an **energy norm**. For a system with a [symmetric positive-definite](@entry_id:145886) descriptor matrix $E$, the stored energy is proportional to $x^T E x$. This motivates defining the [energy inner product](@entry_id:167297) as $\langle u, v \rangle_E = u^T E v$ .

Finding the basis that captures the maximum possible energy from the snapshots is equivalent to solving an eigenvalue problem. This can be elegantly formulated using the **Singular Value Decomposition (SVD)**. Instead of working with the raw snapshots $S$, we consider the energy-weighted snapshot matrix $\tilde{S} = E^{1/2} S$, where $E^{1/2}$ is the [matrix square root](@entry_id:158930) of $E$. The SVD of this weighted matrix is:

$$
\tilde{S} = U \Sigma \mathcal{V}^T
$$

The [left singular vectors](@entry_id:751233), which form the columns of the orthogonal matrix $U$, represent an [orthonormal basis](@entry_id:147779) for the energy-weighted data. The POD basis $V$ is then constructed by transforming this basis back to the original coordinates:

$$
V = E^{-1/2} U_r
$$

Here, $U_r$ contains only the first $r$ columns of $U$. This construction guarantees that the resulting POD basis $V$ is orthonormal with respect to the [energy inner product](@entry_id:167297), i.e., $V^T E V = I_r$.

The singular values $\sigma_k$, which are the diagonal entries of $\Sigma$, have a profound physical meaning: the square of each singular value, $\sigma_k^2$, is directly proportional to the energy captured by the corresponding POD basis mode. The total energy in the snapshot collection is given by $\sum_k \sigma_k^2$. This provides a rigorous and quantitative criterion for truncating the basis: we choose the smallest dimension $r$ such that the captured energy fraction,

$$
\eta(r) = \frac{\sum_{k=1}^r \sigma_k^2}{\sum_{k=1}^m \sigma_k^2}
$$

exceeds a desired threshold, for example, 0.9999. For instance, if a system's dynamics are dominated by a few modes, the singular values will decay rapidly, and a very small $r$ can capture nearly all the system's energy, leading to a highly efficient ROM .

### System-Theoretic Basis Generation: Krylov Subspace Methods

An alternative to the data-driven approach of POD is to construct the basis $V$ using only the system matrices $E, A, B$ of the FOM. This family of methods is rooted in the idea of matching the **moments** of the ROM's transfer function to those of the FOM.

The transfer function of the FOM, which relates the input to the output in the Laplace domain, is given by $H(s) = C(sE - A)^{-1}B$. Expanding this function in a Laurent series around a frequency point $s_0$ yields:

$$
H(s) = \sum_{k=0}^{\infty} m_k (s-s_0)^k
$$

The coefficients $m_k$ are known as the **moments** of the system at $s_0$. A key insight is that if the ROM's transfer function $H_r(s) = C_r(sE_r - A_r)^{-1}B_r$ has the same first $2r$ moments as the FOM, the ROM is considered a very good approximation.

This moment-matching property is intrinsically linked to **Krylov subspaces**. A projection-based ROM with a trial basis $V$ spanning the block Krylov subspace

$$
\mathcal{K}_r( (s_0E-A)^{-1}E, (s_0E-A)^{-1}B ) = \mathrm{span} \{ (s_0E-A)^{-1}B, ((s_0E-A)^{-1}E)(s_0E-A)^{-1}B, \dots \}
$$

and a test basis $W$ spanning a related Krylov subspace will match moments of the transfer function at the expansion point $s_0$.

A particularly important case is [moment matching](@entry_id:144382) at $s = \infty$. This corresponds to matching the coefficients of the expansion $H(s) = \sum_{k=0}^\infty \mu_k / s^{k+1}$. Matching these moments is equivalent to matching the initial time derivatives of the impulse response, meaning the ROM will accurately capture the short-time behavior of the full system. This is crucial for modeling fast transients. For example, in systems with time delays, the short-time behavior before the delay takes effect is governed entirely by the non-delayed dynamics. A ROM that matches moments at infinity will accurately capture this initial response, irrespective of the delay, which does not contribute to the algebraic moments at infinity . Algorithms like the Arnoldi algorithm can be used to efficiently construct an [orthonormal basis](@entry_id:147779) for the Krylov subspace, leading to so-called **Krylov subspace methods** for [model reduction](@entry_id:171175).

### Preserving Physical Properties: Passivity and Stability

A useful ROM must not only be accurate; it must also be physically realistic. For electromagnetic systems, a critical property is **passivity**, which dictates that the system cannot generate energy on its own. A system is passive if the energy stored within it, plus the total energy dissipated, is always less than or equal to the energy supplied to it. For an LTI system with a storage function $V(x) = \frac{1}{2} x^T E x$ (where $E$ is [positive definite](@entry_id:149459)), this can be expressed as a [dissipation inequality](@entry_id:188634) relating the rate of change of stored energy $\dot{V}(t)$ to the power $u^T(t)y(t)$ supplied at the ports.

This time-domain property has a direct and powerful equivalent in the frequency domain: a system is passive if and only if its transfer function $H(s)$ is **positive real** . A transfer function is positive real if it is analytic in the open right-half of the complex plane, and its Hermitian part, $H(s) + H(s)^*$, is positive semidefinite for all $\Re(s)>0$. This condition provides a concrete mathematical test for the passivity of a model.

A standard Galerkin projection ($W=V$) does not automatically guarantee that the ROM will be passive, even if the FOM is. This can lead to unstable simulations and non-physical results. However, **[structure-preserving model reduction](@entry_id:755567)** can be achieved by carefully choosing the projection framework. A fundamental result states that if the FOM is dissipative with respect to an inner product (e.g., the [energy inner product](@entry_id:167297) $\langle \cdot, \cdot \rangle_E$), then a Galerkin projection onto a basis $V$ that is orthonormal with respect to that same inner product ($V^T E V = I$) will produce a ROM that inherits the dissipative structure . For a passive FOM where $ML+L^T M \preceq 0$, the resulting reduced operator $L_r = V^T M L V$ will satisfy $L_r + L_r^T \preceq 0$, guaranteeing the stability and passivity of the ROM. This is a key advantage of the POD-Galerkin approach when an energy-weighted basis is used.

In contrast, purely data-driven methods that do not explicitly account for the system's structure, such as Dynamic Mode Decomposition (DMD), do not inherently guarantee stability. While DMD can be interpreted as an approximation of the system's [evolution operator](@entry_id:182628) (the Koopman operator), it may yield [unstable modes](@entry_id:263056) unless the input data is noise-free and spans an invariant subspace of the dynamics—conditions rarely met in practice .

### Towards Optimal Projection

We have seen how to construct "good" bases $V$. But what is the optimal choice for the test basis $W$? An elegant answer arises if we frame the problem as minimizing the approximation residual in a specific norm. Consider a time-harmonic problem $Ax=b$. With the approximation $x \approx Vy$, the residual is $r(y) = b-AVy$. If we seek to minimize the norm of this residual in the [energy inner product](@entry_id:167297) defined by a Hermitian [positive definite matrix](@entry_id:150869) $E$, i.e., minimize $\|r(y)\|_E^2 = r(y)^* E r(y)$, we can derive the optimal Petrov-Galerkin condition. The solution is remarkably simple and profound: the optimal test basis $W$ that enforces this minimization is given by :

$$
W = EAV
$$

This result provides a clear directive for constructing a test basis that is optimal in a specific, physically meaningful sense.

Taking this quest for optimality a step further, one can ask to find the reduced model that is optimal with respect to a system norm, which measures the overall input-output behavior. A widely used metric is the **Hardy space $\mathcal{H}_2$ norm**, which quantifies the energy amplification of the system in response to impulsive inputs. The **Iterative Rational Krylov Algorithm (IRKA)** is a powerful method designed to find a locally $\mathcal{H}_2$-optimal ROM .

IRKA is based on satisfying the [first-order necessary conditions](@entry_id:170730) for $\mathcal{H}_2$ optimality. These conditions require the ROM to tangentially interpolate the FOM at the mirror images of the ROM's poles. That is, if the reduced model has poles $\{\lambda_1, \dots, \lambda_r\}$, then the projection matrices $V$ and $W$ must be constructed to enforce interpolation at the points $\{-\lambda_1, \dots, -\lambda_r\}$. Since the reduced poles depend on the projection, this creates a [circular dependency](@entry_id:273976). IRKA resolves this through a [fixed-point iteration](@entry_id:137769):
1. Start with an initial set of interpolation points $\{s_i\}$.
2. Construct projection matrices $V$ and $W$ that enforce interpolation at $\{s_i\}$.
3. Compute the poles $\{\lambda_i\}$ of the resulting ROM.
4. Set the new interpolation points to be $\{s_i\} \leftarrow \{-\lambda_i\}$ and repeat.

Upon convergence, the algorithm yields a ROM that satisfies the necessary conditions for $\mathcal{H}_2$ optimality. For descriptor systems where the matrix $E$ may be singular, care must be taken to first isolate the strictly proper part of the transfer function, as the $\mathcal{H}_2$ norm is only defined for such systems. IRKA is then applied to this component .

### Parametric Reduced-Order Models

Often, we are interested in how a system's behavior changes with a varying parameter, $\mu$, which could be frequency, a geometric dimension, or a material property. A **parametric ROM (PROM)** aims to create a single, compact model that is valid over a continuous range of parameter values. The key to an efficient PROM is an **offline-online computational strategy**.

The **Reduced Basis Method (RBM)** is a powerful framework for creating PROMs. It relies on the ability to decompose the parameter-dependent system operator into an **affine** form:

$$
A(\mu) = \sum_{q=1}^{Q} \theta_q(\mu) A_q
$$

where $\theta_q(\mu)$ are scalar functions of the parameter and $A_q$ are constant, parameter-independent matrices. This structure is often present in physical models; for example, the [frequency-dependent permittivity](@entry_id:265694) of a Drude model can be decomposed this way .

With an affine decomposition, the RBM proceeds in two stages:
1.  **Offline Stage (Expensive):** A single, robust trial basis $V$ is constructed to be effective across the entire parameter domain. This is typically done using a **[greedy algorithm](@entry_id:263215)**. Starting with an empty basis, one iteratively finds the parameter value $\mu^*$ where the current ROM is least accurate and adds a snapshot of the FOM solution at $\mu^*$ to the basis. The accuracy is measured by a computationally cheap **[a posteriori error estimator](@entry_id:746617)**, often based on the [dual norm](@entry_id:263611) of the residual. All parameter-independent matrices (e.g., $V^T A_q V$) are precomputed and stored.
2.  **Online Stage (Cheap):** For any new parameter value $\mu$, the scalar functions $\theta_q(\mu)$ are evaluated, and the small, precomputed matrices are combined to form the reduced system. This system is then solved almost instantaneously.

But what if the parameter dependence is **non-affine**? The offline-online strategy seems to fail. The **Empirical Interpolation Method (EIM)** provides a solution . EIM constructs an approximation of the non-[affine function](@entry_id:635019) or operator in an affine form. For a non-[affine function](@entry_id:635019) $f(x, \mu)$, EIM finds a set of basis functions $\{u_q(x)\}$ and a set of "magic points" $\{x_q\}$ such that:

$$
f(x, \mu) \approx \sum_{q=1}^{Q} \alpha_q(\mu) u_q(x)
$$

The coefficients $\alpha_q(\mu)$ are determined by solving a small $Q \times Q$ system obtained by enforcing that the approximation is exact at the magic points. This small system can be solved rapidly in the online stage. By applying EIM to the non-affine terms in the system matrices, one can recover the affine structure needed for the RBM's efficient [offline-online decomposition](@entry_id:177117), dramatically expanding the class of problems amenable to parametric [model reduction](@entry_id:171175).

### Data-Driven Modeling in the Frequency Domain

An entirely different approach to model reduction bypasses the state-space FOM and works directly with input-output frequency response data, such as [scattering parameters](@entry_id:754557) ($S$-parameters) obtained from simulation or measurement. The goal is to find a low-order rational function matrix $H_r(s)$ that accurately fits the data. A common model form is the pole-residue representation:

$$
H_r(s) = \sum_{k=1}^r \frac{R_k}{s-p_k} + D
$$

where $p_k$ are the scalar poles, $R_k$ are matrix residues, and $D$ is a constant feedthrough term.

The **Vector Fitting (VF)** algorithm is a robust and widely used [iterative method](@entry_id:147741) for this task . A direct nonlinear fit for the [poles and residues](@entry_id:165454) is difficult. VF ingeniously reformulates the problem into a sequence of linear least-squares steps. The core idea is to first fit a "relaxed" or linearized rational form, identify the poles of this intermediate fit, and use these poles as the starting point for the next iteration. The steps are:

1.  **Initialization:** Start with an initial guess for the poles $\{\tilde{p}_k\}$, typically stable and spaced over the frequency range of interest.
2.  **Linear Solve:** Formulate and solve a linear least-squares problem to identify the numerator and denominator coefficients of an auxiliary rational function that approximates the data.
3.  **Pole Relocation:** The new, improved poles $\{p_k\}$ are computed as the zeros of the fitted denominator, which is a stable [eigenvalue problem](@entry_id:143898).
4.  **Iteration:** The new poles $\{p_k\}$ become the initial guess for the next iteration. The process is repeated until the poles converge.
5.  **Residue Calculation:** Once the final stable poles are identified, a single linear least-squares problem is solved to find the corresponding residues $R_k$ and the term $D$.

A critical aspect of VF is the subsequent enforcement of physical properties. The rational fit of passive data is not guaranteed to be passive. Therefore, post-processing steps are essential to check for and enforce passivity and stability, ensuring the final macromodel is physically reliable for use in system-level simulations .