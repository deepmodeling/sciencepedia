## Introduction
In the landscape of computational mechanics, meshless methods have emerged as a powerful and flexible alternative to the traditional Finite Element Method (FEM), particularly for problems that challenge the very foundation of mesh-based analysis. Conventional FEM simulations can be severely hampered by issues like mesh distortion in [large deformation](@entry_id:164402) scenarios or the complex, continuous remeshing required to track evolving discontinuities like cracks. Meshless methods address this fundamental limitation by constructing numerical approximations directly from a set of nodes, without relying on a predefined element mesh.

This article provides a comprehensive exploration of these advanced techniques. We will begin by deconstructing their core **Principles and Mechanisms**, focusing on the widely used Element-Free Galerkin (EFG) method and its Moving Least Squares (MLS) approximation. Next, we will explore the diverse **Applications and Interdisciplinary Connections**, showcasing how these methods solve complex problems in solid mechanics, [geomechanics](@entry_id:175967), and beyond. Finally, a series of **Hands-On Practices** will provide concrete exercises to solidify the theoretical concepts and build practical implementation skills.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of meshless methods, focusing on the formulation widely known as the Element-Free Galerkin (EFG) method. We will deconstruct the method into its core components, beginning with the construction of the approximation itself, followed by its application within a Galerkin framework to solve problems in [solid mechanics](@entry_id:164042), and concluding with a discussion on the critical aspects of numerical implementation and stability.

### The Meshless Approximation: Moving Least Squares (MLS)

The foundational departure of meshless methods from the classical Finite Element Method (FEM) is the construction of the approximation for a field variable, such as displacement. Whereas FEM relies on a predefined **mesh** of elements to define [piecewise polynomial](@entry_id:144637) shape functions, meshless methods build the approximation directly from a scattered set of points, or **nodes**, without requiring explicit element connectivity. This distinction has profound consequences for the entire numerical procedure, from approximation theory to the imposition of boundary conditions and [numerical integration](@entry_id:142553) [@problem_id:2661988].

The most prevalent technique for constructing this approximation is the **Moving Least Squares (MLS)** method. At its core, MLS is a local [approximation scheme](@entry_id:267451). For any given point $\boldsymbol{x}$ in the domain where we wish to evaluate the field, MLS constructs a unique polynomial that provides the best fit to the nodal data in the vicinity of $\boldsymbol{x}$.

#### The MLS Formulation

Let us consider a [scalar field](@entry_id:154310) $u(\boldsymbol{x})$ that we wish to approximate. We are given a set of nodes $\{\boldsymbol{x}_I\}_{I=1}^N$ with associated nodal parameters $\{d_I\}_{I=1}^N$. The MLS approximation $u^h(\boldsymbol{x})$ at an evaluation point $\boldsymbol{x}$ is locally represented by a polynomial:
$$
u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{a}(\boldsymbol{x})
$$
Here, $\boldsymbol{p}(\boldsymbol{x})$ is a vector of $m$ polynomial basis functions. For example, in two dimensions, a complete linear basis ($m=3$) is $\boldsymbol{p}^T(\boldsymbol{x}) = \begin{pmatrix} 1 & x & y \end{pmatrix}$, and a complete quadratic basis ($m=6$) is $\boldsymbol{p}^T(\boldsymbol{x}) = \begin{pmatrix} 1 & x & y & x^2 & xy & y^2 \end{pmatrix}$. The vector $\boldsymbol{a}(\boldsymbol{x})$ contains the coefficients of this polynomial, which are themselves functions of the evaluation point $\boldsymbol{x}$.

These coefficients are determined by minimizing a weighted, discrete least-squares functional, $J(\boldsymbol{a}(\boldsymbol{x}))$. This functional measures the sum of squared differences between the local polynomial evaluated at the nodal locations $\boldsymbol{x}_I$ and the nodal parameters $d_I$:
$$
J(\boldsymbol{a}(\boldsymbol{x})) = \sum_{I=1}^{N} w_I(\boldsymbol{x}) [ \boldsymbol{p}^T(\boldsymbol{x}_I) \boldsymbol{a}(\boldsymbol{x}) - d_I ]^2
$$
The function $w_I(\boldsymbol{x})$ is a **weight function** associated with node $I$, which is typically non-negative, has [compact support](@entry_id:276214), and attains its maximum value when $\boldsymbol{x} = \boldsymbol{x}_I$. The weight function ensures that only nodes in the neighborhood of $\boldsymbol{x}$ contribute significantly to the fit.

To find the coefficients $\boldsymbol{a}(\boldsymbol{x})$ that minimize $J$, we enforce the [stationarity condition](@entry_id:191085) $\frac{\partial J}{\partial \boldsymbol{a}} = \boldsymbol{0}$. This leads to a system of linear equations known as the **normal equations**:
$$
\boldsymbol{A}(\boldsymbol{x}) \boldsymbol{a}(\boldsymbol{x}) = \boldsymbol{B}(\boldsymbol{x}) \boldsymbol{d}
$$
where $\boldsymbol{d}$ is the vector of all nodal parameters, and the matrices $\boldsymbol{A}(\boldsymbol{x})$ and $\boldsymbol{B}(\boldsymbol{x})$ are defined as:
$$
\boldsymbol{A}(\boldsymbol{x}) = \sum_{I=1}^{N} w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) \boldsymbol{p}^T(\boldsymbol{x}_I)
$$
$$
\boldsymbol{B}(\boldsymbol{x}) \boldsymbol{d} = \sum_{I=1}^{N} w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) d_I
$$
The matrix $\boldsymbol{A}(\boldsymbol{x})$ is a symmetric $m \times m$ matrix commonly referred to as the **moment matrix** [@problem_id:2661992].

#### Conditions for a Well-Posed Approximation

For a unique solution for the coefficients $\boldsymbol{a}(\boldsymbol{x})$ to exist at a point $\boldsymbol{x}$, the moment matrix $\boldsymbol{A}(\boldsymbol{x})$ must be invertible. This is a critical condition for the MLS approximation to be well-defined. Since $\boldsymbol{A}(\boldsymbol{x})$ is a sum of symmetric, [positive semi-definite](@entry_id:262808) matrices, it is invertible if and only if it is positive definite. This holds if and only if the set of basis vectors evaluated at the nodes within the influence domain, $\{\boldsymbol{p}(\boldsymbol{x}_I) \mid w_I(\boldsymbol{x}) > 0\}$, spans the entire [polynomial space](@entry_id:269905) $\mathbb{R}^m$. Practically, this means two conditions must be met [@problem_id:2661998]:
1.  The number of nodes within the support of the weight functions at $\boldsymbol{x}$ must be at least $m$, the number of basis functions.
2.  The geometric arrangement of these nodes must be non-degenerate. For example, for a linear basis in 2D ($m=3$), the nodes cannot be collinear.

If $\boldsymbol{A}(\boldsymbol{x})$ is invertible, we can solve for $\boldsymbol{a}(\boldsymbol{x})$ and substitute it back into the expression for $u^h(\boldsymbol{x})$:
$$
u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) \sum_{I=1}^{N} w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) d_I
$$
By rearranging the summation, we can express the approximation in a form analogous to the Finite Element Method:
$$
u^h(\boldsymbol{x}) = \sum_{I=1}^{N} N_I(\boldsymbol{x}) d_I
$$
From this, we identify the MLS **shape function** $N_I(\boldsymbol{x})$ associated with node $I$ as [@problem_id:2661992]:
$$
N_I(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) w_I(\boldsymbol{x})
$$
These shape functions are not polynomials but are generally complex rational functions of $\boldsymbol{x}$, as both $\boldsymbol{A}^{-1}(\boldsymbol{x})$ and $w_I(\boldsymbol{x})$ depend on $\boldsymbol{x}$.

#### Polynomial Reproducibility

A key property of the MLS approximation, essential for ensuring the convergence of the numerical method, is its ability to exactly reproduce any polynomial field up to the degree of the basis. This property is known as **m-th [order completeness](@entry_id:160957)** or **[reproducibility](@entry_id:151299)**.

Let us assume the nodal data comes from an arbitrary polynomial $q(\boldsymbol{x})$ of degree at most $k$, where the basis $\boldsymbol{p}(\boldsymbol{x})$ is complete up to degree $k$. We can then write $q(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{c}_q$ for some constant coefficient vector $\boldsymbol{c}_q$. The nodal parameters would be $d_I = q(\boldsymbol{x}_I) = \boldsymbol{p}^T(\boldsymbol{x}_I) \boldsymbol{c}_q$. Substituting this into the expression for $u^h(\boldsymbol{x})$ yields:
$$
u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) \sum_{I=1}^{N} w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) (\boldsymbol{p}^T(\boldsymbol{x}_I) \boldsymbol{c}_q)
$$
Rearranging the terms within the summation:
$$
u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) \left( \sum_{I=1}^{N} w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) \boldsymbol{p}^T(\boldsymbol{x}_I) \right) \boldsymbol{c}_q
$$
The term in the parenthesis is precisely the definition of the moment matrix $\boldsymbol{A}(\boldsymbol{x})$. Therefore, provided $\boldsymbol{A}(\boldsymbol{x})$ is invertible, the expression simplifies beautifully [@problem_id:2661998]:
$$
u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) \boldsymbol{A}(\boldsymbol{x}) \boldsymbol{c}_q = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{c}_q = q(\boldsymbol{x})
$$
This demonstrates that the MLS approximation exactly reproduces the polynomial $q(\boldsymbol{x})$. This property holds if and only if the polynomial basis $\boldsymbol{p}(\boldsymbol{x})$ is complete up to degree $k$ and the moment matrix $\boldsymbol{A}(\boldsymbol{x})$ is invertible at the evaluation point $\boldsymbol{x}$.

### Practical Components of the MLS Approximation

The quality, stability, and computational cost of an MLS-based method depend critically on the choice of two components: the weight functions and their support size.

#### Weight Functions

The weight function $w_I(\boldsymbol{x})$ determines the influence of node $I$ on the approximation at point $\boldsymbol{x}$. For stability and locality, these functions must satisfy several properties. Typically, they are defined in terms of a normalized distance $q = \frac{\|\boldsymbol{x} - \boldsymbol{x}_I\|}{r_s}$, where $r_s$ is the **support radius**.
Key properties include:
-   **Compact Support:** $w(q) = 0$ for $q \ge 1$. This ensures that the approximation at $\boldsymbol{x}$ is purely local, depending only on nodes within a radius $r_s$.
-   **Non-negativity:** $w(q) \ge 0$.
-   **Monotonicity:** The function should be monotonically decreasing with distance.
-   **Smoothness:** The function should be sufficiently smooth (e.g., $C^1$ or $C^2$) to ensure the resulting shape functions are differentiable to the required order.

Commonly used compactly supported weight functions include [@problem_id:2661979]:
-   **Cubic Spline ($C^1$ continuous):** $w(q) = \begin{cases} \frac{2}{3} - 4q^2 + 4q^3 & 0 \le q \le \frac{1}{2} \\ \frac{4}{3} - 4q + 4q^2 - \frac{4}{3}q^3 & \frac{1}{2} < q \le 1 \end{cases}$
-   **Quartic Spline ($C^1$ continuous):** $w(q) = \begin{cases} 1 - 6q^2 + 8q^3 - 3q^4 & 0 \le q \le 1 \\ 0 & q > 1 \end{cases}$
-   **Truncated Gaussian:** $w(q) = \begin{cases} \frac{\exp(-(\alpha q)^2) - \exp(-\alpha^2)}{1 - \exp(-\alpha^2)} & 0 \le q \le 1 \\ 0 & q > 1 \end{cases}$, where $\alpha$ is a [shape parameter](@entry_id:141062).

#### The Support Domain and its Size

The support radius $r_s$ is typically defined relative to the local nodal spacing, $h$, via a dimensionless parameter $\beta$: $r_s = \beta h$. The choice of $\beta$ is one of the most critical decisions in a meshless simulation, as it governs a fundamental trade-off [@problem_id:2661990].

-   **Local Conditioning vs. Global Sparsity:**
    As $\beta$ increases, the support radius grows, encompassing more nodes. This has two primary effects. First, it makes the local moment matrix $\boldsymbol{A}(\boldsymbol{x})$ more robustly invertible and better conditioned, improving the quality of the local approximation. Second, it increases the overlap between [shape functions](@entry_id:141015), which in turn increases the number of non-zero entries in the global stiffness matrix. The number of non-zeros per row in the [stiffness matrix](@entry_id:178659) grows approximately as $\beta^2$ in 2D. Therefore, increasing $\beta$ improves [local stability](@entry_id:751408) at the cost of reduced global matrix sparsity and higher computational expense.

-   **Optimal Range:**
    There is no single "best" value for $\beta$. It must be large enough to ensure that, for any point $\boldsymbol{x}$ in the domain, its support contains a sufficient number of nodes ($>m$) in a non-degenerate configuration to guarantee the invertibility of $\boldsymbol{A}(\boldsymbol{x})$. Using a $\beta$ that is too small leads to ill-conditioning or singularity of $\boldsymbol{A}(\boldsymbol{x})$ and a loss of [polynomial reproduction](@entry_id:753580). Conversely, using a $\beta$ that is excessively large can lead to a different problem: the [shape functions](@entry_id:141015) of neighboring nodes become nearly identical, introducing [linear dependence](@entry_id:149638) into the global approximation basis and causing the *global* stiffness matrix to become severely ill-conditioned [@problem_id:2661990]. An optimal range for $\beta$ exists, which balances [local stability](@entry_id:751408) with global conditioning and computational cost. This range depends on the dimension of the problem and the order of the polynomial basis.

### Constructing the Discrete System: The Element-Free Galerkin (EFG) Method

The Element-Free Galerkin (EFG) method uses the MLS approximants within a standard Galerkin framework to solve the [weak form](@entry_id:137295) of a partial differential equation. We will illustrate this for small-strain linear elasticity. The weak form is: find the displacement $\boldsymbol{u}$ such that for all admissible test functions $\boldsymbol{v}$:
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}):\boldsymbol{\varepsilon}(\boldsymbol{v}) \, \mathrm{d}\Omega = \int_{\Omega} \boldsymbol{b}\cdot \boldsymbol{v}\, \mathrm{d}\Omega + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \boldsymbol{v}\, \mathrm{d}\Gamma
$$
The EFG method introduces the discrete trial and [test functions](@entry_id:166589), $\boldsymbol{u}_h = \sum_I \boldsymbol{N}_I \boldsymbol{d}_I$ and $\boldsymbol{v}_h = \sum_J \boldsymbol{N}_J \boldsymbol{\delta d}_J$, where $\boldsymbol{N}_I$ is a matrix of scalar MLS [shape functions](@entry_id:141015) and $\boldsymbol{d}_I$ are the nodal displacement parameters. This substitution leads to a linear system of equations $\boldsymbol{K}\boldsymbol{d} = \boldsymbol{f}$. However, three key challenges must be addressed that differentiate this process from a standard FEM implementation.

#### 1. Derivatives of Shape Functions

The stiffness matrix $\boldsymbol{K}$ involves integrals of products of the derivatives of [shape functions](@entry_id:141015). As we have seen, MLS shape functions are complex [rational functions](@entry_id:154279). Their derivatives must be computed carefully. Starting from the expression $N_I(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I)$, we can find the gradient $\nabla N_I(\boldsymbol{x})$ by systematically applying the [product rule](@entry_id:144424). This involves derivatives of the basis $\boldsymbol{p}(\boldsymbol{x})$, the weight $w_I(\boldsymbol{x})$, and the inverse of the moment matrix, $\boldsymbol{A}^{-1}(\boldsymbol{x})$. The derivative of the [matrix inverse](@entry_id:140380) is given by the identity $\frac{\partial \boldsymbol{A}^{-1}}{\partial x} = -\boldsymbol{A}^{-1} \frac{\partial \boldsymbol{A}}{\partial x} \boldsymbol{A}^{-1}$.

A more numerically stable approach avoids computing the derivative of $\boldsymbol{A}^{-1}$ explicitly. Instead, one can differentiate the [normal equations](@entry_id:142238) directly. Let $\boldsymbol{a}_I(\boldsymbol{x})$ be the coefficient vector for a field where only node $I$ has a unit displacement ($d_I=1$, $d_J=0$ for $J \ne I$). Then $N_I(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x})\boldsymbol{a}_I(\boldsymbol{x})$, and $\boldsymbol{a}_I(\boldsymbol{x})$ satisfies $\boldsymbol{A}(\boldsymbol{x})\boldsymbol{a}_I(\boldsymbol{x}) = w_I(\boldsymbol{x})\boldsymbol{p}(\boldsymbol{x}_I)$. Differentiating this identity with respect to a coordinate provides a linear system for the derivatives of $\boldsymbol{a}_I(\boldsymbol{x})$, which can be solved and substituted into the derivative of $N_I(\boldsymbol{x})$ [@problem_id:2662041]. Once the gradients are computed, they are assembled into the strain-displacement matrices $\mathcal{B}_I$ that are used to build the stiffness matrix components $K_{IJ} = \int_{\Omega} \mathcal{B}_I^T \mathbb{C} \mathcal{B}_J \, d\Omega$ [@problem_id:2662007].

#### 2. Numerical Integration

In FEM, the integrand of the stiffness matrix is typically a polynomial on each element, allowing for exact evaluation using Gaussian quadrature. In EFG, the integrand $N_I'(\boldsymbol{x}) N_J'(\boldsymbol{x})$ is a complicated rational function. No standard [quadrature rule](@entry_id:175061) can integrate this function exactly. This introduces an unavoidable **[consistency error](@entry_id:747725)** due to numerical integration [@problem_id:2661961].

To manage this error, EFG methods perform numerical quadrature over a **background integration mesh** (or grid of background cells) that is laid over the domain, independent of the node placement [@problem_id:2661988]. The global integral is broken into a sum of integrals over these cells, and a high-order Gaussian quadrature is applied within each cell. The accuracy of the EFG solution is thus intrinsically linked to the fineness of this background mesh. If the integration is not sufficiently accurate (i.e., the mesh is too coarse or the quadrature order too low), a form of **under-integration** occurs, which can lead to instabilities. For instance, if a one-dimensional problem is integrated with a composite [midpoint rule](@entry_id:177487) over cells of size $h$, the leading-order [consistency error](@entry_id:747725) in the bilinear form is proportional to $h^2$ (as the local error is $O(h^3)$) and the second derivative of the integrand, highlighting the dependence on both the integration scheme and the smoothness of the underlying solution [@problem_id:2661961].

#### 3. Imposition of Essential Boundary Conditions

Perhaps the most significant departure from FEM practice lies in the imposition of essential (Dirichlet) boundary conditions. In FEM, [shape functions](@entry_id:141015) possess the **Kronecker delta property**, $N_I(\boldsymbol{x}_J) = \delta_{IJ}$. This means the nodal parameter $d_J$ is the actual physical displacement at node $J$, i.e., $u^h(\boldsymbol{x}_J) = d_J$. Imposing a condition $u(\boldsymbol{x}_J) = \bar{u}$ is as simple as setting the corresponding degree of freedom $d_J = \bar{u}$.

Standard MLS [shape functions](@entry_id:141015) are **non-interpolatory**; they do not satisfy the Kronecker delta property, so $N_I(\boldsymbol{x}_J) \neq \delta_{IJ}$ [@problem_id:2661988]. The nodal parameter $d_I$ is an abstract coefficient and is *not* the physical displacement at node $I$. The value of the approximation at a node is a weighted average of the parameters of neighboring nodes: $u^h(\boldsymbol{x}_J) = \sum_I N_I(\boldsymbol{x}_J) d_I$.

Consequently, simply setting $d_J = \bar{u}$ for a boundary node $J$ does not enforce the condition $u^h(\boldsymbol{x}_J) = \bar{u}$. This direct approach, known as strong imposition, fails and constitutes a "[variational crime](@entry_id:178318)" because the trial function does not belong to the correct [function space](@entry_id:136890). This leads to an inconsistent formulation and a loss of convergence [@problem_id:2662039].

To correctly enforce [essential boundary conditions](@entry_id:173524), one must use a **weak enforcement** method. Common techniques include:
-   **Penalty Method:** A penalty term is added to the [weak form](@entry_id:137295), which penalizes the deviation from the prescribed boundary value. The augmented [weak form](@entry_id:137295) includes a term like $\int_{\Gamma_u} \alpha (u_h - \bar{u}) \cdot v_h \, d\Gamma$, where $\alpha$ is a large penalty parameter. This adds a contribution to both the stiffness matrix and the force vector [@problem_id:2662007].
-   **Lagrange Multipliers:** The boundary condition is enforced exactly by introducing Lagrange multiplier fields on the boundary, which act as reaction forces. This increases the size of the linear system.
-   **Nitsche's Method:** This is a penalty-like method that is consistent and does not require the [penalty parameter](@entry_id:753318) to be excessively large.

These methods are essential for a correct and convergent EFG implementation [@problem_id:2661988], [@problem_id:2662039].

### Stability of Meshless Methods

While powerful, meshless methods are susceptible to several forms of [numerical instability](@entry_id:137058) that must be understood and controlled for reliable simulations. These issues stem from the very choices that define the method: the node distribution, the support size, and the integration scheme [@problem_id:2661967].

#### Local Instability: Rank Deficiency in MLS

As discussed, the MLS approximation itself can be unstable at a point $\boldsymbol{x}$ if the moment matrix $\boldsymbol{A}(\boldsymbol{x})$ is singular or ill-conditioned. This **[rank deficiency](@entry_id:754065)** can occur if the support domain does not contain enough nodes or if the nodes are in a degenerate configuration. This is a local issue that can compromise the accuracy and convergence of the entire method. A practical diagnostic is to monitor the rank and condition number of $\boldsymbol{A}(\boldsymbol{x})$ at all quadrature points during the assembly process. Large condition numbers signal a potential problem that might be fixed by adjusting node placement or increasing the support size [@problem_id:2661967].

#### Global Instability: Spurious Zero-Energy Modes

A more insidious problem is the appearance of **[spurious zero-energy modes](@entry_id:755267)**, often called **[hourglass modes](@entry_id:174855)**. These are non-physical deformation patterns of the nodal cloud that produce zero (or near-zero) strain energy. Consequently, the global stiffness matrix $\boldsymbol{K}$ offers no resistance to these modes, allowing them to grow uncontrollably and contaminate the solution. Such modes are often a consequence of under-integration, where the [quadrature rule](@entry_id:175061) is too coarse to "see" the strain associated with these high-frequency oscillations. While nodal integration is particularly prone to this, even background cell integration can suffer if not sufficiently accurate.

The definitive way to detect these instabilities is to perform an **[eigenvalue analysis](@entry_id:273168)** of the [global stiffness matrix](@entry_id:138630) $\boldsymbol{K}$ (after accounting for [rigid body motion](@entry_id:144691)). The nullspace of $\boldsymbol{K}$ should only contain the physical rigid-body modes. Any additional zero or near-zero eigenvalues correspond to [spurious zero-energy modes](@entry_id:755267) [@problem_id:2661967].

#### Other Instabilities and Diagnostics

-   **Tensile Instability:** In some meshless formulations, particularly those for fracture or [large deformation](@entry_id:164402), the stiffness matrix may develop negative eigenvalues, leading to an instability where the material appears to have negative stiffness under tension. This can be diagnosed in an explicit dynamic simulation by monitoring the total system energy. For a [conservative system](@entry_id:165522), energy should be conserved; a systematic growth in energy, even with a stable time integrator, points to a spatial instability like this [@problem_id:2661967].
-   **Instability in Mixed Formulations:** When solving problems involving constraints like incompressibility, [mixed formulations](@entry_id:167436) (e.g., displacement-pressure) are often used. These require compatibility between the discrete displacement and pressure spaces, mathematically expressed by the **Ladyzhenskaya–Babuška–Brezzi (LBB)** or **inf-sup** condition. If the chosen meshless approximation spaces violate this condition, spurious pressure oscillations ([checkerboarding](@entry_id:747311)) can occur. This can be diagnosed by computing the singular values of the discrete [divergence operator](@entry_id:265975) that links the two fields; an inf-sup constant that tends to zero with refinement indicates instability [@problem_id:2661967].

In summary, the principles of meshless methods offer a compelling alternative to traditional mesh-based techniques, particularly for problems involving large deformations, moving boundaries, or fracture. However, this flexibility comes with a set of unique theoretical and practical challenges related to approximation, integration, boundary conditions, and stability, which must be carefully managed to achieve accurate and robust numerical solutions.