## Introduction
In Riemannian geometry, the choice of metric determines all local geometric properties. A natural question arises: within a family of related metrics, does one stand out as being geometrically "nicer" or "canonical"? The Yamabe problem addresses this for the family of conformal metrics, asking whether any given compact Riemannian manifold admits a conformally related metric of [constant scalar curvature](@entry_id:186408). This seemingly simple question opens a door to a rich and challenging field at the intersection of geometry, analysis, and physics. The primary obstacle is not geometric but analytical, rooted in the properties of a critical nonlinear partial differential equation.

This article navigates the theory and impact of the Yamabe problem. We will begin in the first chapter, **Principles and Mechanisms**, by deriving the foundational Yamabe equation from the geometry of conformal deformations and exploring its variational structure. Next, in **Applications and Interdisciplinary Connections**, we will see how the problem's solution forged profound links to general relativity via the Positive Mass Theorem and provided powerful tools for studying the existence of [positive scalar curvature](@entry_id:203664) metrics. Finally, **Hands-On Practices** will offer a chance to engage directly with the core calculations that underpin the theory.

## Principles and Mechanisms

### The Geometry of Conformal Deformations

At the heart of the Yamabe problem lies the concept of a **conformal deformation** of a Riemannian metric. Given a smooth Riemannian manifold $(M^n, g)$ of dimension $n$, a metric $\tilde{g}$ is said to be **conformal** to $g$ if it is obtained by pointwise rescaling the original metric by a smooth, strictly positive function. That is, there exists a function $f \in C^\infty(M)$ with $f>0$ such that $\tilde{g} = f \cdot g$. This set of all metrics conformal to $g$ is called the **conformal class** of $g$, denoted by $[g]$.

For analytical convenience, the scaling factor is often expressed in specific forms. A common choice is $\tilde{g} = e^{2\phi} g$ for some $\phi \in C^\infty(M)$. An alternative, and particularly useful form for the Yamabe problem when $n \ge 3$, is to write the conformal factor as a power of a positive function $u$:
$$
\tilde{g} = u^{\frac{4}{n-2}} g
$$
where $u \in C^\infty(M)$ and $u > 0$. The exponent $\frac{4}{n-2}$ is chosen precisely to simplify the transformation law of the scalar curvature, a crucial point we will soon explore.

A [conformal change of metric](@entry_id:195227) rescales lengths of tangent vectors, but it preserves angles between them. This means that the "shape" of infinitesimal objects is preserved, while their "size" is altered. This change in size has a direct impact on other geometric quantities, most notably the Riemannian volume element. In a local coordinate system $\{x^i\}$, the volume element $d\mu_g$ is given by $\sqrt{\det(g_{ij})} \, dx^1 \wedge \dots \wedge dx^n$. If we consider a conformal change $\tilde{g} = e^{2\phi}g$, the matrix of components transforms as $(\tilde{g}_{ij}) = e^{2\phi}(g_{ij})$. Using the property that for an $n \times n$ matrix $A$ and a scalar $c$, $\det(cA) = c^n \det(A)$, we find that $\det(\tilde{g}_{ij}) = (e^{2\phi})^n \det(g_{ij})$. Taking the square root yields the transformation law for the volume element [@problem_id:3005219]:
$$
d\mu_{\tilde{g}} = \sqrt{(e^{2\phi})^n \det(g_{ij})} \, dx^1 \wedge \dots \wedge dx^n = e^{n\phi} \sqrt{\det(g_{ij})} \, dx^1 \wedge \dots \wedge dx^n = e^{n\phi} d\mu_g.
$$
If we use the preferred scaling $\tilde{g} = u^{\frac{4}{n-2}}g$, we can relate the two scaling functions by setting $e^{2\phi} = u^{\frac{4}{n-2}}$, which implies $\phi = \frac{2}{n-2} \ln u$. Substituting this into the volume transformation law gives:
$$
d\mu_{\tilde{g}} = \exp\left(n \cdot \frac{2}{n-2} \ln u\right) d\mu_g = u^{\frac{2n}{n-2}} d\mu_g.
$$
This specific scaling of the [volume element](@entry_id:267802) is fundamental to the [variational formulation](@entry_id:166033) of the Yamabe problem.

### The Yamabe Equation and the Conformal Laplacian

The central question of the Yamabe problem is: given a compact Riemannian manifold $(M,g)$, does there exist a metric $\tilde{g}$ conformal to $g$ that has **[constant scalar curvature](@entry_id:186408)**?

To translate this geometric problem into the language of partial differential equations, we must understand how scalar curvature transforms under a conformal change. Let $\tilde{g} = u^{\frac{4}{n-2}} g$. A detailed but standard calculation involving the Christoffel symbols and the Riemann [curvature tensor](@entry_id:181383) yields a remarkable transformation law for the scalar curvatures $R_g$ and $R_{\tilde{g}}$:
$$
R_{\tilde{g}} = u^{-\frac{n+2}{n-2}} \left( -a_n \Delta_g u + R_g u \right),
$$
where $\Delta_g$ is the Laplace-Beltrami operator on $(M,g)$ and $a_n$ is a dimensional constant given by $a_n = \frac{4(n-1)}{n-2}$. The operator appearing on the right-hand side is of such central importance that it is given its own name: the **conformal Laplacian**.
$$
L_g u := -a_n \Delta_g u + R_g u.
$$
The conformal Laplacian is a second-order, linear, self-adjoint [elliptic operator](@entry_id:191407). Its defining property is its simple, or **covariant**, transformation law under conformal changes of the metric. The [scalar curvature](@entry_id:157547) transformation can be written compactly as $R_{\tilde{g}} = u^{-\frac{n+2}{n-2}} L_g u$.

With this operator, the Yamabe problem is transformed. The search for a metric $\tilde{g} = u^{\frac{4}{n-2}}g$ with [constant scalar curvature](@entry_id:186408), say $R_{\tilde{g}} \equiv \lambda$, becomes the search for a smooth positive function $u$ on $M$ that solves the following semilinear elliptic [partial differential equation](@entry_id:141332) [@problem_id:3005232]:
$$
L_g u = \lambda u^{\frac{n+2}{n-2}}.
$$
This is known as the **Yamabe equation**. The power on the right-hand side, $p = \frac{n+2}{n-2}$, is particularly significant. It is not just an artifact of the calculation; it is determined by fundamental scaling principles.

### The Variational Structure and the Critical Sobolev Exponent

The Yamabe equation possesses a variational structure, meaning its solutions can be found as critical points of an associated [energy functional](@entry_id:170311). This functional is the **normalized total scalar curvature**, also known as the Yamabe functional. For a metric $\tilde{g} = u^{\frac{4}{n-2}}g$, its total [scalar curvature](@entry_id:157547) is $\int_M R_{\tilde{g}} \, d\mu_{\tilde{g}}$. This quantity scales with the volume of the manifold, so to obtain a scale-invariant quantity, we normalize it by the total volume raised to an appropriate power. The resulting functional, expressed in terms of the function $u$ and the background metric $g$, is:
$$
Q_g(u) = \frac{\int_M u(L_g u) \, d\mu_g}{\left(\int_M u^{\frac{2n}{n-2}} \, d\mu_g\right)^{\frac{n-2}{n}}} = \frac{\int_M (a_n |\nabla u|_g^2 + R_g u^2) \, d\mu_g}{\left(\int_M |u|^{\frac{2n}{n-2}} \, d\mu_g\right)^{\frac{n-2}{n}}}.
$$
The Euler-Lagrange equation for this functional is precisely the Yamabe equation. The problem is thus reduced to finding a minimizer for $Q_g(u)$ among all smooth positive functions $u$. The [infimum](@entry_id:140118) of this functional over the conformal class is a crucial geometric invariant known as the **Yamabe constant** of the class $[g]$:
$$
\mu(M, [g]) = \inf_{u \in C^\infty(M), u>0} Q_g(u).
$$
The significance of the exponent $\frac{2n}{n-2}$ becomes clear when we analyze the scaling behavior of the functional $Q_g(u)$ [@problem_id:3005220]. Consider the numerator, which is related to the homogeneous Sobolev norm $\|\nabla u\|_{L^2}^2$, and the denominator, which is the $L^p$ norm $\|u\|_{L^p}^2$ for $p = \frac{2n}{n-2}$. Let us examine how the numerator and denominator transform under a simple constant scaling of the metric, $\tilde{g} = e^{2c}g$ for some constant $c$. The gradient term transforms as $\int_M |\nabla u|_{\tilde{g}}^2 d\mu_{\tilde{g}} = \int_M e^{-2c}|\nabla u|_g^2 \cdot e^{nc} d\mu_g = e^{(n-2)c} \int_M |\nabla u|_g^2 d\mu_g$. The $L^p$ norm in the denominator transforms as $(\int_M |u|^p d\mu_{\tilde{g}})^{2/p} = (e^{nc} \int_M |u|^p d\mu_g)^{2/p} = e^{\frac{2n}{p}c} (\int_M |u|^p d\mu_g)^{2/p}$. For the quotient of these two terms to be invariant, the [scaling exponents](@entry_id:188212) must match:
$$
n-2 = \frac{2n}{p} \quad \implies \quad p = \frac{2n}{n-2}.
$$
This exponent $p$ is known as the **critical Sobolev exponent** because it is precisely the exponent for which the Sobolev embedding $H^1(M) \hookrightarrow L^p(M)$ is continuous but not compact. This lack of compactness is the principal analytical difficulty in solving the Yamabe problem, as it implies that minimizing sequences for the functional $Q_g(u)$ are not guaranteed to converge.

If a metric $g$ is a Yamabe metric—that is, it has [constant scalar curvature](@entry_id:186408) and minimizes the functional within its conformal class—it must be a critical point. A first-order [perturbation analysis](@entry_id:178808) confirms this: for any one-parameter family of volume-preserving conformal deformations starting at $g$, the [first variation](@entry_id:174697) of the Yamabe functional must vanish [@problem_id:3005236].

### The Conformal Laplacian and Spectral Geometry

The connection between the Yamabe problem and the spectral theory of the conformal Laplacian provides deep insights. As a self-adjoint [elliptic operator](@entry_id:191407) on a compact manifold, $L_g$ has a discrete, real spectrum of eigenvalues $\lambda_1 \le \lambda_2 \le \dots \to \infty$. The first eigenvalue, $\lambda_1(L_g)$, can be characterized variationally by the Rayleigh quotient:
$$
\lambda_1(L_g) = \inf_{u \in H^1(M) \setminus \{0\}} \frac{\int_M u(L_g u) \, d\mu_g}{\int_M u^2 \, d\mu_g} = \inf_{u \in H^1(M) \setminus \{0\}} \frac{\int_M (a_n |\nabla u|_g^2 + R_g u^2) \, d\mu_g}{\int_M u^2 \, d\mu_g}.
$$
Notice the strong resemblance between the Rayleigh quotient for $\lambda_1(L_g)$ and the Yamabe functional $Q_g(u)$. They share the same numerator, but their denominators differ ($L^2$ norm vs. $L^{\frac{2n}{n-2}}$ norm). Despite this difference, their signs are intrinsically linked. If $\lambda_1(L_g) > 0$, the numerator is always positive for any non-zero function $u$, which implies that $Q_g(u)$ is always positive. Consequently, the Yamabe constant $\mu(M, [g])$ must be positive. Conversely, if $\mu(M, [g]) > 0$, a slightly more involved argument shows $\lambda_1(L_g) > 0$. This leads to a fundamental equivalence [@problem_id:3005218]:
$$
\mathrm{sign}(\mu(M, [g])) = \mathrm{sign}(\lambda_1(L_g)).
$$
This means the geometric problem of finding a positive scalar curvature metric in a conformal class is equivalent to the analytical problem of determining whether the conformal Laplacian is a [positive operator](@entry_id:263696).

Furthermore, the spectrum of $L_g$ determines the stability of [constant scalar curvature](@entry_id:186408) metrics. A metric with [constant scalar curvature](@entry_id:186408) is a critical point of the Yamabe functional. To determine if it is a [local minimum](@entry_id:143537), one must examine the second variation of the functional. This second variation is governed by the operator $L_g$. If the metric $g$ has [constant scalar curvature](@entry_id:186408), then for it to be a strict local minimizer of the Yamabe functional (under volume-preserving conformal perturbations), the operator $L_g$ must be [positive definite](@entry_id:149459) on the space of perturbations. This is guaranteed if its first eigenvalue $\lambda_1(L_g)$ is positive [@problem_id:3005218].

### The Global Picture: The Yamabe Invariant and the Role of the Sphere

The Yamabe constant $\mu(M, [g])$ is an invariant of the conformal class. To understand the global geometry of the manifold $M$, we can consider all possible conformal structures on it. This leads to the definition of the **Yamabe invariant** (or sigma invariant) of the manifold $M$:
$$
\sigma(M) = \sup_{[g]} \mu(M, [g]),
$$
where the [supremum](@entry_id:140512) is taken over all conformal classes $[g]$ on $M$. This invariant carries profound geometric information: a manifold $M$ admits a metric of positive scalar curvature if and only if its Yamabe invariant is positive, $\sigma(M) > 0$ [@problem_id:3005238].

The solution to the Yamabe problem, completed through the work of Yamabe, Trudinger, Aubin, and Schoen, revealed a universal bound. For any compact Riemannian manifold $(M^n, g)$ with $n \ge 3$, its Yamabe constant is bounded above by that of the standard round sphere $(S^n, g_{\mathrm{round}})$:
$$
\mu(M, [g]) \le \mu(S^n, [g_{\mathrm{round}}]).
$$
Equality holds if and only if $(M,g)$ is conformally diffeomorphic to the standard sphere. This result establishes the sphere as the extremal case in [conformal geometry](@entry_id:186351). The value $\mu(S^n, [g_{\mathrm{round}}])$ is explicitly known and is equal to $n(n-1)\omega_n^{2/n}$, where $\omega_n$ is the volume of the unit $n$-sphere.

This extremal property of the sphere is deeply connected to the sharp Sobolev inequality on Euclidean space $\mathbb{R}^n$ [@problem_id:3005231]. By using a [stereographic projection](@entry_id:142378), which is a conformal map from $S^n \setminus \{\text{point}\}$ to $\mathbb{R}^n$, the Yamabe functional on the sphere can be related to the Sobolev quotient on $\mathbb{R}^n$. The minimizers of the Yamabe functional on the sphere correspond precisely to the Aubin-Talenti "bubble" functions that achieve equality in the sharp Sobolev inequality on $\mathbb{R}^n$.

The condition for equality, being conformally equivalent to the sphere, has a clear geometric interpretation for dimensions $n \ge 4$. In these dimensions, a manifold is conformally flat (i.e., locally conformally equivalent to Euclidean space) if and only if its **Weyl tensor** $W_g$ vanishes. Since the sphere is conformally flat, any manifold conformally equivalent to it must also be conformally flat. Therefore, if a manifold $(M^n, g)$ with $n \ge 4$ has a non-vanishing Weyl tensor, it cannot be conformally equivalent to the sphere, which implies a strict inequality in the Yamabe constant: $\mu(M, [g])  \mu(S^n, [g_{\mathrm{round}}])$ [@problem_id:3005231].

### The Analytical Challenge: Loss of Compactness

The main difficulty in proving the existence of a minimizer for the Yamabe functional is the loss of compactness of minimizing sequences. This occurs precisely when the Yamabe constant $\mu(M, [g])$ is close to the value for the sphere, $\mu(S^n, [g_{\mathrm{round}}])$. The reason for this failure is the large, non-[compact group](@entry_id:196800) of conformal [automorphisms](@entry_id:155390) of the standard sphere, $\mathrm{Conf}(S^n) \cong O(n+1, 1)$ [@problem_id:3005228].

This group action can be visualized via [stereographic projection](@entry_id:142378). The [conformal group](@entry_id:156186) of $\mathbb{R}^n$ includes translations and dilations, which are non-compact families of transformations. If we take a minimizer for the Yamabe functional on $S^n$ (for example, a [constant function](@entry_id:152060)) and apply a sequence of [conformal maps](@entry_id:271672) that correspond to dilations on $\mathbb{R}^n$ that focus on a single point, we generate a [sequence of functions](@entry_id:144875) that are all minimizers. However, this sequence does not converge in the standard [function spaces](@entry_id:143478) (like $H^1$). Instead, the energy of the functions concentrates at a single point, forming a "bubble". The existence of such non-converging minimizing sequences demonstrates a fundamental loss of compactness. The key to solving the Yamabe problem was to understand and control this [bubbling phenomenon](@entry_id:183569).

### Advanced Mechanisms: The Positive Mass Theorem and Blow-up Analysis

The definitive resolution of the Yamabe problem for the case $\mu(M, [g])  0$ by Richard Schoen relied on a powerful tool from general relativity: the **Positive Mass Theorem (PMT)**. Schoen's strategy was to rule out the [bubbling phenomenon](@entry_id:183569) on any manifold not conformally equivalent to the sphere.

The core of the argument is a beautiful geometric construction [@problem_id:3005212]. Given a point $p \in M$, one considers the Green's function $G_p$ for the conformal Laplacian $L_g$, which is the solution to $L_g G_p = \delta_p$. Near the point $p$, $G_p$ behaves like the fundamental solution of the Laplacian, $G_p(x) \sim c|x|^{2-n}$. On the punctured manifold $M \setminus \{p\}$, one defines a new metric $\tilde{g} = G_p^{\frac{4}{n-2}} g$. The scalar curvature of this new metric is $R_{\tilde{g}} = G_p^{-\frac{n+2}{n-2}} L_g G_p = 0$, since $L_g G_p$ is zero away from $p$. The singularity of the Green's function at $p$ "blows up" the point to create an "end" of the manifold $(M \setminus \{p\}, \tilde{g})$ which is **asymptotically flat**. This means that far away from the main body of the manifold, the geometry approaches that of Euclidean space.

The PMT states that any complete, [asymptotically flat manifold](@entry_id:181302) with non-negative [scalar curvature](@entry_id:157547) must have non-negative **Arnowitt-Deser-Misner (ADM) mass**, an invariant measured at infinity. Since $(M \setminus \{p\}, \tilde{g})$ is scalar-flat, the PMT applies and guarantees its ADM mass is non-negative. A crucial calculation relates this ADM mass to the constant term in the [asymptotic expansion](@entry_id:149302) of the Green's function at $p$. The PMT thus provides a powerful constraint on the local behavior of the Green's function. This constraint was the key to ruling out the formation of bubbles, thereby proving the compactness of minimizing sequences and solving the Yamabe problem in the positive and locally conformally flat cases.

This type of argument is a prototypical example of **[blow-up analysis](@entry_id:187686)**. When analyzing a sequence of solutions $\{u_k\}$ to the Yamabe equation whose maxima blow up, one rescales the solution around a maximum point. The rescaled profiles converge to a solution of the Yamabe equation on Euclidean space—a standard bubble [@problem_id:3005207]. The PMT is used to show that such blow-up is impossible under certain geometric conditions (e.g., for locally conformally flat manifolds, or for general manifolds in dimensions $3 \le n \le 5$).

For a long time, it was believed that the solution set to the Yamabe equation was always compact on manifolds not conformally equivalent to the sphere. However, in a surprising turn, counterexamples were constructed by Brendle and Marques for certain manifolds with non-zero Weyl tensor in high dimensions ($n \ge 25$). These examples exhibit intricate blow-up patterns, demonstrating that the interaction between background curvature and the critical nonlinearity can be far richer and more complex than previously imagined, and can itself be a source of non-compactness [@problem_id:3005207]. This remains an active area of research, illustrating the deep and enduring legacy of the Yamabe problem in [geometric analysis](@entry_id:157700).