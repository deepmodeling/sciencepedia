## Introduction
In the field of computational mechanics, the Finite Element Method (FEM) has long been the dominant tool for [solving partial differential equations](@entry_id:136409). However, its reliance on a predefined mesh can create significant challenges in problems involving large deformations, evolving discontinuities like cracks, or complex geometries that require frequent and costly remeshing. Meshfree methods, such as the Element-Free Galerkin (EFG) method and the Reproducing Kernel Particle Method (RKPM), have emerged as a powerful alternative, addressing these limitations by constructing numerical approximations directly from a distribution of nodes without the need for element connectivity. This article provides a graduate-level exploration of these advanced computational techniques.

This guide is structured to build a comprehensive understanding from the ground up. The first chapter, **Principles and Mechanisms**, delves into the mathematical heart of [meshfree methods](@entry_id:177458), detailing the Moving Least Squares approximation and the fundamental properties of the resulting shape functions. Following this, **Applications and Interdisciplinary Connections** shifts from theory to practice, demonstrating how these methods are applied to solve challenging problems in solid mechanics, fracture mechanics, and [transport phenomena](@entry_id:147655), while also addressing critical implementation details like numerical integration and boundary condition enforcement. Finally, the **Hands-On Practices** section offers targeted problems to reinforce these concepts and bridge the gap between theory and application. We begin by examining the core principles that distinguish [meshfree methods](@entry_id:177458) from their mesh-based counterparts.

## Principles and Mechanisms

This chapter delineates the foundational principles and constructive mechanisms of [meshfree methods](@entry_id:177458), with a particular focus on the Element-Free Galerkin (EFG) and Reproducing Kernel Particle Method (RKPM). Unlike the traditional Finite Element Method (FEM), which relies on a predefined mesh to establish element connectivity and define shape function domains, [meshfree methods](@entry_id:177458) construct the problem approximation directly from a set of nodes, often referred to as a "node cloud" [@problem_id:2576482]. This departure from mesh-based connectivity grants these methods significant flexibility in handling problems involving [large deformations](@entry_id:167243), moving boundaries, and complex geometries.

### The Moving Least Squares Approximation

The cornerstone of many prominent [meshfree methods](@entry_id:177458), including EFG, is the **Moving Least Squares (MLS)** approximation. The central idea of MLS is to build a continuous approximation of a field not from fixed, element-wise basis functions, but by performing a weighted [least-squares regression](@entry_id:262382) at every point in the domain.

#### The Local Approximation Problem

Consider a set of $N$ nodes, $\{\mathbf{x}_I\}_{I=1}^N$, distributed throughout a domain $\Omega$. Associated with each node is a nodal parameter, or degree of freedom, $d_I$. The goal is to construct an approximation $u_h(\mathbf{x})$ of a field $u(\mathbf{x})$ as a [linear combination](@entry_id:155091) of [shape functions](@entry_id:141015) $\phi_I(\mathbf{x})$ and these nodal parameters:

$u_h(\mathbf{x}) = \sum_{I=1}^{N} \phi_I(\mathbf{x}) d_I$

In the MLS procedure, we determine the value of $u_h(\mathbf{x})$ at an arbitrary evaluation point $\mathbf{x}$ by first hypothesizing a local [polynomial approximation](@entry_id:137391), $u_h(\mathbf{x}, \mathbf{y}) = \mathbf{p}^T(\mathbf{y}) \mathbf{a}(\mathbf{x})$, where $\mathbf{p}(\mathbf{y})$ is a vector of polynomial basis functions (e.g., in 2D for a linear basis, $\mathbf{p}^T(\mathbf{y}) = [1, y_1, y_2]$) and $\mathbf{a}(\mathbf{x})$ is a vector of unknown coefficients that depends on the evaluation point $\mathbf{x}$.

These coefficients are found by minimizing a weighted, squared residual functional, $J$, which measures the discrepancy between the local polynomial and the nodal parameters $d_I$ of the nodes neighboring $\mathbf{x}$:

$J(\mathbf{a}(\mathbf{x})) = \sum_{I=1}^{N} w_I(\mathbf{x}) \left( \mathbf{p}^T(\mathbf{x}_I) \mathbf{a}(\mathbf{x}) - d_I \right)^2$

Here, $w_I(\mathbf{x})$ is a **weight function** that depends on the distance between the evaluation point $\mathbf{x}$ and the node $\mathbf{x}_I$. This function has a [compact support](@entry_id:276214), meaning it is non-zero only within a certain radius of influence around $\mathbf{x}$, effectively creating a local neighborhood for the least-squares fit.

#### Derivation of the MLS Shape Function

To find the coefficient vector $\mathbf{a}(\mathbf{x})$ that minimizes $J$, we take the derivative of $J$ with respect to $\mathbf{a}(\mathbf{x})$ and set it to zero [@problem_id:2576459]:

$\frac{\partial J}{\partial \mathbf{a}(\mathbf{x})} = 2 \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) \left( \mathbf{p}^T(\mathbf{x}_I) \mathbf{a}(\mathbf{x}) - d_I \right) = \mathbf{0}$

Rearranging this yields the so-called [normal equations](@entry_id:142238):

$\left( \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) \mathbf{p}^T(\mathbf{x}_I) \right) \mathbf{a}(\mathbf{x}) = \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) d_I$

This is a linear system of the form $A(\mathbf{x}) \mathbf{a}(\mathbf{x}) = B(\mathbf{x}) \mathbf{d}$, where $\mathbf{d}$ is the vector of all nodal parameters. The matrix $A(\mathbf{x})$ is the crucial **MLS moment matrix**:

$A(\mathbf{x}) = \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) \mathbf{p}^T(\mathbf{x}_I)$

Assuming $A(\mathbf{x})$ is invertible, we can solve for the coefficients:

$\mathbf{a}(\mathbf{x}) = A^{-1}(\mathbf{x}) \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) d_I$

The MLS approximation at point $\mathbf{x}$ is then given by evaluating the fitted polynomial at that same point: $u_h(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) \mathbf{a}(\mathbf{x})$. Substituting the expression for $\mathbf{a}(\mathbf{x})$ gives:

$u_h(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) A^{-1}(\mathbf{x}) \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) d_I$

By comparing this to the standard form $u_h(\mathbf{x}) = \sum_I \phi_I(\mathbf{x}) d_I$, we can identify the MLS shape function for node $I$:

$\phi_I(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) A^{-1}(\mathbf{x}) w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I)$

This expression reveals that the [shape functions](@entry_id:141015) are typically [rational functions](@entry_id:154279) of $\mathbf{x}$ (a polynomial in the numerator and the determinant of $A(\mathbf{x})$ in the denominator) and are constructed "on the fly" at any point where they need to be evaluated [@problem_id:2576480].

#### Invertibility of the Moment Matrix: The Unisolvency Condition

The entire MLS procedure hinges on the invertibility of the moment matrix $A(\mathbf{x})$. The matrix $A(\mathbf{x})$ is symmetric and [positive semi-definite](@entry_id:262808) by construction. For it to be invertible, it must be strictly [positive definite](@entry_id:149459). This leads to a fundamental **unisolvency condition**: for a given polynomial basis $\mathbf{p}(\mathbf{x})$ of dimension $n_p$ (e.g., for a complete quadratic basis in 2D, $m=2, d=2$, $n_p = \binom{2+2}{2} = 6$), the MLS moment matrix $A(\mathbf{x})$ is non-singular if and only if the set of nodes with strictly positive weights, $\{\mathbf{x}_I | w_I(\mathbf{x}) > 0\}$, contains a unisolvent subset [@problem_id:2576535].

This condition has two practical implications [@problem_id:2576459]:
1.  **Sufficient Number of Nodes:** The local support domain at $\mathbf{x}$ must contain at least $n_p$ nodes.
2.  **General Geometric Position:** These nodes must not be arranged in a degenerate configuration. That is, there should be no non-zero polynomial of degree up to $m$ that vanishes at all of these nodal locations. For instance, for a linear basis in $\mathbb{R}^2$ ($n_p=3$), the three active nodes must not be collinear. For a quadratic basis in $\mathbb{R}^2$ ($n_p=6$), the six active nodes must not all lie on a single conic section [@problem_id:2576535].

Failure to meet this condition at any point $\mathbf{x}$ means the MLS approximation is not well-defined there.

### The Reproducing Kernel Particle Method (RKPM)

RKPM offers an alternative but closely related perspective. It begins with a **kernel function**, $W$, which is analogous to the MLS weight function. The goal is to create a **corrected kernel** that guarantees the reproduction of polynomials up to a certain order. The RKPM shape function for node $I$ is constructed as a product of a correction function and the original kernel, along with a nodal quadrature weight $\omega_I$:

$\phi_I^{\mathrm{RKPM}}(\mathbf{x}) = C(\mathbf{x}, \mathbf{x}_I) W_I(\mathbf{x}) \omega_I$

The correction function $C(\mathbf{x}, \mathbf{x}_I)$ is designed to enforce the [polynomial reproduction](@entry_id:753580) property. Following a derivation based on this principle, one arrives at an expression for the RKPM shape function that is strikingly similar to the MLS one [@problem_id:2576480]:

$\phi_I^{\mathrm{RKPM}}(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) M^{-1}(\mathbf{x}) \omega_I W_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I)$

where $M(\mathbf{x})$ is the RKPM moment matrix, defined as $M(\mathbf{x}) = \sum_{J=1}^N \omega_J W_J(\mathbf{x}) \mathbf{p}(\mathbf{x}_J) \mathbf{p}^T(\mathbf{x}_J)$.

A crucial insight is that the MLS and RKPM formulations are essentially equivalent under specific conditions. If the same polynomial basis $\mathbf{p}(\mathbf{x})$ is used, the kernel function is identical to the weight function ($W \equiv w$), and the nodal [quadrature weights](@entry_id:753910) are uniform ($\omega_J = \text{constant}$), then the RKPM [shape functions](@entry_id:141015) become identical to the MLS [shape functions](@entry_id:141015) [@problem_id:2576480]. This reveals a deep connection: both methods are different formalisms for achieving the same goal of constructing high-order, non-interpolatory approximations from a cloud of nodes.

### Fundamental Properties of Meshfree Approximations

The MLS and RKPM construction endows the resulting shape functions with several key properties that dictate their behavior and application.

#### Polynomial Completeness and Accuracy

By construction, if a polynomial basis $\mathbf{p}(\mathbf{x})$ that spans all polynomials up to degree $m$ (denoted $\mathcal{P}_m$) is used and the unisolvency condition is met, the resulting [shape functions](@entry_id:141015) will exactly reproduce any polynomial in $\mathcal{P}_m$. This property is known as **m-th [order completeness](@entry_id:160957)** or consistency [@problem_id:2576517]. For any polynomial $p \in \mathcal{P}_m$, the following identity holds:

$\sum_{I=1}^N \phi_I(\mathbf{x}) p(\mathbf{x}_I) = p(\mathbf{x})$

This property is the source of the high accuracy of [meshfree methods](@entry_id:177458). According to approximation theory, for a sufficiently smooth exact solution $u \in H^{m+1}(\Omega)$ of an elliptic boundary value problem, a method with $m$-th [order completeness](@entry_id:160957) can achieve a convergence rate of $O(h^m)$ in the energy ($H^1$) norm and $O(h^{m+1})$ in the $L^2$ norm, where $h$ is the characteristic nodal spacing [@problem_id:2576517]. Furthermore, if the exact solution happens to be a polynomial of degree at most $m$, the Galerkin solution will be exact (up to errors from [numerical integration](@entry_id:142553) and boundary condition enforcement) [@problem_id:2576517].

#### Partition of Unity

A direct consequence of using a polynomial basis that includes the constant term (i.e., $m \ge 0$) is the **[partition of unity](@entry_id:141893) (PU)** property [@problem_id:2576531]:

$\sum_{I=1}^N \phi_I(\mathbf{x}) = 1, \quad \forall \mathbf{x} \in \Omega$

This property ensures the exact reproduction of constant states, which is the lowest level of consistency required for convergence. In the context of Galerkin methods for physical balance laws, PU is critically important. It guarantees that a [constant function](@entry_id:152060) is a member of the discrete [test space](@entry_id:755876). Using this constant [test function](@entry_id:178872) in the [weak form](@entry_id:137295) recovers the discrete version of the global conservation law (e.g., global force balance), a property verified by the patch test [@problem_id:2576531].

#### Lack of the Kronecker-Delta Property

A defining characteristic of standard MLS and RKPM shape functions is that they are **not interpolatory**. They do not satisfy the **Kronecker-delta property**, meaning that in general [@problem_id:2576486]:

$\phi_I(\mathbf{x}_J) \neq \delta_{IJ}$

This is because the MLS approximation is a weighted best-fit, not a direct interpolation. The value of the approximation at a node, $u_h(\mathbf{x}_J) = \sum_I \phi_I(\mathbf{x}_J) d_I$, is a weighted average of the parameters of all neighboring nodes, and is not generally equal to $d_J$.

This has a profound practical implication: **essential (Dirichlet) boundary conditions cannot be imposed by simply setting the degrees of freedom of boundary nodes**. Doing so would not enforce the desired value on the solution itself. Instead, one must resort to alternative, "weak" enforcement strategies, such as the [penalty method](@entry_id:143559), the use of Lagrange multipliers, or Nitsche's method [@problem_id:2576486]. While variants like Interpolating MLS (IMLS) can be formulated to enforce the Kronecker-delta property, they often do so at the cost of reduced smoothness or poorer [numerical conditioning](@entry_id:136760) [@problem_id:2576486].

#### Smoothness

The smoothness of the MLS shape functions is directly inherited from the smoothness of the weight function $w(\mathbf{x})$. If the weight function is $C^k$ continuous within its support, the resulting shape functions will also be $C^k$ continuous in regions where the set of influencing nodes does not change [@problem_id:2576464]. This provides a straightforward way to construct high-order continuous approximations (e.g., $C^1$ or $C^2$), which is advantageous for solving higher-order PDEs like those for plates and shells.

### Practical Considerations and Parameter Selection

The successful implementation of EFG or RKPM requires careful selection of several key parameters.

#### Choice of Weight Function

The weight function defines the locality of the approximation. Several choices are common, such as polynomial [splines](@entry_id:143749) and truncated Gaussian functions. When selecting a weight function, one must consider its smoothness and computational cost [@problem_id:2576464]. For example:
- A **cubic spline** weight can be constructed to be $C^2$ at its support boundary by enforcing zero value, first, and second derivatives.
- A **truncated Gaussian** weight of the form $w(r) = \exp(-\alpha r^2) - \exp(-\alpha)$ is only $C^0$ at the boundary.
- Computationally, evaluating polynomial weights is typically cheaper than evaluating exponential functions, making them attractive for [large-scale simulations](@entry_id:189129) [@problem_id:2576464].

#### Sizing the Support Domain

The size of the support for each node, typically defined by a radius $r_s$, is one of the most critical parameters. It is often expressed as a multiple of the characteristic nodal spacing $h$, via the ratio $\rho = r_s/h$. The choice of $\rho$ involves a delicate balance [@problem_id:2576527]:
- **If $\rho$ is too small**, a point $\mathbf{x}$ may not have enough neighbors in its support to ensure the moment matrix $A(\mathbf{x})$ is invertible, violating the unisolvency condition. For instance, in 1D with a linear basis, a support radius $r_s = h$ will cause singularity at nodal locations.
- **If $\rho$ is just large enough** to ensure unisolvency (e.g., ensuring at least $n_p$ nodes are in the support), the moment matrix can be ill-conditioned, leading to [numerical instability](@entry_id:137058).
- **Moderately increasing $\rho$** (e.g., to values between 2 and 3 in 2D) typically improves the conditioning of $A(\mathbf{x})$ and the overall stability of the method.
- **If $\rho$ is too large**, the approximation loses its local character. The number of neighbors for each point evaluation increases (scaling as $\rho^d$ in $d$ dimensions [@problem_id:2576464]), drastically increasing computational cost. The resulting global stiffness matrix also becomes denser, which can degrade its condition number.

Therefore, the support size must be scaled with the nodal spacing $h$ (i.e., $\rho$ is kept constant as $h \to 0$) to maintain a constant stencil size, uniform sparsity, and stability [@problem_id:2576527].

#### Numerical Integration

Since the integrand of the [stiffness matrix](@entry_id:178659), $(\nabla \phi_I)^T k \nabla \phi_J$, is a complex rational function, numerical quadrature is indispensable. The Galerkin weak form integrals are computed by partitioning the domain $\Omega$ into a **background mesh** of simple integration cells (e.g., quadrilaterals or triangles), which is independent of the node distribution [@problem_id:2576510].

The accuracy of the [quadrature rule](@entry_id:175061) on these cells is paramount. An insufficient rule will fail to preserve the consistency of the approximation, leading to a loss of the optimal convergence rate—a phenomenon known as failing the **patch test**. A fundamental result states that for a method with $p$-th order [polynomial completeness](@entry_id:177462), the numerical quadrature rule used to compute the stiffness matrix must be exact for polynomials of degree at least $2p-2$ [@problem_id:2576510].

This requirement translates to specific [quadrature rules](@entry_id:753909) for different scenarios:
- **1D Integration:** An $n$-point Gauss-Legendre rule must be used with $n \ge p$.
- **2D Quadrilateral Cells:** An $m \times m$ [tensor product](@entry_id:140694) Gauss rule must be used with $m \ge p$.

Using a rule that is significantly more accurate than this ("over-integration") increases computational cost unnecessarily without improving the asymptotic convergence rate. Using a less accurate rule ("under-integration") can lead to suboptimal convergence or even instability.