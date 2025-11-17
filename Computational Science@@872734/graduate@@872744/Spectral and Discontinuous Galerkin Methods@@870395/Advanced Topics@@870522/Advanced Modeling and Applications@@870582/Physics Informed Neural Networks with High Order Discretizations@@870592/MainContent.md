## Introduction
The fusion of [deep learning](@entry_id:142022) with [scientific computing](@entry_id:143987) has given rise to Physics-Informed Neural Networks (PINNs), a novel approach for [solving partial differential equations](@entry_id:136409) (PDEs) by embedding physical laws directly into the neural network's training process. While promising, the effectiveness of PINNs is often limited by the simplicity of standard [discretization](@entry_id:145012) techniques, which can struggle with solution accuracy and training efficiency. This article addresses this gap by systematically integrating the power and precision of [high-order numerical methods](@entry_id:142601)—specifically spectral and Discontinuous Galerkin (DG) methods—with the PINN framework.

Across the following chapters, you will embark on a comprehensive exploration of this advanced methodology. In **Principles and Mechanisms**, we will delve into the core of the approach, from formulating physics-informed [loss functions](@entry_id:634569) in both strong and weak forms to discretizing them with [high-order accuracy](@entry_id:163460). Next, **Applications and Interdisciplinary Connections** will showcase the versatility of this synthesis, demonstrating how it tackles challenges in complex geometries, inverse problems, and uncertainty quantification. Finally, **Hands-On Practices** will provide concrete opportunities to apply these concepts and solidify your understanding of their implementation. This journey will equip you with the knowledge to build more robust, accurate, and physically consistent neural network solvers for complex scientific and engineering problems.

## Principles and Mechanisms

The successful application of Physics-Informed Neural Networks (PINNs) hinges on the careful construction of a loss function that accurately reflects the underlying physical laws. When integrated with high-order [discretization methods](@entry_id:272547), this process gains mathematical rigor and computational power, but also introduces new layers of complexity. This chapter delves into the core principles and mechanisms governing the formulation, [discretization](@entry_id:145012), and optimization of PINNs in a high-order framework. We will transition from defining the fundamental loss functional to constructing its discrete counterpart using spectral and Discontinuous Galerkin (DG) methods, and finally, explore advanced architectural and regularization strategies that enhance training and solution quality.

### Formulating the Physics-Informed Loss

The objective of a PINN is to find a set of network parameters $\theta$ such that the function $u_{\theta}(\mathbf{x}, t)$ approximated by the neural network satisfies a given Partial Differential Equation (PDE) system. This is achieved by minimizing a loss function that quantifies the extent to which $u_{\theta}$ violates the governing equations and associated constraints. There are two primary approaches to formalizing this residual: the strong form and the weak form.

#### Strong-Form vs. Weak-Form Residuals

Consider an abstract PDE on a domain $\Omega$, written as $F(u) = 0$. The most direct approach to defining a loss is to measure the magnitude of the residual function $F(u_{\theta})$ across the domain. This is known as **strong-form [residual minimization](@entry_id:754272)**. The size of the residual is typically measured using a function space norm, most commonly the squared $L^2(\Omega)$ norm, leading to a loss term of the form:

$J_s(\theta) = \|F(u_{\theta})\|_{L^2(\Omega)}^2 = \int_{\Omega} |F(u_{\theta})(\mathbf{x})|^2 \, \mathrm{d}\mathbf{x}$

For this to be well-defined, the network approximation $u_{\theta}$ must possess sufficient regularity. If $F$ is a [differential operator](@entry_id:202628) of order $m$, $u_{\theta}$ must generally belong to the Sobolev space $H^m(\Omega)$ to ensure that $F(u_{\theta})$ is square-integrable.

An alternative, inspired by classical Galerkin methods, is **weak-form [residual minimization](@entry_id:754272)**. The [weak formulation](@entry_id:142897) of a PDE states that $\langle F(u), v \rangle = 0$ for all [test functions](@entry_id:166589) $v$ in a suitable [test space](@entry_id:755876) $V$. Here, $\langle \cdot, \cdot \rangle$ denotes a duality pairing, typically an integral. For an approximate solution $u_{\theta}$, this equality will not hold for all $v \in V$. The weak-form residual measures the largest violation by considering $F(u_{\theta})$ as a [linear functional](@entry_id:144884) on the [test space](@entry_id:755876) $V$. The magnitude of this violation is the norm of this functional in the [dual space](@entry_id:146945) $V'$, defined as:

$J_w(\theta) = \|F(u_{\theta})\|_{V'}^2 = \left( \sup_{v \in V, v \neq 0} \frac{|\langle F(u_{\theta}), v \rangle|}{\|v\|_V} \right)^2$

The choice of the [test space](@entry_id:755876) $V$ and its norm $\|v\|_V$ is critical and depends on the structure of the operator $F$. For second-order elliptic problems, $V$ is often a subspace of $H^1(\Omega)$. The distinction between these formulations is fundamental: the strong form penalizes the pointwise error in the equation itself, while the weak form penalizes the error in a projectional sense, averaged against a set of test functions [@problem_id:3408318]. The [weak form](@entry_id:137295) naturally incorporates lower-order derivatives and boundary conditions through [integration by parts](@entry_id:136350), making it a powerful framework for methods like Discontinuous Galerkin.

### Constructing the Discrete Loss with High-Order Methods

To train a PINN, the continuous integral-based [loss functions](@entry_id:634569) described above must be approximated by a discrete sum that can be evaluated on a computer. High-order numerical methods provide a systematic and accurate way to perform this discretization.

#### Spectral and Pseudospectral Discretizations

Spectral methods are characterized by the use of global, smooth basis functions that lead to exceptionally fast convergence for smooth solutions.

**Orthogonal Polynomial Bases:** The natural choice of basis functions for spectral methods on a finite interval, say $[-1,1]$, are families of **[orthogonal polynomials](@entry_id:146918)**. Two of the most important are the **Legendre polynomials** $\{P_n(x)\}$ and the **Chebyshev polynomials** $\{T_n(x)\}$. These polynomials are eigenfunctions of respective self-adjoint Sturm-Liouville problems, which guarantees their orthogonality. Specifically, Legendre polynomials are orthogonal with a weight function $w(x)=1$, while Chebyshev polynomials are orthogonal with a weight $w(x)=(1-x^2)^{-1/2}$ [@problem_id:3408369]. An expansion in these bases, $u_N(x) = \sum_{n=0}^N \hat{u}_n \phi_n(x)$, exhibits **[spectral convergence](@entry_id:142546)** for analytic solutions: the error decreases faster than any algebraic power of $1/N$. This rapid convergence is a primary motivation for their use.

**High-Order Quadrature and Collocation Points:** The [discretization](@entry_id:145012) of a loss integral like $\int_{-1}^1 r(x)^2 dx$ relies on **numerical quadrature**. A [quadrature rule](@entry_id:175061) approximates the integral as a weighted sum of function values at specific points: $\int_{-1}^1 r(x)^2 dx \approx \sum_{i=0}^N w_i r(x_i)^2$. For [spectral methods](@entry_id:141737), the choice of quadrature points $\{x_i\}$ is not arbitrary. Using points related to the roots of [orthogonal polynomials](@entry_id:146918) yields highly accurate **Gaussian quadrature** rules.

A particularly important set of points are the **Legendre-Gauss-Lobatto (LGL) nodes**. This set of $N+1$ points on $[-1,1]$ consists of the endpoints $-1$ and $1$, plus the $N-1$ interior roots of $P_N'(x)$, the derivative of the $N$-th Legendre polynomial. The LGL [quadrature rule](@entry_id:175061) is exact for all polynomials of degree up to $2N-1$. Furthermore, interpolation at LGL nodes is very stable; the associated Lebesgue constant grows slowly as $\mathcal{O}(\log N)$, which avoids the explosive error of the Runge phenomenon seen with [equispaced points](@entry_id:637779) and underpins the [spectral accuracy](@entry_id:147277) of interpolation-based methods [@problem_id:3408299]. These nodes are therefore an excellent choice for collocation points in a PINN.

**A Complete Discretized Loss Function:** We can now assemble a complete [loss function](@entry_id:136784) for an initial-boundary value problem by discretizing the residual, boundary, and initial condition terms using high-order quadrature [@problem_id:3408342]. For an equation on a domain $\Omega \times (0,T)$, the continuous loss is a weighted sum of $L^2$ norms:

$L_{\text{cont}} = \lambda_r \|F(u_\theta)\|^2_{L^2(\Omega \times (0,T))} + \lambda_b \|\gamma u_\theta - g\|^2_{L^2(\partial\Omega \times (0,T))} + \lambda_i \|u_\theta(\cdot, 0) - u_0\|^2_{L^2(\Omega)}$

Here, $\gamma$ is the [trace operator](@entry_id:183665) restricting the solution to the boundary. To discretize this, we partition the spatial domain $\Omega$ into a mesh of elements $\mathcal{T}_h$. On each element, we use a high-order [quadrature rule](@entry_id:175061) (e.g., LGL) with nodes $\{x_q^K\}$ and weights $\{w_q^K\}$. The time domain is discretized with a similar rule with nodes $\{t_m\}$ and weights $\{\omega_m\}$. The discrete loss becomes:

$L = \lambda_r \sum_{K \in \mathcal{T}_h} \sum_{q, m} w_q^K J_K(x_q^K) \omega_m |F(u_\theta(x_q^K, t_m))|^2 + \dots$

Crucially, the quadrature sum must include the **Jacobian determinant** $J_K$ arising from mapping the reference quadrature rule to the physical element $K$. This factor correctly accounts for the volume or area of the integration element. Similar terms are constructed for the boundary and initial losses, using appropriate surface Jacobians and [quadrature rules](@entry_id:753909) [@problem_id:3408342].

#### Discontinuous Galerkin Discretizations

For problems where weak formulations are more natural, such as conservation laws, the **Discontinuous Galerkin (DG)** method provides a robust and flexible framework. In DG, the solution is approximated by polynomials that are defined element-wise and are allowed to be discontinuous across element boundaries.

The DG weak form is derived by multiplying the PDE by a [test function](@entry_id:178872) $v_h$ from the same [piecewise polynomial](@entry_id:144637) space, integrating over each element $K$, and applying integration by parts. This process introduces boundary integrals over the faces of each element, $\partial K$. For a conservation law like $u_t + \nabla \cdot \mathbf{f}(u) = 0$, the [weak form](@entry_id:137295) on an element $K$ becomes:

$\int_K u_t v_h \, \mathrm{d}x - \int_K \mathbf{f}(u) \cdot \nabla v_h \, \mathrm{d}x + \int_{\partial K} (\mathbf{f}(u) \cdot \mathbf{n}_K) v_h \, \mathrm{d}s = 0$

Since $u$ is discontinuous, the flux trace $\mathbf{f}(u) \cdot \mathbf{n}_K$ is ambiguous. The core idea of DG is to replace it with a single-valued **numerical flux** $\hat{f}(u^-, u^+; \mathbf{n})$, which depends on the states on both sides of the face ($u^-$ and $u^+$). Summing over all elements and carefully accounting for contributions from interior and boundary faces leads to the full semi-discrete weak form [@problem_id:3408313]. For a PINN based on a DG weak form, the loss function is the squared residual of this global [weak formulation](@entry_id:142897), evaluated for a basis of [test functions](@entry_id:166589) $v_h$.

### Architectural and Algorithmic Enhancements

The principles of [high-order methods](@entry_id:165413) can directly inspire improvements to the PINN architecture and training algorithms.

#### Neural-Spectral Architectures

Instead of using a standard [multilayer perceptron](@entry_id:636847) (MLP) and enforcing the PDE through a collocation-based loss, one can construct a **neural-spectral model**. In this approach, the [network architecture](@entry_id:268981) itself represents a spectral expansion. For example, a network can be designed where the final layer is a [linear combination](@entry_id:155091) of Legendre polynomials [@problem_id:3408339]:

$u_{\mathbf{a}}(x) = \sum_{n=0}^{N} a_{n} P_{n}(x)$

Here, the learnable parameters are the spectral coefficients $\mathbf{a} = (a_0, \dots, a_N)^\top$. The derivatives of $u_{\mathbf{a}}$ are computed analytically via derivatives of the basis polynomials. A [loss function](@entry_id:136784) can be constructed as before, but the optimization is performed with respect to the coefficients $\mathbf{a}$. For linear PDEs, this leads to a simple quadratic loss function, and the gradient $\nabla_{\mathbf{a}} \mathcal{J}(\mathbf{a})$ can be derived in a closed matrix form, resulting in a linear system to be solved. This can be much more efficient and stable than training a general MLP.

#### Overcoming Spectral Bias with Fourier Feature Mappings

A well-known challenge in training PINNs is **[spectral bias](@entry_id:145636)**: standard MLPs with simple [activation functions](@entry_id:141784) struggle to learn high-frequency functions. This limits their ability to represent solutions with fine-scale details. A powerful technique to overcome this is the use of **Fourier feature mappings** [@problem_id:3408303]. The scalar input $x$ is first transformed into a high-dimensional feature vector:

$x \mapsto \gamma(x) = [\cos(\omega_1 x), \sin(\omega_1 x), \dots, \cos(\omega_M x), \sin(\omega_M x)]$

This feature vector is then fed into a standard MLP. By providing high-frequency basis functions as direct inputs, the network no longer needs to construct them from scratch; it only needs to learn the correct linear combination. This allows even shallow networks to represent functions with wavelengths on the order of $O(1/N)$, aligning the expressive power of the PINN with the resolution of a high-order [discretization](@entry_id:145012) of degree $N$ [@problem_id:3408303]. For a DG method on an element of size $h$ with polynomial degree $p$, choosing frequencies $\omega$ on the order of $p/h$ aligns the PINN's input spectrum with the scale of functions the DG basis can resolve [@problem_id:3408303].

#### Handling Nonlinearities: The Problem of Aliasing

When solving nonlinear PDEs, a subtle but critical error known as **aliasing** can arise. Consider computing the term $u^2$ for a function $u_K(x) = \sum_{|k|\le K} \hat{u}_k e^{ikx}$ with a finite number of Fourier modes. The exact product $u_K^2$ contains frequencies up to $|k|=2K$. If this product is evaluated by simply squaring the function values at $N=2K+1$ collocation points (a pseudospectral approach), the discrete Fourier transform will misinterpret the energy from the unresolved high-frequency modes (those with $|k|>K$) as belonging to the resolved modes. This "folding back" of energy is [aliasing](@entry_id:146322), and it can lead to nonphysical behavior and instability [@problem_id:3408308].

To prevent this, **[dealiasing](@entry_id:748248)** techniques are required. In Fourier methods, the standard approach for a [quadratic nonlinearity](@entry_id:753902) is the **3/2-rule**: the input spectra are padded with zeros to a length of at least $3/2$ times the original length, the product is computed in physical space on the corresponding larger grid, and then transformed back and truncated. In the context of DG methods, the same issue appears as under-integration. If $u_h$ is a polynomial of degree $p$, then $u_h^2$ is of degree $2p$. The weak-form integral may involve products of $u_h^2$ with [test functions](@entry_id:166589), leading to integrands of degree $3p$ or higher. The quadrature rule must be accurate enough to integrate these high-degree polynomials exactly; otherwise, aliasing occurs. This is known as **over-integration** or exact integration [@problem_id:3408308].

### Advanced Training and Regularization Strategies

Incorporating deeper physical principles into the training process can significantly improve the robustness and accuracy of PINNs.

#### Loss Function Normalization and Gradient Scaling

A typical PINN loss function is a sum of multiple terms (residual, boundary, initial, etc.). These terms may have different physical units and numerical magnitudes, which can unbalance the optimization process. A principled approach to weighting these terms is to normalize them using characteristic physical scales of the problem (e.g., characteristic velocity $U$, length $L$, and time $T$) [@problem_id:3408342]. For example, the boundary term, representing the squared error in the solution, has units of $U^2$. The corresponding continuous integral has units $U^2 \cdot (\text{Area}) \cdot (\text{Time})$. The weighting factor $\lambda_b$ should be chosen as $\lambda_b = 1/(U^2 |\partial\Omega| T)$ to make the loss term dimensionless and of order one. Applying this principle to all terms helps balance their contributions based on physical significance.

Furthermore, when dealing with high-order derivatives and high-frequency solutions, another issue arises: [gradient scaling](@entry_id:270871). The $m$-th derivative of a Fourier mode $\cos(\omega x)$ scales as $\omega^m$. This means that residual terms involving higher derivatives will have gradients with respect to high-frequency parameters that are much larger than those for low-frequency parameters. This can create a very **stiff** optimization problem, hindering convergence [@problem_id:3408303]. This necessitates adaptive weighting schemes or normalizations that account for derivative order.

#### Physics-Inspired Regularization

Regularization terms can be added to the loss function to enforce desirable properties on the solution, often corresponding to physical principles.

**Smoothness Regularization:** To prevent [overfitting](@entry_id:139093) and obtain smoother solutions, one can penalize a norm of the solution's derivatives. The squared **$H^1$ [seminorm](@entry_id:264573)**, $|u|_{H^1}^2 = \int_\Omega |\nabla u|^2 d\mathbf{x}$, is a common choice. For a solution represented by a spectral expansion, this [seminorm](@entry_id:264573) often has a simple [closed-form expression](@entry_id:267458) in terms of the spectral coefficients. For example, for an axisymmetric function on a sphere expanded in zonal [spherical harmonics](@entry_id:156424) $u = \sum_n \hat{u}_n Y_{n0}$, the [seminorm](@entry_id:264573) is $|u|_{H^1(S^2)}^2 = \sum_n n(n+1) \hat{u}_n^2$ [@problem_id:3408338]. Adding this term to the [loss function](@entry_id:136784) acts as a **Tikhonov regularizer** that penalizes high-frequency coefficients more heavily (due to the $n(n+1)$ factor), thus promoting smoother solutions.

**Conservation Law Enforcement:** For many physical systems, in addition to the governing PDE, there are global invariants, such as the [conservation of energy](@entry_id:140514), mass, or momentum. A powerful advanced technique is to construct a loss term that explicitly enforces these conservation laws. For a linear evolution equation like $u_t + \mathcal{L}u = 0$, one can often derive an [energy balance equation](@entry_id:191484), $\frac{dE}{dt} = -D$, where $E$ is the energy and $D$ is the [dissipation rate](@entry_id:748577). By discretizing this relation using the same high-order framework (e.g., DG matrices), one can formulate a discrete energy balance. A penalty term can then be added to the PINN loss, consisting of the squared residual of this discrete [energy balance equation](@entry_id:191484), integrated over time [@problem_id:3408352]. This forces the PINN to learn a solution that not only satisfies the local PDE but also respects the global physical structure of the system.

#### Diagnosing and Mitigating Training Pathologies

The training dynamics of PINNs can be complex and sometimes stall in **training plateaus**, where the loss stagnates far from zero. These pathologies can often be understood by analyzing the properties of the underlying discrete numerical operator. For a linear PDE on a periodic domain, the DG operator can be analyzed via a **discrete dispersion relation**, $\omega_j(k)$, which gives the frequency of the $j$-th modal branch as a function of wavenumber $k$. Besides the single **physical branch** that approximates the true solution's behavior, DG methods introduce $p$ **spurious branches** corresponding to non-physical, element-local modes.

A training plateau can occur if some of these [spurious modes](@entry_id:163321) correspond to eigenvalues of the linearized training operator that are close to zero. This creates "blind spots" in the [loss landscape](@entry_id:140292) where the gradient is vanishingly small, causing the optimizer to get stuck. The problem lies not in the physical solution but in spurious numerical artifacts that the optimizer cannot effectively remove [@problem_id:3408357]. Mitigation strategies involve modifying the discrete operator to eliminate this near-[null space](@entry_id:151476). This can be achieved with techniques like:
- **Modal Filtering:** Applying a filter that selectively [damps](@entry_id:143944) the highest-degree polynomial modes within each element. This raises the eigenvalues associated with spurious branches without significantly affecting the physical branch.
- **Spectral Viscosity:** Adding a targeted hyper-viscosity term (e.g., $\nu_p(-\Delta)^s u_h$) to the residual operator. This adds dissipation primarily at high wavenumbers, accelerating the decay of [spurious modes](@entry_id:163321) during training [@problem_id:3408357].

By understanding the connection between PINN training dynamics and the spectral properties of the underlying high-order [discretization](@entry_id:145012), we can diagnose and remedy these challenging training issues, leading to more robust and reliable [physics-informed learning](@entry_id:136796).