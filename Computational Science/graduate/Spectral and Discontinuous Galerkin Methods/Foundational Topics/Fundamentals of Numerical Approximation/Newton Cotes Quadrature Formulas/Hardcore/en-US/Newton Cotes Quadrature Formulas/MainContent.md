## Introduction
Numerical integration is a fundamental pillar of computational science, essential for solving problems ranging from calculating physical work to assembling operators in advanced numerical schemes. Among the families of methods for approximating [definite integrals](@entry_id:147612), Newton-Cotes quadrature formulas stand out for their conceptual simplicity, based on the intuitive idea of integrating a polynomial interpolant over [equispaced points](@entry_id:637779). However, this apparent simplicity masks a critical trade-off between order and stability that has profound implications for modern [high-order methods](@entry_id:165413) like spectral and Discontinuous Galerkin (DG) techniques. This article addresses the crucial knowledge gap between the straightforward construction of Newton-Cotes rules and the complex reasons for their limitations in demanding applications.

Over the next chapters, you will embark on a comprehensive exploration of these foundational methods. The "Principles and Mechanisms" chapter will deconstruct the formulas, from their basis in interpolatory quadrature to a rigorous analysis of their precision and the instability that leads to negative weights. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate their use in fields like physics and economics, and critically examine their role within DG methods for tasks such as [mass lumping](@entry_id:175432) and overintegration, contrasting them with more robust alternatives. Finally, the "Hands-On Practices" section will offer practical exercises to solidify your understanding of their theoretical properties and practical consequences. We begin by delving into the core principles that govern the construction and behavior of all Newton-Cotes [quadrature rules](@entry_id:753909).

## Principles and Mechanisms

The approximation of [definite integrals](@entry_id:147612) is a cornerstone of numerical methods for [partial differential equations](@entry_id:143134), and it assumes a particularly central role in the formulation of spectral and discontinuous Galerkin (DG) methods. Within each element of a [computational mesh](@entry_id:168560), the assembly of discrete operators, such as [mass and stiffness matrices](@entry_id:751703), requires the evaluation of integrals involving basis functions and their derivatives. Newton-Cotes quadrature formulas represent one of the most conceptually straightforward families of methods for this task. They are built upon the intuitive idea of replacing the integrand with a simpler function—a polynomial—that can be integrated exactly. While their simplicity is appealing, a deeper investigation reveals [critical properties](@entry_id:260687) and limitations that have profound consequences for the stability and accuracy of high-order [numerical schemes](@entry_id:752822). This chapter elucidates the principles underlying the construction of Newton-Cotes rules, analyzes their properties, and examines the mechanisms through which their limitations manifest in practical applications.

### The Interpolatory Quadrature Principle

The fundamental principle of any Newton-Cotes formula is that of **interpolatory quadrature**. The core idea is to approximate the integral of a function $f(x)$ over an interval $[a, b]$ by integrating a polynomial that interpolates $f(x)$ at a set of prescribed points, known as **quadrature nodes**.

Let us consider a set of $n+1$ distinct nodes $\{x_j\}_{j=0}^n$ within the interval $[a, b]$. We can construct a unique polynomial of degree at most $n$, denoted $p_n(x)$, that agrees with the function $f(x)$ at these nodes, i.e., $p_n(x_j) = f(x_j)$ for all $j \in \{0, 1, \dots, n\}$. The [quadrature rule](@entry_id:175061) is then defined as the exact integral of this [interpolating polynomial](@entry_id:750764):

$$
\int_a^b f(x) \,dx \approx \int_a^b p_n(x) \,dx
$$

To derive the familiar weighted sum form of a quadrature rule, we express the [interpolating polynomial](@entry_id:750764) $p_n(x)$ in the **Lagrange basis**. The Lagrange basis polynomials, $\{\ell_j(x)\}_{j=0}^n$, are polynomials of degree $n$ defined by the property $\ell_j(x_i) = \delta_{ij}$, where $\delta_{ij}$ is the Kronecker delta. The interpolant $p_n(x)$ can thus be written as:

$$
p_n(x) = \sum_{j=0}^n f(x_j) \ell_j(x)
$$

Substituting this into the integral and exploiting the linearity of the [integration operator](@entry_id:272255), we obtain the quadrature formula:

$$
\int_a^b p_n(x) \,dx = \int_a^b \left( \sum_{j=0}^n f(x_j) \ell_j(x) \right) dx = \sum_{j=0}^n f(x_j) \left( \int_a^b \ell_j(x) \,dx \right)
$$

This gives the general form of an interpolatory quadrature rule, $\sum_{j=0}^n w_j f(x_j)$, where the **[quadrature weights](@entry_id:753910)** $w_j$ are defined as the integrals of the corresponding Lagrange basis polynomials:

$$
w_j = \int_a^b \ell_j(x) \,dx
$$

Crucially, the weights $w_j$ depend only on the choice of nodes $\{x_j\}$ and the interval $[a,b]$, not on the function $f(x)$ being integrated. This construction ensures by definition that the quadrature rule is exact for any polynomial of degree up to $n$.

### Closed and Open Newton-Cotes Formulas

Newton-Cotes formulas are a specific class of interpolatory [quadrature rules](@entry_id:753909) where the nodes are equispaced. There are two main families, distinguished by whether the endpoints of the interval are included as nodes.

#### Closed Newton-Cotes Rules

A **closed Newton-Cotes rule** of order $n$ (often referred to as using $n+1$ points) is constructed using $n+1$ [equispaced nodes](@entry_id:168260) that include the endpoints of the interval $[a, b]$. The spacing between nodes is $h = (b-a)/n$, and the nodes are given by:

$$
x_j = a + jh, \quad j = 0, 1, \dots, n
$$

The weights are defined precisely as $w_j = \int_a^b \ell_j(x) \,dx$, where $\ell_j(x)$ are the Lagrange basis polynomials for this specific set of nodes . In the context of spectral and DG methods, it is standard practice to derive these weights on a reference interval, typically $[-1, 1]$, and then scale them for any physical element $[a, b]$. Using the affine map $x(\xi) = \frac{b-a}{2}\xi + \frac{a+b}{2}$, the nodes on the reference interval are $\xi_j = -1 + 2j/n$. The weights on the physical element can be related to the reference weights $\hat{w}_j = \int_{-1}^1 \hat{\ell}_j(\xi) \,d\xi$ by:

$$
w_j = \frac{b-a}{2} \hat{w}_j = \frac{b-a}{2} \int_{-1}^1 \hat{\ell}_j(\xi) \,d\xi
$$

A more general formula for the weights can be derived from first principles by mapping to a reference grid of integers $[0, n]$ . With a [change of variables](@entry_id:141386) $x = a + \xi \frac{b-a}{n}$, the weight $w_i$ can be expressed as:

$$
w_i = \frac{b-a}{n} \frac{(-1)^{n-i}}{i!(n-i)!} \int_0^n \left( \prod_{j=0, j\neq i}^n (\xi-j) \right) d\xi
$$

This expression cleanly separates the scaling factor $(b-a)$ from the geometric part that depends only on the structure of the equispaced grid. Well-known examples of closed Newton-Cotes rules include the Trapezoidal rule ($n=1$) and Simpson's rule ($n=2$).

#### Open Newton-Cotes Rules

In contrast, an **open Newton-Cotes rule** uses nodes that are equispaced in the interior of the interval $(a, b)$, excluding the endpoints. For an $m$-point rule, the interval is divided into $m+1$ subintervals of width $h = (b-a)/(m+1)$. The nodes are:

$$
x_j = a + jh, \quad j = 1, 2, \dots, m
$$

The construction principle remains the same: the weights are the integrals of the Lagrange basis polynomials of degree $m-1$ built on these interior nodes. The most elementary example is the Midpoint rule ($m=1$). As explored in , the exclusion of endpoints has significant operational consequences in DG methods. Since values at element boundaries are needed to compute numerical fluxes, using an open [quadrature rule](@entry_id:175061) for [volume integrals](@entry_id:183482) necessitates a separate step to evaluate the solution at the element faces, as these points are not part of the quadrature node set.

### Degree of Precision and Error Analysis

The **algebraic [degree of precision](@entry_id:143382)** of a [quadrature rule](@entry_id:175061) is the highest degree of polynomial that the rule integrates exactly. By construction, an $(n+1)$-point interpolatory [quadrature rule](@entry_id:175061) has a [degree of precision](@entry_id:143382) of at least $n$. A remarkable feature of Newton-Cotes rules, however, is that this degree can sometimes be higher, an enhancement that arises directly from symmetry .

Consider a closed Newton-Cotes rule on the symmetric interval $[-1, 1]$. The [equispaced nodes](@entry_id:168260) are symmetric with respect to the origin (i.e., if $x_j$ is a node, so is $-x_j$), and this implies the weights are also symmetric ($w_j = w_{n-j}$). The error for an interpolatory rule applied to a polynomial of degree $n+1$ is proportional to the integral of the node polynomial, $\Pi_{n+1}(x) = \prod_{j=0}^n (x-x_j)$.

Let us analyze the parity of $\Pi_{n+1}(x)$:
$$
\Pi_{n+1}(-x) = \prod_{j=0}^n (-x-x_j) = (-1)^{n+1} \prod_{j=0}^n (x+x_j)
$$
Due to the symmetry of the node set, $\{x_j\} = \{-x_j\}$, the product $\prod(x+x_j)$ is identical to $\prod(x-x_j)$. Thus, $\Pi_{n+1}(-x) = (-1)^{n+1}\Pi_{n+1}(x)$.

*   If **$n$ is even**, $n+1$ is odd. Then $\Pi_{n+1}(x)$ is an odd function. The integral of an odd function over a symmetric interval is zero. This means the rule is exact for $x^{n+1}$. For example, Simpson's rule ($n=2$) has nodes $\{-1, 0, 1\}$ and is exact not just for degree 2 polynomials, but also for degree 3. Its [degree of precision](@entry_id:143382) is $3$.

*   If **$n$ is odd**, $n+1$ is even. Then $\Pi_{n+1}(x)$ is an [even function](@entry_id:164802). Its integral over $[-1, 1]$ is generally non-zero. The rule is not exact for $x^{n+1}$. For example, the Trapezoidal rule ($n=1$) has nodes $\{-1, 1\}$ and is exact only up to degree 1.

This parity-dependent behavior means the [degree of precision](@entry_id:143382) for a closed $(n+1)$-point rule is $n+1$ if $n$ is even, and $n$ if $n$ is odd . This can be expressed compactly as $m(n) = n + \frac{1+(-1)^n}{2}$. A similar analysis applies to open Newton-Cotes rules, where the [degree of precision](@entry_id:143382) is $m$ if $m$ is odd and $m-1$ if $m$ is even .

The error of the quadrature rule can be expressed using the Peano Kernel Theorem. For a function $f \in C^{q+1}[a,b]$, where $q$ is the [degree of precision](@entry_id:143382), the error takes the form:
$$
E(f) = C_n (b-a)^{q+2} f^{(q+1)}(\xi), \quad \text{for some } \xi \in (a,b)
$$
The constant $C_n$ and the order of the derivative, $q+1$, depend on $n$ and its parity, reflecting the [degree of precision](@entry_id:143382) . The "free" order of precision gained when $n$ is even translates into an error term involving a higher derivative of $f$, often leading to better accuracy for smooth functions.

### The Instability of High-Order Rules

The ability to construct Newton-Cotes rules of arbitrarily high degree might suggest a path to ever-increasing accuracy. However, this is a treacherous path. High-order Newton-Cotes rules based on [equispaced nodes](@entry_id:168260) are notoriously unstable, a phenomenon that renders them unsuitable for practical high-order methods. This instability manifests in several related ways.

#### Negative Weights and the Runge Phenomenon

A key sign of trouble is the appearance of **[negative quadrature weights](@entry_id:752399)**. While the rules for small $n$ (like Trapezoidal and Simpson's) have strictly positive weights, it is a well-established fact that for closed Newton-Cotes rules, negative weights first appear for $n=8$. For $n \ge 8$ (with the exception of $n=9$), at least one weight is negative .

The existence of negative weights has a devastating consequence: it breaks the positivity property of the integral. The integral of a non-negative function is always non-negative. A quadrature rule with positive weights preserves this property. However, if a weight $w_k$ is negative, one can construct a non-negative function $f(x)$ that is positive at $x_k$ and zero at all other nodes. For such a function, the true integral is positive, but the quadrature approximation $\sum w_j f(x_j) = w_k f(x_k)$ is negative. This qualitative failure is unacceptable in scientific computing.

This instability is a direct consequence of the **Runge phenomenon** for [polynomial interpolation](@entry_id:145762) on [equispaced nodes](@entry_id:168260). For large $n$, the Lagrange basis polynomials $\ell_j(x)$ exhibit wild oscillations near the endpoints of the interval. Since the weights are the integrals of these polynomials, $w_j = \int \ell_j(x) \,dx$, the large negative lobes of the oscillating polynomials can lead to a negative net area, and thus a negative weight .

Furthermore, for a sequence of interpolatory [quadrature rules](@entry_id:753909) to converge to the true integral for any continuous function, a theorem by Pólya and Steklov states that the sum of the [absolute values](@entry_id:197463) of the weights must be uniformly bounded. For closed Newton-Cotes rules, this sum diverges as $n \to \infty$:

$$
\sum_{j=0}^{n} |w_j^{(n)}| \to \infty \quad \text{as } n \to \infty
$$

This divergence implies that the quadrature operator is ill-conditioned. Small errors in the function values $f(x_j)$ can be massively amplified, making the result unreliable.

#### Ill-Conditioning of the Defining System

An alternative way to derive the weights is by enforcing [exactness](@entry_id:268999) for the monomials $x^0, x^1, \dots, x^n$. This leads to a system of linear equations $V^T w = m$, where $V$ is a **Vandermonde matrix** with entries $V_{ij} = x_i^j$ and $m$ is a vector of moments $m_j = \int x^j dx$. Vandermonde matrices based on [equispaced nodes](@entry_id:168260) are notoriously ill-conditioned. The condition number of this matrix, which measures the sensitivity of the solution (the weights $w$) to perturbations, grows exponentially with $n$. A rigorous analysis shows that the [1-norm](@entry_id:635854) condition number $\kappa_1(V)$ for nodes on $[-1,1]$ is bounded below by an expression that grows asymptotically like $(e/2)^n$ . This exponential growth provides a formal linear-algebraic confirmation of the inherent instability of constructing high-order Newton-Cotes weights.

### Implications for DG and Spectral Methods

In the context of DG and [spectral methods](@entry_id:141737), the instability of high-order Newton-Cotes rules is not merely an academic curiosity; it is a fatal flaw. The stability of these methods, particularly for time-dependent problems, often relies on proving that a discrete "energy" does not grow in time. This, in turn, requires the construction of a discrete inner product $(\cdot, \cdot)_Q$ and its associated norm that are equivalent to the continuous $L^2$ inner product.

A discrete inner product based on quadrature is defined as:
$$
(u, v)_Q = \sum_{j=0}^N w_j u(x_j) v(x_j)
$$
For this to define a valid norm $\sqrt{(u,u)_Q}$, the bilinear form must be **[positive definite](@entry_id:149459)**, meaning $(u,u)_Q > 0$ for any non-zero polynomial $u$. If any weight $w_k$ is negative, this property is immediately violated. By choosing a polynomial $u$ from the nodal basis, such as $u = \ell_k(x)$, we find that $(u,u)_Q = (\ell_k, \ell_k)_Q = w_k  0$. Since the discrete [quadratic form](@entry_id:153497) is not positive definite, it cannot be used to define a norm, and any [energy stability](@entry_id:748991) proof that relies on it collapses .

This problem is particularly clear when one considers the **[mass matrix](@entry_id:177093)**. In a nodal DG or [spectral element method](@entry_id:175531) where the basis functions are the Lagrange polynomials $\{\ell_j\}$ associated with the quadrature nodes, the mass matrix entries computed with this quadrature are:
$$
M_{ij} = (\ell_i, \ell_j)_Q = \sum_{k=0}^N w_k \ell_i(x_k) \ell_j(x_k) = \sum_{k=0}^N w_k \delta_{ik} \delta_{jk} = w_i \delta_{ij}
$$
The [mass matrix](@entry_id:177093) becomes diagonal with the [quadrature weights](@entry_id:753910) as its entries. A [symmetric positive definite](@entry_id:139466) mass matrix is essential for the stability of many [explicit time-stepping](@entry_id:168157) schemes. If any weight $w_i$ is negative, the mass matrix is not positive definite, which can lead to catastrophic, non-physical growth in the numerical solution .

For these reasons, high-order Newton-Cotes rules are almost never used in modern spectral or DG codes. The preferred alternatives are [quadrature rules](@entry_id:753909) that guarantee positive weights for any order, such as **Gauss-Legendre** or **Gauss-Lobatto** quadrature. These methods sacrifice the simplicity of [equispaced nodes](@entry_id:168260) for the crucial property of stability. In particular, quadratures with positive weights are compatible with the construction of **Summation-By-Parts (SBP)** operators, which provide a systematic framework for developing provably energy-[stable numerical schemes](@entry_id:755322) . The study of Newton-Cotes formulas thus serves as a powerful lesson: seemingly intuitive constructions in [numerical analysis](@entry_id:142637) must be rigorously interrogated for stability, as the consequences for complex applications can be profound.