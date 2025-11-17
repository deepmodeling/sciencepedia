## Introduction
In the Finite Element Method (FEM), the choice of basis functions is a critical decision that dictates the accuracy and efficiency of a numerical model. While standard Lagrange polynomials are widely used, they present computational inefficiencies for adaptive analyses, where the polynomial degree is increased locally to improve solution accuracy—a process known as [p-refinement](@entry_id:173797). This approach often requires recalculating the entire [element stiffness matrix](@entry_id:139369). This article addresses this gap by introducing a more elegant and powerful alternative: the 1D quadratic [bar element](@entry_id:746680) formulated with [hierarchical shape functions](@entry_id:169076).

This article provides a comprehensive guide to this advanced FEM technique. In the first section, **Principles and Mechanisms**, we will delve into the theoretical construction of [hierarchical shape functions](@entry_id:169076), derive the corresponding [element stiffness matrix](@entry_id:139369), and uncover the powerful property of energetic orthogonality. Following this, the **Applications and Interdisciplinary Connections** section will demonstrate the practical utility of this formulation in [static condensation](@entry_id:176722), p-adaptive refinement, and modeling complex physical phenomena in fields like [thermo-mechanics](@entry_id:172368) and materials science. Finally, a series of **Hands-On Practices** are outlined to provide a structured path for applying these concepts and solidifying your understanding.

## Principles and Mechanisms

In the study of the Finite Element Method, the selection of basis functions is a foundational choice that profoundly influences the accuracy, efficiency, and flexibility of the analysis. While the family of standard Lagrange polynomials provides a straightforward, interpolatory basis, it is not always the most efficient choice, particularly for adaptive analyses where the polynomial degree of elements is locally increased—a strategy known as **[p-refinement](@entry_id:173797)**. This chapter introduces an alternative and powerful approach: the construction of **hierarchical basis functions** for a one-dimensional quadratic [bar element](@entry_id:746680). These bases are designed to be nested, meaning that the set of basis functions for a lower-order [polynomial space](@entry_id:269905) is a true subset of the basis for any higher-order space. This property offers significant computational advantages, particularly in the context of [error estimation](@entry_id:141578) and adaptive modeling.

### The Hierarchical Construction of Shape Functions

We begin by considering the one-dimensional [reference element](@entry_id:168425), defined over the domain $\xi \in [-1, 1]$. For a standard linear ($p=1$) element, the approximation of a field variable, such as displacement $u_h(\xi)$, is constructed using two linear [shape functions](@entry_id:141015), $N_1(\xi)$ and $N_2(\xi)$:

$N_1(\xi) = \frac{1-\xi}{2}$

$N_2(\xi) = \frac{1+\xi}{2}$

These are the familiar linear Lagrange polynomials associated with the nodes at $\xi_1 = -1$ and $\xi_2 = 1$, respectively. They possess the **Kronecker-delta property**, $N_i(\xi_j) = \delta_{ij}$, which ensures that the degrees of freedom, $d_1$ and $d_2$, are precisely the values of the field at the nodes: $u_h(-1) = d_1$ and $u_h(1) = d_2$.

To elevate this approximation from linear to quadratic ($p=2$) in a hierarchical manner, we do not discard the linear basis. Instead, we augment it with a new function that introduces the required quadratic behavior. This additional function, which we will denote $N_b(\xi)$, must be a quadratic polynomial. The complete [quadratic approximation](@entry_id:270629) is then written as:

$u_h(\xi) = d_1 N_1(\xi) + d_2 N_2(\xi) + a_b N_b(\xi)$

Here, $a_b$ is the new degree of freedom associated with the quadratic mode. A critical requirement of the hierarchical framework is that the introduction of higher-order terms must not corrupt the physical meaning of the existing, lower-order degrees of freedom. In our case, $d_1$ and $d_2$ must remain the nodal values of the *quadratic* field $u_h(\xi)$ [@problem_id:2538605]. Let us enforce this condition by evaluating the approximation at the nodes:

At $\xi = -1$:
$u_h(-1) = d_1 N_1(-1) + d_2 N_2(-1) + a_b N_b(-1)$
Using the Kronecker-delta property of the linear functions, $N_1(-1)=1$ and $N_2(-1)=0$. This simplifies to:
$u_h(-1) = d_1(1) + d_2(0) + a_b N_b(-1) = d_1 + a_b N_b(-1)$

For $u_h(-1)$ to equal $d_1$ for any possible value of the new degree of freedom $a_b$, it is necessary that $N_b(-1) = 0$.

Similarly, at $\xi = 1$:
$u_h(1) = d_1 N_1(1) + d_2 N_2(1) + a_b N_b(1)$
With $N_1(1)=0$ and $N_2(1)=1$, this becomes:
$u_h(1) = d_1(0) + d_2(1) + a_b N_b(1) = d_2 + a_b N_b(1)$

For $u_h(1)$ to equal $d_2$, it is necessary that $N_b(1) = 0$.

This reveals the fundamental principle for internal hierarchical modes: they must vanish at the nodes of the lower-order element they enrich [@problem_id:2538579]. Because these functions are zero at the boundaries and typically have a non-zero profile in the interior, they are often referred to as **[bubble functions](@entry_id:176111)**.

To construct a suitable quadratic [bubble function](@entry_id:179039), we seek a quadratic polynomial with roots at $\xi = -1$ and $\xi = 1$. Any such polynomial must be of the form $C(\xi-1)(\xi+1) = C(\xi^2 - 1)$ for some non-zero constant $C$. The choice of $C$ is a matter of normalization. A common and convenient choice is $C=-1$, which yields:

$N_b(\xi) = 1 - \xi^2$

This specific function has the appealing property that its value at the element center is unity, i.e., $N_b(0) = 1$ [@problem_id:2538529]. Other normalizations are possible; for instance, the constant could be chosen to normalize the function's "energy" with respect to the linear modes [@problem_id:2538563]. For the remainder of this chapter, we will adopt $N_b(\xi) = 1 - \xi^2$ as our representative [bubble function](@entry_id:179039), and denote the full basis as $\phi_1=N_1, \phi_2=N_2, \phi_3=N_b$.

### Nodal vs. Modal Degrees of Freedom

With the hierarchical basis established, it is crucial to understand the distinct physical interpretations of the degrees of freedom. While $d_1$ and $d_2$ are **nodal** degrees of freedom representing the field's value at specific points in space, the coefficient $a_b$ is a **modal** degree of freedom that represents the amplitude of a particular shape, or mode, of deformation.

The coefficient $a_b$ does not correspond to the field value at any single point. To see this, let's evaluate the displacement at the element center, $\xi=0$, using our chosen normalization ($N_b(0)=1$):

$u_h(0) = d_1 N_1(0) + d_2 N_2(0) + a_b N_b(0) = d_1(\frac{1}{2}) + d_2(\frac{1}{2}) + a_b(1) = \frac{d_1 + d_2}{2} + a_b$

Rearranging this expression gives us the physical meaning of $a_b$:

$a_b = u_h(0) - \frac{d_1 + d_2}{2}$

This equation shows that the bubble coefficient $a_b$ represents the difference, or deviation, between the true displacement at the element center and the displacement predicted by a purely linear interpolation between the nodal values [@problem_id:2538605]. It quantifies the magnitude of the quadratic "bulge" or "sag" of the displacement field relative to a straight line connecting the endpoints.

### Stiffness Matrix Formulation and Energetic Orthogonality

To utilize this new element in an analysis, we must derive its [stiffness matrix](@entry_id:178659). The entries of the [element stiffness matrix](@entry_id:139369) $\mathbf{K}^e$ for a 1D bar with constant modulus $E$ and area $A$ are given by the [bilinear form](@entry_id:140194):

$K_{ij} = \int_{x_1}^{x_2} EA \frac{d\phi_i}{dx} \frac{d\phi_j}{dx} dx$

To evaluate this integral, we map it to the reference domain $\xi \in [-1,1]$. The physical coordinate $x$ is mapped from $\xi$ using the linear [shape functions](@entry_id:141015): $x(\xi) = N_1(\xi)x_1 + N_2(\xi)x_2$. This [affine mapping](@entry_id:746332) has a constant Jacobian, $J$:

$J = \frac{dx}{d\xi} = \frac{d}{d\xi}\left(\frac{1-\xi}{2}x_1 + \frac{1+\xi}{2}x_2\right) = \frac{x_2 - x_1}{2} = \frac{L}{2}$

where $L$ is the element length. The [chain rule](@entry_id:147422) connects derivatives in the physical and reference domains: $\frac{d}{dx} = \frac{1}{J}\frac{d}{d\xi}$ [@problem_id:2538573]. The differential element transforms as $dx = J\,d\xi$. Substituting these into the stiffness integral gives:

$K_{ij} = \int_{-1}^{1} EA \left(\frac{1}{J}\frac{d\phi_i}{d\xi}\right) \left(\frac{1}{J}\frac{d\phi_j}{d\xi}\right) (J\,d\xi) = \frac{EA}{J} \int_{-1}^{1} \frac{d\phi_i}{d\xi} \frac{d\phi_j}{d\xi} d\xi = \frac{2EA}{L} \int_{-1}^{1} \phi'_i(\xi) \phi'_j(\xi) d\xi$

We now compute the derivatives of our basis functions [@problem_id:2538559]:
$\phi'_1(\xi) = N'_1(\xi) = -\frac{1}{2}$
$\phi'_2(\xi) = N'_2(\xi) = \frac{1}{2}$
$\phi'_3(\xi) = N'_b(\xi) = -2\xi$

Let's compute the entries of the $3 \times 3$ stiffness matrix. The diagonal terms are:
$K_{11} = \frac{2EA}{L} \int_{-1}^{1} (-\frac{1}{2})^2 d\xi = \frac{2EA}{L} (\frac{1}{4}) (2) = \frac{EA}{L}$
$K_{22} = \frac{2EA}{L} \int_{-1}^{1} (\frac{1}{2})^2 d\xi = \frac{2EA}{L} (\frac{1}{4}) (2) = \frac{EA}{L}$
$K_{33} = \frac{2EA}{L} \int_{-1}^{1} (-2\xi)^2 d\xi = \frac{2EA}{L} \int_{-1}^{1} 4\xi^2 d\xi = \frac{8EA}{L} [\frac{\xi^3}{3}]_{-1}^{1} = \frac{8EA}{L}(\frac{2}{3}) = \frac{16EA}{3L}$ [@problem_id:2538529]

The off-diagonal terms involving the linear functions are:
$K_{12} = \frac{2EA}{L} \int_{-1}^{1} (-\frac{1}{2})(\frac{1}{2}) d\xi = \frac{2EA}{L} (-\frac{1}{4}) (2) = -\frac{EA}{L}$

Now, critically, we examine the coupling terms between the linear modes and the bubble mode:
$K_{13} = \frac{2EA}{L} \int_{-1}^{1} (-\frac{1}{2})(-2\xi) d\xi = \frac{2EA}{L} \int_{-1}^{1} \xi d\xi = \frac{2EA}{L} [\frac{\xi^2}{2}]_{-1}^{1} = 0$
$K_{23} = \frac{2EA}{L} \int_{-1}^{1} (\frac{1}{2})(-2\xi) d\xi = \frac{2EA}{L} \int_{-1}^{1} -\xi d\xi = -\frac{2EA}{L} [\frac{\xi^2}{2}]_{-1}^{1} = 0$

The coupling terms are zero. This is a remarkable and powerful feature of this basis construction. The reason for this decoupling lies in the symmetry of the integrand. The derivatives of the linear [shape functions](@entry_id:141015) are constants ([even functions](@entry_id:163605)), while the derivative of the quadratic bubble is a linear function of $\xi$ (an odd function). The product of an even and an [odd function](@entry_id:175940) is odd, and the [definite integral](@entry_id:142493) of an odd function over a symmetric interval like $[-1,1]$ is always zero [@problem_id:2538559]. This property is known as **energetic orthogonality** or decoupling, as the [strain energy](@entry_id:162699) contains no cross-terms between the linear and bubble modes [@problem_id:2538563].

Assembling the full matrix reveals a [block-diagonal structure](@entry_id:746869) [@problem_id:2538530] [@problem_id:2538532]:

$\mathbf{K}^e = \frac{EA}{L} \begin{pmatrix} 1 & -1 & 0 \\ -1 & 1 & 0 \\ 0 & 0 & \frac{16}{3} \end{pmatrix}$

The top-left $2 \times 2$ block is exactly the stiffness matrix for a standard linear [bar element](@entry_id:746680). The quadratic mode contributes its own scalar stiffness, but does not alter the stiffness relationship between the nodal degrees of freedom.

### Static Condensation and Adaptive Analysis

The [block-diagonal structure](@entry_id:746869) of the [stiffness matrix](@entry_id:178659) has profound practical implications. Consider the element-level system of equations $\mathbf{K}^e \mathbf{d}^e = \mathbf{f}^e$, partitioned into nodal (n) and internal (i) degrees of freedom:

$\begin{pmatrix} \mathbf{K}_{nn}  \mathbf{K}_{ni} \\ \mathbf{K}_{in}  \mathbf{K}_{ii} \end{pmatrix} \begin{pmatrix} \mathbf{u}_n \\ \mathbf{a}_i \end{pmatrix} = \begin{pmatrix} \mathbf{f}_n \\ \mathbf{f}_i \end{pmatrix}$

Because internal degrees of freedom are not shared between elements, they can be eliminated at the element level before assembly into the global system. This process is called **[static condensation](@entry_id:176722)**. The general formula for the condensed [stiffness matrix](@entry_id:178659) relating only the nodal DOFs is:

$\mathbf{K}_{\text{cond}} = \mathbf{K}_{nn} - \mathbf{K}_{ni} \mathbf{K}_{ii}^{-1} \mathbf{K}_{in}$

For our hierarchical element, the coupling matrices $\mathbf{K}_{ni}$ and $\mathbf{K}_{in}$ are null matrices. This leads to a trivial [condensation](@entry_id:148670) [@problem_id:2538541]:

$\mathbf{K}_{\text{cond}} = \mathbf{K}_{nn} - \mathbf{0} = \mathbf{K}_{nn} = \frac{EA}{L} \begin{pmatrix} 1  -1 \\ -1  1 \end{pmatrix}$

This confirms that the condensed [stiffness matrix](@entry_id:178659) for the quadratic hierarchical element is identical to the [stiffness matrix](@entry_id:178659) of a linear element. The effect of the [bubble function](@entry_id:179039) is captured by solving for its coefficient $a_b$ *after* the global solution for nodal displacements is found (a process called recovery).

This framework is exceptionally well-suited for **p-adaptive analysis**. To enrich an element from quadratic ($p=2$) to cubic ($p=3$), one simply adds a cubic [bubble function](@entry_id:179039) (e.g., proportional to $\xi(\xi^2-1)$) to the basis. The existing $3 \times 3$ stiffness matrix becomes the top-left sub-block of a new $4 \times 4$ matrix, preserving all previous calculations. Furthermore, the magnitude of the internal coefficients provides a natural [a posteriori error indicator](@entry_id:746618). After solving a problem with a $p=2$ basis, one can solve a local problem on each element to find the amplitude of the next hierarchical mode (e.g., the cubic bubble). The energy of this higher-order correction, given by $\eta_e^2 = \mathbf{a}_i^T \mathbf{K}_{ii} \mathbf{a}_i$, serves as an excellent estimate of the [local error](@entry_id:635842). Elements where this indicator is large are prime candidates for [p-refinement](@entry_id:173797), allowing computational effort to be focused only where it is needed most [@problem_id:2538549].