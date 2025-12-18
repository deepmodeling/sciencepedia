## Introduction
The power of spectral and discontinuous Galerkin (DG) methods lies in their ability to achieve [high-order accuracy](@entry_id:163460) for the numerical solution of [partial differential equations](@entry_id:143134). This accuracy is rooted in the [weak formulation](@entry_id:142897), which transforms the differential equation into a system of [integral equations](@entry_id:138643) over each element in the computational domain. While this formulation is mathematically elegant, the practical challenge remains: how do we compute these integrals efficiently and accurately? For all but the simplest cases, analytical integration is intractable, creating a knowledge gap that must be filled by robust [numerical integration](@entry_id:142553), or quadrature, techniques.

This article serves as a guide to the specialized [spectral integration](@entry_id:755177) techniques that are the computational engine of modern high-order methods. By mastering these concepts, you will gain the ability to build [numerical schemes](@entry_id:752822) that are not only accurate but also stable and computationally efficient. Across the following chapters, you will embark on a journey from fundamental principles to real-world applications.

*   In **Principles and Mechanisms**, we will dissect the core [quadrature rules](@entry_id:753909), such as Gaussian and Clenshaw-Curtis quadrature. You will learn how their construction maximizes accuracy and how their choice profoundly impacts the structure of system matrices through concepts like [mass lumping](@entry_id:175432), aliasing, and the stability-enforcing Summation-by-Parts property.

*   In **Applications and Interdisciplinary Connections**, we will explore how these integration techniques are applied to tackle complex simulations in fields like computational fluid dynamics and materials science. You will see how they enable accurate modeling on complex geometries and are essential for ensuring physical conservation laws and numerical stability.

*   Finally, **Hands-On Practices** will provide you with the opportunity to solidify your understanding by working through concrete problems that highlight the [critical properties](@entry_id:260687) and trade-offs of different integration strategies.

We begin by establishing the mathematical foundations of these essential computational tools.

## Principles and Mechanisms

The implementation of spectral and discontinuous Galerkin methods relies fundamentally on the accurate and efficient evaluation of integrals over each element in the computational domain. These integrals, which arise from the weak formulation of a [partial differential equation](@entry_id:141332), typically involve products of basis functions, their derivatives, and problem-specific coefficients. While these integrals can sometimes be computed analytically for simple cases, this approach is often intractable or computationally prohibitive for general problems, especially those involving nonlinear terms or complex geometries. Consequently, [numerical integration](@entry_id:142553), or **quadrature**, stands as a cornerstone of practical spectral and DG methods. This chapter explores the principles and mechanisms of the specialized quadrature techniques that are central to the [high-order accuracy](@entry_id:163460) and stability of these methods.

### Gaussian Quadrature: Maximizing Polynomial Exactness

The primary objective of a [numerical quadrature](@entry_id:136578) rule is to approximate a [definite integral](@entry_id:142493) with a weighted sum of the integrand's values at a [discrete set](@entry_id:146023) of points, known as **quadrature nodes** (or points). For an integral over the reference interval $[-1, 1]$, the general form is:
$$
\int_{-1}^{1} f(x) \, dx \approx \sum_{j=1}^{N} w_j f(x_j)
$$
where $\{x_j\}_{j=1}^N$ are the nodes and $\{w_j\}_{j=1}^N$ are the corresponding **[quadrature weights](@entry_id:753910)**. The power of a [quadrature rule](@entry_id:175061) is measured by its **[degree of exactness](@entry_id:175703)**, which is the highest degree of a polynomial that the rule can integrate exactly.

For a rule with $N$ nodes, we have $2N$ free parameters to choose: the $N$ nodes and the $N$ weights. It is natural to ask how these parameters can be selected to achieve the highest possible [degree of exactness](@entry_id:175703). The family of **Gaussian quadrature** rules is the answer to this question. The core idea is that by strategically placing the nodes, one can achieve a [degree of exactness](@entry_id:175703) of $2N-1$. This remarkable result is achieved when the quadrature nodes are chosen to be the roots of the $N$-th degree polynomial from a family of orthogonal polynomials associated with the integration domain and a given weight function. For the unweighted inner product on $[-1, 1]$, the relevant orthogonal polynomials are the Legendre polynomials.

The family of Gauss-type quadratures based on Legendre polynomials can be categorized by the constraints placed on the inclusion of the interval endpoints, $\pm 1$ .

*   **Gauss-Legendre Quadrature:** This rule imposes no constraints on the node locations, using all $2N$ degrees of freedom to maximize accuracy. The optimal choice for the $N$ nodes is the set of roots of the degree-$N$ Legendre polynomial, $P_N(x)$. These roots are all real, distinct, and lie strictly within the open interval $(-1, 1)$. This rule is often called simply "Gauss quadrature". It achieves the maximal possible [degree of exactness](@entry_id:175703), which is $2N-1$.

*   **Gauss-Lobatto-Legendre (GLL) Quadrature:** This rule pre-assigns two nodes to be at the endpoints, $x = -1$ and $x = 1$. The remaining $N-2$ interior nodes are chosen to maximize the [degree of exactness](@entry_id:175703) under this constraint. The optimal locations for these interior nodes are the roots of $P'_{N-1}(x)$, the first derivative of the Legendre polynomial of degree $N-1$. With $N$ total points (including the two fixed endpoints), the GLL rule has a [degree of exactness](@entry_id:175703) of $2N-3$. This rule is exceptionally important in nodal DG and [spectral element methods](@entry_id:755171) because the inclusion of endpoints simplifies inter-element communication and the imposition of boundary conditions.

*   **Gauss-Radau Quadrature:** This rule represents an intermediate case where exactly one endpoint is pre-assigned as a node (e.g., $x = -1$). The remaining $N-1$ nodes are then chosen optimally. These $N$ nodes are the roots of the polynomial $P_N(x) + P_{N-1}(x)$ (if the fixed node is at $x=-1$) or $P_N(x) - P_{N-1}(x)$ (if the fixed node is at $x=1$). This rule has a [degree of exactness](@entry_id:175703) of $2N-2$.

The trade-off is clear: for a fixed number of points $N$, including endpoints as nodes reduces the degree of [polynomial exactness](@entry_id:753577). However, the practical benefits of having nodes at element boundaries often make Gauss-Lobatto-Legendre quadrature the preferred choice in many high-order methods.

### Clenshaw-Curtis Quadrature: A Fast Transform-Based Alternative

An alternative approach to constructing a high-order [quadrature rule](@entry_id:175061) is to first approximate the integrand $f(x)$ with a polynomial interpolant and then integrate this interpolant exactly. **Clenshaw-Curtis quadrature** is a prominent method based on this idea .

The method proceeds by interpolating the function $f(x)$ at the $N+1$ **Chebyshev-Lobatto** nodes, which are the [extrema](@entry_id:271659) of the degree-$N$ Chebyshev polynomial of the first kind, $T_N(x)$, given by $x_j = \cos(\frac{\pi j}{N})$ for $j=0, 1, \dots, N$. The resulting degree-$N$ polynomial interpolant, expressed in the basis of Chebyshev polynomials, is then integrated analytically from $-1$ to $1$.

A key advantage of Clenshaw-Curtis quadrature is its computational efficiency. The coefficients of the Chebyshev interpolant can be computed from the function values at the nodes via a **Discrete Cosine Transform (DCT)**. Specifically, because the Chebyshev-Lobatto grid includes the endpoints, the appropriate transform is the **DCT of type I (DCT-I)** . Since the DCT can be computed rapidly using algorithms based on the Fast Fourier Transform (FFT) in $\mathcal{O}(N \log N)$ operations, the entire quadrature sum can also be evaluated very quickly. This is in contrast to Gauss-Legendre quadrature, for which no equally fast transform-based method is available.

While an $(N+1)$-point Gauss-Legendre rule has a higher [degree of exactness](@entry_id:175703) ($2N+1$) than an $(N+1)$-point Clenshaw-Curtis rule (which is exact only for polynomials of degree $N$), for smooth, well-resolved functions, both methods exhibit [exponential convergence](@entry_id:142080). The practical advantages of nested nodes (the nodes for a $2N$-point rule include all the nodes from the $N$-point rule) and the fast transform implementation make Clenshaw-Curtis an attractive option, particularly in [pseudospectral methods](@entry_id:753853). It is important to note that although both GLL and Clenshaw-Curtis are Lobatto-type quadratures (i.e., they include endpoints), their interior nodes and weights are different, as GLL nodes are derived from roots of derivatives of Legendre polynomials, while Clenshaw-Curtis nodes are [extrema](@entry_id:271659) of Chebyshev polynomials .

### Quadrature and the Discontinuous Galerkin Mass Matrix

In the context of DG methods, [quadrature rules](@entry_id:753909) are essential for computing the entries of the elemental **mass matrix**, $M$, whose entries are defined by the $L^2$ inner product of basis functions: $M_{ij} = \int_{K} \varphi_i(x) \varphi_j(x) \, dx$. The choice of both the polynomial basis $\{\varphi_i\}$ and the quadrature rule profoundly impacts the structure and accuracy of the resulting computed mass matrix, which we denote $M^h$.

#### Modal Basis and Orthonormality

A **[modal basis](@entry_id:752055)** consists of a set of polynomials that are orthogonal with respect to the $L^2$ inner product. For the interval $[-1, 1]$, the canonical choice is the Legendre polynomials, $\{P_k(x)\}$. These polynomials arise as the [eigenfunctions](@entry_id:154705) of a Sturm-Liouville problem, which guarantees their orthogonality . Specifically, they satisfy:
$$
\int_{-1}^{1} P_m(x) P_n(x) \, dx = \frac{2}{2n+1} \delta_{mn}
$$
where $\delta_{mn}$ is the Kronecker delta. By scaling these polynomials to be orthonormal, creating a basis $\{\psi_k\}$, the exact mass matrix becomes the identity matrix, $M=I$. If we compute this mass matrix using a [quadrature rule](@entry_id:175061) that is exact for all products $\psi_i(x) \psi_j(x)$, the computed matrix $M^h$ will also be the identity. Since $\psi_i$ and $\psi_j$ are polynomials of degree up to $N$ (for a basis of $\mathbb{P}^N$), their product has degree up to $2N$. Therefore, any [quadrature rule](@entry_id:175061) with a [degree of precision](@entry_id:143382) of at least $2N$ (for example, an $(N+1)$-point Gauss-Legendre rule) will yield the exact identity mass matrix .

#### Nodal Basis and Mass Lumping

A **nodal basis** is constructed using Lagrange polynomials $\{\ell_i\}_{i=0}^N$ associated with a set of interpolation nodes $\{x_j\}_{i=0}^N$. This basis is defined by the cardinal property $\ell_i(x_j) = \delta_{ij}$. A remarkable and computationally vital phenomenon occurs when the quadrature nodes are chosen to be the *same* as the interpolation nodes of the Lagrange basis. In this case, the computed [mass matrix](@entry_id:177093) becomes diagonal. This is known as **[mass lumping](@entry_id:175432)**. The entries of the computed [mass matrix](@entry_id:177093) $M^h$ are:
$$
M^h_{ij} = \sum_{q=0}^{N} w_q \ell_i(x_q) \ell_j(x_q) = \sum_{q=0}^{N} w_q \delta_{iq} \delta_{jq} = w_i \delta_{ij}
$$
The resulting [mass matrix](@entry_id:177093) $M^h$ is diagonal with the [quadrature weights](@entry_id:753910) as its diagonal entries. This diagonal structure is highly desirable as it makes the matrix trivial to invert, greatly simplifying [time-stepping schemes](@entry_id:755998).

It is crucial, however, to distinguish between a computed diagonal matrix and the exact mass matrix .
- If one uses an $(N+1)$-point Lagrange basis on the Gauss-Legendre nodes and the corresponding $(N+1)$-point GL quadrature, the integrand $\ell_i(x)\ell_j(x)$ has degree at most $2N$. The GL rule is exact up to degree $2N+1$, so the quadrature is exact. In this specific case, the computed [diagonal matrix](@entry_id:637782) *is* the exact [mass matrix](@entry_id:177093).
- In the more common DG practice of using a Lagrange basis on the $(N+1)$-point Gauss-Lobatto-Legendre nodes with the GLL quadrature, [mass lumping](@entry_id:175432) still occurs and $M^h$ is diagonal. However, the GLL rule is only exact for polynomials of degree up to $2(N+1)-3 = 2N-1$. Since the product of two degree-$N$ Lagrange polynomials can have degree $2N$, the quadrature is not exact. The resulting diagonal matrix $M^h$ is an *approximation* to the true (and generally full) [mass matrix](@entry_id:177093) $M$. While this introduces a [quadrature error](@entry_id:753905), the computational benefit of a [diagonal mass matrix](@entry_id:173002) is often considered a worthwhile trade-off.

### Extensions to Higher Dimensions and General Geometries

The principles of [spectral integration](@entry_id:755177) must be extended to handle realistic simulations in two or three dimensions and on domains with curved boundaries.

#### Isoparametric Mapping and the Jacobian

To apply these methods to a general "physical" element $K$ in $\mathbb{R}^d$, we define a smooth, invertible mapping $\boldsymbol{x}(\boldsymbol{\xi})$ from a "reference" element $\widehat{K}$ (e.g., the square $[-1,1]^2$) to $K$. In an **isoparametric** formulation, this mapping is represented using the same polynomial basis functions that are used for the solution itself:
$$
\boldsymbol{x}(\boldsymbol{\xi}) = \sum_{a=1}^{N_{nodes}} \boldsymbol{x}_a \varphi_a(\boldsymbol{\xi})
$$
where $\{\boldsymbol{x}_a\}$ are the coordinates of the nodes in the physical element and $\{\varphi_a\}$ are the basis functions (e.g., Lagrange polynomials) on the [reference element](@entry_id:168425) .

To evaluate an integral over the physical element $K$, we use the [change of variables theorem](@entry_id:160749) from [multivariable calculus](@entry_id:147547). The integral is pulled back to the reference element $\widehat{K}$, where standard [quadrature rules](@entry_id:753909) can be applied. The transformation introduces the determinant of the mapping's **Jacobian matrix**, $J(\boldsymbol{\xi}) = \det(\partial \boldsymbol{x} / \partial \boldsymbol{\xi})$. The differential volume elements are related by $dV = |J(\boldsymbol{\xi})| d\boldsymbol{\xi}$. The [integral transformation](@entry_id:159691) is thus:
$$
\int_{K} g(\boldsymbol{x}) \, dV = \int_{\widehat{K}} g(\boldsymbol{x}(\boldsymbol{\xi})) |J(\boldsymbol{\xi})| \, d\boldsymbol{\xi}
$$
The absolute value of the Jacobian determinant is essential to ensure a positive volume measure, regardless of the orientation of the mapping.

#### Tensor-Product Quadrature

For quadrilateral or [hexahedral elements](@entry_id:174602) that can be mapped from a reference square or cube, the most common [multi-dimensional integration](@entry_id:142320) strategy is **[tensor-product quadrature](@entry_id:145940)** . An $N_x \times N_y$ rule on $[-1,1]^2$ is constructed by taking all pairs of 1D quadrature nodes and the product of their corresponding weights. If $\{(\xi_i, w_i^{(x)})\}$ and $\{(\eta_j, w_j^{(y)})\}$ are the 1D rules in each direction, the 2D rule is:
$$
\int_{-1}^{1}\int_{-1}^{1} f(\xi, \eta) \, d\xi d\eta \approx \sum_{i=1}^{N_x}\sum_{j=1}^{N_y} w_i^{(x)} w_j^{(y)} f(\xi_i, \eta_j)
$$
The exactness of this rule follows directly from the 1D case. If the 1D rules are exact for polynomials of degree up to $d_x$ and $d_y$ respectively, the tensor-product rule will be exact for all bivariate polynomials $p(\xi, \eta)$ that are in the tensor-[product space](@entry_id:151533) $\mathbb{P}^{d_x} \otimes \mathbb{P}^{d_y}$ (i.e., polynomials of separate degrees up to $d_x$ in $\xi$ and $d_y$ in $\eta$). For example, a [tensor product](@entry_id:140694) of two $N$-point Gauss-Legendre rules will be exact for all polynomials with separate degrees up to $2N-1$ in each variable.

### Aliasing Error and Under-Integration

When solving nonlinear PDEs, a crucial source of error known as **aliasing** or **under-[integration error](@entry_id:171351)** can arise if the quadrature rule is not sufficiently accurate. This error occurs when evaluating products of basis functions, such as the term $u^2$ in Burgers' equation .

If our solution is approximated by a polynomial of degree $p$, the nonlinear term $u^2$ is a polynomial of degree $2p$. To integrate this term exactly (or a product like $u^2 v$, where $v$ is a [test function](@entry_id:178872) of degree $p$), the quadrature rule must be exact for polynomials of degree up to $3p$. More generally, to compute the mass matrix entries for $u$ and $v$ from a space $\mathbb{P}^p$, the product $uv$ is of degree $2p$, and thus the [quadrature rule](@entry_id:175061) must have a [degree of precision](@entry_id:143382) of at least $2p$ for exact evaluation .

When the [degree of precision](@entry_id:143382) is insufficient, aliasing occurs. The mechanism can be understood by analogy to signal processing. A discrete grid (or a [finite set](@entry_id:152247) of quadrature points) can only resolve a finite range of frequencies (or polynomial degrees). High-frequency content in the exact function that is beyond this range is not simply discarded; instead, it is "folded back" and spuriously represented as low-frequency content.

Let's consider a concrete example. Suppose we approximate the integral of a product of two degree-$p$ polynomials, $u(x)$ and $v(x)$, using an $(p+1)$-point GLL quadrature rule. This rule has a [degree of exactness](@entry_id:175703) of $2(p+1)-3 = 2p-1$. The integrand $u(x)v(x)$ has degree up to $2p$. The quadrature rule is therefore not exact for the highest-degree component of the product, which arises from the term $a_p b_p P_p(x)^2$, where $a_p$ and $b_p$ are the coefficients of the degree-$p$ Legendre polynomial in the expansions of $u$ and $v$. All other products of basis functions have degree at most $2p-1$ and are integrated exactly. The error is thus entirely concentrated in the integration of this single highest-order term. A direct calculation shows this error is non-zero and proportional to the product of the highest-mode coefficients, $a_p b_p$ . This demonstrates precisely how under-integration causes an [aliasing error](@entry_id:637691) that contaminates the computation.

This problem is exacerbated on curvilinear elements, where the integrand includes the non-constant Jacobian determinant, further increasing the polynomial degree and demanding even higher-order [quadrature rules](@entry_id:753909) for [exactness](@entry_id:268999) . In practice, one may intentionally under-integrate to reduce computational cost, but this must be done with care, as the resulting [aliasing](@entry_id:146322) can introduce numerical instabilities.

### Summation-by-Parts and Energy Stability

A more advanced application of quadrature theory in [high-order methods](@entry_id:165413) is in the construction of provably [stable numerical schemes](@entry_id:755322). This is often achieved by designing discrete operators that mimic fundamental continuous identities, such as integration by parts. The **Summation-by-Parts (SBP)** property formalizes this mimicry.

On a set of GLL nodes, the collocation [differentiation matrix](@entry_id:149870) $D$ and the diagonal norm matrix $H = \mathrm{diag}(w_1, \dots, w_N)$ formed from the GLL [quadrature weights](@entry_id:753910) are not independent. They are intimately linked through the SBP property, which is a discrete analogue of the integration-by-parts formula $\int u'v \, dx = [uv] - \int uv' \, dx$. This property can be expressed in matrix form as :
$$
H D + D^{\top} H = B
$$
where $B$ is a [boundary operator](@entry_id:160216) matrix that has non-zero entries only corresponding to the endpoints of the interval. Specifically, for nodes on $[-1,1]$, $B = e_N e_N^{\top} - e_1 e_1^{\top}$. This identity ensures that the discrete inner product, $(u,v)_H = u^{\top} H v$, mimics [integration by parts](@entry_id:136350) perfectly:
$$
(Du,v)_H + (u,Dv)_H = u_N v_N - u_1 v_1
$$

The SBP property is not just an algebraic curiosity; it is the key to proving the stability of a [semi-discretization](@entry_id:163562) by showing that a discrete energy norm is non-increasing or conserved. Consider the [linear advection equation](@entry_id:146245), $u_t + a u_x = 0$, on a periodic domain. The continuous $L^2$ energy, $\frac{1}{2} \int u^2 \, dx$, is conserved. We seek a numerical scheme that conserves a discrete analogue of this energy, defined as $\frac{1}{2} \|u\|_H^2 = \frac{1}{2} u^{\top} H u$.

By constructing a global spatial operator using elemental SBP operators and coupling the elements with an energy-conservative numerical flux (such as a central flux), one can show that the total discrete energy is exactly conserved . The SBP property allows the contribution from the differentiation within each element to be expressed purely in terms of fluxes at the element boundaries. When summed over all elements in a periodic domain, these interface fluxes cancel perfectly if the numerical flux is chosen correctly, leading to $\frac{d}{dt} \|u\|_H^2 = 0$. This demonstrates a profound connection: the specific choice of [quadrature weights](@entry_id:753910) (which define $H$) is not just a matter of accuracy, but is structurally necessary for constructing discrete operators that guarantee the stability of the numerical method.