## Introduction
In the realm of computational mechanics, the quest for numerical methods that can accurately and efficiently model complex physical phenomena is ongoing. While the Finite Element Method (FEM) has been the cornerstone of engineering simulation for decades, its reliance on a predefined mesh creates significant bottlenecks when dealing with problems involving [large deformations](@entry_id:167243), evolving discontinuities like cracks, or intricate geometries. The Element-Free Galerkin (EFG) method emerges as a powerful alternative, belonging to a class of [meshfree methods](@entry_id:177458) designed to overcome these very limitations. This article provides a comprehensive exploration of the EFG method, bridging theory with practical application. The first chapter, **Principles and Mechanisms**, will dissect the mathematical core of EFG, focusing on the Moving Least Squares approximation and its consequences. Following this, the **Applications and Interdisciplinary Connections** chapter will showcase the method's utility in fields from [fracture mechanics](@entry_id:141480) to biomechanics. Finally, the **Hands-On Practices** section will guide you through implementing key aspects of the method. We begin by examining the foundational principles that distinguish EFG from its mesh-based counterparts.

## Principles and Mechanisms

The Element-Free Galerkin (EFG) method represents a significant departure from the mesh-based structure of the Finite Element Method (FEM). While it retains the robust variational framework of a Galerkin method, it liberates the approximation of the solution field from the constraints of a predefined element mesh. This chapter delves into the fundamental principles and mathematical mechanisms that underpin the EFG method, from the construction of its unique shape functions to the practical challenges of numerical implementation and their sophisticated solutions.

### The Core Idea: A Galerkin Method Without a Mesh

At its heart, the EFG method is a **Galerkin method**. This means it seeks an approximate solution to a [boundary value problem](@entry_id:138753) by working with its **[weak form](@entry_id:137295)**, or [variational formulation](@entry_id:166033), rather than its strong form (the original partial differential equation). To illustrate, consider a generic scalar diffusion problem governed by the equation $-\nabla \cdot (k \nabla u) = f$ in a domain $\Omega$, with appropriate boundary conditions. The [weak form](@entry_id:137295) is derived by multiplying the equation by a [test function](@entry_id:178872) $v$ and integrating over the domain. Applying the divergence theorem (integration by parts) leads to a statement of the form: find a trial solution $u$ such that for all admissible test functions $v$, the following integral equation holds:

$$
\int_{\Omega} k \nabla v \cdot \nabla u \, d\Omega = \int_{\Omega} v f \, d\Omega + \int_{\Gamma_{N}} v \bar{t} \, dS
$$

where the right-hand side incorporates the source term $f$ and any [natural boundary conditions](@entry_id:175664) involving the flux $\bar{t}$ . In a standard Galerkin procedure, we discretize this equation by representing the unknown solution $u$ as a [linear combination](@entry_id:155091) of basis functions, often called **shape functions**, $\phi_I$:

$$
u(\mathbf{x}) \approx u^h(\mathbf{x}) = \sum_{I} \phi_I(\mathbf{x}) d_I
$$

Here, the $d_I$ are unknown coefficients, or nodal parameters, associated with a set of points, or **nodes**, scattered throughout the domain. Substituting this approximation into the weak form yields a system of linear algebraic equations that can be solved for the coefficients $d_I$.

The defining characteristic of EFG, and [meshfree methods](@entry_id:177458) in general, is how these [shape functions](@entry_id:141015) $\phi_I(\mathbf{x})$ are constructed. In FEM, the [shape functions](@entry_id:141015) are [piecewise polynomials](@entry_id:634113) defined on a mesh of elements, and their value at a point depends only on the nodes of the element containing that point. In EFG, there are no elements. The shape functions are constructed "on the fly" at any evaluation point $\mathbf{x}$ using a local cloud of nodes, without any predefined element connectivity. This requires a new mathematical engine for building the approximation, which is the **Moving Least Squares** (MLS) method .

### The Heart of the Approximation: Moving Least Squares (MLS)

The Moving Least Squares method is a powerful technique for constructing a continuous and smooth approximation of a function from a set of scattered data points. It is the cornerstone of the EFG method's approximation space.

#### The MLS Concept

The intuition behind MLS is to perform a weighted [least-squares regression](@entry_id:262382) locally at every point in the domain. For any given evaluation point $\mathbf{x}$, we seek a polynomial that best fits the nodal parameter values $d_I$ at the nodes $\mathbf{x}_I$ in the vicinity of $\mathbf{x}$. The "nearness" of a node is determined by a **weight function** that decays with distance from $\mathbf{x}$. Because this fitting procedure is repeated for each evaluation point, the resulting best-fit polynomial "moves" throughout the domain, giving the method its name. The value of the EFG approximation $u^h(\mathbf{x})$ is then defined as the value of this locally fitted polynomial evaluated at $\mathbf{x}$.

#### Formal Derivation of MLS Shape Functions

Let us formalize this procedure. At an evaluation point $\mathbf{x}$, we express the local approximation, which we denote $u_{loc}(\mathbf{y})$, as a [linear combination](@entry_id:155091) of polynomial basis functions $p_j(\mathbf{y})$. For a linear basis in two dimensions, for instance, the [basis vector](@entry_id:199546) would be $p(\mathbf{y}) = \begin{pmatrix} 1 & y_1 & y_2 \end{pmatrix}^T$. The local approximation is then written as:

$$
u_{loc}(\mathbf{y}) = p^T(\mathbf{y}) a(\mathbf{x})
$$

The coefficient vector $a(\mathbf{x})$ depends on the evaluation point $\mathbf{x}$ because it is determined by a least-squares fit that is centered at $\mathbf{x}$. Specifically, we find $a(\mathbf{x})$ by minimizing a weighted, discrete $L_2$ norm of the errors between the local polynomial and the nodal parameters $d_I$ at the surrounding nodal locations $\mathbf{x}_I$:

$$
J(\mathbf{a}, \mathbf{x}) = \sum_{I=1}^{N} w(\mathbf{x} - \mathbf{x}_I) \left( p^T(\mathbf{x}_I) a(\mathbf{x}) - d_I \right)^2
$$

Here, $w(\mathbf{x} - \mathbf{x}_I)$ is a weight function that depends on the distance between the evaluation point $\mathbf{x}$ and the node $\mathbf{x}_I$. To find the coefficients $a(\mathbf{x})$ that minimize $J$, we set its derivative with respect to each component of $a$ to zero, $\frac{\partial J}{\partial a} = \mathbf{0}$. This yields the so-called **[normal equations](@entry_id:142238)** of the weighted [least-squares problem](@entry_id:164198) :

$$
A(\mathbf{x}) a(\mathbf{x}) = B(\mathbf{x}) \mathbf{d}
$$

where $\mathbf{d}$ is the vector of all nodal parameters. The matrices $A(\mathbf{x})$ and $B(\mathbf{x})$ are defined as:

$$
A(\mathbf{x}) = \sum_{J=1}^{N} w(\mathbf{x} - \mathbf{x}_J) p(\mathbf{x}_J) p^T(\mathbf{x}_J)
$$

$$
B(\mathbf{x}) = \begin{bmatrix} w(\mathbf{x}-\mathbf{x}_1) p(\mathbf{x}_1) & w(\mathbf{x}-\mathbf{x}_2) p(\mathbf{x}_2) & \cdots & w(\mathbf{x}-\mathbf{x}_N) p(\mathbf{x}_N) \end{bmatrix}
$$

The matrix $A(\mathbf{x})$ is often called the **moment matrix**. Assuming $A(\mathbf{x})$ is invertible (which requires a sufficient number of nodes to be within the influence of the weight function), we can solve for the coefficients:

$$
a(\mathbf{x}) = A(\mathbf{x})^{-1} B(\mathbf{x}) \mathbf{d}
$$

The EFG approximation at $\mathbf{x}$, denoted $u^h(\mathbf{x})$, is defined as the value of this local polynomial at that point, i.e., $u^h(\mathbf{x}) = p^T(\mathbf{x}) a(\mathbf{x})$. Substituting the expression for $a(\mathbf{x})$ gives:

$$
u^h(\mathbf{x}) = p^T(\mathbf{x}) A(\mathbf{x})^{-1} B(\mathbf{x}) \mathbf{d} = \sum_{I=1}^{N} \left[ p^T(\mathbf{x}) A(\mathbf{x})^{-1} w(\mathbf{x} - \mathbf{x}_I) p(\mathbf{x}_I) \right] d_I
$$

By comparing this to the standard form $u^h(\mathbf{x}) = \sum_I \phi_I(\mathbf{x}) d_I$, we can identify the [closed-form expression](@entry_id:267458) for the MLS shape function associated with node $I$:

$$
\phi_I(\mathbf{x}) = p^T(\mathbf{x}) \left( \sum_{J=1}^{N} w(\mathbf{x} - \mathbf{x}_J) p(\mathbf{x}_J) p^T(\mathbf{x}_J) \right)^{-1} w(\mathbf{x} - \mathbf{x}_I) p(\mathbf{x}_I)
$$

This expression reveals the complex, rational nature of the [shape functions](@entry_id:141015). They depend not only on the position of node $I$ but on the positions of all nodes $J$ that are within the "[domain of influence](@entry_id:175298)" defined by the weight function centered at $\mathbf{x}$.

#### A Concrete Example

The abstract formula for the [shape functions](@entry_id:141015) can be made clear with a simple one-dimensional example. Consider three nodes at $x_1=0$, $x_2=1$, and $x_3=2$, and let us use a linear polynomial basis $p(x) = \begin{pmatrix} 1 & x \end{pmatrix}^T$ and a Gaussian-type weight function $w(r) = \exp(-r^2/\sigma^2)$. Following the derivation above, one can construct the $2 \times 2$ moment matrix $A(x)$, invert it, and perform the matrix-vector multiplications. This yields a specific, albeit complex, expression for each shape function. For instance, the shape function for the middle node, $\phi_2(x)$, can be shown through algebraic manipulation to be :

$$
\phi_2(x) = \frac{x w_1(x)w_2(x) + (2-x)w_2(x)w_3(x)}{w_1(x)w_2(x) + 4w_1(x)w_3(x) + w_2(x)w_3(x)}
$$

where $w_I(x) = \exp(-(x-x_I)^2/\sigma^2)$. Interestingly, in the specific case of two nodes in 1D at $x_1=0$ and $x_2=1$ with a linear basis and uniform weights ($w_I(x)=1$), the MLS shape functions simplify exactly to the standard linear finite [element shape functions](@entry_id:198891): $\phi_1(x) = 1-x$ and $\phi_2(x) = x$ . This shows that FEM can be viewed as a special case of the more general MLS approximation framework.

### Properties and Implications of MLS Shape Functions

The unique construction of MLS shape functions endows them with several important properties that have profound implications for the accuracy and implementation of the EFG method.

#### Completeness and Accuracy

The most important property of MLS [shape functions](@entry_id:141015) is their ability to exactly reproduce the polynomial basis used in their construction. This property is known as **m-th [order completeness](@entry_id:160957)** or [polynomial reproduction](@entry_id:753580). If the MLS fit uses a basis $\mathcal{P}_m$ containing all polynomials up to total degree $m$, then for any polynomial $p(\mathbf{x}) \in \mathcal{P}_m$, the approximation exactly recovers it from its nodal samples :

$$
\sum_{I=1}^{N} \phi_I(\mathbf{x}) p(\mathbf{x}_I) = p(\mathbf{x})
$$

This is a direct and powerful consequence of the [least-squares](@entry_id:173916) fitting procedure. A trivial but important case is $m=0$, where the basis is just the constant $1$. In this case, completeness implies $\sum_I \phi_I(\mathbf{x}) = 1$, a property known as **[partition of unity](@entry_id:141893)**.

Completeness is not just an abstract mathematical property; it is the foundation of the method's accuracy. Approximation theory, via tools like the Bramble-Hilbert lemma, guarantees that an [approximation scheme](@entry_id:267451) with $m$-th [order completeness](@entry_id:160957) will achieve an optimal convergence rate. For a sufficiently smooth solution to an elliptic problem, the error in the [energy norm](@entry_id:274966) (e.g., the $H^1$ Sobolev norm) is of order $O(h^m)$, and the error in the $L^2$ norm is of order $O(h^{m+1})$, where $h$ is a measure of the nodal spacing . This means that by using a higher-order polynomial basis (e.g., quadratic, $m=2$), we can achieve much faster convergence as the node density increases. Furthermore, if the exact solution happens to be a polynomial of degree less than or equal to $m$, the EFG solution will be exact, apart from errors introduced by numerical integration and boundary condition enforcement. This property is known as **Galerkin [exactness](@entry_id:268999)** .

#### The Kronecker Delta Problem and Boundary Conditions

While powerful, MLS [shape functions](@entry_id:141015) have a characteristic that poses a significant practical challenge. Unlike standard FEM [shape functions](@entry_id:141015), they are generally not interpolatory. This means that the shape function $\phi_I$ evaluated at a nodal location $\mathbf{x}_J$ is not equal to one if $I=J$ and zero otherwise. That is, MLS [shape functions](@entry_id:141015) **do not satisfy the Kronecker delta property**:

$$
\phi_I(\mathbf{x}_J) \neq \delta_{IJ}
$$

This is because the value of the approximation at a node, $u^h(\mathbf{x}_J) = \sum_I \phi_I(\mathbf{x}_J) d_I$, is a weighted average of the parameters of all nodes within its local neighborhood, not simply the parameter $d_J$ .

This property has a critical consequence for the imposition of **[essential boundary conditions](@entry_id:173524)** (e.g., prescribed displacements in solid mechanics). In FEM, one can simply set the nodal parameter $d_J$ of a boundary node $\mathbf{x}_J$ to the prescribed value $\bar{u}$. In EFG, this direct approach fails because setting $d_J=\bar{u}$ does not guarantee that the solution itself will equal $\bar{u}$ at that point.

To overcome this, a variety of techniques must be employed to enforce [essential boundary conditions](@entry_id:173524) in a "weak" sense within the Galerkin framework. Common methods include the use of **Lagrange multipliers**, the **[penalty method](@entry_id:143559)**, or **Nitsche's method**. Each of these methods modifies the weak form to enforce the boundary constraint, but they add complexity to the system of equations. It is worth noting that special variants, such as **Interpolating MLS** (which use singular weight functions), can be designed to satisfy the Kronecker delta property, but this often comes at the cost of reduced smoothness or poorer [numerical conditioning](@entry_id:136760) .

#### Choice of Weight Function

The weight function $w(\mathbf{x} - \mathbf{x}_I)$ is a crucial ingredient in the MLS approximation. It defines the size and shape of the local [domain of influence](@entry_id:175298) for each evaluation point. Typically, these are radially [symmetric functions](@entry_id:149756) with **[compact support](@entry_id:276214)**, meaning they are non-zero only within a certain radius $\rho$ of their center and zero everywhere else .

The choice of weight function affects both the quality of the approximation and the computational cost. Key considerations include:
*   **Smoothness**: The [differentiability](@entry_id:140863) of the MLS shape functions $\phi_I(\mathbf{x})$ is directly inherited from the [differentiability](@entry_id:140863) of the weight function $w$ (provided the set of neighboring nodes does not change). For solving second-order PDEs, the shape functions must be at least $C^1$, requiring the weight function to be at least $C^1$. Polynomial [spline](@entry_id:636691) weight functions are often designed to be $C^2$ or higher at their support boundary to ensure smooth derivatives everywhere. In contrast, a simple "truncated Gaussian" weight function is only $C^0$ continuous at its boundary and can introduce kinks in the shape function derivatives .
*   **Support Size**: The support radius $\rho$ determines how many nodes influence the approximation at a given point. A larger support leads to a smoother approximation but increases the computational cost, as the number of neighbors involved in the MLS fit at each point scales with $\rho^d$ in $d$ dimensions.
*   **Computational Cost**: The cost of evaluating the weight function itself matters. Low-order polynomials (e.g., cubic or quartic [splines](@entry_id:143749)) are computationally cheaper to evaluate than functions involving exponentials, like the Gaussian weight .

### The "Galerkin" in EFG: Numerical Integration

Having constructed the [shape functions](@entry_id:141015), we must return to the Galerkin [weak form](@entry_id:137295) and evaluate the necessary integrals to assemble the final [system matrix](@entry_id:172230) (e.g., the [stiffness matrix](@entry_id:178659)).

#### The Need for a Background Grid

The stiffness matrix entries typically involve integrals of products of shape function derivatives, such as $K_{IJ} = \int_{\Omega} \nabla \phi_I \cdot \nabla \phi_J \, d\Omega$. Since the shape functions $\phi_I$ are complex [rational functions](@entry_id:154279), these integrands are far too complicated for analytical integration. Therefore, numerical integration, or **quadrature**, is essential.

Because EFG has no inherent element structure, there is no natural grid on which to perform this quadrature. The solution is to introduce an independent **background integration grid** that covers the entire domain $\Omega$. This grid, typically composed of simple shapes like quadrilaterals or triangles, serves only as a framework for numerical integration and is completely decoupled from the set of nodes used for the MLS approximation. Standard [quadrature rules](@entry_id:753909), such as **Gaussian quadrature**, are then applied within each cell of this background grid [@problem_id:3754011, @problem_id:2576510]. This decoupling of the approximation nodes from the integration mesh is a key feature and a source of great flexibility in EFG.

#### Quadrature Accuracy and the Patch Test

The numerical integration must be performed with sufficient accuracy to avoid corrupting the solution and losing the convergence rates promised by the completeness of the MLS [shape functions](@entry_id:141015). The guiding principle for selecting a [quadrature rule](@entry_id:175061) is the **Patch Test**. Passing the patch test ensures that the numerical method can exactly reproduce a polynomial solution of a certain degree, which is a [necessary condition for convergence](@entry_id:157681).

For a linear elliptic problem and an MLS approximation with $p$-th [order completeness](@entry_id:160957), a [sufficient condition](@entry_id:276242) to pass the patch test is that the [quadrature rule](@entry_id:175061) used to compute the stiffness matrix must be able to integrate any polynomial of degree up to $2p-2$ exactly . For example:
*   For a **linear basis** ($p=1$), the rule must be exact for polynomials of degree $2(1)-2=0$. A single-point Gauss rule is sufficient.
*   For a **quadratic basis** ($p=2$), the rule must be exact for polynomials of degree $2(2)-2=2$. This requires a $2 \times 2$ Gauss rule on quadrilateral cells or a 3-point rule on triangular cells.

Using a rule with lower order can lead to instability and loss of accuracy, while using a much higher order (over-integration) unnecessarily increases computational cost.

### Advanced Topics and Challenges

While the principles outlined above form the basis of EFG, several advanced topics and challenges arise in its practical application, leading to the development of sophisticated solutions.

#### Stabilized Nodal Integration

While the background grid approach is robust, it is also computationally expensive, as it requires evaluating the complex MLS [shape functions](@entry_id:141015) at every quadrature point within every cell. A much faster alternative would be **Direct Nodal Integration** (DNI), where the domain integral is approximated by a simple weighted sum of the integrand evaluated only at the nodes.

Unfortunately, naive DNI leads to severe numerical instability. The stiffness matrix becomes **rank-deficient**, admitting non-physical, zero-energy deformation modes known as **[spurious modes](@entry_id:163321)**. This occurs because DNI only samples the strain energy at the nodes. It is possible to have a deformation mode where the strain is zero *at every node* but non-zero in the regions between the nodes. DNI completely misses the energy of such a mode, leading to an unstable system .

To overcome this, methods like **Stabilized Conforming Nodal Integration (SCNI)** have been developed. SCNI consists of two main ideas:
1.  **Gradient Smoothing**: The pointwise gradient of the shape function, $\nabla N_a(\mathbf{x}_i)$, is replaced by a "smoothed" gradient, $\nabla \bar{N}_a(\mathbf{x}_i)$, defined as the average gradient over a nodal cell (e.g., a Voronoi cell). Using the divergence theorem, this can be computed as a boundary integral over the cell, which ensures consistency and helps pass the patch test.
2.  **Stabilization**: The [stiffness matrix](@entry_id:178659) built from smoothed gradients alone can still be too "soft". To restore full stability, a stabilization term is added. This term is designed to penalize the difference between the original local gradient and the smoothed gradient. This gives a non-zero energy to the [spurious modes](@entry_id:163321), effectively removing them from the solution while preserving the accuracy for physically correct modes .

#### Handling Complex Geometries

One of the great promises of [meshfree methods](@entry_id:177458) is their ability to handle complex geometries and evolving discontinuities, such as growing cracks, without the need for cumbersome remeshing. However, these situations also present unique challenges.

When an evaluation point $\mathbf{x}$ is near a concave boundary or the edge of a void, its circular [domain of influence](@entry_id:175298) will be truncated. The set of "visible" nodes within its support becomes geometrically biased, lying within a wedge-shaped region. This can cause the moment matrix $A(\mathbf{x})$ to become ill-conditioned or even singular, because the nodal positions no longer provide sufficient information in all directions. When the moment matrix fails, the MLS reproducing conditions break down, and the local approximation quality is lost .

Advanced EFG formulations address this by incorporating **visibility criteria**. Before constructing the MLS approximation, a ray-tracing or similar check is performed to determine which neighboring nodes are "visible" from the evaluation point without being occluded by a boundary. Then, to counteract the geometric bias of the remaining visible nodes, **moment correction** techniques are employed. These methods modify the weights with an affine correction term, whose coefficients are calculated to enforce certain properties on the moment matrix—for instance, forcing its first-moment terms to be zero. This restores the well-posedness of the local MLS problem and allows for accurate modeling even in the presence of complex geometric features, making EFG a powerful tool for applications like fracture mechanics .