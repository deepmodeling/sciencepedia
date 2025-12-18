## Introduction
In the study of isolated gravitational systems within General Relativity, defining fundamental quantities like total mass and angular momentum is a non-trivial challenge, as the gravitational field itself contributes to the system's energy. The Arnowitt-Deser-Misner (ADM) formalism provides the definitive answer, establishing a robust framework for calculating these [conserved charges](@entry_id:145660) by examining the gravitational field's behavior at the asymptotic boundaries of spacetime. This article bridges the gap between the abstract theory and its practical application, guiding the reader through the foundational concepts that are indispensable for modeling systems like [binary black hole mergers](@entry_id:746798).

Across the following chapters, you will gain a comprehensive understanding of the ADM charges. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, exploring the concepts of [asymptotic flatness](@entry_id:158269), the integral definitions of the charges, and their deep connection to spacetime symmetries and the Positive Mass Theorem. Following this foundation, the **Applications and Interdisciplinary Connections** chapter will demonstrate the formalism's crucial role in constructing initial data for numerical simulations, validating their accuracy through conservation laws, and forging connections to astrophysics and [black hole thermodynamics](@entry_id:136383). Finally, the **Hands-On Practices** section offers a series of guided problems, allowing you to apply these concepts to canonical spacetimes like Minkowski and Schwarzschild, solidifying your theoretical knowledge through practical calculation.

## Principles and Mechanisms

In the study of isolated gravitational systems, such as [binary black hole mergers](@entry_id:746798) or collapsing stars, a fundamental challenge is to quantify global properties like the total mass, momentum, and angular momentum. These concepts, while straightforward in Newtonian physics, require a careful and rigorous definition in the context of General Relativity, where the gravitational field itself carries energy and momentum. The Arnowitt-Deser-Misner (ADM) formalism provides a robust framework for defining these [conserved quantities](@entry_id:148503) by examining the asymptotic structure of the gravitational field on a spacelike hypersurface. This chapter delves into the principles and mechanisms underpinning the ADM charges, from their mathematical definition to their profound theoretical implications and practical limitations.

### Asymptotic Flatness and Boundary Conditions

The ADM formalism is rooted in the Hamiltonian, or $3+1$, decomposition of spacetime. Within this framework, we consider an initial data set on a three-dimensional spacelike Cauchy slice, $\Sigma$, characterized by its intrinsic Riemannian metric, $\gamma_{ij}$, and its [extrinsic curvature](@entry_id:160405), $K_{ij}$. The concept of an "isolated system" is mathematically captured by the condition of **[asymptotic flatness](@entry_id:158269)**: far from the central source, spacetime should approach the flat Minkowski spacetime. On the slice $\Sigma$, this means that as the coordinate radius $r = \sqrt{x^i x^i}$ approaches infinity, the spatial metric $\gamma_{ij}$ should approach the Euclidean metric $\delta_{ij}$, and the [extrinsic curvature](@entry_id:160405) $K_{ij}$ should approach zero.

However, for the ADM integrals to yield finite and physically meaningful quantities, more precise [fall-off conditions](@entry_id:157952) are required. The minimal set of conditions that ensures the ADM mass, linear momentum, and angular momentum are finite, independent of the choice of asymptotic origin, and invariant under appropriate [coordinate transformations](@entry_id:172727) are known as the Regge-Teitelboim conditions . These conditions involve not only the rate of decay but also the parity of the asymptotic fields under inversion of the coordinates, $\vec{x} \mapsto -\vec{x}$.

Specifically, the spatial metric $\gamma_{ij}$ and extrinsic curvature $K_{ij}$ must satisfy the following [asymptotic behavior](@entry_id:160836):

1.  **Spatial Metric ($\gamma_{ij}$):**
    *   $\gamma_{ij} = \delta_{ij} + \mathcal{O}(r^{-1})$. For the ADM mass to be well-defined and independent of the origin of the coordinate system, the leading $\mathcal{O}(r^{-1})$ term must have **even parity**.
    *   The derivatives must fall off as $\partial_k \gamma_{ij} = \mathcal{O}(r^{-2})$ and $\partial_l \partial_k \gamma_{ij} = \mathcal{O}(r^{-3})$.
    *   Sufficient differentiability, typically $\gamma_{ij} \in \mathcal{C}^2$, is required for the constraint equations to hold asymptotically.

2.  **Extrinsic Curvature ($K_{ij}$):**
    *   $K_{ij} = \mathcal{O}(r^{-2})$. For the ADM angular momentum integral to converge, the leading $\mathcal{O}(r^{-2})$ term must have **odd parity**. As we will see, this parity choice cancels a potentially divergent term in the angular momentum definition.
    *   The derivative must fall off as $\partial_k K_{ij} = \mathcal{O}(r^{-3})$.
    *   Sufficient [differentiability](@entry_id:140863), typically $K_{ij} \in \mathcal{C}^1$, is needed.

These parity conditions are not arbitrary mathematical constraints; they are essential for isolating the physical charges from gauge-dependent artifacts arising from coordinate choices, such as shifting the origin of the asymptotic coordinate system .

### Integral Definitions and Numerical Computation

With the appropriate asymptotic behavior established, the ADM [conserved quantities](@entry_id:148503) are defined as [surface integrals](@entry_id:144805) over a 2-sphere $S_r$ in the limit as its radius $r$ approaches infinity. Let $n^i = x^i/r$ be the outward-pointing [unit normal vector](@entry_id:178851) on $S_r$.

The **ADM energy**, or mass, $M_{\text{ADM}}$ is defined by:
$$
M_{\text{ADM}} = \frac{1}{16\pi} \lim_{r\to\infty} \oint_{S_r} (\partial_j h_{ij} - \partial_i h) n^i dS
$$
where $h_{ij} = \gamma_{ij} - \delta_{ij}$ is the [metric perturbation](@entry_id:157898) and $h = \delta^{kl}h_{kl}$ is its trace. The integrand, which involves first derivatives of the metric, falls off as $\mathcal{O}(r^{-2})$. Since the [area element](@entry_id:197167) $dS$ grows as $r^2$, the integral converges to a finite value. By applying the [divergence theorem](@entry_id:145271), this [surface integral](@entry_id:275394) can be converted into a volume integral over the interior of the slice :
$$
M_{\text{ADM}} = \frac{1}{16\pi} \int_{\Sigma} (\partial_i \partial_j h_{ij} - \nabla^2 h) dV
$$
This equivalence is not only theoretically elegant but also practically useful in numerical relativity, allowing for mass to be computed either as a flux through a boundary or as a sum over the computational grid. For the important special case of conformally flat initial data, where the spatial metric is given by $\gamma_{ij} = \psi^4 \delta_{ij}$ for some conformal factor $\psi$, the ADM mass formula simplifies significantly to :
$$
M_{\text{ADM}} = -\frac{1}{8\pi} \lim_{r\to\infty} \oint_{S_r} (\vec{\nabla} \psi^4) \cdot \vec{n} \, dS = -\frac{1}{2} \lim_{r\to\infty} r^2 \partial_r (\psi^4)
$$
where the last equality holds if $\psi$ is spherically symmetric asymptotically.

The **ADM linear momentum** $P_i$ is defined in terms of the [extrinsic curvature](@entry_id:160405):
$$
P_i = \frac{1}{8\pi} \lim_{r\to\infty} \oint_{S_r} (K_{ij} - K \gamma_{ij}) n^j dS
$$
where $K = \gamma^{ij}K_{ij}$ is the trace of the [extrinsic curvature](@entry_id:160405). The integrand is required to fall off as $\mathcal{O}(r^{-2})$ for convergence, which is guaranteed by the asymptotic conditions on $K_{ij}$.

The **ADM angular momentum** $J_i$ is the moment of the linear [momentum density](@entry_id:271360). Its definition involves the asymptotic rotational Killing vectors of Euclidean space, $\phi^k_{(i)} = \epsilon_{ikj} x^j$, which provide the "[lever arm](@entry_id:162693)" :
$$
J_i = \frac{1}{8\pi} \lim_{r\to\infty} \oint_{S_r} \epsilon_{ikj} x^k (K^j{}_l - \delta^j_l K) n^l dS
$$
Here, the presence of the lever arm $x^k = r n^k$ would make the integral diverge if the integrand were $\mathcal{O}(r^{-2})$. However, the odd-parity condition imposed on the $\mathcal{O}(r^{-2})$ part of $K_{ij}$ causes the integral of this leading-order term to vanish over the sphere. The finite value of $J_i$ thus arises from higher-order contributions, ensuring the integral is well-defined  .

### Physical Interpretation as Asymptotic Multipoles

The ADM charges are not just abstract mathematical quantities; they correspond directly to the [multipole moments](@entry_id:191120) of the asymptotic gravitational field. By expanding the metric and extrinsic curvature in terms of tensor spherical harmonics, we can identify which parts of the field carry the information about mass, momentum, and angular momentum .

*   The **ADM mass $M_{\text{ADM}}$** is sourced by the monopole ($l=0$), even-parity component of the $\mathcal{O}(r^{-1})$ part of the [metric perturbation](@entry_id:157898), $h^{(1)}_{ij}$. This component is precisely what one would expect from the Newtonian potential of a point mass, $h_{ij} \approx (2M/r)\delta_{ij}$.

*   The **ADM [linear momentum](@entry_id:174467) $P_i$** is sourced by the dipole ($l=1$), odd-parity component of the $\mathcal{O}(r^{-2})$ part of the extrinsic curvature, $K^{(2)}_{ij}$.

*   The **ADM angular momentum $J_i$** is sourced by the dipole ($l=1$), even-parity component of the *next-to-leading order* term in the extrinsic curvature, $K^{(3)}_{ij}$.

This decomposition reveals a beautiful hierarchy: the global charges of the spacetime are encoded in the lowest-order [multipole moments](@entry_id:191120) of the asymptotic gravitational field. It also provides a physical interpretation for the parity conditions: they serve to isolate these specific multipole components, which transform correctly under Poincaré transformations, from other gauge-dependent or higher-order effects.

### Theoretical Foundations: Symmetries and Conservation

The profound significance of the ADM charges stems from their role as conserved quantities associated with the [asymptotic symmetries](@entry_id:155403) of spacetime. An [isolated system](@entry_id:142067) in an [asymptotically flat spacetime](@entry_id:192015) is expected to respect the symmetries of the Minkowski background at large distances—namely, the Poincaré symmetries of time translations, spatial translations, rotations, and boosts.

In the Hamiltonian formulation, every continuous symmetry has a corresponding conserved charge, which is the generator of that symmetry transformation. The ADM charges are precisely the Hamiltonian generators for the asymptotic Poincaré group at **spatial infinity** ($i^0$)  .
*   $M_{\text{ADM}}$ is the generator of asymptotic time translations.
*   $P_i$ are the generators of asymptotic spatial translations.
*   $J_i$ are the generators of asymptotic rotations.

This connection establishes why the ADM charges are conserved (i.e., time-independent). They are tied to the [fundamental symmetries](@entry_id:161256) of the asymptotic spacetime structure.

A subtle but crucial point arises when one considers the full set of symmetries that preserve the asymptotic boundary conditions. This full set, known as the Spi group, is an infinite-dimensional group that includes not only the Poincaré transformations but also "[supertranslations](@entry_id:755663)"—angle-dependent translations at infinity . If all these symmetries had well-behaved generators, there would be an infinite number of [conserved charges](@entry_id:145660), obscuring the physical meaning of mass and momentum.

This is where the Regge-Teitelboim parity conditions play their most profound role. By imposing these parity constraints on the phase space of [gravitational fields](@entry_id:191301), one ensures that only the generators corresponding to the ten-dimensional Poincaré subgroup remain finite and integrable. The charges associated with [supertranslations](@entry_id:755663) either vanish or become ill-defined. Thus, the parity conditions are a physical requirement that selects the standard Poincaré group as the true asymptotic symmetry group, thereby uniquely identifying the ten ADM charges as the physically meaningful conserved quantities of the isolated system .

### The Positive Mass Theorem

One of the most celebrated results in classical General Relativity is the **Positive Mass Theorem**, which establishes a fundamental property of the ADM mass. The theorem provides a crucial stability condition for gravity, ensuring that asymptotically flat spacetimes cannot have negative total energy, which would allow for catastrophic decay of the vacuum.

The theorem states :

> For any complete, asymptotically flat initial data set $(\Sigma, \gamma_{ij}, K_{ij})$ that satisfies the **Dominant Energy Condition** (DEC), the ADM [energy-momentum four-vector](@entry_id:156403) $P^{\mu}$ is a future-directed and causal (timelike or null) vector. This implies that the ADM mass is non-negative, $M_{\text{ADM}} \ge 0$.
>
> Furthermore, the theorem includes a **rigidity statement**: If $M_{\text{ADM}} = 0$, then the initial data set must be trivial, corresponding to a slice of flat Minkowski spacetime. That is, $(\Sigma, \gamma_{ij})$ is isometric to Euclidean space $(\mathbb{R}^3, \delta_{ij})$, and the [extrinsic curvature](@entry_id:160405) $K_{ij}$ is zero everywhere.

The Dominant Energy Condition, which stipulates that the energy density $\rho$ as measured by any observer is non-negative and that the energy-momentum flux can never travel faster than light (formally, $\rho \ge \|j\|$), is a physically reasonable constraint on matter.

The original proof by Schoen and Yau used techniques from [differential geometry](@entry_id:145818), while a later, more elegant proof by Edward Witten introduced the use of [spinors](@entry_id:158054) . Witten's proof strategy involves defining a special [spinor](@entry_id:154461) field $\psi$ on the slice $\Sigma$ that satisfies the Witten equation, $D\!\!\!/ \psi = 0$, and asymptotes to a constant value. From this [spinor](@entry_id:154461), one constructs the Nester-Witten 2-form. Using Stokes' theorem, the ADM mass can be expressed as the volume integral of the [exterior derivative](@entry_id:161900) of this 2-form. The key insight is that, by using the Einstein [constraint equations](@entry_id:138140) and the dominant energy condition, this volume integrand can be shown to be manifestly non-negative. This directly implies $M_{\text{ADM}} \ge 0$, and the rigidity statement follows from showing that the integrand can only be zero if the spacetime is flat.

### Context and Limitations in Numerical Relativity

While the ADM charges are foundational, it is critical for practitioners in numerical relativity to understand their context and limitations.

First, the ADM mass can be compared with other definitions, such as the **Komar mass**, which is defined for stationary spacetimes possessing a timelike Killing vector $\xi^{\mu}$. For such spacetimes, the Komar and ADM masses are equal . However, the ADM definition is more general, as it does not require an exact symmetry, only an asymptotic one, and thus applies to dynamical, radiating spacetimes.

The most important distinction is between the ADM framework at spatial infinity ($i^0$) and the Bondi-Sachs framework at **[future null infinity](@entry_id:261525)** ($\mathscr{I}^{+}$) .
*   **Spatial Infinity ($i^0$) and ADM Mass:** The ADM mass is a single, conserved quantity for the entire evolution. It is calculated on a spacelike slice and represents the total energy content of that slice, including the energy that is "in flight" in the form of gravitational waves. As such, $M_{\text{ADM}}$ does not decrease as the system radiates energy. It is the total mass of the system as measured "from outside of space and time."
*   **Null Infinity ($\mathscr{I}^{+}$) and Bondi Mass:** The Bondi mass, $M_{\text{B}}$, is defined on cuts of [future null infinity](@entry_id:261525), where outgoing radiation is actually detected. In a radiating spacetime, the Bondi mass is *not* conserved. It decreases with time according to the famous Bondi mass-loss formula, which states that the rate of [mass loss](@entry_id:188886) is equal to the flux of energy carried away by gravitational waves.

This distinction is crucial: ADM mass is a conserved charge characterizing the entire spacetime, while Bondi mass is a time-dependent quantity that reflects the dynamic process of energy loss through radiation.

This has direct consequences for modern numerical simulations, which often employ **hyperboloidal foliations**. These are Cauchy slices that, instead of approaching spatial infinity ($i^0$), extend to and intersect [future null infinity](@entry_id:261525) ($\mathscr{I}^{+}$) . On such slices, the fundamental assumptions of the ADM formalism are violated: the boundary is at $\mathscr{I}^{+}$, the asymptotic [symmetry group](@entry_id:138562) is the BMS group, and the slice normal becomes null. Consequently, **ADM charges are not defined on hyperboloidal slices**. The physically appropriate quantities to compute on the boundary of these slices are the Bondi-Sachs charges and their associated fluxes, which provide a direct measure of the emitted [gravitational radiation](@entry_id:266024).