## Introduction
The ability to design, operate, and ensure the safety of a nuclear reactor hinges on a quantitative understanding of the neutron population within its core. The behavior of these neutrons—their movement, their interactions with matter, and the chain reactions they sustain—is the engine that drives the reactor. To move from the microscopic probabilities of nuclear interactions to the macroscopic performance of a power-generating system, a rigorous mathematical and physical framework is essential. This framework is built upon the concepts of neutron flux, current, and the resulting reaction rates.

This article addresses the fundamental need to bridge the gap between microscopic nuclear data and observable reactor behavior. It provides a comprehensive exploration of the theoretical tools used to describe and quantify the neutron field. By mastering these concepts, you will gain insight into the core principles that underpin modern [nuclear reactor simulation](@entry_id:1128946) and analysis.

The article is structured to build your understanding systematically. The "Principles and Mechanisms" chapter will establish the formal definitions of angular and scalar neutron flux, [neutron current](@entry_id:1128689), and cross sections, culminating in the fundamental formula for calculating reaction rates and its practical implementation in the [multigroup method](@entry_id:1128305). Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these concepts are applied to solve real-world problems in reactor design, safety analysis, computational physics, and even in related fields like fusion energy and materials science. Finally, the "Hands-On Practices" section provides targeted problems to solidify your comprehension and apply these principles in practical scenarios. Our exploration begins with the foundational concepts that form the bedrock of reactor physics.

## Principles and Mechanisms

The behavior of neutrons within a nuclear reactor is governed by their transport through and interaction with matter. To quantify these phenomena, we must first establish a rigorous mathematical and physical framework. This chapter introduces the fundamental quantities used to describe the neutron population—flux and current—and develops the principles for calculating the rates of nuclear reactions, which are the ultimate drivers of reactor performance. We will explore these concepts from first principles and extend them to the practical methodologies used in modern reactor simulation.

### Fundamental Quantities: Neutron Flux and Current

The state of the neutron population in a reactor is dynamic and complex, varying with position, energy, and direction of travel. A complete description requires a [phase-space distribution](@entry_id:151304) function that captures all this information.

#### The Angular Neutron Flux

The most fundamental quantity in [neutron transport](@entry_id:159564) theory is the **[angular neutron flux](@entry_id:1121012)**, denoted $\psi(\mathbf{r}, \boldsymbol{\Omega}, E, t)$. This is a scalar function of seven variables: position $\mathbf{r}$, direction of motion (a [unit vector](@entry_id:150575)) $\boldsymbol{\Omega}$, kinetic energy $E$, and time $t$. The angular flux is formally defined as the rate at which neutrons, characterized by a [specific energy](@entry_id:271007) and direction, traverse a unit area oriented perpendicular to their direction of motion.

To build this concept from a more elementary quantity, consider the **angular neutron [number density](@entry_id:268986)**, $n(\mathbf{r}, \boldsymbol{\Omega}, E, t)$, which represents the expected number of neutrons per unit volume, per unit solid angle around $\boldsymbol{\Omega}$, and per unit energy around $E$. Neutrons of energy $E$ travel at a speed $v(E)$. In a small time interval $dt$, these neutrons travel a distance $ds = v(E)dt$. The number of such neutrons crossing a small area $dA$ normal to $\boldsymbol{\Omega}$ is the number contained in the [volume element](@entry_id:267802) $dV = dA \cdot ds = dA \cdot v(E)dt$. This number is $n(\mathbf{r}, \boldsymbol{\Omega}, E, t) \, dV \, d\boldsymbol{\Omega} \, dE$. The rate of crossing per unit area, per unit solid angle, and per unit energy is therefore $n(\mathbf{r}, \boldsymbol{\Omega}, E, t)v(E)$. This leads to the fundamental relationship:

$$ \psi(\mathbf{r}, \boldsymbol{\Omega}, E, t) = v(E) n(\mathbf{r}, \boldsymbol{\Omega}, E, t) $$

The units of angular flux are typically neutrons $\cdot \text{cm}^{-2} \cdot \text{s}^{-1} \cdot \text{sr}^{-1} \cdot \text{MeV}^{-1}$. Due to its definition, the angular flux can also be interpreted as the total path length traveled per unit time, per unit volume, by neutrons of a specific energy and direction. This interpretation is key to understanding the calculation of reaction rates. 

#### The Scalar Neutron Flux

While the angular flux provides a complete description, in many applications, particularly those involving reaction rates in isotropic media, it is sufficient to know the total number of neutrons at a point, regardless of their direction. This leads to the definition of the **scalar neutron flux**, denoted $\phi(\mathbf{r}, E, t)$. It is obtained by integrating the angular flux over all possible directions (a solid angle of $4\pi$ steradians):

$$ \phi(\mathbf{r}, E, t) = \int_{4\pi} \psi(\mathbf{r}, \boldsymbol{\Omega}, E, t) \, d\boldsymbol{\Omega} $$

The [scalar flux](@entry_id:1131249) has units of neutrons $\cdot \text{cm}^{-2} \cdot \text{s}^{-1} \cdot \text{MeV}^{-1}$. Physically, it represents the total path length traveled per unit volume, per unit time, by all neutrons of energy $E$ at position $\mathbf{r}$, irrespective of their direction of travel. Alternatively, since $\phi = \int v(E)n(\mathbf{r}, \boldsymbol{\Omega}, E, t)d\boldsymbol{\Omega} = v(E)N(\mathbf{r}, E, t)$, where $N(\mathbf{r}, E, t)$ is the total neutron number density at energy $E$, the [scalar flux](@entry_id:1131249) can be seen as the product of the neutron density and their speed. It quantifies the total "neutron traffic" at a point. 

#### The Neutron Current Density

The scalar flux describes the magnitude of neutron motion, but not its directionality. To describe the net flow of neutrons, we define the **neutron current density** vector, $\mathbf{J}(\mathbf{r}, E, t)$. This vector quantity is the first angular moment of the angular flux:

$$ \mathbf{J}(\mathbf{r}, E, t) = \int_{4\pi} \boldsymbol{\Omega} \, \psi(\mathbf{r}, \boldsymbol{\Omega}, E, t) \, d\boldsymbol{\Omega} $$

The neutron current density vector points in the direction of the net flow of neutrons. Its magnitude represents the net number of neutrons of energy $E$ crossing a unit area oriented perpendicular to the direction of net flow, per unit time. For an arbitrarily oriented surface with a [unit normal vector](@entry_id:178851) $\mathbf{n}$, the [scalar product](@entry_id:175289) $\mathbf{J} \cdot \mathbf{n}$ gives the net rate of neutron flow per unit area across that surface.

It is crucial to distinguish between scalar flux and current. An isotropic angular flux, where $\psi$ is independent of $\boldsymbol{\Omega}$, results in a large scalar flux but a zero net current, as neutrons cross any given surface equally in both directions. A net current arises only when the angular flux is anisotropic. For instance, consider a steady-state, monoenergetic neutron population with an angular flux that has a [linear dependence](@entry_id:149638) on $\mu = \cos\theta$, where $\theta$ is the [polar angle](@entry_id:175682) with respect to the $z$-axis: $\psi(\mu) = \psi_0(1+a\mu)$. Here, a positive value of the anisotropy parameter $a$ implies that more neutrons are traveling in the forward ($+z$) direction than in the backward ($-z$) direction. The [scalar flux](@entry_id:1131249) is calculated as $\phi = \int_0^{2\pi}d\varphi \int_{-1}^1 d\mu \, \psi_0(1+a\mu) = 4\pi\psi_0$. The net current, however, is non-zero only in the $z$-direction: $J_z = \int_0^{2\pi}d\varphi \int_{-1}^1 d\mu \, (\mu) \psi_0(1+a\mu) = \frac{4\pi}{3} a \psi_0$. This demonstrates that current is a direct measure of the anisotropy of the neutron field. 

### The Physics of Neutron Interactions: Cross Sections and Reaction Rates

Neutrons traversing a medium interact with atomic nuclei through various processes such as absorption, scattering, and fission. The likelihood of these interactions is quantified by cross sections, which, when combined with the neutron flux, determine the rates of these reactions.

#### Microscopic and Macroscopic Cross Sections

The intrinsic probability of a specific interaction between a single neutron of energy $E$ and a single target nucleus is described by the **microscopic cross section**, $\sigma_x(E)$, for reaction type $x$. This quantity has units of area and can be thought of as the effective target area the nucleus presents to the incident neutron for that reaction. A common unit for microscopic cross sections is the barn, where $1 \text{ barn} = 10^{-24} \text{ cm}^2$.

In reactor analysis, we are concerned with the bulk properties of materials. We define the **macroscopic cross section**, $\Sigma_x(\mathbf{r}, E)$, as the probability of a reaction of type $x$ occurring per unit path length traveled by a neutron in the material at position $\mathbf{r}$. If the material contains a single nuclide with [number density](@entry_id:268986) $N$ (nuclei per unit volume), the [macroscopic cross section](@entry_id:1127564) is given by:

$$ \Sigma_x(\mathbf{r}, E) = N(\mathbf{r}) \sigma_x(E) $$

The units of $\Sigma_x$ are inverse length (e.g., $\text{cm}^{-1}$). If the material is a mixture of nuclides, the total macroscopic cross section is the sum of the contributions from each constituent nuclide $i$: $\Sigma_x(\mathbf{r}, E) = \sum_i N_i(\mathbf{r}) \sigma_{x,i}(E)$. 

#### The Fundamental Reaction Rate Formula

The **reaction rate density**, $R_x(\mathbf{r}, E)$, is the number of reactions of type $x$ occurring per unit volume, per unit time, and per unit energy at $(\mathbf{r}, E)$. It is found by combining the physical interpretations of scalar flux and macroscopic cross section. The scalar flux $\phi(\mathbf{r}, E)$ is the total path length traveled by neutrons of energy $E$ per unit volume per unit time. The macroscopic cross section $\Sigma_x(E)$ is the probability of reaction $x$ per unit path length. Therefore, their product gives the reaction rate density:

$$ R_x(\mathbf{r}, E) = \Sigma_x(\mathbf{r}, E) \phi(\mathbf{r}, E) $$

To find the total reaction rate density for reaction $x$ at a point $\mathbf{r}$, integrated over all neutron energies, we simply integrate this expression over $E$:

$$ R_x(\mathbf{r}) = \int_0^{\infty} \Sigma_x(\mathbf{r}, E) \phi(\mathbf{r}, E) \, dE $$

This integral formula is one of the most fundamental and widely used equations in reactor physics. It links the nuclear data ($\Sigma_x$) and the neutron population ($\phi$) to a macroscopic observable (the reaction rate). The total number of reactions of type $x$ occurring per second in a volume $V$ is then simply $\int_V R_x(\mathbf{r}) dV$. 

This framework holds when the interaction probability is independent of the neutron's direction. If the cross section itself is anisotropic, $\Sigma_x(\mathbf{r}, E, \boldsymbol{\Omega})$, one must revert to the angular flux to compute the reaction rate density correctly: $R_x(\mathbf{r}, E) = \int_{4\pi} \Sigma_x(\mathbf{r}, E, \boldsymbol{\Omega}) \psi(\mathbf{r}, E, \boldsymbol{\Omega}) d\boldsymbol{\Omega}$. 

#### Distinguishing Reaction Types: Sinks and Sources

The neutron balance within a reactor is an accounting of processes that remove neutrons (sinks) and processes that produce them (sources). Reaction rates are the basis for quantifying these terms.

*   **Removal Reactions (Sinks):** The simplest sink term is **absorption**, where a neutron is captured by a nucleus and effectively removed from the population. The absorption rate, $R_a(\mathbf{r})$, is calculated by integrating over all initial neutron states that lead to absorption:
    $$ R_a(\mathbf{r}) = \int_0^\infty dE \int_{4\pi} d\boldsymbol{\Omega} \; \Sigma_a(\mathbf{r},E) \, \psi(\mathbf{r},E,\boldsymbol{\Omega}) = \int_0^\infty \Sigma_a(\mathbf{r},E) \phi(\mathbf{r},E) \, dE $$

*   **Source Reactions:** Other reactions act as sources, producing neutrons or changing their state.
    1.  **Scattering Source:** In a scattering event, a neutron is not lost but is transferred from an initial state $(E, \boldsymbol{\Omega})$ to a final state $(E', \boldsymbol{\Omega}')$. The **differential macroscopic [scattering cross section](@entry_id:150101)**, $\Sigma_s(\mathbf{r}; E \to E', \boldsymbol{\Omega} \to \boldsymbol{\Omega}')$, describes this transfer. The rate at which neutrons appear in the final state $(E', \boldsymbol{\Omega}')$ due to scattering from all possible initial states is the **in-scatter source density**, found by integrating over all initial energies and directions:
        $$ R_s(\mathbf{r},E',\boldsymbol{\Omega}') = \int_0^\infty dE \int_{4\pi} d\boldsymbol{\Omega} \; \Sigma_s(\mathbf{r};E,\boldsymbol{\Omega}\to E',\boldsymbol{\Omega}') \, \psi(\mathbf{r},E,\boldsymbol{\Omega}) $$

    2.  **Fission Source:** In a fission event, one neutron is absorbed, and several new neutrons are produced. This is the primary source term in a self-sustaining reactor. The total rate of fission neutron production per unit volume, $S_f(\mathbf{r})$, is found by multiplying the fission reaction rate by the average number of neutrons produced per fission, $\nu(E)$:
        $$ S_f(\mathbf{r}) = \int_0^\infty dE \int_{4\pi} d\boldsymbol{\Omega} \; \nu(\mathbf{r},E) \, \Sigma_f(\mathbf{r},E) \, \psi(\mathbf{r},E,\boldsymbol{\Omega}) $$
        These newly born neutrons have a characteristic energy distribution, the **fission spectrum** $\chi(E')$, and are typically emitted isotropically (uniformly in all directions). To get the **fission source rate density** into a specific state $(E', \boldsymbol{\Omega}')$, we distribute the total production rate $S_f(\mathbf{r})$ according to these probabilities:
        $$ R_f(\mathbf{r},E',\boldsymbol{\Omega}') = S_f(\mathbf{r}) \cdot \frac{\chi(\mathbf{r},E')}{4\pi} = \frac{\chi(\mathbf{r},E')}{4\pi} \int_0^\infty dE \int_{4\pi} d\boldsymbol{\Omega} \; \nu(\mathbf{r},E) \, \Sigma_f(\mathbf{r},E) \, \psi(\mathbf{r},E,\boldsymbol{\Omega}) $$

These integral expressions for sink and source terms form the building blocks of the [neutron transport equation](@entry_id:1128709), which is the master equation governing neutron behavior. 

### From Continuous Energy to Multigroup: Practical Reaction Rate Calculation

Solving the full energy- and angle-dependent transport equation is computationally intensive. Practical reactor analysis relies on simplified models, the most common of which is the **[multigroup method](@entry_id:1128305)**. This method discretizes the continuous energy variable into a finite number of energy "groups".

#### The Principle of Reaction Rate Preservation and Flux Weighting

The core challenge of the [multigroup method](@entry_id:1128305) is to define group-averaged cross sections, or **group constants**, that preserve the essential physics of the continuous-energy model. The most fundamental requirement is the preservation of reaction rates.

Let an energy group $g$ be defined by the interval $[E_g, E_{g-1}]$. The total reaction rate for reaction $x$ within this group is $\int_{E_g}^{E_{g-1}} \Sigma_x(E) \phi(E) dE$. We seek a single group cross section $\Sigma_{x,g}$ and a single group flux $\phi_g$ such that their product equals this integrated reaction rate:

$$ \Sigma_{x,g} \phi_g \stackrel{!}{=} \int_{E_g}^{E_{g-1}} \Sigma_x(E) \phi(E) \, dE $$

By convention, the **group flux** $\phi_g$ is defined as the integral of the scalar flux over the group's energy range:

$$ \phi_g = \int_{E_g}^{E_{g-1}} \phi(E) \, dE $$

Substituting this definition into the preservation condition and solving for the group cross section yields the unique solution:

$$ \Sigma_{x,g} = \frac{\int_{E_g}^{E_{g-1}} \Sigma_x(E) \phi(E) \, dE}{\int_{E_g}^{E_{g-1}} \phi(E) \, dE} $$

This formula shows that the group cross section must be an average of the continuous-energy cross section, weighted by the continuous-[energy flux](@entry_id:266056) spectrum $\phi(E)$. This is known as **flux weighting**. This result is of paramount importance: it reveals that group constants are not merely material properties but depend on the energy spectrum of the neutrons in which they are situated. Since the spectrum varies throughout a reactor, generating accurate group constants is a non-trivial, iterative process. 

#### Scattering Transfer Matrices and Particle Conservation

The concept of flux weighting extends to scattering. The **multigroup scattering transfer cross section**, $\Sigma_{s,g' \to g}$, represents the [effective cross section](@entry_id:1124176) for neutrons in a source group $g'$ to scatter into a destination group $g$. It is defined to preserve the total rate of scattering from group $g'$ to group $g$:

$$ \Sigma_{s,g' \to g} \phi_{g'} = \int_{E_g}^{E_{g-1}} dE \int_{E_{g'}}^{E_{g'-1}} dE' \, \Sigma_s^{(0)}(E' \to E) \phi(E') $$

Here, $\Sigma_s^{(0)}(E' \to E)$ is the zeroth angular moment of the differential scattering kernel (i.e., the part that couples to the scalar flux). Solving for the transfer cross section gives:

$$ \Sigma_{s,g' \to g} = \frac{\int_{E_{g'}}^{E_{g'-1}} \phi(E') \left[ \int_{E_g}^{E_{g-1}} \Sigma_s^{(0)}(E' \to E) \, dE \right] dE'}{\phi_{g'}} $$

A crucial property of these transfer cross sections arises from particle conservation. A neutron that scatters out of an energy $E'$ must appear at some other energy $E$. Summing the transfer cross sections from a source group $g'$ over all possible destination groups $g$ must therefore equal the total [scattering cross section](@entry_id:150101) for group $g'$, $\Sigma_{s,g'}$. This is the "row-sum" property of the scattering matrix:

$$ \sum_{g=1}^{G} \Sigma_{s,g' \to g} = \Sigma_{s,g'} $$

where $\Sigma_{s,g'}$ is the flux-weighted total [scattering cross section](@entry_id:150101) for group $g'$. This property is a fundamental consistency check in the generation of multigroup libraries. 

#### The Impact of Weighting Choice

While flux weighting is designed to preserve reaction rates, other weighting schemes can be used to preserve different physical quantities. For example, in perturbation theory, it is often desirable to preserve reactivity worths, which are bilinear functionals involving both the forward flux $\phi$ and the **adjoint flux** $\phi^\dagger$ (a measure of neutron importance). This leads to adjoint-weighted or bilinear-weighted cross sections. Similarly, to preserve power distributions, one might use a weighting function proportional to the power produced in each group, $\phi_g \Sigma_{f,g} E_{f,g}$.

A numerical example demonstrates the importance of this choice. Consider a two-group problem where we wish to collapse the fission cross section $\Sigma_{f,g}$ into a single group value $\bar{\Sigma}_f$. If we use flux weighting, the resulting one-group reaction rate $\bar{R}_f = (\sum \phi_g) \bar{\Sigma}_f$ will exactly match the true two-group reaction rate $\sum (\phi_g \Sigma_{f,g})$. However, if we use adjoint weighting or power weighting to compute $\bar{\Sigma}_f$, the resulting $\bar{R}_f$ will generally *not* match the true reaction rate. This is because these weighting schemes are tailored to preserve different quantities (reactivity and power, respectively), not the reaction rate itself. This highlights that there is no [universal set](@entry_id:264200) of group constants; they must be generated with a specific application and preservation goal in mind. 

### Advanced Topics and Applications

The fundamental principles of flux, current, and reaction rates are applied in numerous advanced contexts, from modeling heterogeneous systems to developing high-fidelity computational methods.

#### Behavior at Material Interfaces

Reactors are inherently heterogeneous, composed of distinct regions of fuel, cladding, moderator, and control materials. Understanding how neutron flux and current behave at the interfaces between these materials is crucial. Within the framework of diffusion theory ($\mathbf{J} = -D \nabla\phi$), two fundamental [interface conditions](@entry_id:750725) apply at any interface with no surface sources or sinks:

1.  **Continuity of Scalar Flux:** The scalar flux $\phi$ must be continuous across the interface. A discontinuity in $\phi$ would imply an infinite gradient, which, by Fick's Law, would produce an unphysical infinite current.
2.  **Continuity of Normal Current:** The component of the [neutron current](@entry_id:1128689) density vector normal to the interface, $\mathbf{J} \cdot \mathbf{n}$, must be continuous. This is a direct consequence of neutron conservation: in steady state, the rate at which neutrons leave one side of the interface must equal the rate at which they enter the other.

These two conditions, $[ \phi ]_{\mathcal{S}} = 0$ and $[ \mathbf{J} \cdot \mathbf{n} ]_{\mathcal{S}} = 0$, can also be written entirely in terms of the scalar flux as $[ \phi ]_{\mathcal{S}} = 0$ and $[ D \frac{\partial \phi}{\partial n} ]_{\mathcal{S}} = 0$. Since the diffusion coefficient $D$ is a material property and is discontinuous across the interface, the second condition implies that the normal derivative of the flux, $\frac{\partial \phi}{\partial n}$, must be discontinuous to compensate. 

#### Resonance Self-Shielding

The simple reaction rate formula $R_x = \Sigma_x \phi$ belies a deep non-linear coupling. The flux $\phi(E)$ is itself determined by the cross sections of the medium. This interplay is most dramatic in the case of **resonance absorption**. Certain nuclides, like Uranium-238, have microscopic absorption cross sections with extremely large, [narrow peaks](@entry_id:921519) at specific energies, known as resonances.

In a material containing such an absorber, neutrons slowing down through the [resonance energy](@entry_id:147349) region are absorbed at a very high rate. This intense absorption creates a severe local depression in the neutron flux at and near the [resonance energy](@entry_id:147349). The flux "shields" itself—where the cross section is highest, the flux is lowest. Consequently, the total absorption rate, $\int \Sigma_a(E) \phi(E) dE$, is significantly lower than what would be calculated by naively multiplying the cross section by an unperturbed flux (i.e., the flux that would exist if the resonance were absent).

To handle this in practical calculations, one defines a **self-shielded cross section**, $\Sigma_a^{\text{ss}}(E)$. This is an effective cross section that, by definition, reproduces the correct reaction rate when multiplied by the easily calculated *unperturbed* flux, $\phi_0(E)$:

$$ \Sigma_a^{\text{ss}}(E) \phi_0(E) \stackrel{!}{=} \Sigma_a(E) \phi(E) \quad \implies \quad \Sigma_a^{\text{ss}}(E) = \Sigma_a(E) \frac{\phi(E)}{\phi_0(E)} $$

The factor $\phi(E)/\phi_0(E)$ is the flux depression factor. Calculating this factor is a central problem in [resonance theory](@entry_id:147047). This demonstrates that the [effective cross section](@entry_id:1124176) of a material depends not just on its composition, but also on its geometry and the surrounding materials, which together determine the degree of flux depression. 

#### Conservation and Correction in Numerical Simulations

The principles of neutron balance and reaction rate preservation are not just theoretical constructs; they are the bedrock of numerical methods for reactor analysis.

*   **Numerical Balance Checks:** The continuous neutron balance equation, which in [diffusion theory](@entry_id:1123718) is $\nabla \cdot \mathbf{J} + \Sigma_a \phi = S$, can be integrated over a finite control volume (or mesh cell) $V_i$. Using the [divergence theorem](@entry_id:145271), this yields an exact integral balance:
    $$ \oint_{\partial V_i} \mathbf{J} \cdot \mathbf{n} \, dA + \int_{V_i} \Sigma_a \phi \, dV = \int_{V_i} S \, dV $$
    This states that for any cell, **Net Leakage Out + Total Absorption = Total Source**. Numerical methods like the Finite Volume Method (FVM) are designed to preserve this balance discretely. A crucial verification step in any reactor simulation code is to compute a **per-cell residual** based on the computed flux and current values. For a converged solution, this residual should be close to zero. A normalized local and global balance check, which accounts for the cancellation of currents at interior cell faces, provides a powerful diagnostic for code correctness and solution accuracy. 

*   **Superhomogenization (SPH):** When complex fuel assemblies are represented by single "homogenized" regions in a full-core simulation, errors are inevitably introduced because the true intra-assembly flux shape is lost. The **Superhomogenization (SPH) method** is an advanced technique to correct for this. It uses a high-fidelity reference solution (e.g., from a detailed transport calculation of the single assembly) to generate corrective factors for the homogenized cross sections. The goal is to enforce a key physical principle, most commonly the preservation of reaction rates.

    The procedure is iterative. A low-order diffusion calculation is performed with the homogenized cross sections. The resulting reaction rates are compared to the reference rates, and a multiplicative SPH factor is computed for each group: $f_g = R_{r,g}^{\text{ref}} / R_{r,g}^{\text{lo}}$. The homogenized cross sections are updated ($\Sigma_{r,g}^{\text{SPH}} = f_g \Sigma_{r,g}^{\text{hom}}$), and the diffusion calculation is repeated. This process continues until the factors converge to unity, at which point the low-order model, despite its simplicity, reproduces the correct integrated reaction rates of the high-fidelity solution. This method is a direct and powerful application of the reaction rate preservation principle in a practical simulation workflow. 