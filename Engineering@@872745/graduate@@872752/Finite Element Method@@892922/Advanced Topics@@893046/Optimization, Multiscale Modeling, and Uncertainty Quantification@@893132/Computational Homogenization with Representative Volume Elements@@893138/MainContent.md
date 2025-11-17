## Introduction
In modern engineering and materials science, predicting the behavior of advanced materials like [composites](@entry_id:150827), polymers, and biological tissues is a central challenge. These materials derive their unique properties from complex, heterogeneous microstructures, which are often too detailed to include in a full-scale structural simulation. Computational homogenization provides a powerful and rigorous bridge between these scales, allowing us to derive an effective, homogeneous material model from the explicit simulation of a small, [representative sample](@entry_id:201715) of its microstructure. This article addresses the fundamental question: how can we computationally determine macroscopic material properties from the underlying microscale physics in a consistent and accurate manner? Over the next three chapters, you will build a comprehensive understanding of this multiscale method. The journey begins in **'Principles and Mechanisms'**, where we will dissect the theoretical bedrock of the method, including the crucial Hill-Mandel condition and the definition of a Representative Volume Element (RVE). Next, **'Applications and Interdisciplinary Connections'** will showcase the versatility of this framework, demonstrating its use for modeling complex nonlinearities, coupled multi-physics, and in advanced computational design. Finally, **'Hands-On Practices'** will provide the opportunity to apply these concepts, guiding you through the essential steps of building, solving, and verifying RVE simulations to cement your theoretical knowledge.

## Principles and Mechanisms

The transition from a detailed, heterogeneous microscopic description of a material to a simplified, homogeneous macroscopic model is governed by rigorous principles that ensure mechanical and energetic consistency. This chapter delineates these foundational principles, beginning with the cornerstone concept of energetic consistency, and builds towards the practical definition and computational use of a Representative Volume Element (RVE).

### The Principle of Macro-Homogeneity: The Hill-Mandel Condition

The fundamental postulate underpinning first-order [computational homogenization](@entry_id:163942) is the requirement of energetic consistency between the microscopic and macroscopic scales. This principle, known as the **Hill-Mandel macro-homogeneity condition**, ensures that the work done by macroscopic stresses on macroscopic strains is equal to the volume average of the work done by microscopic stresses on microscopic strains.

To formalize this, let us consider a material [volume element](@entry_id:267802), the RVE, occupying a domain $\Omega_{\mu}$ in a quasi-static state with negligible body forces. The microscopic state is described by the Cauchy stress field $\boldsymbol{\sigma}(\mathbf{x})$ and the [infinitesimal strain](@entry_id:197162) field $\boldsymbol{\varepsilon}(\mathbf{x})$. The corresponding macroscopic state is described by the macroscopic stress $\boldsymbol{\Sigma}$ and strain $\boldsymbol{E}$, which are defined as work-conjugate quantities. The Hill-Mandel condition states that for any admissible virtual change in the macroscopic strain, $\delta\boldsymbol{E}$, and the corresponding microscopic virtual strain field, $\delta\boldsymbol{\varepsilon}(\mathbf{x})$, the following equality must hold [@problem_id:2546336]:

$$
\boldsymbol{\Sigma} : \delta\boldsymbol{E} = \langle \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} \rangle
$$

where the operator $\langle \cdot \rangle$ denotes the volume average over the RVE domain, defined as $\langle f \rangle = \frac{1}{|\Omega_{\mu}|} \int_{\Omega_{\mu}} f(\mathbf{x}) \, \mathrm{d}V$. Physically, this condition equates the macroscopic [virtual work](@entry_id:176403) density (or [stress power](@entry_id:182907)) with the averaged microscopic [virtual work](@entry_id:176403) density. It is not merely a definition but a powerful constraint that dictates which microscopic fields are admissible and how the macroscopic variables must be defined to ensure the scale transition is energetically sound. Any valid [homogenization](@entry_id:153176) scheme must satisfy this condition.

### Macroscopic Variables and the Stress Averaging Rule

The Hill-Mandel condition provides the framework for defining the macroscopic [state variables](@entry_id:138790). The macroscopic strain $\boldsymbol{E}$ is typically defined as the volume average of the microscopic strain field, $\boldsymbol{E} = \langle \boldsymbol{\varepsilon} \rangle$. The question then is, what is the corresponding definition of the macroscopic stress $\boldsymbol{\Sigma}$? The answer emerges directly from the Hill-Mandel condition.

Let us consider a general variation of the microscopic strain field, $\delta\boldsymbol{\varepsilon}(\mathbf{x})$. We can substitute this into the Hill-Mandel condition:
$\boldsymbol{\Sigma} : \langle \delta\boldsymbol{\varepsilon} \rangle = \langle \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} \rangle$. Rearranging this gives:

$$
\langle (\boldsymbol{\sigma} - \boldsymbol{\Sigma}) : \delta\boldsymbol{\varepsilon} \rangle = 0
$$

This equation does not immediately imply $\boldsymbol{\Sigma} = \langle \boldsymbol{\sigma} \rangle$ because the microscopic strain variation $\delta\boldsymbol{\varepsilon}$ is a field that is generally not uniform. However, by leveraging the [principle of virtual work](@entry_id:138749) at the microscale, we can arrive at this crucial relationship. For a general nonlinear material, let's consider the specific case of periodic boundary conditions applied to a heterogeneous RVE [@problem_id:2546309]. The microscopic [displacement field](@entry_id:141476) $\mathbf{u}(\mathbf{x})$ is decomposed into a mean part and a fluctuating part, $\mathbf{u}(\mathbf{x}) = \boldsymbol{E} \cdot \mathbf{x} + \tilde{\mathbf{u}}(\mathbf{x})$. The corresponding strain is $\boldsymbol{\varepsilon}(\mathbf{x}) = \boldsymbol{E} + \nabla^s \tilde{\mathbf{u}}(\mathbf{x})$, where $\nabla^s$ is the symmetric [gradient operator](@entry_id:275922). The variations are thus related by $\delta\boldsymbol{\varepsilon} = \delta\boldsymbol{E} + \nabla^s(\delta\tilde{\mathbf{u}})$.

Substituting this into the Hill-Mandel condition yields:

$$
\boldsymbol{\Sigma} : \delta\boldsymbol{E} = \langle \boldsymbol{\sigma} : (\delta\boldsymbol{E} + \nabla^s(\delta\tilde{\mathbf{u}})) \rangle = \langle \boldsymbol{\sigma} \rangle : \delta\boldsymbol{E} + \langle \boldsymbol{\sigma} : \nabla^s(\delta\tilde{\mathbf{u}}) \rangle
$$

The [weak form](@entry_id:137295) of microscopic equilibrium, $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$, is precisely the statement that the virtual work of the internal stresses over any admissible fluctuation vanishes: $\langle \boldsymbol{\sigma} : \nabla^s(\delta\tilde{\mathbf{u}}) \rangle = 0$. The Hill-Mandel condition therefore simplifies to $\boldsymbol{\Sigma} : \delta\boldsymbol{E} = \langle \boldsymbol{\sigma} \rangle : \delta\boldsymbol{E}$. Since this must hold for any arbitrary macroscopic virtual strain $\delta\boldsymbol{E}$, it leads to the fundamental **stress averaging rule**:

$$
\boldsymbol{\Sigma} = \langle \boldsymbol{\sigma} \rangle
$$

This elegant result establishes that the work-conjugate macroscopic stress is simply the volume average of the microscopic stress field. This relationship, along with $\boldsymbol{E} = \langle \boldsymbol{\varepsilon} \rangle$, forms the primary linkage between the two scales.

### Admissible Boundary Conditions for the RVE

The primary task in a [computational homogenization](@entry_id:163942) analysis is to solve the microscopic [boundary value problem](@entry_id:138753) on the RVE for a given macroscopic strain $\boldsymbol{E}$. The boundary conditions (BCs) applied to the RVE must be "admissible," meaning they enforce the condition $\boldsymbol{E} = \langle \boldsymbol{\varepsilon} \rangle$ and satisfy the Hill-Mandel condition. The choice of BCs is realized through constraints on the displacement fluctuation field $\tilde{\mathbf{u}}(\mathbf{x})$ from the [kinematic decomposition](@entry_id:751020) $\mathbf{u}(\mathbf{x}) = \boldsymbol{E} \cdot \mathbf{x} + \tilde{\mathbf{u}}(\mathbf{x})$ [@problem_id:2546304].

There are three standard classes of admissible boundary conditions [@problem_id:2546333]:

1.  **Kinematically Uniform Boundary Conditions (KUBC)**: Also known as linear Dirichlet BCs, these impose the affine displacement field directly on the boundary $\partial\Omega_{\mu}$:
    $$ \mathbf{u}(\mathbf{x}) = \boldsymbol{E} \cdot \mathbf{x} \quad \forall \mathbf{x} \in \partial\Omega_{\mu} $$
    This prescription is equivalent to demanding that the displacement fluctuation vanishes on the boundary, $\tilde{\mathbf{u}}(\mathbf{x}) = \mathbf{0}$ for $\mathbf{x} \in \partial\Omega_{\mu}$. The appropriate function space for the fluctuation field is therefore the Sobolev space $H^1_0(\Omega_{\mu})^d$, which contains functions with square-integrable gradients that are zero on the boundary. These conditions kinematically over-constrain the RVE boundary.

2.  **Statically Uniform Boundary Conditions (SUBC)**: Also known as uniform traction or Neumann BCs, these are stress-controlled conditions. A uniform macroscopic stress $\boldsymbol{\Sigma}$ is prescribed by applying a corresponding [traction vector](@entry_id:189429) field $\mathbf{t}(\mathbf{x})$ on the boundary:
    $$ \mathbf{t}(\mathbf{x}) = \boldsymbol{\sigma}(\mathbf{x}) \cdot \mathbf{n}(\mathbf{x}) = \boldsymbol{\Sigma} \cdot \mathbf{n}(\mathbf{x}) \quad \forall \mathbf{x} \in \partial\Omega_{\mu} $$
    where $\mathbf{n}(\mathbf{x})$ is the outward unit normal. For this problem to be well-posed, [rigid body motions](@entry_id:200666) of the RVE must be suppressed, for instance by fixing the displacement at a point and the rotation at another. The fluctuation field $\tilde{\mathbf{u}}$ is sought in the quotient space $H^1(\Omega_{\mu})^d / \mathcal{R}$, where $\mathcal{R}$ is the space of [rigid body motions](@entry_id:200666). This is practically achieved by enforcing integral constraints such as $\langle \tilde{\mathbf{u}} \rangle = \mathbf{0}$ and $\langle \text{skw}(\nabla \tilde{\mathbf{u}}) \rangle = \mathbf{0}$ [@problem_id:2546304]. These conditions kinematically under-constrain the RVE boundary.

3.  **Periodic Boundary Conditions (PBC)**: These conditions are most natural for materials with a periodic [microstructure](@entry_id:148601), but they are widely used for random media as well. They enforce [periodicity](@entry_id:152486) on the displacement fluctuations and anti-periodicity on the tractions. For any pair of corresponding points $\mathbf{x}^+$ and $\mathbf{x}^-$ on opposite faces of the RVE:
    $$ \tilde{\mathbf{u}}(\mathbf{x}^+) = \tilde{\mathbf{u}}(\mathbf{x}^-) \quad \text{and} \quad \mathbf{t}(\mathbf{x}^+) = -\mathbf{t}(\mathbf{x}^-) $$
    The displacement condition can be written in terms of the total displacement as a [jump condition](@entry_id:176163): $\mathbf{u}(\mathbf{x}^+) - \mathbf{u}(\mathbf{x}^-) = \boldsymbol{E} \cdot (\mathbf{x}^+ - \mathbf{x}^-)$. The fluctuation field $\tilde{\mathbf{u}}$ belongs to the space of periodic functions $H^1_{\text{per}}(\Omega_{\mu})^d$. To ensure a unique solution, the rigid body translation mode is removed by enforcing $\langle \tilde{\mathbf{u}} \rangle = \mathbf{0}$.

### The Concept of the Representative Volume Element (RVE)

Not any arbitrary volume of a heterogeneous material can serve as a basis for homogenization. A sample domain qualifies as a **Representative Volume Element (RVE)** only if it is large enough to be statistically representative of the entire material and if its computed macroscopic response is independent of the specific boundary conditions applied.

#### Variational Bounds and the Mechanical Criterion

For a finite-sized sample, the choice of admissible BCs affects the computed effective properties. The over-constraining nature of KUBC prevents the boundary from deforming freely, leading to an artificially stiff response. Conversely, the under-constraining nature of SUBC allows for deformation modes that might not be present in the bulk material, leading to an artificially compliant response. These observations are formalized by variational principles of mechanics, which establish rigorous bounds on the effective [stiffness tensor](@entry_id:176588) $\mathbb{C}^*$ of the infinite medium [@problem_id:2546284]. The effective stiffness computed with KUBC, $\mathbb{C}^{\mathrm{DIR}}$, provides an upper bound, while the stiffness computed with SUBC, $\mathbb{C}^{\mathrm{NEU}}$, provides a lower bound:

$$
\mathbb{C}^{\mathrm{NEU}} \preceq \mathbb{C}^* \preceq \mathbb{C}^{\mathrm{DIR}}
$$

where the relation $\mathbb{A} \preceq \mathbb{B}$ for fourth-order tensors means that $\boldsymbol{\eta} : \mathbb{A} : \boldsymbol{\eta} \le \boldsymbol{\eta} : \mathbb{B} : \boldsymbol{\eta}$ for any symmetric second-order tensor $\boldsymbol{\eta}$. The stiffness computed with PBC, $\mathbb{C}^{\mathrm{PER}}$, typically lies between these bounds.

As the size $L$ of the sample domain increases, these bounds converge towards the true effective tensor $\mathbb{C}^*$. This convergence forms the basis of the **mechanical criterion for an RVE**: a volume $\Omega_L$ is considered an RVE when it is sufficiently large such that the apparent effective properties are insensitive (within a prescribed tolerance) to the choice of admissible boundary conditions. That is, $\mathbb{C}^{\mathrm{NEU}}(L) \approx \mathbb{C}^{\mathrm{PER}}(L) \approx \mathbb{C}^{\mathrm{DIR}}(L)$.

#### Statistical Criteria for Random Media

For materials that are not periodic but are statistically homogeneous, such as a random two-phase composite, the concept of a repeating unit cell does not apply [@problem_id:2546282]. Instead, the RVE must be defined based on statistical principles. We assume the material's property field, e.g., the stiffness $\mathbb{C}(\mathbf{x}, \omega)$, is a **stationary** and **ergodic** random field, where $\omega$ denotes a specific realization from a probability space.

*   **Stationarity** implies that the statistical properties of the field (e.g., mean, variance, [correlation functions](@entry_id:146839)) are invariant with respect to [spatial translation](@entry_id:195093).
*   **Ergodicity** is a more powerful assumption that allows us to replace [ensemble averages](@entry_id:197763) (averages over many different realizations $\omega$) with spatial averages over a single, sufficiently large realization [@problem_id:2546305]. This is the central hypothesis that makes single-RVE simulations physically meaningful.

The ergodicity assumption holds under "mixing" conditions, which essentially state that the material properties at two distant points are statistically independent. This is quantified by the [spatial correlation](@entry_id:203497) length, $\ell_c$, which measures the distance over which microstructural features are correlated. This leads to the **statistical criterion for an RVE**: the size of the element, $L$, must be significantly larger than the [correlation length](@entry_id:143364), $L \gg \ell_c$. When this condition is met, the [ergodicity](@entry_id:146461) assumption ensures that spatial averages of microstructural descriptors (e.g., volume fractions, two-point statistics) computed over the RVE converge to their true ensemble-average values, making the geometry of the domain statistically representative.

In summary, for a random medium, a domain qualifies as an RVE if it meets both the statistical criterion ($L \gg \ell_c$) and the mechanical criterion (insensitivity to BCs and realization) [@problem_id:2546282].

### Computational Procedure for Effective Properties

With the foundational principles established, the practical procedure for computing the effective linear [elastic stiffness tensor](@entry_id:196425) $\mathbb{C}^*$ of an RVE can be summarized as follows [@problem_id:2546292]:

1.  **Discretize the RVE**: Create a finite element (FE) mesh of the RVE domain $\Omega_{\mu}$, ensuring the mesh is fine enough to resolve the geometric and material details of the microstructure.

2.  **Select a Basis of Load Cases**: To determine all the components of the symmetric fourth-order tensor $\mathbb{C}^*$, a set of linearly independent macroscopic strain tests must be performed. In three dimensions, this requires 6 tests. A standard choice is a basis $\{\boldsymbol{E}^{(k)}\}_{k=1}^{6}$ consisting of three uniaxial strains and three pure shear strains.

3.  **Solve Microscopic BVP for Each Load Case**: For each basis strain $\boldsymbol{E}^{(k)}$:
    a.  Apply admissible boundary conditions (e.g., KUBC or PBC) to the RVE's FE model to enforce the macroscopic strain $\boldsymbol{E}^{(k)}$.
    b.  Solve the microscopic linear elastic boundary value problem, $\nabla \cdot (\mathbb{C}(\mathbf{x}) : \boldsymbol{\varepsilon}(\mathbf{u}^{(k)})) = \mathbf{0}$, to find the microscopic [displacement field](@entry_id:141476) $\mathbf{u}^{(k)}(\mathbf{x})$.
    c.  Post-process the solution to find the microscopic strain field $\boldsymbol{\varepsilon}^{(k)}(\mathbf{x})$ and the stress field $\boldsymbol{\sigma}^{(k)}(\mathbf{x}) = \mathbb{C}(\mathbf{x}) : \boldsymbol{\varepsilon}^{(k)}(\mathbf{x})$.

4.  **Compute Macroscopic Stresses**: For each load case, compute the corresponding macroscopic stress $\boldsymbol{\Sigma}^{(k)}$ by volume averaging the microscopic stress field:
    $$
    \boldsymbol{\Sigma}^{(k)} = \langle \boldsymbol{\sigma}^{(k)} \rangle = \frac{1}{|\Omega_{\mu}|} \int_{\Omega_{\mu}} \boldsymbol{\sigma}^{(k)}(\mathbf{x}) \, \mathrm{d}V
    $$

5.  **Assemble the Effective Stiffness Tensor**: The components of the effective [stiffness tensor](@entry_id:176588) $\mathbb{C}^*$ are found by solving the system of linear equations relating the macroscopic stress and strain pairs:
    $$
    \boldsymbol{\Sigma}^{(k)} = \mathbb{C}^* : \boldsymbol{E}^{(k)} \quad \text{for } k=1, \dots, 6
    $$
    If the standard basis strains are used, the columns of the $6 \times 6$ [matrix representation](@entry_id:143451) of $\mathbb{C}^*$ are simply the computed macroscopic stress vectors (in Voigt notation).

### Advanced Topics and Practical Considerations

The first-order homogenization framework, while powerful, has important extensions and limitations that are critical for its correct application.

#### Nonlinear Materials and the FE² Method

When the microscopic constitutive law is nonlinear and history-dependent (e.g., plasticity, damage), the effective response also becomes nonlinear. The **FE² method** is a powerful computational strategy for such problems. It involves a two-scale analysis: a macroscopic FE simulation is run, and at each macroscopic Gauss point, a full microscopic FE simulation is performed on an RVE to determine the local macroscopic [stress response](@entry_id:168351).

The core of the FE² algorithm at a single macro-Gauss point involves the following [@problem_id:2546309]:
1.  **Stress Update**: Given the history of macroscopic strain and the current increment, the macroscopic strain $\boldsymbol{E}$ is imposed on the RVE (e.g., via PBC). The nonlinear microscopic BVP is solved incrementally to find the updated microscopic stress field $\boldsymbol{\sigma}(\mathbf{x})$. The macroscopic stress is then returned to the macro-solver using the averaging rule: $\boldsymbol{\Sigma} = \langle \boldsymbol{\sigma} \rangle$.
2.  **Consistent Tangent Modulus**: For the macroscopic Newton-Raphson solver to achieve a quadratic [rate of convergence](@entry_id:146534), it requires the consistent macroscopic tangent modulus, $\mathbb{C}^{\text{alg}} = \frac{\partial \boldsymbol{\Sigma}}{\partial \boldsymbol{E}}$. This is not simply the average of the microscopic tangent, $\langle \mathbb{c}^{\text{alg}} \rangle$. A [consistent linearization](@entry_id:747732) of the entire micro-problem shows that the correct tangent is:
    $$
    \mathbb{C}^{\text{alg}} = \left\langle \mathbb{c}^{\text{alg}} : \frac{\partial \boldsymbol{\varepsilon}}{\partial \boldsymbol{E}} \right\rangle = \left\langle \mathbb{c}^{\text{alg}} : \left( \mathbf{I}^{s} + \nabla^{s}\left(\frac{\partial \tilde{\mathbf{u}}}{\partial \boldsymbol{E}}\right) \right) \right\rangle
    $$
    Here, $\mathbb{c}^{\text{alg}}$ is the microscopic [algorithmic tangent](@entry_id:165770), $\mathbf{I}^{s}$ is the fourth-order symmetric identity tensor, and $\frac{\partial \tilde{\mathbf{u}}}{\partial \boldsymbol{E}}$ is the sensitivity of the microscopic displacement fluctuation field with respect to a change in macroscopic strain. This sensitivity must be computed by solving an additional linear system derived from linearizing the discrete microscopic [equilibrium equations](@entry_id:172166).

#### Finite-Size Effects and Bias in Random Media

As noted earlier, applying PBC to a finite sample of a random, non-periodic medium is an approximation. This introduces artificial [periodicity](@entry_id:152486) that suppresses long-wavelength fluctuations and creates spurious correlations, leading to a systematic **finite-size bias** in the computed effective properties. The expectation of the apparent stiffness from a finite RVE, $\mathbb{E}[\mathbb{C}_L^{\mathrm{PBC}}]$, is generally not equal to the true bulk stiffness $\mathbb{C}^*$, with the bias decaying as the RVE size $L$ increases, often scaling as $\mathcal{O}(\ell_c/L)$ [@problem_id:2546301].

To mitigate this bias in practical computations, an advanced technique is **[oversampling](@entry_id:270705) and windowing**. The strategy involves:
1.  Solving the microscopic problem with PBC on an enlarged domain $\Omega_{\alpha L}$ with side length $\alpha L$, where $\alpha > 1$.
2.  Computing the effective properties not by averaging over the entire domain, but by using a weighted average concentrated on the central window of size $L$. The weighting (or window) function smoothly tapers to zero near the boundaries of the larger domain.
This method effectively de-emphasizes the contributions from the boundary regions most affected by the artificial periodicity, yielding a more accurate, less biased estimate of the true bulk response.

#### Limitations and Failure Modes

The validity of first-order [homogenization](@entry_id:153176) hinges on the assumption of **[scale separation](@entry_id:152215)**, which posits a clear separation between the [characteristic length](@entry_id:265857) scale of the microstructure ($\ell_c$) and the length scale of variation of the macroscopic fields. This assumption can be violated under certain conditions.

*   **Microscale Strain Localization**: If the constitutive behavior at the microscale exhibits [strain softening](@entry_id:185019) (a decrease in stress with increasing strain), the microscopic [boundary value problem](@entry_id:138753) can become ill-posed. This is because the governing equations may lose [ellipticity](@entry_id:199972), leading to the formation of **[strain localization](@entry_id:176973) bands** [@problem_id:2546338]. In a standard local continuum model, these bands have zero theoretical width, and in an FE simulation, their width is dictated by the non-physical mesh size. This [pathological mesh dependency](@entry_id:184469) breaks [scale separation](@entry_id:152215), as the internal length scale of the localization band becomes comparable to the RVE size itself. The computed RVE response is no longer objective, and this [ill-posedness](@entry_id:635673) propagates to the macroscale, causing the homogenized tangent to lose positive definiteness and the overall FE² solution to exhibit spurious macroscopic [mesh dependency](@entry_id:198563). The remedy for this [pathology](@entry_id:193640) lies in regularizing the microscale problem by using an "enriched" continuum theory (e.g., gradient-enhanced, nonlocal, or viscous models) that introduces a physical internal length scale.

*   **Broken Ergodicity**: The ability to replace an [ensemble average](@entry_id:154225) with a single spatial average is not universally guaranteed. The [ergodicity](@entry_id:146461) assumption fails if the probability space of the random medium can be decomposed into multiple disjoint, translation-invariant subsets with positive probability [@problem_id:2546305]. A physical example is a polycrystal where different realizations might belong to distinct families of crystallographic textures. A spatial average over a single realization will converge to a value characteristic of its particular family, which is not necessarily the same as the unconditional ensemble average over all families. In this case of **[broken ergodicity](@entry_id:154097)**, a single RVE is no longer "representative" of the ensemble. Similarly, media with very slow-decaying, long-range correlations (e.g., covariance decaying as $\|\mathbf{r}\|^{-\alpha}$ with $\alpha \le d$ in $d$ dimensions) can also exhibit non-ergodic behavior, where the homogenized properties may remain random even in the infinite-volume limit.