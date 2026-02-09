## Introduction
In the quest for higher fidelity in computational fluid dynamics (CFD), high-order numerical methods have become indispensable tools for accurately simulating complex flow phenomena. Among the most promising modern approaches is the Flux Reconstruction (FR) framework, also known as the Correction Procedure via Reconstruction (CPR). This powerful and elegant framework not only delivers high-order accuracy but also resolves a long-standing challenge in the field: the unification of seemingly disparate methods like Discontinuous Galerkin (DG) and Spectral Difference (SD) schemes into a single, cohesive family. This article provides a graduate-level exploration of FR/CPR, bridging its theoretical foundations with its practical applications.

This article will guide you through the essential aspects of the FR/CPR framework across three comprehensive chapters. The journey begins in **"Principles and Mechanisms,"** which deconstructs the mathematical formulation from first principles, detailing the flux reconstruction process and establishing the fundamental properties of conservation, stability, and parallel efficiency. Next, **"Applications and Interdisciplinary Connections"** explores how these theoretical principles are applied to solve real-world engineering challenges, from handling complex geometries and boundary conditions to robustly capturing shock waves and extending the method to multiphysics problems. Finally, **"Hands-On Practices"** offers a set of targeted problems designed to solidify your understanding of the core mechanics and stability considerations, providing a practical complement to the theoretical discussion.

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms of the Flux Reconstruction (FR) framework, also known as the Correction Procedure via Reconstruction (CPR). We will dissect the mathematical construction of these schemes, beginning from the fundamental conservation laws and culminating in an understanding of how they unify a broad class of modern high-order methods.

### From Integral Conservation to a Discontinuous Weak Form

The starting point for any conservative numerical method is the integral form of the governing conservation law. For a system of hyperbolic conservation laws given in differential form as $\partial_t u + \nabla \cdot f(u) = 0$, where $u$ is the state vector and $f(u)$ is the flux tensor, we can integrate over any arbitrary fixed control volume $K$ within the computational domain $\Omega$. Applying the Divergence Theorem yields:

$$
\frac{\mathrm{d}}{\mathrm{d}t} \int_{K} u \, \mathrm{d}x + \int_{\partial K} f(u) \cdot n \, \mathrm{d}s = 0
$$

This equation provides an exact statement of conservation: the rate of change of the quantity $u$ inside the volume $K$ is precisely balanced by the net flux of $u$ across its boundary $\partial K$, where $n$ is the outward-pointing unit normal vector.

Element-based methods like FR/CPR partition the domain $\Omega$ into a set of non-overlapping elements $\{K\}$. A defining characteristic of these methods is that the approximate solution is represented by a polynomial within each element, with no requirement for continuity across the inter-element boundaries. This use of a **discontinuous trial space** is a key departure from traditional continuous finite element methods.

To formulate a numerical scheme, we derive an element-wise **weak form**. This is achieved by multiplying the differential form of the PDE by a **test function** $\varphi$ and integrating over a single element $K$. Crucially, like the solution, the test functions are also polynomials defined independently on each element and can be discontinuous across interfaces.

$$
\int_{K} \left( \frac{\partial u}{\partial t} + \nabla \cdot f(u) \right) \varphi \, \mathrm{d}x = 0
$$

A critical step is to apply integration by parts to the flux term. This transfers the spatial derivative from the potentially discontinuous (and thus non-differentiable in a classical sense) flux function $f(u)$ to the smooth polynomial test function $\varphi$:

$$
\int_{K} \frac{\partial u}{\partial t} \varphi \, \mathrm{d}x - \int_{K} f(u) \cdot \nabla \varphi \, \mathrm{d}x + \int_{\partial K} (f(u) \cdot n) \varphi \, \mathrm{d}s = 0
$$

At this juncture, the discontinuity of the solution presents a challenge. At any point on the boundary $\partial K$, the solution $u$ has two distinct values: the interior trace, denoted $u^-$, and the exterior trace from the neighboring element, denoted $u^+$. Consequently, the physical flux $f(u) \cdot n$ is ill-defined. To resolve this ambiguity and to establish communication between elements, the physical flux in the boundary integral is replaced by a single-valued **numerical flux**, $f^*(u^-, u^+)$. This function is designed to be consistent with the physical flux (i.e., $f^*(u, u) = f(u)$) and conservative (the flux leaving one element equals the flux entering its neighbor). This leads to the final element-wise weak formulation underpinning FR/CPR and related methods [@problem_id:3959942]:

$$
\int_{K} u_t \, \varphi \, \mathrm{d}x - \int_{K} f(u) \cdot \nabla \varphi \, \mathrm{d}x + \int_{\partial K} f^*(u^-, u^+) \cdot n \, \varphi \, \mathrm{d}s = 0
$$

While this weak form is the foundation of the Discontinuous Galerkin (DG) method, the FR/CPR framework provides an alternative, but related, interpretation based on directly reconstructing the flux polynomial, which we explore next.

### The Core Mechanism: Reconstructing the Flux

The central idea of Flux Reconstruction is to systematically construct a single, continuous flux polynomial within each element that incorporates the correct interface information. This procedure can be broken down into three main steps.

#### Step 1: The Local Flux Polynomial

Within each element, the solution $u$ is approximated by a polynomial $u_h(\xi)$ of degree $p$, where $\xi$ is the coordinate on a standard reference element (e.g., $[-1,1]$ in one dimension). This polynomial is uniquely defined by its values at $p+1$ distinct **solution points**. When the physical flux function $f(u)$ is applied to this solution polynomial, the resulting function $f(u_h(\xi))$ may not be a polynomial of degree $p$, especially for nonlinear conservation laws. For example, if $f(u) = u^2$ and $u_h$ is degree $p$, then $f(u_h)$ is degree $2p$.

The FR method does not attempt to work with this high-degree polynomial. Instead, it constructs a **local flux polynomial**, denoted $f^{\mathrm{loc}}(\xi)$, by finding the unique polynomial of degree at most $p$ that interpolates the physical flux values evaluated at the $p+1$ solution points [@problem_id:3959972]. This process effectively projects the true flux function back into the degree-$p$ polynomial space.

#### Step 2: The Reconstructed Flux and Correction Functions

The local flux polynomial $f^{\mathrm{loc}}(\xi)$ is inherently discontinuous at element boundaries because it is constructed using only information from within a single element. The goal is to "correct" this polynomial so that its values at the element boundaries match the single-valued numerical flux, $\hat{f}$, which is shared with the neighboring element.

This is achieved by adding a correction polynomial to $f^{\mathrm{loc}}(\xi)$ to form the **reconstructed flux polynomial**, $f^{\mathrm{rec}}(\xi)$. In one dimension, on the reference interval $[-1,1]$, this takes the form [@problem_id:3959917]:

$$
f^{\mathrm{rec}}(\xi) = f^{\mathrm{loc}}(\xi) + \big(\hat{f}_L - f^{\mathrm{loc}}(-1)\big) g_L(\xi) + \big(\hat{f}_R - f^{\mathrm{loc}}(1)\big) g_R(\xi)
$$

Let us dissect this crucial formula:
-   $f^{\mathrm{loc}}(\xi)$ is the local degree-$p$ flux polynomial described above.
-   $\hat{f}_L$ and $\hat{f}_R$ are the single-valued numerical fluxes at the left ($\xi=-1$) and right ($\xi=1$) boundaries, respectively, computed using a Riemann solver.
-   The terms $\big(\hat{f}_L - f^{\mathrm{loc}}(-1)\big)$ and $\big(\hat{f}_R - f^{\mathrm{loc}}(1)\big)$ are the **flux discrepancies** at the boundaries. They represent the difference between the required continuous flux and the element's internal, discontinuous flux value.
-   $g_L(\xi)$ and $g_R(\xi)$ are the **correction functions**. These are fixed polynomials (typically of degree $p+1$) designed to apply the flux discrepancy corrections. To ensure that $f^{\mathrm{rec}}(\xi)$ matches the numerical fluxes at the boundaries, these functions must satisfy cardinal interpolation-like properties at the endpoints:
    -   $g_L(-1)=1$ and $g_L(1)=0$
    -   $g_R(-1)=0$ and $g_R(1)=1$

By substituting $\xi=-1$ into the formula for $f^{\mathrm{rec}}(\xi)$, we can verify that the properties of $g_L$ and $g_R$ guarantee $f^{\mathrm{rec}}(-1) = \hat{f}_L$. Similarly, at $\xi=1$, we find $f^{\mathrm{rec}}(1) = \hat{f}_R$. Thus, the reconstructed flux is continuous across element boundaries by construction [@problem_id:3959977].

#### Step 3: Forming the Semi-Discrete Update

With a continuous and differentiable flux polynomial $f^{\mathrm{rec}}(\xi)$ now defined across the element, the spatial component of the semi-discrete update is simply its derivative. For a one-dimensional element with Jacobian $J$, the update for the solution polynomial $u_h(\xi, t)$ is given by the strong-form statement:

$$
\frac{\mathrm{d} u_h(\xi, t)}{\mathrm{d} t} = -\frac{1}{J} \frac{\partial f^{\mathrm{rec}}(\xi)}{\partial \xi}
$$

In practice, this continuous equation is projected onto the polynomial basis by enforcing it at the $p+1$ solution points. This procedure, which starts with a local flux, computes a correction based on interface data, and reconstructs a new flux whose derivative is used for the update, is the essence of the Flux Reconstruction/Correction Procedure via Reconstruction framework.

### Fundamental Properties of the FR/CPR Framework

The elegant construction of the FR/CPR scheme endows it with several highly desirable properties that are critical for modern CFD simulations.

#### Local and Global Conservation

A cornerstone of the FR framework is that it is **locally conservative** by construction. To see this, consider the rate of change of the element-averaged solution, $\bar{u}_h = \frac{1}{\Delta x} \int_{\text{element}} u_h \, dx$. In the reference element, this corresponds to integrating the semi-discrete update over $\xi \in [-1,1]$:

$$
\frac{\mathrm{d}}{\mathrm{d} t} \int_{-1}^{1} u_h(\xi) \, \mathrm{d}\xi = -\frac{1}{J} \int_{-1}^{1} \frac{\partial f^{\mathrm{rec}}(\xi)}{\partial \xi} \, \mathrm{d}\xi
$$

By the Fundamental Theorem of Calculus, the integral on the right-hand side telescopes to the boundary values:

$$
\int_{-1}^{1} \frac{\partial f^{\mathrm{rec}}(\xi)}{\partial \xi} \, \mathrm{d}\xi = f^{\mathrm{rec}}(1) - f^{\mathrm{rec}}(-1)
$$

As established previously, the reconstructed flux is designed to match the numerical fluxes at the boundaries, $f^{\mathrm{rec}}(1) = \hat{f}_R$ and $f^{\mathrm{rec}}(-1) = \hat{f}_L$. Substituting these in and converting back to physical coordinates ($J = \Delta x/2$) yields the familiar finite volume update for the cell average:

$$
\frac{\mathrm{d} \bar{u}_h}{\mathrm{d} t} = -\frac{1}{\Delta x} (\hat{f}_R - \hat{f}_L)
$$

This result demonstrates that the evolution of the total amount of the conserved quantity within an element depends only on the fluxes at its boundaries, which is the definition of local conservation [@problem_id:3959943]. When summing over all elements in a domain, the conservative property of the numerical flux ($\hat{f}_R$ of one element is the negative of $\hat{f}_L$ of its neighbor) ensures that interior fluxes cancel, leading to global conservation. It is important to note that while this cancellation is exact for the continuous integral, preserving it at the fully discrete level requires the discrete differentiation and integration operators to satisfy a **Summation-By-Parts (SBP)** property, which mimics the integration-by-parts rule discretely [@problem_id:3959943] [@problem_id:3959956].

#### Compact Stencil and Parallel Efficiency

A significant practical advantage of the FR/CPR framework is its **compact communication stencil**. The semi-discrete update for the degrees of freedom within a given element $e$ depends only on information from within that element and the numerical fluxes, $\hat{f}_L^{(e)}$ and $\hat{f}_R^{(e)}$, at its two boundaries.

The numerical flux at an interface is computed using only the solution values from the two elements that share that interface. For example, $\hat{f}_R^{(e)}$ is a function of the solution traces from element $e$ and its right neighbor, element $e+1$. Consequently, the update for element $e$ depends only on data from itself and its immediate neighbors, $e-1$ and $e+1$. This nearest-neighbor coupling holds true regardless of the polynomial degree $p$. This is in stark contrast to high-order finite difference methods, where increasing the order of accuracy necessarily widens the stencil, complicating boundary conditions and reducing parallel efficiency. The compact stencil of FR/CPR makes it exceptionally well-suited for massively parallel computations [@problem_id:3959971].

#### Stability via Summation-By-Parts

Proving the stability of a numerical scheme—ensuring that the solution does not grow unboundedly due to numerical errors—is paramount. For FR/CPR, stability proofs are elegantly formulated by interpreting the framework through the lens of Summation-By-Parts (SBP) operators.

The design of an FR/CPR scheme involves specifying the locations of **solution points**, which are interior collocation nodes where the solution is represented, and **flux points**, which are the locations where the flux is corrected (typically the element interfaces at $\xi = \pm 1$). This separation allows for a powerful decoupling of concerns: the placement of solution points can be optimized for quadrature accuracy in the element interior, while the enforcement of interface physics for stability is handled at the fixed flux points [@problem_id:3959997].

Through specific choices of solution points, quadrature rules (which define a discrete inner product, or mass matrix), and correction functions, the FR/CPR differentiation operator can be shown to satisfy the SBP property. This property is a discrete analogue of integration by parts, and it allows the energy contribution from the volume of an element to be expressed solely in terms of its boundary values. When combined with a dissipative numerical flux (such as an upwind flux for advection or an entropy-stable flux for nonlinear systems), the SBP structure guarantees that the total discrete energy of the system is non-increasing, thus proving numerical stability [@problem_id:3959956].

### A Unifying Framework for High-Order Methods

One of the most powerful aspects of the Flux Reconstruction framework is its generality. By adjusting the correction functions $g_L(\xi)$ and $g_R(\xi)$, one can generate an entire family of different high-order schemes.

#### The Connection to Finite Volume Methods

The fundamental consistency of the FR framework can be demonstrated by examining its behavior in the limit of zero-degree polynomial approximation ($p=0$). In this case, the solution $u_h$ is a constant within each element. For the semi-discrete update to be well-defined, the derivative of the reconstructed flux, $\partial_\xi f^{\mathrm{rec}}$, must also be constant. This requires the correction functions $g_L(\xi)$ and $g_R(\xi)$ to be linear polynomials. With this choice, the FR update for the constant cell-average value $u_i$ reduces exactly to the classic first-order finite volume scheme [@problem_id:3959988]:

$$
\frac{d u_i}{dt} = -\frac{1}{\Delta x_i} (F_{i+1/2} - F_{i-1/2})
$$

This shows that the sophisticated machinery of FR is built upon, and consistent with, the foundational principles of finite volume methods.

#### Unifying Discontinuous Galerkin, Spectral Difference, and Other Schemes

The choice of correction functions is a key degree of freedom. By constructing families of correction functions, often controlled by a single parameter $c$, FR/CPR can be shown to be algebraically equivalent to various other well-known high-order methods [@problem_id:3959966]. For example:

-   **Nodal Discontinuous Galerkin (DG) Method:** For a specific value of the parameter, $c=c_{\mathrm{DG}}$, the correction operator in the FR scheme becomes identical to the lifting operator in the nodal DG method. This establishes a direct algebraic equivalence between the two frameworks.
-   **Spectral Difference (SD) Method:** The SD method constructs its flux polynomial differently, by collocating at a separate set of "flux points". Again, a specific choice of correction functions (and thus a specific parameter value, $c=c_{\mathrm{SD}}$) can be found that makes the FR reconstructed flux polynomial identical to that of the SD method.
-   **Huynh's g2/g3 Schemes:** These are particular, named instances within the FR family, corresponding to specific, well-studied choices of correction functions.

This unifying property is of profound theoretical and practical importance. It demonstrates that many seemingly disparate methods are, in fact, members of a single, continuous family. This allows for a unified analysis of stability and accuracy and enables the development of hybrid schemes that can leverage the best properties of different methods within a single simulation.