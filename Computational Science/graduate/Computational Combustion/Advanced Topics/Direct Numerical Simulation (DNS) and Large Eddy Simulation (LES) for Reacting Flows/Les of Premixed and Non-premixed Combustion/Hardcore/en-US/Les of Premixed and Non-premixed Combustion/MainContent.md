## Introduction
The simulation of [turbulent combustion](@entry_id:756233) is a cornerstone of modern engineering design and scientific discovery, from developing cleaner engines to understanding astrophysical phenomena. Large-Eddy Simulation (LES) has emerged as a powerful tool in this domain, offering a compromise between the prohibitive cost of Direct Numerical Simulation (DNS) and the inherent limitations of Reynolds-Averaged Navier-Stokes (RANS) models. However, the application of LES to [reacting flows](@entry_id:1130631) presents a formidable challenge: the filtering process inherent to LES obscures the small-scale interactions where turbulence and chemistry are most intimately and non-linearly coupled. This gives rise to the 'closure problem' for the filtered chemical source terms and subgrid [scalar transport](@entry_id:150360), a central knowledge gap that must be addressed for predictive simulations.

This article provides a comprehensive overview of the principles and practices for closing these terms in the LES of premixed and [non-premixed combustion](@entry_id:1128819). It is structured to guide the reader from fundamental theory to practical application.
First, **Principles and Mechanisms** will dissect the closure problem, detailing the unclosed terms that arise from Favre-filtering the governing equations. We will explore the physics of [turbulence-chemistry interaction](@entry_id:756223) across different [combustion regimes](@entry_id:1122679) and introduce the cornerstone modeling frameworks designed to capture these effects, including the G-Equation, Presumed PDF methods, and the Flamelet concept.
Next, **Applications and Interdisciplinary Connections** will demonstrate how these theoretical models are deployed to solve complex, real-world problems. We will examine the simulation of intricate flame structures, the prediction of transient events like extinction and reignition, and the extension of these methods to critical interdisciplinary areas such as [pollutant formation](@entry_id:1129911) and alternative fuels.
Finally, **Hands-On Practices** offers a set of targeted problems designed to reinforce the theoretical concepts, providing practical experience with the core techniques discussed.

## Principles and Mechanisms

The simulation of turbulent reacting flows via Large-Eddy Simulation (LES) introduces a set of unique challenges that stem from the non-linear coupling between fluid dynamics, chemical kinetics, and [molecular transport](@entry_id:195239) at scales smaller than the computational grid. The filtering operation, central to LES, separates the flow variables into resolved and unresolved components, but in doing so, generates unclosed terms in the governing equations. This chapter elucidates the fundamental principles behind the closure of these terms, focusing on the key mechanisms that govern turbulent combustion and the modeling strategies designed to capture them.

### The Closure Problem in Reacting LES

In [variable-density flows](@entry_id:1133710), such as those encountered in combustion, it is advantageous to use Favre (or density-weighted) filtering. For any quantity $\phi$, the Favre-filtered value $\tilde{\phi}$ is defined as $\tilde{\phi} = \overline{\rho \phi} / \bar{\rho}$, where $\bar{\rho}$ is the spatially filtered density. This formulation simplifies the filtered continuity and momentum equations by avoiding explicit subgrid terms in the convective transport. However, closure problems remain for virtually every other term in the governing equations.

#### Subgrid-Scale Scalar Flux

The transport of scalars, such as species mass fractions and enthalpy, is fundamental to combustion. Consider the conservation equation for a species $k$ with [mass fraction](@entry_id:161575) $Y_k$. Applying the Favre-filtering procedure to the species transport equation results in:
$$
\partial_t(\bar{\rho} \tilde{Y}_k) + \nabla \cdot (\bar{\rho} \tilde{\mathbf{u}} \tilde{Y}_k) = \nabla \cdot (\overline{\rho D_k \nabla Y_k}) - \nabla \cdot (\bar{\rho} \widetilde{\mathbf{u}'' Y_k''}) + \overline{\dot{\omega}}_k
$$
where $\tilde{\mathbf{u}}$ is the Favre-filtered velocity, $D_k$ is the molecular diffusivity, $\dot{\omega}_k$ is the chemical source term, and $\mathbf{u}'' = \mathbf{u} - \tilde{\mathbf{u}}$ and $Y_k'' = Y_k - \tilde{Y}_k$ are the Favre fluctuations. The term $\bar{\rho} \widetilde{\mathbf{u}'' Y_k''}$ represents the **subgrid-scale (SGS) convective flux** of species $k$. It is an unclosed term that describes the transport of species due to unresolved turbulent eddies.

For modeling purposes, it is common to rearrange the equation to isolate all unclosed transport effects into a single SGS [flux vector](@entry_id:273577), $\mathbf{q}_{Y_k}$. This leads to a filtered equation of the form:
$$
\partial_t(\bar{\rho} \tilde{Y}_k) + \nabla \cdot (\bar{\rho} \tilde{\mathbf{u}} \tilde{Y}_k) = \nabla \cdot (\bar{\rho} D_k \nabla \tilde{Y}_k) - \nabla \cdot \mathbf{q}_{Y_k} + \overline{\dot{\omega}}_k
$$
By comparing this with the formally derived equation, the unclosed SGS flux is precisely defined as :
$$
\mathbf{q}_{Y_k} = \underbrace{\bar{\rho} \widetilde{\mathbf{u}''Y_k''}}_{\text{SGS Convective Flux}} - \underbrace{\left( \overline{\rho D_k \nabla Y_k} - \bar{\rho}D_k \nabla \tilde{Y}_k \right)}_{\text{SGS Diffusive Flux Correction}}
$$
At high Reynolds numbers, the SGS convective flux dominates. A common closure strategy is the **mixed model**, which combines the strengths of two distinct approaches. First, a **gradient-diffusion model** relates the flux to the gradient of the resolved scalar, providing a mechanism for SGS dissipation:
$$
(\mathbf{q}_{Y_k})_{\text{GD}} = -\bar{\rho} D_t \nabla \tilde{Y}_k
$$
Here, $D_t$ is the eddy diffusivity, typically related to the eddy viscosity $\nu_t$ via a turbulent Schmidt number, $Sc_t = \nu_t / D_t$. The eddy viscosity can be modeled using, for instance, the Smagorinsky model: $\nu_t = (C_s \Delta)^2 |\tilde{S}|$, where $\Delta$ is the filter width, $C_s$ is a model constant, and $|\tilde{S}|$ is the magnitude of the resolved strain-rate tensor.

Second, a **[scale-similarity model](@entry_id:1131262)** posits that the structure of the SGS flux is similar to the flux generated by the smallest resolved scales. This is computed by applying a second, wider "test" filter (denoted by a hat, $\hat{\cdot}$) to the resolved field:
$$
(\mathbf{q}_{Y_k})_{\text{SS}} = C_{ss} \bar{\rho} \left( \widehat{\tilde{\mathbf{u}}\tilde{Y}_k} - \hat{\tilde{\mathbf{u}}}\hat{\tilde{Y}}_k \right)
$$
where $C_{ss}$ is a model coefficient. The final mixed model for the SGS species flux is a [linear combination](@entry_id:155091) of these two components, capturing both SGS energy dissipation and the structural characteristics of turbulent transport .

#### The Filtered Energy Equation and Variable-Density Effects

In combustion, large heat release causes significant density variations and strong velocity divergence (dilatation). Filtering the internal [energy equation](@entry_id:156281) reveals additional unclosed terms of great physical importance . The Favre-filtered internal energy ($e$) equation can be written as:
$$
\frac{\partial (\bar{\rho} \tilde{e})}{\partial t} + \frac{\partial (\bar{\rho} \tilde{e} \tilde{u}_j)}{\partial x_j} = -\bar{p} \frac{\partial \tilde{u}_j}{\partial x_j} + \bar{\tau}_{ij} \frac{\partial \tilde{u}_i}{\partial x_j} - \frac{\partial \tilde{q}_j}{\partial x_j} + \bar{\rho} \tilde{\dot{\omega}}_T + \Pi_p + \Xi_w - \frac{\partial J^{\text{sgs},e}_j}{\partial x_j} - \dots
$$
where $\bar{p}$ is the filtered pressure, $\bar{\tau}_{ij}$ is the resolved [viscous stress](@entry_id:261328), $\tilde{q}_j$ is the filtered heat flux, $\tilde{\dot{\omega}}_T$ is the filtered heat release rate, and $J^{\text{sgs},e}_j$ is the SGS convective flux of internal energy. Two crucial unclosed source terms emerge:

1.  **Pressure-Dilatation Correction ($\Pi_p$)**: Defined as $\Pi_p = -(\overline{p \partial u_j/\partial x_j} - \bar{p} \partial \tilde{u}_j/\partial x_j)$, this term represents the subgrid-scale work done by pressure forces. In regions of intense heat release, thermal expansion causes large positive velocity divergence ($\nabla \cdot \mathbf{u} > 0$). The pressure-dilatation term describes the exchange between thermal energy and kinetic energy at subgrid scales and can be a significant term in the energy budget near flame fronts.

2.  **Subgrid-Scale Viscous Work ($\Xi_w$)**: Defined as $\Xi_w = \overline{\tau_{ij} \partial u_i/\partial x_j} - \bar{\tau}_{ij} \partial \tilde{u}_i/\partial x_j}$, this term represents the irreversible dissipation of kinetic energy into internal energy (heat) by viscosity at unresolved scales. Since [viscous dissipation](@entry_id:143708) is always non-negative, $\Xi_w$ is a source of internal energy. In flame zones with high temperature gradients (affecting viscosity) and high strain rates, this term can become locally important.

For low-Mach-number reacting flows, [acoustic waves](@entry_id:174227) are filtered out, but dilatation due to heat release is retained. Numerical methods for these flows often employ a **projection method** to enforce the divergence constraint on the velocity field. This leads to an [elliptic equation](@entry_id:748938) for the mechanical pressure. In [variable-density flows](@entry_id:1133710), the [pressure correction](@entry_id:753714) step involves the term $(1/\bar{\rho}) \nabla \pi$. Consequently, the resulting pressure Poisson equation (PPE) is of a variable-coefficient form :
$$
\nabla \cdot \left( \frac{1}{\bar{\rho}} \nabla \pi \right) = \frac{1}{\Delta t} \left( \nabla \cdot \tilde{\mathbf{u}}^{\star} - S \right)
$$
Here, $\tilde{\mathbf{u}}^{\star}$ is a predicted intermediate velocity, and $S$ is the velocity divergence source term arising from heat release and diffusion. The operator on the left-hand side is a variable-coefficient [elliptic operator](@entry_id:191407), which requires specialized solvers. The corresponding Neumann boundary condition at a wall with normal $\mathbf{n}$ also incorporates the variable density:
$$
\mathbf{n} \cdot \left( \frac{1}{\bar{\rho}} \nabla \pi \right) = \frac{1}{\Delta t} \left( \mathbf{n} \cdot \tilde{\mathbf{u}}^{\star} - g \right)
$$
where $g$ is the prescribed normal velocity at the boundary. Proper formulation of this pressure equation is critical for numerically stable and accurate LES of low-Mach combustion.

### Regime-Dependent Modeling of the Filtered Reaction Rate

The most formidable challenge in reacting LES is the closure of the filtered chemical source term, $\overline{\dot{\omega}}_k$. Chemical reaction rates are typically strong, exponential functions of temperature and polynomial functions of species concentrations. Due to this high nonlinearity, the filtered reaction rate is not equal to the reaction rate evaluated at the filtered fields: $\overline{\dot{\omega}_k(T, \mathbf{Y})} \neq \dot{\omega}_k(\tilde{T}, \tilde{\mathbf{Y}})$.

The physical nature of the interaction between turbulence and chemistry varies dramatically depending on the relative time and length scales of the two processes. Therefore, before a model can be chosen, the local combustion regime must be identified.

#### Combustion Regime Identification

For **[premixed combustion](@entry_id:1130127)**, the interaction is often characterized by the Karlovitz number ($Ka$) and the Damköhler number ($Da$). The Karlovitz number, $Ka = \tau_f / \tau_k$, compares the flame time scale ($\tau_f \sim \delta_L/S_L$, with $\delta_L$ the laminar flame thickness and $S_L$ the [laminar flame speed](@entry_id:202145)) to the smallest turbulent time scale (the Kolmogorov scale, $\tau_k$). The regime boundaries are approximately:
-   $Ka \lt 1$: **Corrugated Flamelets Regime**. Turbulence wrinkles the thin flame sheet but does not alter its internal structure.
-   $1 \lt Ka \lt 100$: **Thin Reaction Zones Regime**. The smallest eddies penetrate the flame's preheat zone, but the inner reaction layer remains largely intact.
-   $Ka \gt 100$: **Broken Reaction Zones Regime**. Turbulence is so intense that it disrupts the entire flame structure, leading to distributed reactions.

For **[non-premixed combustion](@entry_id:1128819)**, the key parameters are the subfilter Damköhler number, $Da = \tau_{\text{flow}} / \tau_{\text{chem}}$, and the scalar dissipation rate, $\chi = 2D |\nabla Z|^2$, which measures the strain rate on the mixing layer.
-   If $Da \gg 1$ and $\chi$ is below the extinction value $\chi_{\text{crit}}$, the chemistry is fast and reactions occur in thin, stable **flamelets**.
-   If $Da \lesssim 1$ or $\chi > \chi_{\text{crit}}$, the flamelet structure may be disrupted or extinguished, leading to a **broken reaction zone**.

As an illustrative example, consider two points in a non-premixed flame . At a point with low subfilter turbulence and small mixture fraction gradients, one might find $Da = 2.25$ and $\chi = 10~\text{s}^{-1}$. Since $Da > 1$ and $\chi$ is below a typical extinction value (e.g., $\chi_{\text{crit}}=15~\text{s}^{-1}$), this region is in the [flamelet regime](@entry_id:1125055). At another point with strong turbulence and steep gradients, one might find $Da = 0.75$ and $\chi = 57.6~\text{s}^{-1}$. Here, $Da  1$ and $\chi > \chi_{\text{crit}}$, indicating a broken reaction zone. Similarly, for premixed flames, points can be classified based on local $Ka$ and $Da$ values . The choice of an appropriate LES closure must be guided by this regime classification.

### Closures for Premixed Combustion

#### The Level-Set (G-Equation) Approach

In the corrugated flamelets regime ($Ka \lt 1$), the flame can be modeled as an infinitely thin interface separating reactants and products. The **G-Equation** is a kinematic model that tracks the position of this interface, defined as the zero level-set of a [scalar field](@entry_id:154310) $G(\mathbf{x}, t)$. The filtered transport equation for $G$ is :
$$
\frac{\partial G}{\partial t} + \tilde{\mathbf{u}} \cdot \nabla G = S_T |\nabla G| = S_L \Xi |\nabla G|
$$
Here, the flame front is convected by the resolved flow $\tilde{\mathbf{u}}$ and propagates normal to itself at a speed $S_T$. This [turbulent burning velocity](@entry_id:1133501) $S_T$ is modeled as the [laminar burning velocity](@entry_id:1127023) $S_L$ multiplied by a **subgrid [wrinkling factor](@entry_id:1134139)** $\Xi \ge 1$. This factor accounts for the increased flame surface area due to unresolved turbulent eddies.

The closure problem shifts to modeling $\Xi$. Two common approaches are:
1.  **Fractal Models**: These are based on the idea that the subgrid flame surface has a fractal character. A typical model is $\Xi = (\Delta/\eta_c)^{D-2}$, where $\Delta$ is the filter width, $\eta_c$ is an inner [cutoff scale](@entry_id:748127), and $D$ is a [fractal dimension](@entry_id:140657).
2.  **Power-Law Models**: These relate $\Xi$ to the subgrid turbulent intensity, often derived from the subgrid kinetic energy $k_{\text{sgs}}$. An example form is $\Xi = 1 + C_w (\sqrt{2k_{\text{sgs}}}/S_L)^m (\Delta/\delta_L)^n$, often including an efficiency function to account for wrinkling reduction at high subgrid Karlovitz numbers.

Numerically, the $G$-equation is a Hamilton-Jacobi equation that requires specialized, high-order, [non-oscillatory schemes](@entry_id:1128816) (like WENO) and a periodic [reinitialization](@entry_id:143014) step to maintain $G$ as a [signed-distance function](@entry_id:754834) ($|\nabla G|=1$).

#### The Presumed PDF Approach

When the [flame structure](@entry_id:1125069) is not a simple interface or when it is fully subgrid, a volumetric approach is needed. The **presumed Probability Density Function (PDF)** method is a powerful framework for this. For [premixed combustion](@entry_id:1130127), a **progress variable** $c$ is defined (e.g., based on temperature or product mass fraction), with $c=0$ in unburned reactants and $c=1$ in fully burned products.

The filtered reaction rate $\overline{\dot{\omega}_c}$ is then modeled by integrating the instantaneous rate $\dot{\omega}_c(c)$ over the subgrid PDF of the [progress variable](@entry_id:1130223), $p(c)$:
$$
\overline{\dot{\omega}_c} = \bar{\rho} \widetilde{\dot{\omega}_c} \approx \bar{\rho} \int_0^1 \dot{\omega}_c(c') p(c' | \tilde{c}, \widetilde{c''^2}) \, \mathrm{d}c'
$$
The core of the model is the "presumed" shape of $p(c')$. Since $c$ is bounded between $0$ and $1$, the **Beta-PDF** is an excellent choice . The Beta-PDF is defined by two parameters, $\alpha$ and $\beta$, which can be uniquely determined from the first two moments of the distribution: the Favre-filtered mean $\tilde{c}$ and the subgrid variance $\widetilde{c''^2} \equiv \widetilde{c^2} - \tilde{c}^2$. These moments are obtained by solving their own transport equations. This approach transforms the closure problem for the highly nonlinear function $\dot{\omega}_c(c)$ into a closure problem for the transport of the variance $\widetilde{c''^2}$, which is generally more tractable.

### Closures for Non-Premixed Combustion: The Flamelet Framework

For [non-premixed flames](@entry_id:752599) in the [flamelet regime](@entry_id:1125055), a powerful analogy can be drawn: the complex three-dimensional turbulent flame can be viewed as an ensemble of quasi-one-dimensional, laminar flamelet structures. These structures are embedded within the turbulent flow field and are convected and strained by it.

The thermochemical state within these flamelets can be parameterized by a [conserved scalar](@entry_id:1122921), the **mixture fraction** $Z$, and a parameter representing the intensity of local mixing, the **[scalar dissipation](@entry_id:1131248) rate** $\chi$. The core of the flamelet approach is to pre-compute the solutions to the 1D steady-state [flamelet equations](@entry_id:1125053) for a range of [scalar dissipation](@entry_id:1131248) rates. These solutions populate a **[flamelet library](@entry_id:1125054)**, $\mathcal{L}$, which stores all relevant thermochemical quantities $\phi$ (temperature, species mass fractions, density) as functions of $Z$ and $\chi$: $\phi = \phi(Z, \chi)$.

To couple this library to the LES, the filtered value of any scalar $\tilde{\phi}$ is computed by integrating the flamelet solution over the subgrid joint PDF of $Z$ and $\chi$, denoted $P(Z, \chi)$ :
$$
\tilde{\phi} = \frac{\iint \rho(Z,\chi) \phi(Z,\chi) P(Z, \chi | \tilde{Z}, \widetilde{Z''^2}, \tilde{\chi}) \, \mathrm{d}Z \, \mathrm{d}\chi}{\iint \rho(Z,\chi) P(Z, \chi | \tilde{Z}, \widetilde{Z''^2}, \tilde{\chi}) \, \mathrm{d}Z \, \mathrm{d}\chi}
$$
The joint PDF is typically modeled as statistically independent or with a presumed factorization, $P(Z, \chi) = P_Z(Z) P_\chi(\chi)$. Common choices are a Beta-PDF for the mixture fraction $Z$ (parameterized by $\tilde{Z}$ and its variance $\widetilde{Z''^2}$) and a log-normal PDF for $\chi$ (parameterized by its mean $\tilde{\chi}$ and variance). The LES then involves solving transport equations for the moments ($\tilde{Z}, \widetilde{Z''^2}, \tilde{\chi}$) and retrieving the filtered thermochemical state from the flamelet library via PDF integration at every point and time step.

### Advanced Mechanisms and Model Fidelity

#### Differential Diffusion Effects

Standard [flamelet models](@entry_id:749445) often assume equal diffusivity for all species and heat (the unity Lewis number assumption, $\mathrm{Le}_k=1$). However, in reality, light species like H and H$_2$ diffuse much faster than heavier species. This **[differential diffusion](@entry_id:195870)** has significant effects on [flame structure](@entry_id:1125069) and temperature.

Incorporating these effects requires a more sophisticated flamelet formulation . First, the concept of a single [scalar dissipation](@entry_id:1131248) rate must be refined. With species-specific diffusivities $D_k$, the [effective diffusivity](@entry_id:183973) of the mixture fraction, $D_Z$, becomes a function of local composition and temperature. The [scalar dissipation](@entry_id:1131248) rate must be defined consistently as $\chi_Z = 2 D_Z(\mathbf{Y}, T) |\nabla Z|^2$. Second, and more critically, differential diffusion breaks the unique relationship between enthalpy and mixture fraction. This means that enthalpy, $h$, must be treated as a third independent parameter in the [flamelet library](@entry_id:1125054). The flamelet solution becomes $\phi = \phi(Z, \chi, h)$, and the LES must solve an additional transport equation for the filtered enthalpy to account for non-adiabatic effects and heat loss driven by non-unity Lewis numbers.

#### Modeling Extinction and Non-Equilibrium

The flamelet assumption implies that chemistry is in a steady state dictated by the local strain rate. However, in highly turbulent flames, local extinction and reignition are common. Simple [flamelet models](@entry_id:749445) based on a steady, single-valued "S-curve" response of temperature to strain can fail to capture this [intermittency](@entry_id:275330).

A crucial distinction arises between two types of PDF-based [closures](@entry_id:747387) :
1.  **Conditional-Mean Closure**: This approach models the conditional mean reaction rate, $\overline{\dot{\omega}|Z}$, directly from a flamelet library (e.g., using the stable burning branch). The filtered rate is then $\overline{\dot{\omega}} = \int \overline{\dot{\omega}|Z} P(Z) dZ$. This method is computationally efficient but implicitly assumes the flame is always burning at the subgrid level.
2.  **Joint Presumed PDF Closure**: A more advanced approach uses a joint PDF of both mixture fraction and a progress variable, $P(Z, c)$. This allows the subgrid distribution of $c$ to be bimodal, representing a mixture of burning ($c=1$) and extinguished ($c=0$) fluid pockets.

Consider a scenario with intermittent extinction where the true subgrid state at $Z=Z_{\text{st}}$ has a probability $\alpha$ of being fully burned ($c=1$) and $1-\alpha$ of being extinguished ($c=0$). A conditional-mean closure, assuming a fully burning state, would calculate a rate proportional to $1$. In contrast, a joint PDF closure would correctly weight the reaction rate by the probability of the burning state, calculating a rate proportional to $\alpha$. In a case with $\alpha=0.4$, the conditional-mean model would over-predict the reaction rate by a factor of $1/0.4 = 2.5$. This highlights how accurately modeling the shape of the subgrid PDF is essential for capturing complex [non-equilibrium phenomena](@entry_id:198484) like extinction.