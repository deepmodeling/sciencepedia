## Introduction
In the world of [inverse problems](@entry_id:143129) and [data assimilation](@entry_id:153547), where we infer hidden causes from observed effects, a robust mathematical foundation is paramount. The function spaces $L^2(\Omega)$ and $H^1(\Omega)$ provide this essential framework, offering a language to rigorously quantify data, model physical states, and enforce desirable solution properties like smoothness. Without a deep understanding of these spaces, attempts to solve inverse problems can lead to unstable, non-physical results, as the very concepts of 'error', 'smoothness', and even 'solution' lack precise definition. This article bridges this gap by systematically exploring the theory and application of these foundational mathematical tools.

This article is structured to build your expertise from the ground up. In **Principles and Mechanisms**, we will construct the $L^2$ and $H^1$ spaces, exploring their geometric properties, the concept of [weak derivatives](@entry_id:189356), and the critical theorems that govern their structure. Following this, **Applications and Interdisciplinary Connections** will demonstrate how this theory translates into practice, showing how the choice of space impacts regularization, boundary conditions, and problem formulation in fields from [medical imaging](@entry_id:269649) to [geophysics](@entry_id:147342). Finally, **Hands-On Practices** will solidify your understanding through guided exercises on computing gradients, analyzing problem [well-posedness](@entry_id:148590), and applying the core concepts to practical scenarios.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms of the [function spaces](@entry_id:143478) that form the mathematical bedrock for modern [inverse problems](@entry_id:143129) and data assimilation: the Lebesgue space $L^2(\Omega)$ and the Sobolev space $H^1(\Omega)$. Understanding their structure is not merely a theoretical exercise; it is essential for correctly formulating problems, defining appropriate measures of [data misfit](@entry_id:748209) and solution regularity, analyzing the [well-posedness](@entry_id:148590) of the resulting models, and devising effective computational algorithms. We will systematically construct these spaces from first principles, explore their geometric properties, and elucidate their profound connections to the [partial differential equations](@entry_id:143134) that govern physical systems.

### The Hilbert Space $L^2(\Omega)$: The Foundation for Data and States

The most fundamental space in the variational approach to data assimilation is the space of **square-[integrable functions](@entry_id:191199)**, denoted $L^2(\Omega)$. Its structure is uniquely suited for quantifying energy, variance, and [mean-squared error](@entry_id:175403), making it the natural setting for both physical [state variables](@entry_id:138790) and observational data.

#### Defining the Space and the "Almost Everywhere" Convention

Intuitively, the space $L^2(\Omega)$ consists of all measurable functions $u$ defined on a domain $\Omega \subset \mathbb{R}^d$ for which the integral of their square is finite:
$$
\int_{\Omega} |u(x)|^2 dx  \infty
$$
This condition ensures that the "energy" or "total variance" of the function is finite. However, a subtle but critical issue arises from the properties of the Lebesgue integral. If two functions, $u(x)$ and $v(x)$, are identical everywhere except on a set of measure zero (a **[null set](@entry_id:145219)**), the Lebesgue integral cannot distinguish between them. For instance, their squared difference would integrate to zero:
$$
\int_{\Omega} |u(x) - v(x)|^2 dx = 0
$$
This poses a problem for defining a norm, which must satisfy the property that $\|f\| = 0$ if and only if $f=0$. If we treated functions pointwise, $\|u-v\|=0$ would not imply $u=v$ everywhere.

To resolve this, we adopt a foundational convention: we declare two functions $u$ and $v$ to be equivalent, written $u \sim v$, if they are equal **[almost everywhere](@entry_id:146631)** (a.e.), meaning the set $\{x \in \Omega \mid u(x) \neq v(x)\}$ is a [null set](@entry_id:145219). The space $L^2(\Omega)$ is formally defined not as a space of individual functions, but as the space of **equivalence classes** of square-[integrable functions](@entry_id:191199) under this relation [@problem_id:3383661]. An element of $L^2(\Omega)$ is thus a collection of functions that are all identical from the perspective of integration. This seemingly abstract step is profoundly practical. It ensures that the quantity $(\int_{\Omega} |u|^2 dx)^{1/2}$ is a true norm on the space of [equivalence classes](@entry_id:156032). Furthermore, it means that cost functionals, such as a standard [least-squares](@entry_id:173916) misfit, are insensitive to changes in a function on a [null set](@entry_id:145219). For a linear [observation operator](@entry_id:752875) $H$, the value of $J(u) = \frac{1}{2}\int_{\Omega} |H u(x) - y(x)|^{2} dx$ depends only on the equivalence classes of $u$ and $y$, making the formulation robust and well-defined [@problem_id:3383661]. It is crucial to recognize that the boundary $\partial\Omega$ of a domain in $\mathbb{R}^d$ typically has a $d$-dimensional Lebesgue measure of zero. Consequently, modifying a function's values only on the boundary does not change its [equivalence class](@entry_id:140585) in $L^2(\Omega)$.

#### The Inner Product and Hilbert Space Structure

The space $L^2(\Omega)$ is more than just a [normed vector space](@entry_id:144421); it is a **Hilbert space**, meaning its norm is induced by an inner product. For any two real-valued functions (equivalence classes) $u, v \in L^2(\Omega)$, the **$L^2$ inner product** is defined as:
$$
\langle u, v \rangle_{L^2} = \int_{\Omega} u(x)v(x) \, dx
$$
This integral is guaranteed to be finite. A simple way to see this is by using the elementary inequality $|ab| \le \frac{1}{2}(a^2 + b^2)$, which leads to $\int |uv| dx \le \frac{1}{2} (\int u^2 dx + \int v^2 dx)  \infty$. The **$L^2$ norm** is then naturally defined as the square root of the inner product of a function with itself:
$$
\|u\|_{L^2} = \sqrt{\langle u, u \rangle_{L^2}} = \left( \int_{\Omega} |u(x)|^2 dx \right)^{1/2}
$$
The inner product endows the space with a geometric structure, defining notions of orthogonality and projection. A cornerstone of this geometry is the **Cauchy-Schwarz inequality**:
$$
|\langle u, v \rangle_{L^2}| \le \|u\|_{L^2} \|v\|_{L^2}
$$
This fundamental inequality can be elegantly proven by considering the non-negativity of the norm. For any scalar $t \in \mathbb{R}$, the function $u+tv$ is in $L^2(\Omega)$, and its squared norm must be non-negative:
$$
0 \le \|u+tv\|_{L^2}^2 = \langle u+tv, u+tv \rangle_{L^2} = \|u\|_{L^2}^2 + 2t\langle u, v \rangle_{L^2} + t^2\|v\|_{L^2}^2
$$
The right-hand side is a quadratic polynomial in $t$ that is always non-negative. This is only possible if its discriminant is non-positive: $(2\langle u, v \rangle_{L^2})^2 - 4\|u\|_{L^2}^2\|v\|_{L^2}^2 \le 0$. Rearranging this gives the Cauchy-Schwarz inequality [@problem_id:3383696]. This property is essential for proving the continuity of operators and functionals, forming the basis of countless stability estimates in inverse problems.

#### The Parallelogram Law and the Uniqueness of $L^2$

The family of Lebesgue spaces, $L^p(\Omega)$, consists of functions for which $\int |u|^p dx$ is finite. A natural question is why $p=2$ holds such a privileged position. The answer lies in the **[parallelogram law](@entry_id:137992)**, a geometric identity that must be satisfied by any norm that arises from an inner product:
$$
\|u+v\|^2 + \|u-v\|^2 = 2(\|u\|^2 + \|v\|^2)
$$
A fundamental result in functional analysis, the Jordan-von Neumann theorem, states that a norm is induced by an inner product if and only if it satisfies this law. It turns out that among all $L^p$ spaces, only the $L^2$ norm satisfies the [parallelogram law](@entry_id:137992) [@problem_id:3383658]. To see this, consider two functions with disjoint support, for instance, [characteristic functions](@entry_id:261577) $u=\chi_{E_1}$ and $v=\chi_{E_2}$ over [disjoint sets](@entry_id:154341) $E_1, E_2$. The law fails for any $p \neq 2$. This profound geometric distinction is why only $L^2(\Omega)$ is a Hilbert space among the $L^p$ family. This is not merely a theoretical curiosity; it has deep practical consequences for optimization.

#### Duality, the Riesz Representation Theorem, and Gradients

The **dual space** of a [normed space](@entry_id:157907) $X$, denoted $X'$, consists of all [continuous linear functionals](@entry_id:262913) on $X$—that is, all [linear maps](@entry_id:185132) from $X$ to the real numbers that are bounded. The **Riesz [representation theorem](@entry_id:275118)** for Hilbert spaces provides a remarkable identification: for every functional $\ell \in H'$, there exists a unique element $u_\ell \in H$ such that the action of the functional is given by the inner product: $\ell(v) = \langle u_\ell, v \rangle_H$ for all $v \in H$. This theorem establishes an [isometric isomorphism](@entry_id:273188) between a Hilbert space and its dual.

For $L^2(\Omega)$, this means we can identify $L^2(\Omega)'$ with $L^2(\Omega)$ itself [@problem_id:3383701]. Any [continuous linear functional](@entry_id:136289) on $L^2(\Omega)$ can be represented as an inner product with some function in $L^2(\Omega)$. This "[self-duality](@entry_id:140268)" is the key to simple gradient calculations in optimization. For a [least-squares](@entry_id:173916) [cost functional](@entry_id:268062) $J(u) = \frac{1}{2}\|Au-y\|_{L^2}^2$, its Fréchet derivative is a functional that, by the Riesz theorem, can be identified with an element of $L^2(\Omega)$ itself: the gradient. This gradient is found to be $\nabla J(u) = A^*(Au-y)$, where $A^*$ is the adjoint of $A$. The gradient is simply the adjoint operator acting on the residual, an element of the same space $L^2(\Omega)$ [@problem_id:3383658].

This contrasts sharply with optimization in $L^p$ spaces for $p \neq 2$. These spaces are not self-dual; the dual of $L^p(\Omega)$ is $L^{p'}(\Omega)$, where $1/p + 1/p' = 1$. The derivative of a functional naturally lives in the [dual space](@entry_id:146945) $L^{p'}(\Omega)$, and its representation as a "gradient" back in the primal space $L^p(\Omega)$ involves a nonlinear duality map, complicating the geometry of optimization considerably [@problem_id:3383658].

### The Sobolev Space $H^1(\Omega)$: Incorporating Smoothness

While $L^2(\Omega)$ is ideal for representing data, many [inverse problems](@entry_id:143129) involve estimating spatially distributed fields that are solutions to partial differential equations (PDEs). PDEs encode relationships between a function and its derivatives. Furthermore, regularization often takes the form of penalizing non-smooth solutions. This requires a [function space](@entry_id:136890) that can accommodate not just the function itself, but also its derivatives.

#### The Weak Derivative

Classical derivatives are only defined for sufficiently smooth functions. This is too restrictive for the often non-smooth solutions encountered in [data assimilation](@entry_id:153547). The concept of a **[weak derivative](@entry_id:138481)** (or [distributional derivative](@entry_id:271061)) extends the notion of differentiation to a much broader class of functions.

The definition is motivated by the integration by parts formula. For a smooth function $u$ and a smooth [test function](@entry_id:178872) $\varphi$ that vanishes on the boundary $\partial\Omega$ (denoted $\varphi \in C_c^\infty(\Omega)$), [integration by parts](@entry_id:136350) gives:
$$
\int_{\Omega} \frac{\partial u}{\partial x_i}(x) \varphi(x) \, dx = - \int_{\Omega} u(x) \frac{\partial \varphi}{\partial x_i}(x) \, dx
$$
We turn this formula into a definition. For a [locally integrable function](@entry_id:175678) $u$, we say that a function $g_i$ is the weak partial derivative of $u$ with respect to $x_i$ if $g_i$ satisfies this relationship for *all* [test functions](@entry_id:166589) $\varphi \in C_c^\infty(\Omega)$:
$$
\int_{\Omega} g_i(x) \varphi(x) \, dx = - \int_{\Omega} u(x) \frac{\partial \varphi}{\partial x_i}(x) \, dx
$$
If such a function $g_i$ exists and belongs to $L^2(\Omega)$, we denote it by $\partial_{x_i} u$ and say that the [weak derivative](@entry_id:138481) of $u$ is square-integrable [@problem_id:3383704].

#### Defining the Sobolev Space $H^1(\Omega)$

With the [weak derivative](@entry_id:138481) defined, we can now construct the **Sobolev space $H^1(\Omega)$**. It is the space of all functions in $L^2(\Omega)$ whose first-order [weak derivatives](@entry_id:189356) are also in $L^2(\Omega)$:
$$
H^1(\Omega) = \{ u \in L^2(\Omega) \mid \nabla u \in L^2(\Omega)^d \}
$$
where $\nabla u = (\partial_{x_1}u, \dots, \partial_{x_d}u)$ is the [weak gradient](@entry_id:756667). This space is also a Hilbert space, equipped with the **$H^1$ inner product**:
$$
\langle u, v \rangle_{H^1} = \int_{\Omega} \left( u(x)v(x) + \nabla u(x) \cdot \nabla v(x) \right) dx = \langle u, v \rangle_{L^2} + \langle \nabla u, \nabla v \rangle_{L^2}
$$
The corresponding **$H^1$ norm** is:
$$
\|u\|_{H^1} = \sqrt{\|u\|_{L^2}^2 + \|\nabla u\|_{L^2}^2}
$$
This norm simultaneously controls the size of the function and the size of its gradient [@problem_id:3383704, @problem_id:3383658]. The [bilinear form](@entry_id:140194) $a(u,v) = \langle u, v \rangle_{H^1}$ associated with the inner product generates the squared norm, $a(u,u) = \|u\|_{H^1}^2$, by definition, for any open set $\Omega$ [@problem_id:3383714].

#### Application: Tikhonov Regularization in $H^1$

The $H^1$ norm is the quintessential tool for **Tikhonov regularization** in [inverse problems](@entry_id:143129) governed by PDEs. A typical regularized [cost functional](@entry_id:268062) takes the form:
$$
J(u) = \frac{1}{2}\|Au-y\|^2 + \frac{\alpha}{2}\|u\|_{H^1}^2
$$
The first term measures misfit to data, while the second term, the **regularization penalty**, penalizes functions with large magnitude or large gradients. This discourages oscillatory, non-physical solutions. Because the $H^1$ norm is the norm of a Hilbert space, the penalty term $\frac{\alpha}{2}\|u\|_{H^1}^2$ is strictly convex and coercive. For $\alpha  0$, this ensures that the overall [cost functional](@entry_id:268062) $J(u)$ becomes strictly convex and coercive on $H^1(\Omega)$, which guarantees the existence of a unique, stable minimizer [@problem_id:3383704]. The choice of the $H^1$ space for regularization transforms an often [ill-posed problem](@entry_id:148238) into a well-posed one.

### Boundary Conditions and Subspaces: The Role of $H_0^1(\Omega)$ and the Trace Theorem

Many physical problems involve prescribed values on the boundaries of a domain, known as Dirichlet boundary conditions. Accommodating these constraints within the [weak formulation](@entry_id:142897) requires further refinement of our [function space](@entry_id:136890) framework.

#### The Challenge of Boundary Values and the Trace Theorem

A key feature of $L^2$ and $H^1$ functions is that they are defined as [equivalence classes](@entry_id:156032), insensitive to changes on [null sets](@entry_id:203073). Since the boundary $\partial\Omega$ is a [null set](@entry_id:145219), the notion of a function's value "at the boundary" is not straightforward. For a general $u \in H^1(\Omega)$, its pointwise value at a boundary point is not well-defined.

The **Trace Theorem** provides the rigorous solution. It states that for a domain $\Omega$ with a sufficiently regular boundary (e.g., a **Lipschitz boundary**, which allows for corners but not cusps), there exists a continuous, linear, and surjective operator called the **[trace operator](@entry_id:183665)**:
$$
\mathrm{Tr}: H^1(\Omega) \to H^{1/2}(\partial\Omega)
$$
This operator maps a function in $H^1(\Omega)$ to its "boundary value," which resides in a fractional Sobolev space $H^{1/2}(\partial\Omega)$ on the boundary. The continuity of the operator is expressed by the inequality $\|\mathrm{Tr}\,u\|_{H^{1/2}(\partial\Omega)} \le C\|u\|_{H^1(\Omega)}$ [@problem_id:3383680]. Surjectivity means that for any valid boundary data $g \in H^{1/2}(\partial\Omega)$, there exists a function $u \in H^1(\Omega)$ whose trace is $g$. This also guarantees the existence of a continuous right-inverse, or **[lifting operator](@entry_id:751273)**, $E: H^{1/2}(\partial\Omega) \to H^1(\Omega)$ that constructs such a function [@problem_id:3383680]. This theorem is the foundation for analyzing problems with boundary data or boundary observations.

#### The Space $H_0^1(\Omega)$: Enforcing Homogeneous Dirichlet Conditions

To model problems where the state is fixed at zero on the boundary (a **homogeneous Dirichlet condition**), we introduce the crucial subspace $H_0^1(\Omega)$. It is formally defined as the closure of the space of infinitely differentiable functions with [compact support](@entry_id:276214), $C_c^\infty(\Omega)$, in the $H^1$ norm. Intuitively, it is the space of $H^1$ functions that can be approximated arbitrarily well by [smooth functions](@entry_id:138942) that vanish near the boundary.

A fundamental theorem provides an equivalent and more practical characterization for Lipschitz domains: $H_0^1(\Omega)$ is precisely the kernel of the [trace operator](@entry_id:183665) [@problem_id:3383703].
$$
H_0^1(\Omega) = \{ u \in H^1(\Omega) \mid \mathrm{Tr}(u) = 0 \text{ on } \partial\Omega \}
$$
Thus, seeking a solution within the space $H_0^1(\Omega)$ is the correct variational way to enforce the condition $u=0$ on $\partial\Omega$. It is a common misconception that $C_c^\infty(\Omega)$ is dense in $H^1(\Omega)$; it is only dense in the proper subspace $H_0^1(\Omega)$ [@problem_id:3383703].

#### The Poincaré Inequality and an Equivalent Norm on $H_0^1(\Omega)$

On a bounded domain, functions in $H_0^1(\Omega)$ satisfy the **Poincaré inequality**, which provides control of the function's $L^2$ norm by the $L^2$ norm of its gradient:
$$
\|u\|_{L^2} \le C_P \|\nabla u\|_{L^2} \quad \text{for all } u \in H_0^1(\Omega)
$$
This inequality is a direct consequence of the function vanishing at the boundary. It fails for general $H^1(\Omega)$ functions, as any non-zero [constant function](@entry_id:152060) has a zero gradient but a non-zero norm.

The Poincaré inequality implies that on $H_0^1(\Omega)$, the gradient [seminorm](@entry_id:264573) $\|\nabla u\|_{L^2}$ is, in fact, a full norm equivalent to the standard $H^1$ norm [@problem_id:3383714]. This allows the inner product on $H_0^1(\Omega)$ to be simplified to $\langle u, v \rangle_{H_0^1} = \int_{\Omega} \nabla u \cdot \nabla v \, dx$, which is often more convenient in the analysis of PDEs.

#### Natural vs. Essential Boundary Conditions

The distinction between $H^1(\Omega)$ and $H_0^1(\Omega)$ clarifies the difference between two types of boundary conditions in [variational problems](@entry_id:756445).
- **Essential Boundary Conditions**, like Dirichlet conditions, are imposed "essentially" by restricting the space of admissible functions (e.g., seeking a solution in $H_0^1(\Omega)$).
- **Natural Boundary Conditions**, like Neumann conditions ($\partial u / \partial n = 0$), arise "naturally" from the [variational principle](@entry_id:145218) when no constraints are placed on the boundary values of the test functions. For example, minimizing an energy functional over the entire space $H^1(\Omega)$ leads to a [weak formulation](@entry_id:142897) whose strong form includes a homogeneous Neumann condition, not a Dirichlet one [@problem_id:3383704].

### Duality and Embeddings: The Deeper Structure

The relationships between $L^2$, $H^1$, and their duals reveal a rich structure that is central to the modern theory of PDEs and their numerical solution.

#### The Gelfand Triple

When dealing with homogeneous Dirichlet problems, three spaces are inextricably linked: $H_0^1(\Omega)$, $L^2(\Omega)$, and the dual space of $H_0^1(\Omega)$, denoted $H^{-1}(\Omega)$. They form a **Gelfand Triple** (or rigging of Hilbert spaces):
$$
H_0^1(\Omega) \hookrightarrow L^2(\Omega) \hookrightarrow H^{-1}(\Omega)
$$
The symbol $\hookrightarrow$ denotes an **embedding** that is both **continuous** and **dense**.
- **Continuous Embedding:** The inclusion map is bounded. For instance, $\|u\|_{L^2} \le C\|u\|_{H^1}$ shows the continuity of $H_0^1(\Omega) \hookrightarrow L^2(\Omega)$.
- **Dense Embedding:** The image of the smaller space is dense in the larger one. For example, $H_0^1(\Omega)$ is dense in $L^2(\Omega)$, meaning any $L^2$ function can be approximated by an $H_0^1$ function. Similarly, $L^2(\Omega)$ is dense in $H^{-1}(\Omega)$ [@problem_id:3383656].

The Gelfand triple provides the natural setting for the weak formulation of many [evolution equations](@entry_id:268137) and optimization problems, where the state lives in $H_0^1$, data and residuals may live in $L^2$, and forcing terms or gradients can be general distributions in $H^{-1}$ [@problem_id:3383656].

#### Duality in $H_0^1(\Omega)$ and the Poisson Problem

We saw that $L^2(\Omega)$ is identified with its dual via the $L^2$ inner product. The situation is different and more profound for $H_0^1(\Omega)$ (equipped with the gradient inner product $\langle u,v\rangle_{H_0^1} = \int \nabla u \cdot \nabla v \, dx$). The Riesz [representation theorem](@entry_id:275118) states that the map $R_{H_0^1}$ that takes a function $u \in H_0^1(\Omega)$ to the functional $\langle u, \cdot \rangle_{H_0^1} \in H^{-1}(\Omega)$ is an [isometric isomorphism](@entry_id:273188).

The inverse of this map, $R_{H_0^1}^{-1}: H^{-1}(\Omega) \to H_0^1(\Omega)$, has a remarkable interpretation. Given a functional $f \in H^{-1}(\Omega)$, finding its representation $u = R_{H_0^1}^{-1}(f)$ is equivalent to solving the variational problem: find $u \in H_0^1(\Omega)$ such that $\int_{\Omega} \nabla u \cdot \nabla v \, dx = \langle f, v \rangle_{H^{-1},H_0^1}$ for all $v \in H_0^1(\Omega)$. This is precisely the [weak formulation](@entry_id:142897) of the **Poisson equation** with homogeneous Dirichlet boundary conditions, $-\Delta u = f$. Therefore, the inverse of the Riesz map on $H_0^1(\Omega)$ *is* the solution operator for the Dirichlet-Poisson problem [@problem_id:3383701]. This establishes a deep identity between the geometric structure of the function space and the solution of a fundamental PDE.

Any function $f \in L^2(\Omega)$ also defines a functional in $H^{-1}(\Omega)$ via the pairing $v \mapsto \int f v \, dx$. This action is bounded on $H_0^1(\Omega)$ due to the Cauchy-Schwarz and Poincaré inequalities. This is the mechanism by which $L^2(\Omega)$ continuously embeds into $H^{-1}(\Omega)$, allowing $L^2$ source terms and observations to be incorporated into [variational problems](@entry_id:756445) posed on $H_0^1$ [@problem_id:3383701].

#### Sobolev Embedding Theorems: Regularity and Observation Operators

How "regular" is a function in $H^1(\Omega)$? For instance, is it continuous? Can we evaluate it at a point? The **Sobolev embedding theorems** provide the answer, which depends critically on the dimension $d$ of the space $\Omega \subset \mathbb{R}^d$ [@problem_id:3383692].

-   **If $d=1$:** $H^1(\Omega)$ embeds continuously into the space of Hölder continuous functions, $C^{0,1/2}(\overline{\Omega})$. In particular, every function in $H^1(\Omega)$ has a unique continuous representative. This implies that for any point $x_0 \in \overline{\Omega}$, the point-[evaluation map](@entry_id:149774) $u \mapsto u(x_0)$ is a [continuous linear functional](@entry_id:136289) on $H^1(\Omega)$. Thus, pointwise observations are well-defined in 1D problems.

-   **If $d=2$:** This is a "critical" case. $H^1(\Omega)$ embeds continuously into $L^q(\Omega)$ for *any* finite $q \ge 1$, but it does *not* embed into $L^\infty(\Omega)$ or the space of continuous functions $C^0(\overline{\Omega})$. Functions in $H^1(\Omega)$ can be unbounded (e.g., with logarithmic singularities). Consequently, pointwise evaluation $u \mapsto u(x_0)$ is generally not a well-defined or continuous operation for functions in $H^1(\mathbb{R}^2)$.

-   **If $d2$:** $H^1(\Omega)$ embeds continuously into $L^q(\Omega)$ only for $q \le 2^* = \frac{2d}{d-2}$. The exponent $2^*$ is the **critical Sobolev exponent**. For exponents greater than this, the embedding fails. Like the 2D case, functions are not guaranteed to be continuous, and pointwise observations are ill-defined.

These theorems have direct implications for [data assimilation](@entry_id:153547): an [observation operator](@entry_id:752875) that involves pointwise evaluation of the state is mathematically valid if the state space is $H^1(\Omega)$ with $d=1$, but is ill-posed for $d \ge 2$.

#### Compact Embeddings and the Rellich-Kondrachov Theorem

A stronger property than continuity is **compactness**. A continuous embedding may map a bounded set to another bounded set, but a **[compact embedding](@entry_id:263276)** maps a bounded set to a pre-compact set (a set whose closure is compact). The practical importance of this is that any bounded sequence in the starting space will have a subsequence whose image converges strongly in the target space. This property is the engine behind many existence proofs for solutions to nonlinear PDEs and optimization problems.

The **Rellich-Kondrachov theorem** specifies when Sobolev [embeddings](@entry_id:158103) are compact. For a bounded Lipschitz domain, the embedding $H^1(\Omega) \hookrightarrow L^q(\Omega)$ is compact for all exponents $q$ that are "subcritical," i.e., $q  2^*$ (where $2^* = \frac{2d}{d-2}$ for $d2$, and $2^*=\infty$ for $d=2$) [@problem_id:3383692]. The embedding into the critical space $L^{2^*}(\Omega)$ is continuous but notably *not* compact. This compactness is crucial for establishing properties like the weak [lower semi-continuity](@entry_id:146149) of cost functionals involving boundary observations, which underpins the existence of optimal solutions in data assimilation [@problem_id:3383680].