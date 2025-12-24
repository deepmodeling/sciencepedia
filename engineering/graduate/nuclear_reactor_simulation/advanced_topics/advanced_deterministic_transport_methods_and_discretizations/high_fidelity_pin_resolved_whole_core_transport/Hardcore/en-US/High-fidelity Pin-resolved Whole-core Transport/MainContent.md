## Introduction
High-fidelity, pin-resolved whole-core transport simulation represents the cutting edge of [computational reactor physics](@entry_id:1122805), providing the most accurate and detailed predictions of neutron behavior inside a nuclear reactor. Unlike traditional methods that rely on spatial and energy homogenization, which can obscure important local effects, these advanced techniques aim to solve the fundamental transport equation with explicit geometric and material detail. This approach closes the gap between simplified models and physical reality, enabling unprecedented predictive capability.

This article provides a comprehensive guide to the principles, applications, and practices of [high-fidelity transport](@entry_id:1126064). The journey begins in the "Principles and Mechanisms" chapter, where we will deconstruct the Boltzmann transport equation and the core numerical methods—such as the [multigroup method](@entry_id:1128305), [discrete ordinates](@entry_id:1123828), and the Method of Characteristics—used to solve it. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these methods are employed to analyze complex, real-world phenomena like [multiphysics feedback](@entry_id:1128317) and [fuel burnup](@entry_id:1125355), highlighting connections to thermal-hydraulics, computer science, and [uncertainty quantification](@entry_id:138597). Finally, the "Hands-On Practices" section will allow you to solidify your knowledge by tackling targeted computational problems. We begin by laying the theoretical groundwork, exploring the foundational equation and the discretization strategies that make its numerical solution possible.

## Principles and Mechanisms

High-fidelity, pin-resolved whole-core transport simulations represent the state-of-the-art in reactor physics analysis. These methods aim to solve the fundamental governing equation of neutron behavior, the Boltzmann transport equation, with minimal approximation in geometry, energy, and angle. This chapter elucidates the core principles and mechanisms that underpin these advanced computational models, beginning with the foundational transport equation and systematically exploring the discretization techniques and physical models required for its solution in a realistic reactor environment.

### The Linear Boltzmann Transport Equation

The behavior of the neutron population within a nuclear reactor is statistically governed by the **linear Boltzmann transport equation**. This equation is a rigorous statement of [particle balance](@entry_id:753197) within a differential element of phase space, which comprises position $\vec{r}$, direction of motion $\vec{\Omega}$, and energy $E$. For a steady-state (time-independent) system, the rate at which neutrons are lost from a phase space element must equal the rate at which they are gained. This balance can be expressed mathematically as follows :

$$
\vec{\Omega}\cdot\nabla \psi(\vec{r},\vec{\Omega},E) + \Sigma_t(\vec{r},E)\,\psi(\vec{r},\vec{\Omega},E)
= S_s(\vec{r},\vec{\Omega},E) + S_f(\vec{r},\vec{\Omega},E)
$$

The left-hand side of the equation represents the loss terms:
-   **Streaming Term ($\vec{\Omega}\cdot\nabla \psi$)**: This term, also known as the transport or drift term, accounts for the net loss of neutrons from a differential spatial volume due to their free flight. $\psi(\vec{r},\vec{\Omega},E)$ is the **[angular neutron flux](@entry_id:1121012)**, representing the number of neutrons at position $\vec{r}$ with energy $E$ traveling in direction $\vec{\Omega}$, per unit area, per unit time, per unit solid angle, and per unit energy.
-   **Collision Term ($\Sigma_t\psi$)**: This term accounts for the removal of neutrons from the phase space element $(\vec{r},\vec{\Omega},E)$ through interactions with atomic nuclei. $\Sigma_t(\vec{r},E)$ is the **total macroscopic cross section**, which represents the total probability of any type of interaction per unit path length.

The right-hand side of the equation represents the source or gain terms:
-   **Scattering Source ($S_s$)**: This term accounts for neutrons that enter the phase space element by scattering from other directions $\vec{\Omega}'$ and energies $E'$. It is an integral term:
    $$
    S_s(\vec{r},\vec{\Omega},E) = \int_{4\pi}\!d\Omega' \int_{0}^{\infty}\!dE'\, \Sigma_s(\vec{r}; E'\to E, \vec{\Omega}'\cdot\vec{\Omega})\,\psi(\vec{r},\vec{\Omega}',E')
    $$
    Here, $\Sigma_s(\vec{r}; E'\to E, \vec{\Omega}'\cdot\vec{\Omega})$ is the **double-[differential scattering cross section](@entry_id:1123684)**, which gives the probability for a neutron of initial energy $E'$ and direction $\vec{\Omega}'$ to scatter into a final energy $E$ and direction $\vec{\Omega}$.

-   **Fission Source ($S_f$)**: This term accounts for new neutrons produced by fission events. Fission is typically assumed to be isotropic (independent of outgoing direction $\vec{\Omega}$). The rate of fission is induced by neutrons of all energies. For a critical reactor, this source term is formulated as part of an eigenvalue problem:
    $$
    S_f(\vec{r},\vec{\Omega},E) = \frac{\chi(\vec{r},E)}{4\pi k_{\mathrm{eff}}} \int_{4\pi}\!d\Omega' \int_{0}^{\infty}\!dE'\, \nu\Sigma_f(\vec{r},E')\,\psi(\vec{r},\vec{\Omega}',E')
    $$
    Here, $\nu\Sigma_f(\vec{r},E')$ is the neutron production cross section, $\chi(\vec{r},E)$ is the **fission spectrum** (the probability distribution of energies for neutrons born from fission), and $k_{\mathrm{eff}}$ is the **effective multiplication factor**. The eigenvalue $k_{\mathrm{eff}}$ is the ratio of neutrons produced in one generation to the neutrons lost in the preceding generation. A self-sustaining chain reaction corresponds to $k_{\mathrm{eff}} = 1$.

### Energy Discretization: The Multigroup Method

The continuous energy dependence of the transport equation, especially the highly complex and resonant behavior of cross sections, makes a direct numerical solution infeasible. The standard approach is the **[multigroup method](@entry_id:1128305)**, which partitions the energy domain into a finite number of discrete energy groups, $g = 1, \dots, G$ . The equation is then integrated over each energy group interval, $[E_g, E_{g-1}]$.

The core challenge in this process is handling terms like $\int \Sigma_x(E) \psi(E) dE$. A closed system of equations can only be obtained by introducing an approximation. The fundamental assumption of the [multigroup method](@entry_id:1128305) is the **separability of the flux** within an energy group. It is assumed that the angular flux can be approximated as the product of a group-dependent amplitude and a known, pre-calculated energy shape function, $\widehat{\varphi}_p(E)$:
$$
\psi(\vec{r},\vec{\Omega},E) \approx \psi_g(\vec{r},\vec{\Omega})\,\widehat{\varphi}_p(E) \quad \text{for } E \in [E_g, E_{g-1}]
$$
where $\psi_g(\vec{r},\vec{\Omega})$ is the group-integrated angular flux. The shape function $\widehat{\varphi}_p(E)$ is a **weighting spectrum**, typically obtained from detailed, fine-group calculations of a representative local geometry (like a single pin cell) and material composition $p$.

By applying this assumption and integrating the continuous-energy transport equation over group $g$, we arrive at the **steady-state multigroup neutron transport [eigenvalue equation](@entry_id:272921)** :

$$
\vec{\Omega}\cdot\nabla \psi_g(\vec{r},\vec{\Omega})+\Sigma_{t,g}(\vec{r})\,\psi_g(\vec{r},\vec{\Omega})
=\sum_{g'=1}^{G}\int_{4\pi}\Sigma_{s,g'\to g}(\vec{r},\vec{\Omega}'\cdot\vec{\Omega})\,\psi_{g'}(\vec{r},\vec{\Omega}')\,d\Omega'
+\frac{\chi_g(\vec{r})}{k_{\mathrm{eff}}}\sum_{g'=1}^{G}\nu\Sigma_{f,g'}(\vec{r})\,\phi_{g'}(\vec{r})
$$

Here, the group-integrated [scalar flux](@entry_id:1131249) is $\phi_g(\vec{r}) = \int_{4\pi} \psi_g(\vec{r},\vec{\Omega}) d\Omega$. The continuous cross sections have been replaced by **[multigroup cross sections](@entry_id:1128302)** (or group constants). These constants are generated by averaging the continuous-energy data over each group, weighted by the assumed flux spectrum $\widehat{\varphi}_p(E)$. This averaging is performed to preserve the total reaction rates within each group and spatial region, a principle known as **reaction-rate preservation** . For any reaction type $x$, the macroscopic group constant for a material region $V_m$ is defined as:

$$
\Sigma_{x,g}^{m} = \frac{\int_{V_m} \int_{E_{g}}^{E_{g-1}} \Sigma_{x}(E, \vec{r}) \phi(E, \vec{r})\,dE\,d\vec{r}}{\int_{V_m} \int_{E_{g}}^{E_{g-1}} \phi(E, \vec{r})\,dE\,d\vec{r}}
$$

This explicit dependence on the flux spectrum $\phi(E, \vec{r})$ is crucial. It highlights that [multigroup cross sections](@entry_id:1128302) are not fundamental properties of a nuclide but are effective parameters that depend on the local neutron environment, material composition, and temperature. Using a "flat" or unweighted spectrum can lead to significant errors, especially in energy ranges with strong resonances .

### Treatment of Resonance Self-Shielding

One of the most significant challenges in generating group constants is the treatment of **[resonance self-shielding](@entry_id:1130933)**. In the epithermal energy range, heavy nuclides like $^{238}\mathrm{U}$ exhibit large, narrow resonance peaks in their absorption cross sections. In these energy regions, the neutron flux is strongly depressed because the high [absorption probability](@entry_id:265511) rapidly removes neutrons. This means the effective reaction rate, $\int \Sigma_a(E)\phi(E)dE$, is much lower than what would be calculated if the flux were assumed to be flat.

To capture this effect without resolving every resonance, high-fidelity methods employ techniques like the **[subgroup method](@entry_id:1132605)** or **[probability table method](@entry_id:1130196)** . Instead of representing a group cross section with a single averaged value, the [subgroup method](@entry_id:1132605) represents the statistical distribution of the cross section within the group. It replaces the continuous function $\Sigma_x(E)$ with a discrete set of cross-section values (subgroups) $\{ \sigma_{x,k} \}$ and associated probabilities $\{ w_k \}$.

The parameters of this discrete representation are determined by requiring that it reproduces key integral properties of the true cross section distribution. For instance, a two-subgroup model for absorption might be constructed to preserve the first two unconditioned moments (mean and variance) of $\sigma_a(E)$ and a crucial flux-weighted functional that captures the self-shielding effect. Under the [narrow resonance approximation](@entry_id:1128424) for a heterogeneous pin cell, this functional is often of the form $\langle \frac{\sigma_a}{\sigma_0 + \sigma_t} \rangle$, where $\sigma_0$ is the background cross section of the surrounding material and $\sigma_t$ is the total cross section of the resonant isotope.

For example, given a resonant isotope with mean absorption $\langle \sigma_a \rangle = 100$ barns, variance $3600$ barns$^2$, a background $\sigma_0 = 10$ barns, and a target functional value of $0.843$, a valid two-subgroup representation can be constructed. One such representation is: subgroup 1 with $\sigma_{a,1} = 203.9$ barns and weight $w_1 = 0.25$; and subgroup 2 with $\sigma_{a,2} = 65.4$ barns and weight $w_2 = 0.75$. This simple discrete model can accurately reproduce the effects of self-shielding within a multigroup transport calculation .

### Discretization of the Angular Variable

The multigroup transport equation still contains a continuous dependence on the angular variable $\vec{\Omega}$. The most common technique for discretizing angle in [high-fidelity transport](@entry_id:1126064) codes is the **Discrete Ordinates ($S_N$) method** . This method replaces the continuous angular domain with a [finite set](@entry_id:152247) of discrete directions $\{\vec{\Omega}_d\}_{d=1}^M$ and associated weights $\{w_d\}_{d=1}^M$. The angular flux $\psi_g(\vec{r}, \vec{\Omega})$ is now only solved for at these discrete directions, becoming $\psi_{g,d}(\vec{r})$. Integrals over the [solid angle](@entry_id:154756) are replaced by weighted sums:

$$
\int_{4\pi} f(\vec{\Omega})\,d\Omega \approx \sum_{d=1}^M w_d f(\vec{\Omega}_d)
$$

The set of directions and weights is called a **quadrature set**. The accuracy of the $S_N$ method depends critically on the quality of this set. A good quadrature set must be able to accurately integrate polynomials of the [direction cosines](@entry_id:170591) $(\mu, \eta, \xi)$ up to a certain order, as this is equivalent to integrating the spherical harmonics $Y_{lm}(\vec{\Omega})$. To exactly integrate all [spherical harmonics](@entry_id:156424) up to degree $L$, a [quadrature set](@entry_id:156430) must satisfy a series of **[moment conditions](@entry_id:136365)**. For a quadrature to be exact for $L=3$, it must satisfy, among others, the zeroth and second [moment conditions](@entry_id:136365), while its symmetry ensures the odd moments vanish :

-   **Zeroth Moment (Normalization):** $\sum_{d=1}^{M} w_d = 4\pi$
-   **Second Moments (Isotropy):** $\sum_{d=1}^{M} w_d \mu_d^2 = \sum_{d=1}^{M} w_d \eta_d^2 = \sum_{d=1}^{M} w_d \xi_d^2 = \frac{4\pi}{3}$

Modern quadrature sets are typically of the **level-symmetric** type, which possess high degrees of symmetry to satisfy these conditions efficiently and mitigate **[ray effects](@entry_id:1130607)**, which are unphysical oscillations in the flux caused by angular discretization.

### Discretization of Space and Geometry Modeling

Representing the complex spatial domain of a reactor core at the pin level is a major challenge. A typical Pressurized Water Reactor (PWR) fuel pin consists of a cylindrical UO$_2$ fuel pellet, a small helium-filled gap, and a Zircaloy cladding, all situated within a square lattice cell filled with coolant. A high-fidelity model must represent these components with geometric and material fidelity . For instance, a typical fuel pin might have a fuel radius of $0.410\,\mathrm{cm}$, a gap thickness of $0.008\,\mathrm{cm}$, and a cladding thickness of $0.057\,\mathrm{cm}$, resulting in an outer radius of $0.475\,\mathrm{cm}$ within a lattice pitch of $1.260\,\mathrm{cm}$.

Two main families of [spatial discretization](@entry_id:172158) methods are used:

1.  **Exact-Geometry Methods**: The premier method in this class is the **Method of Characteristics (MOC)**, often paired with a **Constructive Solid Geometry (CSG)** representation. MOC solves the transport equation along a set of parallel straight-line tracks that crisscross the domain. The geometry is described exactly by analytical surfaces (circles, planes), and the lengths of the track segments (chords) within each homogeneous material region are calculated precisely. This approach avoids geometric approximations and enforces particle conservation for each physical material region, up to [angular quadrature](@entry_id:1121013) and source approximation errors .

2.  **Structured Mesh Methods**: These methods, such as the **Finite Volume Method (FVM)**, impose a regular (e.g., Cartesian) mesh over the complex geometry. Cells that are intersected by [material interfaces](@entry_id:751731), known as **cut cells**, require special treatment. Typically, a volume-fraction homogenization is used to define [effective material properties](@entry_id:167691) for the entire cell. While this approach benefits from the simplicity of structured meshes, it introduces errors by smearing the sharp physical discontinuities of material properties. Enforcing flux continuity across a mesh face that does not align with a physical interface can introduce artificial numerical diffusion, biasing local reaction rates and the representation of self-shielding . When [coarse-mesh methods](@entry_id:1122586) are used, preserving both reaction rates and leakage currents often requires the introduction of **Discontinuity Factors (DFs)** at the boundaries of homogenized regions.

### Boundary Conditions

To obtain a unique solution to the transport equation on a [finite domain](@entry_id:176950) $D$, the angular flux must be specified for all incoming directions at the boundary $\Gamma$. This is a prescription on the set of phase space points $(\vec{r}, \vec{\Omega})$ where $\vec{r} \in \Gamma$ and the direction $\vec{\Omega}$ points into the domain, i.e., $\vec{\Omega} \cdot \hat{n}(\vec{r})  0$, where $\hat{n}(\vec{r})$ is the outward [unit normal vector](@entry_id:178851). Common boundary conditions include :

-   **Vacuum Boundary**: This condition models a boundary adjacent to a void from which no neutrons return. The incoming flux is simply set to zero:
    $$
    \psi(\vec{r}, \vec{\Omega}) = 0 \quad \text{for } \vec{\Omega} \cdot \hat{n}(\vec{r})  0
    $$

-   **Specularly Reflecting Boundary**: This condition models a [plane of symmetry](@entry_id:198308). An outgoing neutron in direction $\vec{\Omega}_{\text{out}}$ is perfectly reflected back into the domain in a new direction $\vec{\Omega}_{\text{in}}$. The incoming flux is set equal to the outgoing flux in the mirror-reflected direction:
    $$
    \psi(\vec{r}, \vec{\Omega}_{\text{in}}) = \psi\big(\vec{r}, \vec{\Omega}_{\text{out}}\big) \quad \text{where } \vec{\Omega}_{\text{in}} = \vec{\Omega}_{\text{out}} - 2 (\vec{\Omega}_{\text{out}} \cdot \hat{n}(\vec{r})) \hat{n}(\vec{r})
    $$

-   **Periodic Boundary**: This condition is used to model an infinite, repeating lattice. A neutron that leaves one face of the domain re-enters the opposite face with the same direction. For two opposite faces $\Gamma_L$ and $\Gamma_R$ with corresponding points $\vec{r}_L$ and $\vec{r}_R$, the condition is:
    $$
    \psi(\vec{r}_R, \vec{\Omega}) = \psi(\vec{r}_L, \vec{\Omega}) \quad \text{for } \vec{\Omega} \text{ incoming at } \vec{r}_R
    $$

### Solving the Eigenvalue Problem

After discretization in energy, angle, and space, the transport equation becomes a very large [matrix eigenvalue problem](@entry_id:142446). It can be written in operator form as a [generalized eigenvalue problem](@entry_id:151614), $\mathcal{T}\phi = \frac{1}{k}\mathcal{F}\phi$, or rearranged into the standard form for power iteration :
$$
\mathcal{G}\phi = k\phi \quad \text{where } \mathcal{G} = \mathcal{T}^{-1}\mathcal{F}
$$
The operator $\mathcal{G}$ is known as the **fission-iteration operator**. Its largest-magnitude eigenvalue is the [effective multiplication factor](@entry_id:1124188), $k_{\mathrm{eff}}$, and the corresponding eigenvector is the [fundamental mode](@entry_id:165201) flux distribution.

-   **Power Iteration**: The simplest method to find the dominant eigenpair is power iteration. It converges linearly with a rate determined by the **dominance ratio**, $|k_2/k_1|$, where $k_1$ and $k_2$ are the largest and second-largest eigenvalues.

-   **Advanced Solvers**: For large, complex cores, the dominance ratio can be close to 1, leading to slow convergence. Furthermore, analysis of reactor dynamics and safety often requires knowledge of higher-order eigenmodes, which correspond to flux "tilt" shapes. Methods based on **Krylov subspaces**, such as the **Arnoldi iteration** and **block subspace iteration**, are used to find multiple eigenpairs simultaneously. These methods build a subspace that captures the action of the operator $\mathcal{G}$ and then extract approximate eigenpairs via a Rayleigh-Ritz projection. Their convergence is governed by spectral gaps, such as $|\lambda_{p+1}/\lambda_p|$ for a block of size $p$ . Since the transport operator is not self-adjoint (non-normal), a proper [modal analysis](@entry_id:163921) requires the use of both right eigenvectors (the flux modes) and left eigenvectors (the adjoint flux or importance modes) .

### Multiphysics Coupling at the Pin Level

The macroscopic cross sections that define the transport operator $\mathcal{T}$ are not constant; they depend strongly on the local thermophysical conditions of the materials. A high-fidelity simulation must couple the neutronics calculation with a **Thermal-Hydraulics (TH)** model that calculates the temperature and density fields. This coupling introduces critical feedback mechanisms .

-   **Doppler Feedback**: As the fuel temperature ($T_f$) increases, the thermal motion of fuel nuclei broadens the absorption resonances. This increases the effective [resonance absorption](@entry_id:1130927) cross section, $\Sigma_{a,\mathrm{fuel}}$. A common first-order model for this effect is:
    $$
    \Sigma_{a,\mathrm{fuel}}(T_f) \approx \Sigma_{a,\mathrm{fuel}}(T_{f0}) \sqrt{\frac{T_f}{T_{f0}}}
    $$
    This increase in absorption leads to a decrease in reactivity, providing a crucial and prompt [negative feedback mechanism](@entry_id:911944) that stabilizes the reactor.

-   **Moderator Density Feedback**: As the coolant heats up, its density ($\rho_m$) decreases. Since macroscopic cross sections are directly proportional to [number density](@entry_id:268986), a decrease in moderator density leads to a proportional decrease in its scattering and absorption capabilities:
    $$
    \Sigma_{x,\mathrm{mod}}(\rho_m) = \Sigma_{x,\mathrm{mod}}(\rho_{m0}) \left(\frac{\rho_m}{\rho_{m0}}\right)
    $$
    This reduces the moderation of fast neutrons, which can lead to either negative or positive reactivity feedback, depending on the reactor design and moderation regime.

In a coupled simulation, the neutronics solver calculates the pin-power distribution. This power is used by the TH solver to update the fuel temperature and coolant density fields. These updated fields are then used to re-evaluate the cross sections, and the neutronics solver is run again. This iterative process continues until a converged, self-consistent state is achieved.