## Introduction
In the [finite element method](@entry_id:136884), the choice of element formulation represents a fundamental compromise between accuracy and computational cost. While [simple tensor](@entry_id:201624)-product constructions offer a structured approach, they often introduce more degrees of freedom than necessary, particularly within the element's interior. This raises a critical question for computational scientists and engineers: how can we formulate elements that are both accurate and computationally economical? The serendipity family of finite elements provides a sophisticated answer, born from the quest for greater efficiency in numerical simulations. These elements are cleverly designed to reduce the number of unknowns by omitting specific interior nodes, without sacrificing the order of polynomial accuracy on the element's boundaries.

This article delves into the theory and practice of [serendipity element](@entry_id:754705) formulations. The first chapter, **Principles and Mechanisms**, will uncover the core ideas behind their construction, contrasting them with tensor-product elements and formally defining their [polynomial spaces](@entry_id:753582). We will deconstruct the ubiquitous 8-node [serendipity element](@entry_id:754705) and analyze its approximation properties and potential stability pitfalls like [hourglassing](@entry_id:164538). Following this theoretical foundation, the **Applications and Interdisciplinary Connections** chapter will bridge theory to practice, demonstrating how these elements perform in fields such as [solid mechanics](@entry_id:164042), fluid dynamics, and high-performance computing. You will learn about their strengths and weaknesses in specific scenarios, from modeling [plate bending](@entry_id:184758) to their efficiency on modern GPU architectures. Finally, the **Hands-On Practices** section offers a chance to solidify your understanding through targeted exercises, reinforcing the key concepts of element construction, assembly, and numerical analysis.

## Principles and Mechanisms

The formulation of finite elements is a study in trade-offs, balancing representational power against computational cost. While tensor-product constructions offer simplicity and structure, the serendipity family of elements emerged from a desire for greater efficiency, seeking to reduce the number of degrees of freedom (DOFs) required to achieve a given [order of accuracy](@entry_id:145189). This chapter delves into the principles governing the construction of [serendipity elements](@entry_id:171371), the mechanisms by which they are formulated, and the practical consequences of their use in numerical simulations.

### The Quest for Efficiency: Serendipity vs. Tensor-Product Elements

The most direct method for constructing polynomial bases on quadrilateral or [hexahedral elements](@entry_id:174602) is the **tensor-product** approach. For a two-dimensional reference quadrilateral, $\hat{K} = [-1, 1]^2$, the tensor-product [polynomial space](@entry_id:269905) of order $p$, denoted $Q_p(\hat{K})$, is formed by the tensor product of one-dimensional [polynomial spaces](@entry_id:753582) of degree $p$:
$$
Q_p(\hat{K}) = \mathbb{P}_p(\xi) \otimes \mathbb{P}_p(\eta) = \operatorname{span}\{\xi^i \eta^j \mid 0 \le i \le p, 0 \le j \le p\}
$$
A nodal basis for this space is naturally defined on a grid of $(p+1) \times (p+1)$ points. For $p \ge 2$, this necessitates nodes in the interior of the element, in addition to those on the vertices and edges. The total number of degrees of freedom for a $Q_p$ element is $(p+1)^2$. These elements, also known as Lagrangian elements, are valued for their simple structure, which is particularly advantageous in [high-order methods](@entry_id:165413). For instance, when [nodal points](@entry_id:171339) are chosen at the abscissae of Gauss-Lobatto-Legendre (GLL) quadrature, the resulting element mass matrix becomes diagonal, a property that drastically reduces the computational cost of explicit time-integration schemes. [@problem_id:3423025]

The primary motivation for the **[serendipity element](@entry_id:754705)** family, denoted $S_p$, is computational economy. The goal is to create an element that reduces the number of DOFs—specifically by removing interior nodes—while preserving the polynomial degree on the element's boundary. [@problem_id:3558265] The "serendipity" lies in discovering that many of the interior basis functions of the $Q_p$ space can be removed without degrading the asymptotic convergence rate for certain classes of problems.

The fundamental distinction arises from this treatment of the element interior. The $Q_p$ element is complete in the tensor-product sense, meaning it can exactly reproduce any polynomial in the space $Q_p(\hat{K})$. In contrast, the $S_p$ element, for $p \ge 2$, is constructed to be only **edge-wise complete**. This means the restriction, or trace, of its [polynomial space](@entry_id:269905) to any of the four edges is the full one-dimensional [polynomial space](@entry_id:269905) $\mathbb{P}_p$. To achieve this with fewer nodes, the interior [polynomial completeness](@entry_id:177462) is sacrificed. Specifically, the $S_p$ space is a proper subspace of $Q_p$, $S_p(\hat{K}) \subset Q_p(\hat{K})$. The basis functions that are removed correspond to those associated with the interior nodes of the $Q_p$ element. These are often called **[bubble functions](@entry_id:176111)**, as they are zero on the entire element boundary. For example, the 9-node biquadratic element, $Q_2$, has a central node whose shape function is proportional to $(1-\xi^2)(1-\eta^2)$. This function contains the monomial $\xi^2\eta^2$. The 8-node [serendipity element](@entry_id:754705), $S_2$, omits this central node, and its [polynomial space](@entry_id:269905) consequently lacks the $\xi^2\eta^2$ term. [@problem_id:3553809] [@problem_id:3558265] In general, the $S_p$ space for $p \ge 2$ cannot exactly reproduce the highest-order mixed monomial $\xi^p\eta^p$, a capability inherent to the $Q_p$ space.

### Formal Construction and Dimension

To move beyond this intuitive picture, a more rigorous definition of the serendipity space is required. One such formalization is based on the concept of **superlinear degree**.

**Definition:** The superlinear degree of a monomial $x^i y^j$, denoted $\operatorname{sldeg}(x^i y^j)$, is defined as the sum of its exponents that are of degree two or greater:
$$
\operatorname{sldeg}(x^i y^j) := (\text{if } i \ge 2 \text{ then } i \text{ else } 0) + (\text{if } j \ge 2 \text{ then } j \text{ else } 0)
$$
The serendipity space $S_r(\hat{K})$ is then defined as the span of all monomials in $Q_r(\hat{K})$ whose superlinear degree is at most $r$. [@problem_id:2557610]

Let us apply this definition to construct the monomial bases for small values of $r$:
-   **For $r=1$:** A monomial $x^i y^j$ must have $i, j \le 1$. In this case, no exponent is $\ge 2$, so the superlinear degree is always 0. Since $0 \le 1$, all monomials in $Q_1(\hat{K})$ are included. The basis is $\{1, x, y, xy\}$, and $\dim(S_1) = 4$. This space is identical to $Q_1(\hat{K})$.

-   **For $r=2$:** We consider monomials in $Q_2(\hat{K})$.
    -   Terms like $1, x, y, xy$ have $\operatorname{sldeg}=0 \le 2$.
    -   Terms like $x^2, y^2, x^2y, xy^2$ have $\operatorname{sldeg}=2 \le 2$. For instance, $\operatorname{sldeg}(x^2y^1) = 2+0=2$.
    -   The term $x^2y^2$ has $\operatorname{sldeg}(x^2y^2) = 2+2=4 > 2$. This monomial is excluded.
    The resulting basis is $\{1, x, y, xy, x^2, y^2, x^2y, xy^2\}$, and $\dim(S_2) = 8$.

-   **For $r=3$:** Following the same logic, the basis contains all monomials from $Q_3(\hat{K})$ except those where the superlinear degree exceeds 3. This excludes terms like $x^2y^2$ ($\operatorname{sldeg}=4$), $x^3y^2$ ($\operatorname{sldeg}=5$), etc. The resulting basis has $\dim(S_3) = 12$.

-   **For $r=4$:** The condition $\operatorname{sldeg}(x^i y^j) \le 4$ now admits the monomial $x^2y^2$ since its superlinear degree is $2+2=4$. The dimension becomes $\dim(S_4) = 17$. [@problem_id:3442367]

This systematic counting can be generalized. By partitioning the set of monomials based on their exponents and applying [combinatorial principles](@entry_id:174121), one can derive a closed-form, piecewise formula for the dimension of $S_r(\hat{K})$ as defined here [@problem_id:3442397]:
$$
\dim S_r(\hat{K}) =
\begin{cases}
4r  \text{if } 1 \le r \le 3 \\
\frac{1}{2}(r^2+3r+6)  \text{if } r \ge 4
\end{cases}
$$
This exercise demonstrates that "serendipity" is a constructive principle, and the precise [polynomial space](@entry_id:269905) depends on the specific definition employed. The superlinear degree criterion provides one systematic, though not unique, way to generate such spaces.

### The 8-Node Serendipity Element ($S_2$) in Detail

The most ubiquitous member of the serendipity family is the 8-node biquadratic element, which corresponds to the space $S_2(\hat{K})$. Its practical importance merits a detailed look at the construction of its nodal basis functions, $\{\phi_i\}_{i=1}^8$. These functions must satisfy the **Kronecker-delta property**, $\phi_i(\boldsymbol{x}_j) = \delta_{ij}$, at the eight nodal locations (four vertices and four edge midpoints).

A pedagogically illuminating way to derive these functions is to build them constructively. [@problem_id:3442376]

1.  **Midside Node Functions:** Consider the function for the node at $(\xi, \eta) = (0, -1)$. This function, $\phi_5$, must be 1 at this node and 0 at all seven other nodes. It must therefore vanish on the three edges $\xi=-1$, $\xi=1$, and $\eta=1$. A simple polynomial that satisfies these zero conditions is $(1-\xi^2)(1+\eta)$. Wait, it should be zero at $\eta=1$, so we use $(1-\eta)$. Let's try $(1-\xi^2)(1-\eta)$. This expression is zero on edges $\xi=\pm 1$ and $\eta=1$. To find the full shape function, we introduce a constant $C$ and enforce the condition $\phi_5(0,-1)=1$:
    $$
    \phi_5(\xi, \eta) = C (1-\xi^2)(1-\eta) \implies \phi_5(0, -1) = C(1-0^2)(1-(-1)) = 2C = 1 \implies C = \frac{1}{2}
    $$
    Thus, $\phi_5(\xi, \eta) = \frac{1}{2}(1-\xi^2)(1-\eta)$. By construction, this function is zero at all other nodes. The functions for the other [midside nodes](@entry_id:176308) are found by rotation.

2.  **Corner Node Functions:** Now consider the function for the corner node at $(\xi, \eta) = (-1, -1)$. A simple starting point is the bilinear shape function for that corner, $L_1(\xi, \eta) = \frac{1}{4}(1-\xi)(1-\eta)$. This function is 1 at $(-1,-1)$ and 0 at the other three corners. However, it is non-zero at the adjacent [midside nodes](@entry_id:176308), $(0, -1)$ and $(-1, 0)$. We can correct this by subtracting multiples of the midside [shape functions](@entry_id:141015) we just derived, $\phi_5$ and $\phi_8$:
    $$
    \phi_1(\xi, \eta) = L_1(\xi, \eta) - c_5 \phi_5(\xi, \eta) - c_8 \phi_8(\xi, \eta)
    $$
    We find the constants by enforcing $\phi_1(0,-1)=0$ and $\phi_1(-1,0)=0$. This yields $c_5 = L_1(0,-1) = 1/2$ and $c_8 = L_1(-1,0) = 1/2$. Substituting and simplifying gives:
    $$
    \phi_1(\xi, \eta) = \frac{1}{4}(1-\xi)(1-\eta) - \frac{1}{2}\left(\frac{1}{2}(1-\xi^2)(1-\eta)\right) - \frac{1}{2}\left(\frac{1}{2}(1-\xi)(1-\eta^2)\right) = -\frac{1}{4}(1-\xi)(1-\eta)(1+\xi+\eta)
    $$

This constructive process, sometimes conceptualized as a form of **blending function** interpolation [@problem_id:2592257], yields the full set of eight [shape functions](@entry_id:141015). The standard forms are [@problem_id:3553809] [@problem_id:3442376]:
- For corner nodes $(\xi_i, \eta_i) \in \{-1, 1\}^2$: $\phi_i(\xi, \eta) = \frac{1}{4}(1+\xi_i\xi)(1+\eta_i\eta)(\xi_i\xi + \eta_i\eta - 1)$
- For [midside nodes](@entry_id:176308) on vertical edges $(\xi_i, 0)$: $\phi_i(\xi, \eta) = \frac{1}{2}(1+\xi_i\xi)(1-\eta^2)$
- For [midside nodes](@entry_id:176308) on horizontal edges $(0, \eta_i)$: $\phi_i(\xi, \eta) = \frac{1}{2}(1-\xi^2)(1+\eta_i\eta)$

A crucial property of these functions is that when restricted to an edge, they exactly reproduce the one-dimensional quadratic Lagrange basis functions for the three nodes on that edge. This is the concrete realization of the "edge-wise quadratic completeness" that defines the element. [@problem_id:3553809]

### Approximation Properties and Performance Trade-offs

What is the practical cost of removing the interior modes from the tensor-[product space](@entry_id:151533)? A key result from [finite element approximation](@entry_id:166278) theory is that for a method to achieve an optimal convergence rate of order $k$ in the $H^1$ norm and $k+1$ in the $L^2$ norm for a solution $u \in H^{k+1}$, the element's [polynomial space](@entry_id:269905) must contain the complete [polynomial space](@entry_id:269905) of total degree $k$, denoted $P_k$.

Careful analysis of the serendipity space $S_k(\hat{K})$ reveals that, despite being a subset of $Q_k(\hat{K})$, it does contain $P_k(\hat{K})$. For any monomial $x^i y^j$ with total degree $i+j \le k$, its superlinear degree is also guaranteed to be less than or equal to $k$. [@problem_id:2557610] Therefore, since $P_k(\hat{K}) \subset S_k(\hat{K}) \subset Q_k(\hat{K})$, both serendipity and tensor-product elements achieve the **same optimal asymptotic convergence rates** on shape-regular meshes of parallelograms (affine mappings).

This leads to a nuanced discussion of performance based on the problem being solved [@problem_id:3423025]:

-   **For Elliptic Problems (e.g., Poisson's equation, linear elasticity):** Since both $S_p$ and $Q_p$ elements provide the same [order of accuracy](@entry_id:145189), but $S_p$ does so with significantly fewer DOFs (for $p > 1$), the [serendipity elements](@entry_id:171371) are generally more efficient. They offer a higher accuracy-per-DOF, making them an attractive choice for such problems.

-   **For Advection-Dominated Problems (e.g., wave propagation):** The situation is reversed. The "sacrificed" interior modes of the $Q_p$ space are crucial for accurately capturing the behavior of multi-dimensional waves, especially those propagating obliquely to the mesh grid. Their omission in $S_p$ elements leads to higher [numerical dispersion](@entry_id:145368) errors. Furthermore, the tensor-product structure of $Q_p$ elements allows for the use of nodal sets (like GLL points) that yield a [diagonal mass matrix](@entry_id:173002), making [explicit time-stepping](@entry_id:168157) algorithms computationally inexpensive. Serendipity elements lack this property and result in a fully-populated [mass matrix](@entry_id:177093) that must be inverted at every time step. For these reasons, $Q_p$ elements are strongly preferred for [advection-dominated problems](@entry_id:746320).

As a quantitative illustration of the relationship between the spaces, consider the best-approximation of a function from the tensor-product space $Q_2(\hat{K})$ within its serendipity subspace $S_2(\hat{K})$. The [orthogonal complement](@entry_id:151540) of $S_2(\hat{K})$ in $Q_2(\hat{K})$ is spanned by the function $u(x,y) = P_2(x)P_2(y)$, where $P_2$ is the Legendre polynomial of degree 2. The best approximation to $u$ in $S_2(\hat{K})$ with respect to the $L^2$ norm is its orthogonal projection, which is simply the zero function. The same holds true for the $H^1$ norm. A direct calculation of the norms of this error function $u$ reveals that the ratio of the squared errors is a constant, $\|u\|_{H^1}^2 / \|u\|_{L^2}^2 = 31$, providing a precise measure of how the energy of this "missing" mode is distributed between the function and its gradient. [@problem_id:3442370]

### Practical Considerations: Isoparametric Mapping and Stability

The theoretical properties discussed above assume a simple mapping from the reference element. In practice, elements are distorted to fit complex geometries, which introduces further subtleties.

-   **The Patch Test:** A fundamental consistency requirement for any finite element is that it must pass the **patch test**, meaning it can exactly reproduce a constant strain state. For [isoparametric elements](@entry_id:173863), this is equivalent to being able to reproduce an arbitrary linear displacement field. As long as the element's [shape functions](@entry_id:141015) form a partition of unity (i.e., $\sum \phi_i = 1$), which is true for all standard elements including serendipity types, the linear patch test is passed, even for general distorted (bilinear) quadrilateral shapes. This ensures convergence. [@problem_id:2592257] However, these elements generally fail higher-order patch tests on distorted geometries. For instance, an $S_2$ element cannot exactly represent a [quadratic field](@entry_id:636261) on a general quadrilateral because the [isoparametric mapping](@entry_id:173239) to parent coordinates introduces terms (like $\xi^2\eta^2$) that are not in the element's polynomial basis. [@problem_id:2592257]

-   **Numerical Integration and Hourglass Modes:** A critical stability issue, known as **[hourglassing](@entry_id:164538)**, can arise from the interplay between the element formulation and the numerical quadrature used to compute the [stiffness matrix](@entry_id:178659). Consider the 8-node [serendipity element](@entry_id:754705) ($S_2$) in a [linear elasticity](@entry_id:166983) problem. The [stiffness matrix](@entry_id:178659) involves an integral of the form $\int B^T D B \, d\Omega$. This integral is evaluated numerically using a Gaussian quadrature rule.
    -   Using a **[reduced integration](@entry_id:167949)** scheme, such as a $2 \times 2$ Gauss rule, is computationally cheaper. However, it can render the element unstable. A non-rigid body deformation mode is called an hourglass mode if it produces zero strain at all four $2 \times 2$ quadrature points. Because the computed strain energy is a sum over only these points, such a mode has zero strain energy and corresponds to a spurious, non-physical mode in the nullspace of the stiffness matrix. This can be proven formally: for an $S_2$ element with 16 DOFs, the stiffness matrix assembled with a $2 \times 2$ rule has a rank of at most $4 \times 3 = 12$. Since there are only 3 [rigid-body motion](@entry_id:265795) modes, the nullity of the stiffness matrix ($16 - 12 \ge 4$) is larger than the dimension of the rigid-body [nullspace](@entry_id:171336), guaranteeing the existence of at least one spurious [zero-energy mode](@entry_id:169976). [@problem_id:3442368]
    -   Using a **full integration** scheme, such as a $3 \times 3$ Gauss rule, resolves this issue for affine (parallelogram) elements. This rule can exactly integrate the [strain energy density](@entry_id:200085) polynomial. In this case, zero computed strain energy implies that the strain field is identically zero everywhere in the element, which is only possible for a [rigid-body motion](@entry_id:265795). Thus, no [hourglass modes](@entry_id:174855) exist. This stability comes at the cost of more expensive [numerical integration](@entry_id:142553). [@problem_id:3442368]

In conclusion, [serendipity elements](@entry_id:171371) represent a sophisticated and efficient alternative to tensor-product elements. They are built on a principle of economization, retaining boundary accuracy while reducing interior complexity. This design choice leads to a rich set of behaviors and trade-offs that are critical for the informed practitioner to understand, spanning [approximation theory](@entry_id:138536), [computational efficiency](@entry_id:270255) for different physical problems, and [numerical stability](@entry_id:146550).