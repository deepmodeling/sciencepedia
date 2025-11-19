## Introduction
In [computational engineering](@entry_id:178146), we are constantly tasked with modeling and simulating continuous physical fields like temperature, velocity, and stress. But how do we handle these fields—which are functions—in a way that provides mathematical guarantees for the correctness and stability of our numerical methods? The answer lies not in treating each function as an isolated case, but in viewing them as elements of a vast, structured collection: a **[function space](@entry_id:136890)**. This framework, equipped with tools for measuring size and distance called **norms**, forms the theoretical bedrock upon which reliable computational science is built. This article bridges the gap between abstract [functional analysis](@entry_id:146220) and practical application, revealing why these concepts are indispensable for any modern engineer or scientist working with simulations.

This article is structured to build your understanding from the ground up.
*   First, **Principles and Mechanisms** will lay the theoretical groundwork. We will define what makes a collection of functions a vector space, introduce norms and inner products to give these spaces geometric structure, and explore the profound consequences of properties like completeness and the non-equivalence of norms in infinite dimensions.
*   Next, **Applications and Interdisciplinary Connections** will bring the theory to life. We will see how the physics of elasticity, [fluid mechanics](@entry_id:152498), and [plate bending](@entry_id:184758) dictates the choice of specific Sobolev spaces, and how different norms are strategically used to solve practical problems in signal processing, machine learning, and uncertainty quantification.
*   Finally, **Hands-On Practices** will offer a chance to engage directly with these ideas, guiding you through constructing [orthogonal functions](@entry_id:160936), finding best approximations, and verifying the convergence of a Finite Element Method simulation.

By navigating these chapters, you will gain a robust conceptual understanding of the mathematical machinery that powers modern [computational engineering](@entry_id:178146).

## Principles and Mechanisms

In the study and application of computational engineering, physical fields such as temperature, velocity, or stress are represented by functions. To analyze these fields and the differential equations that govern them, it is profoundly useful to treat functions not as individual objects, but as points within a larger, structured collection—a **[function space](@entry_id:136890)**. This chapter introduces the foundational principles of [function spaces](@entry_id:143478) and the tools used to measure size and distance within them, namely **norms** and **inner products**. Understanding these concepts is essential, as they provide the theoretical framework that guarantees the correctness, stability, and convergence of many computational methods.

### Functions as Vectors: The Concept of a Function Space

At its core, a [function space](@entry_id:136890) is a **vector space** whose elements are functions. A set of functions $V$ forms a vector space over the real numbers $\mathbb{R}$ if it satisfies two [closure properties](@entry_id:265485):
1.  **Closure under addition:** If $f$ and $g$ are in $V$, then their pointwise sum $(f+g)(x) = f(x) + g(x)$ is also in $V$.
2.  **Closure under [scalar multiplication](@entry_id:155971):** If $f$ is in $V$ and $\alpha$ is any real number, then the function $(\alpha f)(x) = \alpha f(x)$ is also in $V$.
(These operations must also satisfy the standard vector space axioms, which are inherited from the properties of real numbers).

This abstract definition has direct physical relevance. Consider modeling the temperature distribution $T(x)$ in a room represented by a domain $\Omega \subset \mathbb{R}^3$. One might naively consider the set of all physically possible temperature fields. However, constraints can prevent this set from forming a vector space. For instance, if we consider temperature on an absolute scale (e.g., Kelvin), all temperatures must be non-negative. Let's define the set $S_{\mathrm{abs}} = \{ T: \Omega \to \mathbb{R} \mid T(x) \ge 0 \text{ a.e.} \}$. While the sum of two non-negative functions is non-negative, multiplying a non-negative function by a negative scalar (e.g., $\alpha = -1$) produces a non-positive function, which is not in $S_{\mathrm{abs}}$ (unless the function is identically zero). Thus, $S_{\mathrm{abs}}$ fails the [closure property](@entry_id:136899) for scalar multiplication and is not a vector space [@problem_id:2395874].

A more robust approach in many physical and numerical models is to work with fluctuations around a [reference state](@entry_id:151465). If we fix a reference temperature field $T_{\mathrm{ref}}(x)$ and study the fluctuation field $\theta(x) = T(x) - T_{\mathrm{ref}}(x)$, the set of all possible fluctuations $\theta$ forms a vector space. If $T_1$ and $T_2$ are two possible temperature distributions, their fluctuations are $\theta_1$ and $\theta_2$. The fluctuation corresponding to the sum $T_1+T_2$ is not simply $\theta_1+\theta_2$, but the structure of the fluctuation space itself is a proper vector space. If we consider the space of square-integrable functions, $L^2(\Omega)$, any fluctuation $\theta$ is also in $L^2(\Omega)$, and any linear combination of such fluctuations remains in $L^2(\Omega)$ [@problem_id:2395874].

Boundary conditions also affect the structure of the function space. Consider functions in the Sobolev space $H^1(\Omega)$, which possess square-integrable weak gradients (a concept we will formalize later). The set of functions that are zero on the boundary $\partial\Omega$, denoted $H_0^1(\Omega)$, is a vector space because the sum of two functions that are zero on the boundary is also zero on the boundary, as is any scalar multiple. This is a **[vector subspace](@entry_id:151815)** of $H^1(\Omega)$. In contrast, the set of functions that equal a specific, nonzero temperature $T_b$ on the boundary is not a vector space. If $T_1|_{\partial\Omega} = T_b$ and $T_2|_{\partial\Omega} = T_b$, then $(T_1+T_2)|_{\partial\Omega} = 2T_b$, so the set is not closed under addition. Such a set is an **affine subspace**, a translation of a [vector subspace](@entry_id:151815) (in this case, a translation of $H_0^1(\Omega)$) [@problem_id:2395874].

### Measuring Functions: Norms and Inner Products

Once we establish that a set of functions forms a vector space, we need a way to measure the "size" or "magnitude" of a function. This is the role of a **norm**. A norm on a vector space $V$ is a function $\| \cdot \|: V \to [0, \infty)$ that satisfies three properties for any vectors $f, g \in V$ and any scalar $\alpha \in \mathbb{R}$:

1.  **Positive Definiteness:** $\|f\| \ge 0$, and $\|f\| = 0$ if and only if $f$ is the [zero vector](@entry_id:156189).
2.  **Homogeneity:** $\|\alpha f\| = |\alpha| \|f\|$.
3.  **Triangle Inequality:** $\|f + g\| \le \|f\| + \|g\|$.

A vector space equipped with a norm is called a **[normed vector space](@entry_id:144421)**. A common misconception is that norms must be dimensionless quantities. This is not a mathematical requirement; if a function has physical units (e.g., Kelvin), its norm will typically carry those same units [@problem_id:2395874].

For function spaces, several norms are ubiquitous in engineering:
*   The **supremum norm** (or **[infinity norm](@entry_id:268861)**), $\|f\|_{\infty} = \sup_{x \in \Omega} |f(x)|$, measures the maximum absolute value of the function. It is central to the concept of uniform convergence.
*   The **$L^p$ norms**, for $1 \le p  \infty$, are defined by $\|f\|_{L^p} = \left( \int_{\Omega} |f(x)|^p \,dx \right)^{1/p}$. The two most common are:
    *   The **$L^1$ norm**, $\|f\|_{L^1} = \int_{\Omega} |f(x)| \,dx$, which measures the total "area" under the absolute value of the function.
    *   The **$L^2$ norm**, $\|f\|_{L^2} = \left( \int_{\Omega} |f(x)|^2 \,dx \right)^{1/2}$, which is closely related to concepts of energy or power.

A particularly important class of [normed spaces](@entry_id:137032) are those where the norm is induced by an **inner product**. An inner product $\langle \cdot, \cdot \rangle: V \times V \to \mathbb{R}$ is a bilinear, symmetric, [positive definite](@entry_id:149459) operation. It generalizes the dot product of geometric vectors. The [induced norm](@entry_id:148919) is given by $\|f\| = \sqrt{\langle f, f \rangle}$. The standard $L^2$ norm is induced by the **$L^2$ inner product**:
$$ \langle f, g \rangle_{L^2} = \int_{\Omega} f(x) g(x) \,dx $$
An inner product provides geometric structure, most notably the concept of **orthogonality**: two functions $f$ and $g$ are orthogonal if $\langle f, g \rangle = 0$.

This framework can be generalized. For instance, in [modal analysis](@entry_id:163921), solutions to Sturm-Liouville problems are orthogonal with respect to a **[weighted inner product](@entry_id:163877)** of the form $\langle f,g\rangle_w = \int_a^b f(x)g(x)w(x)\,dx$, where $w(x)$ is a positive weight function [@problem_id:2395850]. Similarly, in heat transfer problems, the **[energy norm](@entry_id:274966)** $\left(\int_{\Omega} k(x) |\nabla \theta(x)|^2 \,dx\right)^{1/2}$, where $k(x)$ is the thermal conductivity, arises naturally from the physics and provides a crucial tool for analysis [@problem_id:2395874].

### Equivalence of Norms and the Challenge of Infinite Dimensions

In [finite-dimensional vector spaces](@entry_id:265491) like $\mathbb{R}^n$, all norms are **equivalent**. This means that if a sequence of vectors converges to zero in one norm, it converges to zero in all other norms. Formally, for any two norms $\|\cdot\|_a$ and $\|\cdot\|_b$, there exist positive constants $C_1$ and $C_2$ such that for every vector $v$,
$$ C_1 \|v\|_a \le \|v\|_b \le C_2 \|v\|_a $$
This equivalence implies that the notion of convergence is the same regardless of which norm we choose.

A fundamental and often surprising feature of infinite-dimensional [function spaces](@entry_id:143478) is that **this is no longer true**. Different norms can induce fundamentally different notions of size and convergence.

To see this, consider the [space of continuous functions](@entry_id:150395) on the interval $[0,1]$, denoted $C([0,1])$, equipped with the supremum norm $\|\cdot\|_{\infty}$ and the $L^1$ norm $\|\cdot\|_{L^1}$. We can construct a [sequence of functions](@entry_id:144875) that demonstrates the non-equivalence of these norms [@problem_id:1859229]. Consider the sequence of "[triangular pulse](@entry_id:275838)" functions $\{f_n\}_{n=2}^\infty$, where each $f_n$ is a triangle of height $n$ and base $2/n$, centered at $x=1/2$.
*   The supremum norm is simply the maximum value of the function: $\|f_n\|_{\infty} = n$.
*   The $L^1$ norm is the area under the curve, which is the area of the triangle: $\|f_n\|_{L^1} = \frac{1}{2} \times \text{base} \times \text{height} = \frac{1}{2} \times \frac{2}{n} \times n = 1$.

The ratio of the norms for this sequence is $\|f_n\|_{\infty} / \|f_n\|_{L^1} = n$. As $n \to \infty$, this ratio grows without bound. This proves that there can be no constant $C_2$ such that $\|f\|_{\infty} \le C_2 \|f\|_{L^1}$ for all $f \in C([0,1])$. The norms are not equivalent. The sequence $\{f_n\}$ is "large" and growing in the supremum norm, but it is "small" (of constant size 1) in the $L^1$ norm. This has profound implications for analysis and computation: specifying convergence in a [function space](@entry_id:136890) requires specifying *which norm* is being used.

### Completeness: Cauchy Sequences and Banach Spaces

A key property of a [normed space](@entry_id:157907) is **completeness**. Intuitively, a space is complete if there are no "holes" or "missing points." This is formalized using the concept of a **Cauchy sequence**. A sequence $\{f_n\}$ is a Cauchy sequence if its elements get arbitrarily close to each other as the sequence progresses, i.e., $\|f_n - f_m\| \to 0$ as $n, m \to \infty$.

A [normed vector space](@entry_id:144421) is **complete** if every Cauchy sequence in the space converges to a limit that is *also in the space*. A complete [normed space](@entry_id:157907) is called a **Banach space**. A complete [inner product space](@entry_id:138414) is called a **Hilbert space**.

Completeness is not an abstract triviality; many intuitive spaces of "nice" functions are, in fact, not complete. Consider the space of continuously differentiable functions on $[-1,1]$, denoted $C^1([-1,1])$, equipped with the [supremum norm](@entry_id:145717) $\|\cdot\|_\infty$. Can a sequence of differentiable functions converge uniformly (i.e., in the supremum norm) to a function that is not differentiable? The answer is yes [@problem_id:2395834].

A classic counterexample involves the sequence $f_n(x) = \sqrt{x^2 + 1/n^2}$. Each function $f_n$ is smooth and continuously differentiable on $[-1,1]$. However, as $n \to \infty$, this sequence converges uniformly to the function $f(x) = \sqrt{x^2} = |x|$. The limit function $f(x)=|x|$ is continuous, but it is not differentiable at $x=0$.
The sequence $\{f_n\}$ is a sequence of elements in $C^1([-1,1])$. It is a Cauchy sequence in the [supremum norm](@entry_id:145717). But its limit, $|x|$, is not in $C^1([-1,1])$. Therefore, the space $(C^1([-1,1]), \|\cdot\|_{\infty})$ is not complete [@problem_id:1850272]. This failure of completeness motivates the development of more comprehensive spaces, such as Sobolev spaces, which "fill in" these holes.

### Key Function Spaces in Engineering

Computational engineering relies on several key types of complete function spaces.

#### The Lebesgue Spaces $L^p(\Omega)$

The Lebesgue space $L^p(\Omega)$ is, roughly speaking, the completion of the [space of continuous functions](@entry_id:150395) under the $L^p$ norm. It contains all functions $f$ for which $\|f\|_{L^p}$ is finite. These spaces are Banach spaces for $1 \le p \le \infty$, and $L^2(\Omega)$ is a Hilbert space.

An important subtlety is that membership in one $L^p$ space does not necessarily imply membership in another, especially on unbounded domains. A canonical example is the normalized **[sinc function](@entry_id:274746)**, $f(x) = \frac{\sin(\pi x)}{\pi x}$, defined on $\mathbb{R}$ [@problem_id:2395885].
*   **Is sinc in $L^1(\mathbb{R})$?** No. The integral of its absolute value, $\int_{-\infty}^{\infty} |\frac{\sin(\pi x)}{\pi x}| \,dx$, diverges. This can be shown by comparison with the harmonic series. Although the function decays, it does not decay fast enough for its absolute value to be integrable.
*   **Is sinc in $L^2(\mathbb{R})$?** Yes. The integral of its square, $\int_{-\infty}^{\infty} \left(\frac{\sin(\pi x)}{\pi x}\right)^2 \,dx$, converges. The integrand decays like $1/x^2$ for large $x$, which is integrable. In fact, using Plancherel's theorem from Fourier analysis, one can show that $\| \text{sinc} \|_{L^2(\mathbb{R})} = 1$.

This example highlights that the choice of $p$ in $L^p(\Omega)$ is critical and reflects different properties of the functions being modeled.

#### The Sobolev Spaces $H^s(\Omega)$

Sobolev spaces are arguably the most important function spaces for the theory of partial differential equations (PDEs). They are designed to handle functions that may not have classical derivatives but possess **[weak derivatives](@entry_id:189356)**. A function $g$ is the [weak derivative](@entry_id:138481) of $f$ if it satisfies the integration-by-parts formula for all smooth "[test functions](@entry_id:166589)" with [compact support](@entry_id:276214).

The Sobolev space $H^1(\Omega)$ consists of all functions in $L^2(\Omega)$ whose weak gradients also belong to $L^2(\Omega)$. It is a Hilbert space equipped with the norm:
$$ \|u\|_{H^1(\Omega)}^2 = \|u\|_{L^2(\Omega)}^2 + \|\nabla u\|_{L^2(\Omega)^d}^2 $$
This norm simultaneously controls the size of the function and the size of its first derivative. Convergence in this space is therefore very strong. If a sequence of approximations $\{u_h\}$ converges to a function $u$ in the $H^1(\Omega)$ norm, meaning $\|u_h - u\|_{H^1(\Omega)} \to 0$, then by the very definition of the norm, two things must happen simultaneously [@problem_id:2395897]:
1.  $\|u_h - u\|_{L^2(\Omega)} \to 0$ (The functions converge in $L^2$).
2.  $\|\nabla u_h - \nabla u\|_{L^2(\Omega)^d} \to 0$ (Their gradients also converge in $L^2$).

This built-in control over derivatives makes Sobolev spaces the natural setting for the weak (or variational) formulations of PDEs that underpin methods like the Finite Element Method (FEM).

#### Dual Spaces and Distributions

For every [normed vector space](@entry_id:144421) $V$, we can define its **[dual space](@entry_id:146945)**, denoted $V'$. The [dual space](@entry_id:146945) is the vector space of all **[bounded linear functionals](@entry_id:271069)** on $V$—that is, all [linear maps](@entry_id:185132) $L: V \to \mathbb{R}$ for which there exists a constant $M$ such that $|L(f)| \le M \|f\|_V$ for all $f \in V$.

A prime example of an object that is best understood as an element of a dual space is the **Dirac delta**, $\delta_{x_0}$ [@problem_id:2395841]. In engineering, this is used to model a [point source](@entry_id:196698), a point load, or an instantaneous impulse. It is often written heuristically as a "function" that is zero everywhere except at $x_0$ and whose integral is one. However, no such classical function exists.

The modern, rigorous definition of the Dirac delta is as a functional. Specifically, it is the **evaluation functional** acting on a space of continuous functions, such as $C([0,1])$. For any continuous function $f \in C([0,1])$, the functional $\delta_{x_0}$ is defined as:
$$ \delta_{x_0}(f) = f(x_0) $$
This mapping is linear. It is also bounded with respect to the supremum norm $\|\cdot\|_\infty$, since $|\delta_{x_0}(f)| = |f(x_0)| \le \sup_{x \in [0,1]} |f(x)| = \|f\|_\infty$. Because it is a [bounded linear functional](@entry_id:143068), $\delta_{x_0}$ is a legitimate element of the [dual space](@entry_id:146945) $C([0,1])^*$ [@problem_id:2395841].

It cannot, however, be represented by integration against an $L^1$ or $L^2$ function. No function $g(x)$ exists such that $f(x_0) = \int_0^1 g(x)f(x)\,dx$ for all continuous $f$. If such a $g$ existed, it would have to be zero [almost everywhere](@entry_id:146631), which would make the integral zero, a contradiction. Furthermore, point evaluation is not a bounded functional on $L^2([0,1])$, as one can construct a sequence of $L^2$-bounded functions whose value at $x_0$ grows infinitely large. The proper mathematical object representing $\delta_{x_0}$ is a **measure**—the unit point mass at $x_0$—which is not a function [@problem_id:2395841]. These objects, often called **distributions**, live in dual spaces.

### Applications in Computational Engineering

The abstract machinery of function spaces provides the practical foundation for designing and analyzing computational methods.

#### Approximation Theory and Orthogonal Projections

A central problem in [computational engineering](@entry_id:178146) is to approximate a complex function $v$ (e.g., the exact solution of a PDE) by a simpler function $s^\star$ from a chosen subspace $S$ (e.g., the space of [piecewise polynomials](@entry_id:634113) used in FEM). The "best" approximation is the one that minimizes the error, $\|v - s\|$. When the norm is induced by an inner product (i.e., in a Hilbert space), this problem has an elegant geometric solution.

The **Projection Theorem** states that if $S$ is a [closed subspace](@entry_id:267213) of a Hilbert space $H$, then for any $v \in H$, there exists a unique best approximation $s^\star \in S$. This best approximation is uniquely characterized by the **Orthogonality Principle**: the error vector $(v - s^\star)$ must be orthogonal to every vector in the subspace $S$ [@problem_id:2395838].
$$ \langle v - s^\star, s \rangle = 0 \quad \text{for all } s \in S $$
This principle is the cornerstone of many approximation methods. For example, in a finite-dimensional subspace $S = \text{span}\{s_1, \dots, s_k\}$, the principle reduces to a system of linear equations for the coefficients of the approximation. For the weighted least-squares problem in $\mathbb{R}^m$ with inner product $\langle x,y \rangle_W = x^\top W y$, the [orthogonality principle](@entry_id:195179) directly yields the famous **[normal equations](@entry_id:142238)** $A^\top W A c^\star = A^\top W b$ for the [best approximation](@entry_id:268380) $s^\star = A c^\star$ to a vector $b$ [@problem_id:2395838].

As a concrete example, finding the [best linear approximation](@entry_id:164642) $p^\star(x)=ax+b$ to the function $v(x)=x^2$ on $[0,1]$ in the $L^2$ norm involves enforcing that the error $x^2 - (ax+b)$ is orthogonal to the basis functions $\{1, x\}$. This yields a system of two [linear equations](@entry_id:151487) for $a$ and $b$, whose solution is $(a,b) = (1, -1/6)$, giving the best approximation $p^\star(x) = x - 1/6$ [@problem_id:2395838].

#### Guarantees for PDE Solvers: The Lax-Milgram Theorem

The [weak formulation](@entry_id:142897) of many [boundary-value problems](@entry_id:193901) takes the abstract form: find $u \in V$ such that $a(u,v) = \ell(v)$ for all $v \in V$. Here, $V$ is a Hilbert space (like $H_0^1(\Omega)$), $a(\cdot,\cdot)$ is a [bilinear form](@entry_id:140194) related to the PDE operator, and $\ell(\cdot)$ is a [linear functional](@entry_id:144884) related to the source term.

The **Lax-Milgram Theorem** provides a powerful guarantee for the existence and uniqueness of a solution to this problem. It states that a unique solution exists if three conditions are met [@problem_id:2395836]:
1.  **Continuity of $a(\cdot,\cdot)$**: The [bilinear form](@entry_id:140194) is bounded, i.e., $|a(u,v)| \le M \|u\|_V \|v\|_V$ for some constant $M$. This ensures the operator is not "too large."
2.  **Coercivity of $a(\cdot,\cdot)$**: The bilinear form is bounded below, i.e., $a(v,v) \ge \alpha \|v\|_V^2$ for some constant $\alpha  0$. This condition, also called $V$-[ellipticity](@entry_id:199972), ensures the problem is well-posed and prevents [zero-energy modes](@entry_id:172472).
3.  **Continuity of $\ell(\cdot)$**: The [linear functional](@entry_id:144884) is bounded, i.e., $|\ell(v)| \le C \|v\|_V$. This means the source term corresponds to a finite "energy."

For a diffusion-reaction equation like $-\nabla \cdot (k \nabla u) + cu = f$, with appropriate assumptions on the coefficients ($k(x) \ge k_0  0$, $c(x) \ge c_0  0$) and the [source term](@entry_id:269111) ($f \in L^2(\Omega)$), one can rigorously verify that the corresponding bilinear and linear forms satisfy these three conditions on $V=H_0^1(\Omega)$. The Lax-Milgram theorem then not only guarantees a unique weak solution exists but also provides an *a priori* [stability estimate](@entry_id:755306), $\|u\|_V \le \frac{1}{\alpha} \|\ell\|_{V'}$, which is fundamental to proving the convergence of numerical methods like FEM [@problem_id:2395836].

#### Bases for Function Spaces and Spectral Methods

Just as the vector space $\mathbb{R}^3$ is spanned by the basis vectors $\{\mathbf{i}, \mathbf{j}, \mathbf{k}\}$, infinite-dimensional [function spaces](@entry_id:143478) can also be spanned by a **basis of functions**. If the basis functions are mutually orthogonal, they form an especially powerful tool for representing other functions as a series expansion.

A prime source of such bases comes from the eigenfunctions of **Sturm-Liouville problems**, which are second-order linear [eigenvalue problems](@entry_id:142153) of the form $L[y] = \lambda w y$ subject to self-adjoint boundary conditions. Sturm-Liouville theory guarantees that for a regular problem on a finite interval, the resulting eigenfunctions $\{y_n\}$ are mutually orthogonal with respect to the [weighted inner product](@entry_id:163877) defined by the weight function $w(x)$. After normalization, these [eigenfunctions](@entry_id:154705) form a **complete orthonormal basis** for the Hilbert space $L^2_w([a,b])$ [@problem_id:2395850]. This means any function $f$ in this space can be represented as a generalized Fourier series $f = \sum c_n y_n$, where the coefficients are found by projection: $c_n = \langle f, y_n \rangle_w$.

The most famous example is the standard Fourier series on $[-\pi, \pi]$, where the basis functions are $\{\sin(kx), \cos(kx)\}$. The efficiency of representing a function with such a series is intimately tied to the function's smoothness. A key result of Fourier analysis is that the faster the Fourier coefficients $\hat{f}(k)$ decay as the frequency $|k| \to \infty$, the smoother the function $f$ is. Specifically, if $|\hat{f}(k)|$ decays like $|k|^{-p}$, this implies a certain number of continuous derivatives for $f$. For example, if $|\hat{f}(k)| \le C(1+|k|)^{-3}$, this rate of decay is sufficient to prove that the function is continuously differentiable, $f \in C^1$, but not necessarily twice continuously differentiable, $f \notin C^2$ [@problem_id:2395896]. This principle is the theoretical engine behind **spectral methods**, which achieve extremely rapid ("exponential") convergence for problems with smooth solutions by representing them in a basis of infinitely differentiable functions (like Fourier series or Chebyshev polynomials).