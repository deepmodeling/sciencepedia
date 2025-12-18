## Introduction
The neutronic behavior of a nuclear reactor is inextricably linked to its material composition, which evolves continuously as fuel is consumed. This process, quantified by burnup, means that [nuclear cross sections](@entry_id:1128920)—the fundamental probabilities governing neutron interactions—are not static values but dynamic functions of the reactor's operational history. Ignoring this evolution leads to significant inaccuracies in predicting reactor performance, compromising safety analyses and operational efficiency. This article addresses this critical challenge by providing a comprehensive overview of burnup-dependent cross section updates. First, the **Principles and Mechanisms** chapter will dissect the fundamental link between isotopic composition, burnup, and cross sections, including the crucial depletion-transport feedback loop. Next, the **Applications and Interdisciplinary Connections** chapter will explore how these principles are applied in practical core simulation, fuel cycle management, and safety analysis. Finally, **Hands-On Practices** will offer an opportunity to apply these concepts to solve concrete problems in reactor physics.

## Principles and Mechanisms

The neutronic behavior of a nuclear reactor is fundamentally governed by its material composition. The rates of all crucial reactions—fission, capture, and scattering—are determined by macroscopic cross sections, which represent the collective interaction probabilities of the nuclides within the system. During reactor operation, these nuclide inventories change continuously through [transmutation](@entry_id:1133378) and decay, a process tracked by the metric of **burnup**. Consequently, macroscopic cross sections are not static properties but evolve dynamically with burnup. Understanding the principles and mechanisms of this evolution is paramount for accurate reactor analysis, fuel management, and safety assessment.

### The Fundamental Link Between Composition, Burnup, and Cross Sections

The probability of a specific neutron interaction within a material is quantified by the **macroscopic cross section**, denoted $\Sigma_x$ for a reaction of type $x$ (e.g., fission, capture). It is defined as the sum of the contributions from all individual nuclide species present in the material:

$$
\Sigma_x(E) = \sum_i N_i \sigma_x^i(E)
$$

Here, $N_i$ is the [number density](@entry_id:268986) (atoms per unit volume) of nuclide $i$, and $\sigma_x^i(E)$ is the **microscopic cross section**, which is the intrinsic probability of a neutron of energy $E$ undergoing reaction $x$ with a single nucleus of species $i$.

As a reactor operates and generates energy, its fuel composition changes. The number densities $N_i$ are thus functions of the operational history. This history is commonly quantified by **burnup**, $B$, defined as the thermal energy released per unit initial mass of heavy metal (e.g., uranium, plutonium). For a system operating at a specific power $p(t)$ (power per unit mass), the burnup accumulated over a time interval $\Delta t$ can be calculated. If we assume the specific power $p$ is constant over a time step $\Delta t$, the burnup increment $\Delta B$ is simply $\Delta B = p \cdot \Delta t$. To express this in standard units, such as megawatt-days per kilogram of heavy metal ($\mathrm{MWd}/\mathrm{kgHM}$), from a specific power in watts per gram ($\mathrm{W}/\mathrm{gHM}$) and time in seconds, a [unit conversion](@entry_id:136593) is necessary :

$$
\Delta B \left[\frac{\mathrm{MWd}}{\mathrm{kgHM}}\right] = \frac{p \left[\frac{\mathrm{W}}{\mathrm{gHM}}\right] \cdot \Delta t [\mathrm{s}]}{86400000}
$$

Since the number densities $N_i$ evolve as energy is produced, they are fundamentally functions of burnup, $N_i(B)$. This directly implies that the macroscopic cross section also becomes a function of burnup:

$$
\Sigma_x(E, B) = \sum_i N_i(B) \sigma_x^i(E)
$$

In this idealized formulation, we assume that the microscopic cross sections $\sigma_x^i(E)$ are fundamental constants that do not change with burnup. Under this assumption, the change in the macroscopic cross section with respect to burnup is driven solely by the change in isotopic composition :

$$
\frac{\partial \Sigma_x(E, B)}{\partial B} = \sum_i \frac{\partial N_i(B)}{\partial B} \sigma_x^i(E)
$$

This equation represents the primary mechanism of burnup-dependent cross sections: as the fuel is irradiated, the quantities of different nuclides change, and this shifting composition alters the bulk neutronic properties of the material. However, this is an incomplete picture. In reality, the microscopic cross sections themselves are also affected by the changing reactor state, creating a more complex feedback loop.

### The Depletion-Transport Coupling Loop

To understand why even the effective microscopic cross sections change, we must examine the coupled nature of nuclide depletion and [neutron transport](@entry_id:159564). The evolution of the nuclide number densities $N_i$ is governed by the **Bateman equations**, a system of coupled [first-order ordinary differential equations](@entry_id:264241) that balance the production and destruction of each species. In matrix form, this can be written as :

$$
\frac{\mathrm{d}\mathbf{N}(t)}{\mathrm{d}t} = \mathbf{A}(\phi, \sigma) \mathbf{N}(t)
$$

where $\mathbf{N}(t)$ is the vector of all nuclide number densities. The **[depletion matrix](@entry_id:1123564)** $\mathbf{A}$ contains the rate coefficients for all [transmutation](@entry_id:1133378) and decay processes. Its diagonal elements, $A_{ii}$, represent the total destruction rate of nuclide $i$ from decay and neutron absorption, while its off-diagonal elements, $A_{ji}$, represent the production rate of nuclide $j$ from nuclide $i$. Crucially, the terms related to neutron-induced reactions are products of the neutron flux $\phi$ and effective microscopic cross sections $\bar{\sigma}$. For example:

- **Destruction (diagonal term):** $A_{ii} = -\lambda_i - \phi \bar{\sigma}_{a,i}$
- **Production (off-diagonal term):** $A_{ji} = b_{i \to j}\lambda_i + \phi \bar{\sigma}_{i \to j}$

Here, $\lambda_i$ is the decay constant, $b_{i \to j}$ is the decay branching fraction, and $\bar{\sigma}$ represents spectrum-averaged microscopic cross sections. The matrix $\mathbf{A}$ is therefore not a constant but a function of the neutron flux.

This leads to a fundamental feedback loop:

1.  The current nuclide composition $\mathbf{N}(B)$ defines the macroscopic cross sections $\mathbf{\Sigma}(B)$.
2.  The macroscopic cross sections $\mathbf{\Sigma}(B)$ determine the properties of the medium for the [neutron transport equation](@entry_id:1128709). Solving the transport equation for this medium yields the neutron flux spectrum, $\phi(E, B)$.
3.  The neutron flux $\phi(E, B)$ and the microscopic cross sections $\sigma(E)$ determine the reaction rates that populate the [depletion matrix](@entry_id:1123564) $\mathbf{A}$.
4.  The [depletion matrix](@entry_id:1123564) $\mathbf{A}$ governs the rate at which the nuclide composition $\mathbf{N}(B)$ changes over the next burnup step.

This cycle, where composition affects the flux and the flux affects the evolution of the composition, is the core of the depletion problem. It necessitates that cross sections be re-evaluated, or updated, periodically as burnup accumulates.

### Burnup-Induced Spectral Changes

A key consequence of the depletion-transport loop is that the shape of the [neutron energy spectrum](@entry_id:1128692), $\phi(E,B)$, changes with burnup. These spectral shifts have a profound impact on reaction rates and effective cross sections.

#### Spectral Hardening and Softening

The terms **spectral hardening** and **spectral softening** describe shifts in the average energy of the neutron population.
- **Spectral Hardening:** The spectrum shifts towards higher energies. This typically occurs when strong thermal absorbers are introduced into the system, depressing the thermal flux and increasing the relative importance of the fast and epithermal flux.
- **Spectral Softening:** The spectrum shifts towards lower energies. This occurs when thermal absorbers are removed, allowing more neutrons to thermalize and increasing the thermal flux relative to the fast flux.

Two common phenomena in a reactor core illustrate these effects. First, as burnup increases, fission products such as $^{135}\text{Xe}$ and $^{149}\text{Sm}$, which are powerful thermal neutron absorbers, accumulate in the fuel. Concurrently, fissile plutonium isotopes are produced. This general increase in thermal absorption causes **spectral hardening**. An interesting consequence is that while absorption in the thermal range is suppressed, the increased flux in the epithermal range can enhance reaction rates for nuclides with strong resonances in that region. For example, the resonance capture rate in $^{238}\text{U}$ can increase due to spectral hardening, even as the overall thermal flux decreases .

Conversely, in a Pressurized Water Reactor (PWR), reactivity is controlled early in the fuel cycle by dissolving boric acid (a strong thermal absorber) in the moderator. As the fuel burns and its intrinsic reactivity decreases, the boron concentration is gradually reduced (a process called letdown). This removal of a thermal absorber causes **spectral softening** .

These competing effects can be illustrated with a simplified two-group model. The ratio of thermal flux ($\phi_2$) to fast flux ($\phi_1$) can be shown to be equal to the ratio of the macroscopic down-scattering cross section to the macroscopic thermal absorption cross section, $\phi_2/\phi_1 = \Sigma_{s,1\to 2} / \Sigma_{a,2}$. As burnup $B$ increases, the buildup of absorbers increases $\Sigma_{a,2}(B)$, which decreases the flux ratio (hardening). If temperature $T$ also changes, it affects both the moderator density (and thus $\Sigma_{s,1\to 2}(T)$) and the effective thermal absorption cross sections, adding another layer of complexity .

### The Process of Generating Burnup-Dependent Cross Sections

To account for these complex, coupled effects in practical reactor simulations, burnup-dependent multigroup cross section libraries are generated. This is a sophisticated process founded on the principle of **reaction rate preservation**.

The goal is to find a set of [multigroup cross sections](@entry_id:1128302), $\Sigma_{x,g}$, that, when used in a simulation with a simplified group-wise flux $\Phi_g$, reproduce the same total reaction rate as would be calculated with continuous-energy data. For a given energy group $g$, the reaction rate must be conserved:

$$
R_{x,g}(B) = \int_{E_{g-1}}^{E_g} \Sigma_x(E, B) \phi(E, B) \mathrm{d}E = \Sigma_{x,g}(B) \Phi_g(B)
$$

where $\Phi_g(B) = \int_{E_{g-1}}^{E_g} \phi(E, B) \mathrm{d}E$. Rearranging this equation gives the definition of the multigroup [macroscopic cross section](@entry_id:1127564):

$$
\Sigma_{x,g}(B) = \frac{\int_{E_{g-1}}^{E_g} \Sigma_x(E, B) \phi(E, B) \mathrm{d}E}{\int_{E_{g-1}}^{E_g} \phi(E, B) \mathrm{d}E}
$$

This equation reveals a critical insight: to preserve reaction rates, the continuous-energy cross section must be weighted by the true, burnup-dependent neutron flux spectrum, $\phi(E,B)$ . Using any other weighting function (e.g., a generic $1/E$ spectrum or a flat spectrum) is an approximation that will introduce errors.

This leads to the standard computational procedure for generating burnup-dependent libraries, often performed with specialized lattice physics codes :
1.  **Define Burnup Steps:** Select a series of discrete burnup points ($B_0, B_1, \dots, B_n$) at which cross sections will be calculated.
2.  **Deplete and Solve:** For each burnup point $B_i$:
    a.  Start with the nuclide composition $N_j(B_{i-1})$ from the previous step.
    b.  Perform a depletion calculation over the burnup step $\Delta B = B_i - B_{i-1}$ to estimate the composition $N_j(B_i)$. This may involve a [predictor-corrector scheme](@entry_id:636752).
    c.  Using the composition $N_j(B_i)$, solve the detailed [neutron transport equation](@entry_id:1128709) for a representative geometry (e.g., a [fuel pin cell](@entry_id:1125360) or assembly) to obtain the high-fidelity, continuous-energy (or fine-group) [neutron spectrum](@entry_id:752467) $\phi(E, B_i)$. This step must include treatments for complex physical effects like [resonance self-shielding](@entry_id:1130933).
    d.  **Collapse:** Use the calculated spectrum $\phi(E, B_i)$ as the weighting function to condense the fundamental pointwise cross section data (from sources like ENDF) into the desired multigroup structure, producing a set of cross sections $\Sigma_{x,g}(B_i)$.
3.  **Tabulate:** The resulting sets of [multigroup cross sections](@entry_id:1128302) are tabulated against burnup and other state variables (like fuel temperature or moderator density). These tables can then be interpolated during full-core reactor simulations, providing an accurate yet computationally efficient way to model the effects of [fuel burnup](@entry_id:1125355).

### Advanced Considerations: Spatial and History Effects

The principles described above form the basis of burnup calculations, but real-world reactor modeling requires addressing further complexities related to spatial variations and operational history.

#### Spatial Dependence

In a full reactor core, the neutron flux is not uniform; it typically peaks in the center and falls off towards the edges. This spatial variation in flux, $\phi(r, z, t)$, leads to spatially varying power density, $p(r, z, t)$. Consequently, burnup is accumulated at different rates throughout the core, leading to a spatially dependent burnup distribution, $B(r, z)$. Since isotopic evolution is driven by local reaction rates, the nuclide inventories also become spatially dependent, $N_i(r, z, B)$. This chain of dependencies means that macroscopic cross sections must be treated as local properties, $\Sigma_{x,g}(r, z, B)$, requiring simulations to track and update them for thousands of individual regions within the core .

#### Resonance Self-Shielding

**Resonance self-shielding** is a critical effect where the high absorption cross section within a resonance peak causes a localized depression in the neutron flux. This means the effective, spectrum-averaged cross section is lower than it would be in an unperturbed flux. The **Bondarenko method** is a common technique to handle this, parameterizing the effect using a **background cross section**, $\sigma_0$. This parameter represents the total cross section of all *other* nuclides in the mixture, per atom of the resonance absorber in question. As burnup proceeds, the composition of these "other" nuclides changes, causing $\sigma_0$ to evolve with burnup. This, in turn, changes the degree of self-shielding. Therefore, the **self-shielding factor**, $f_i$, which is the ratio of the shielded to the unshielded (infinite dilution) cross section, becomes a function of burnup, $f_i(B)$ . This adds another burnup-dependent mechanism affecting the effective microscopic cross sections.

#### Spectral History Effects

Perhaps the most subtle mechanism is **spectral history**. This refers to the fact that the nuclide composition at a given burnup $B$ is not uniquely determined by the value of $B$ alone. It also depends on the *path* taken to reach that burnup—specifically, the history of the [neutron spectrum](@entry_id:752467) that drove the transmutations.

Consider two identical fuel assemblies burned to the exact same final burnup, $B^*$.
- Assembly A is burned in a consistently soft spectrum.
- Assembly B is burned for the first half of its life in a hard spectrum (e.g., near a control rod) and the second half in a soft spectrum.

Even though they end at the same burnup and in the same instantaneous state, their final isotopic compositions will be different. The harder spectrum in Assembly B's early life would have promoted different reaction pathways (e.g., more resonance capture in $^{238}\text{U}$, leading to more $^{239}\text{Pu}$). Because their final compositions are different, their macroscopic cross sections at burnup $B^*$ will also be different. This path-dependence, or "memory" of the prior spectral environment, is the essence of the spectral history effect . It underscores that truly accurate burnup-dependent cross sections are not just functions of burnup, but functionals of the entire operational history.