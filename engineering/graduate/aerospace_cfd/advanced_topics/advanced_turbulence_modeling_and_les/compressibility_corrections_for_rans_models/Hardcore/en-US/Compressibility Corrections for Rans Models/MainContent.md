## Introduction
Reynolds-Averaged Navier-Stokes (RANS) models are the cornerstone of computational fluid dynamics (CFD) for industrial applications, offering a balance between accuracy and computational cost. However, these models, often developed and calibrated for incompressible flows, exhibit critical deficiencies when applied to high-speed flight, combustion, and other environments where fluid compressibility is significant. This breakdown stems from the omission of key physical phenomena unique to compressible turbulence, leading to inaccurate predictions of aerodynamic forces, heat transfer, and mixing rates. To bridge this gap, a class of modifications known as [compressibility corrections](@entry_id:747585) has been developed to restore physical fidelity to RANS closures.

This article provides a comprehensive overview of [compressibility corrections](@entry_id:747585) for RANS models, structured to build from fundamental principles to practical application. The first chapter, "Principles and Mechanisms," delves into the theoretical foundations, explaining why standard averaging fails and introducing the new physics, such as [dilatational dissipation](@entry_id:748437), that emerges in high-speed flows. The second chapter, "Applications and Interdisciplinary Connections," explores the practical impact of these corrections in fields like [high-speed aerodynamics](@entry_id:272086) and [reacting flows](@entry_id:1130631), demonstrating their necessity for accurate engineering predictions. Finally, "Hands-On Practices" offers targeted exercises to solidify understanding of key concepts. We begin by examining the fundamental framework required to properly analyze turbulent compressible flows.

## Principles and Mechanisms

### The Necessity of a Compressible Framework: Favre Averaging

In the study of incompressible turbulent flows, the Reynolds-Averaged Navier-Stokes (RANS) equations are formulated by decomposing instantaneous quantities into a mean and a fluctuating component, a procedure known as Reynolds averaging. This approach is highly successful when density variations are negligible. However, in high-speed flows, significant variations in density, temperature, and pressure are intrinsic to the dynamics. These variations introduce a [strong coupling](@entry_id:136791) between the velocity field and the thermodynamic state of the fluid, a coupling that complicates the standard averaging process.

Let us consider the convective term in the momentum equation, $\rho u_i u_j$. If we apply the classical Reynolds decomposition, where $\rho = \overline{\rho} + \rho'$ and $u_i = \overline{u_i} + u_i'$, the time-average of this term becomes:
$$ \overline{\rho u_i u_j} = \overline{(\overline{\rho} + \rho')(\overline{u_i} + u_i')(\overline{u_j} + u_j')} $$
Expanding this expression and applying the averaging operator yields:
$$ \overline{\rho u_i u_j} = \overline{\rho}\overline{u_i}\overline{u_j} + \overline{\rho}\overline{u_i'u_j'} + \overline{u_i}\overline{\rho'u_j'} + \overline{u_j}\overline{\rho'u_i'} + \overline{\rho'u_i'u_j'} $$
Compared to the incompressible case, where the averaged [convective flux](@entry_id:158187) is simply $\rho (\overline{u_i}\overline{u_j} + \overline{u_i'u_j'})$, the compressible form introduces several new, unclosed correlation terms. These include the **turbulent mass flux**, $\overline{\rho'u_i'}$, and a triple correlation, $\overline{\rho'u_i'u_j'}$. Attempting to derive and solve transport equations for each of these new terms would dramatically increase the complexity of the [turbulence closure problem](@entry_id:268973).

To circumvent this difficulty, the standard approach in [compressible turbulence modeling](@entry_id:747593) is to employ **density-weighted averaging**, also known as **Favre averaging**. In this framework, any instantaneous quantity $\phi$ is decomposed as $\phi = \tilde{\phi} + \phi''$, where the Favre average $\tilde{\phi}$ is defined as:
$$ \tilde{\phi} \equiv \frac{\overline{\rho \phi}}{\overline{\rho}} $$
The corresponding fluctuation, $\phi''$, has the useful property that its density-weighted average is zero: $\overline{\rho \phi''} = 0$. Note that for the density itself, we retain the Reynolds decomposition, $\rho = \overline{\rho} + \rho'$.

Applying this decomposition to the velocity components, $u_i = \tilde{u_i} + u_i''$, let us re-examine the averaged convective flux:
$$ \overline{\rho u_i u_j} = \overline{\rho (\tilde{u_i} + u_i'')(\tilde{u_j} + u_j'')} = \overline{\rho\tilde{u_i}\tilde{u_j} + \rho\tilde{u_i}u_j'' + \rho u_i''\tilde{u_j} + \rho u_i''u_j''} $$
By linearity of the averaging operator and the fact that Favre-averaged quantities $\tilde{u_i}$ are defined in terms of averages, we can write:
$$ \overline{\rho u_i u_j} = \overline{\rho}\tilde{u_i}\tilde{u_j} + \tilde{u_i}\overline{\rho u_j''} + \tilde{u_j}\overline{\rho u_i''} + \overline{\rho u_i''u_j''} $$
By the definition of the Favre fluctuation, the second and third terms vanish, leaving a much simpler form:
$$ \overline{\rho u_i u_j} = \overline{\rho}\tilde{u_i}\tilde{u_j} + \overline{\rho u_i''u_j''} $$
The term $\tau_{ij}^F \equiv \overline{\rho u_i''u_j''}$ is the **Favre-averaged Reynolds stress tensor**. Its appearance preserves the structural analogy with the incompressible RANS equations. The Favre-averaged momentum equation contains a mean convective flux, $\overline{\rho}\tilde{u_i}\tilde{u_j}$, and a single unclosed tensor representing the [turbulent momentum transport](@entry_id:1133519). All the complex interactions involving [density fluctuations](@entry_id:143540) are now implicitly contained within this single tensor, greatly simplifying the closure task . From this point forward, unless otherwise specified, all mean velocities and temperatures will be understood as Favre-averaged quantities.

### The Physics of Compressible Turbulence

Having established the appropriate averaging framework, we must now examine the new physical phenomena that arise in compressible turbulence. The fundamental difference from incompressible turbulence is the ability of the fluid to undergo volumetric changes, which allows for the existence of [acoustic waves](@entry_id:174227).

A powerful conceptual tool for understanding this is the **Helmholtz decomposition**, which allows any vector field, such as the fluctuating velocity $\mathbf{u}'$, to be split into a solenoidal ([divergence-free](@entry_id:190991)) component $\mathbf{u}_s$ and a dilatational or irrotational (curl-free) component $\mathbf{u}_d$:
$$ \mathbf{u}' = \mathbf{u}_s + \mathbf{u}_d \quad \text{where} \quad \nabla \cdot \mathbf{u}_s = 0 \quad \text{and} \quad \nabla \times \mathbf{u}_d = \mathbf{0} $$
In incompressible turbulence, the condition $\nabla \cdot \mathbf{u} = 0$ requires that the flow be purely solenoidal; the turbulent eddies are vortical in nature. In compressible turbulence, however, both components exist. The solenoidal part corresponds to the familiar **vortical modes** of turbulence, while the dilatational part corresponds to **acoustic modes** that are coupled to fluctuations in pressure, density, and temperature . The total turbulent kinetic energy, $k$, can thus be partitioned into a solenoidal contribution $k_s$ and a dilatational contribution $k_d$.

The parameter that governs the importance of these dilatational effects is the **turbulent Mach number**, $M_t$. It is defined as the ratio of a characteristic velocity of the turbulent fluctuations to the local mean speed of sound, $a$. The characteristic velocity is taken as the root-mean-square (RMS) of the fluctuation magnitude, $u'_{rms} = \sqrt{\overline{u'_i u'_i}}$. In the context of Favre averaging, the turbulent kinetic energy per unit mass is $k = \frac{1}{2}\widetilde{u_i'' u_i''}$, so the RMS velocity is $\sqrt{2k}$. This leads to the standard definition:
$$ M_t = \frac{\sqrt{2k}}{a} $$
As $M_t \to 0$, the turbulent fluctuations are much slower than the speed of sound, and the flow behaves incompressibly; the energy is almost entirely in vortical modes, and the solenoidal [energy spectrum](@entry_id:181780) resembles its classic incompressible counterpart. As $M_t$ increases, a non-trivial fraction of the turbulent energy is transferred to the [acoustic modes](@entry_id:263916). For instance, in a high-altitude boundary layer with $k = 1500 \, \mathrm{m^2/s^2}$ and a temperature of $T=220 \, \mathrm{K}$, the speed of sound is approximately $a \approx 297 \, \mathrm{m/s}$. The turbulent Mach number is $M_t = \sqrt{2 \times 1500} / 297 \approx 0.18$. While this may seem small, many compressibility effects scale with $M_t^2$, implying corrections on the order of $3-4\%$, which are often non-negligible in aerospace applications . Crucially, the strength of compressibility effects depends on the local temperature; for a fixed $k$, a lower temperature implies a lower speed of sound and thus a higher $M_t$.

### Key Compressible Mechanisms and Their Modeling Implications

The interaction between vortical and [acoustic modes](@entry_id:263916), and the coupling of turbulence to thermodynamics, manifests as specific terms in the exact transport equation for [turbulent kinetic energy](@entry_id:262712). Standard incompressible RANS models omit these terms, necessitating the development of [compressibility corrections](@entry_id:747585).

#### Dilatational Dissipation

The rate of [viscous dissipation](@entry_id:143708) of kinetic energy is physically tied to the fluid's strain rate. The total instantaneous [dissipation rate](@entry_id:748577) per unit volume, $\Phi$, can be decomposed into two parts:
$$ \Phi = 2 \mu s_{ij} s_{ij} + \mu_b \theta^2 $$
where $s_{ij}$ is the deviatoric strain-rate tensor associated with shearing and rotational motions, and $\theta = \nabla \cdot \mathbf{u}$ is the dilatation associated with volumetric changes. The first term leads to the **solenoidal dissipation rate**, $\epsilon_s$, which is the only form of viscous dissipation in incompressible flow. The second term, involving the bulk viscosity $\mu_b$, is the source of the **[dilatational dissipation](@entry_id:748437) rate**, $\epsilon_d$. In the context of the TKE budget, this term is defined as:
$$ \epsilon_d = \frac{\overline{\mu_b (\theta')^2}}{\overline{\rho}} $$
where $\theta' = \nabla \cdot \mathbf{u}'$ is the fluctuating dilatation. This term represents the viscous damping of compressive and expansive motions, which are predominantly carried by the [acoustic modes](@entry_id:263916) of turbulence . For many gases, Stokes' hypothesis ($\mu_b = 0$) is assumed, which would imply $\epsilon_d=0$. However, more advanced theory and [direct numerical simulation](@entry_id:149543) (DNS) have shown that an *effective* [dilatational dissipation](@entry_id:748437) arises even with $\mu_b=0$ through non-linear mechanisms. DNS studies show that for moderate turbulent Mach numbers, the [dilatational dissipation](@entry_id:748437) scales as $\epsilon_d \propto M_t^2 \epsilon_s$. This provides a clear target for modeling: any [compressibility correction](@entry_id:274425) should introduce an additional dissipation term that grows with $M_t^2$.

#### Pressure-Dilatation Correlation

The pressure-[strain tensor](@entry_id:193332), $\Pi_{ij} = \overline{p'(\partial u'_i/\partial x_j + \partial u'_j/\partial x_i)}$, represents the redistribution of turbulent kinetic energy among its components by fluctuating pressure forces. In incompressible flow, where $\nabla \cdot \mathbf{u}' = 0$, the trace of this tensor is zero ($\Pi_{kk}=0$), meaning it only shuffles energy between the [normal stresses](@entry_id:260622) and does not alter the total TKE, $k$.

In [compressible flow](@entry_id:156141), the trace is non-zero:
$$ \Pi_{kk} = \overline{p'(\partial u'_k/\partial x_k + \partial u'_k/\partial x_k)} = 2 \overline{p'\theta'} $$
The term $\overline{p'\theta'}$ is the **pressure-dilatation correlation**. It represents a net rate of work done by pressure fluctuations on the fluctuating volume changes, serving as a [direct exchange](@entry_id:145804) mechanism between turbulent kinetic energy and internal energy of the fluid. It is a source or sink term in the TKE budget and is one of the most important physical mechanisms unique to compressible turbulence. Modeling this term is a central challenge, as its sign and magnitude depend sensitively on the flow regime.

#### Pressure-Strain Redistribution

Beyond its trace, the full pressure-strain tensor $\Pi_{ij}$ is also modified by compressibility . In Reynolds Stress Models (RSMs), this tensor is typically split into a **rapid part**, $\Pi_{ij}^{(r)}$, which depends on the mean strain rate and governs the immediate response of turbulence to mean flow deformation, and a **slow part**, $\Pi_{ij}^{(s)}$, which is responsible for the [return-to-isotropy](@entry_id:754321) tendency of turbulence. Compressibility affects both:
1.  Mean dilatation, $\theta = \nabla \cdot \mathbf{\tilde{u}}$, is a new scalar quantity that can enter the model for the rapid term, introducing new isotropic and anisotropic contributions.
2.  The slow, [return-to-isotropy](@entry_id:754321) process is observed to be hindered by compressibility. This is modeled by making the coefficients of the slow term functions of the turbulent Mach number $M_t$, typically reducing the term's magnitude as $M_t$ increases.

### Impact on RANS Closures and Model Corrections

The physical mechanisms described above must be incorporated into practical RANS [closures](@entry_id:747387), which are most often based on the Boussinesq hypothesis.

#### The Boussinesq Hypothesis in Compressible Flow

In the Favre-averaged framework, the Boussinesq hypothesis relates the Reynolds stresses to the mean strain rate:
$$ -\overline{\rho u_i'' u_j''} = 2 \mu_t \left(\tilde{S}_{ij} - \frac{1}{3}\tilde{S}_{kk}\delta_{ij}\right) - \frac{2}{3}\overline{\rho}k\delta_{ij} $$
where $\tilde{S}_{ij}$ is the mean [strain rate tensor](@entry_id:198281). The eddy viscosity, $\mu_t$, is commonly modeled using a two-equation model (e.g., $k-\epsilon$ or $k-\omega$). A baseline model might take the incompressible form $\mu_t = \overline{\rho} C_\mu \frac{k^2}{\epsilon}$. While the explicit factor of mean density $\overline{\rho}$ correctly scales the momentum transport with mass density, this is insufficient . The quantities $k$ and $\epsilon$ (the [dissipation rate](@entry_id:748577)) are themselves governed by transport equations whose [source and sink](@entry_id:265703) terms are altered by compressibility. A simple multiplication by $\overline{\rho}$ fails to capture the reduction in turbulent mixing efficiency caused by dilatational effects. Therefore, the model for $\mu_t$ itself, or the transport equations for $k$ and $\epsilon$, must be corrected.

#### Canonical Problems Driving Correction Development

The need for and form of [compressibility corrections](@entry_id:747585) are largely informed by their failure to predict certain canonical high-speed flows.

**The Compressible Mixing Layer:** A foundational problem is the planar mixing layer between two parallel streams of different velocities. Empirically, the growth rate of this layer is dramatically suppressed as the relative Mach number of the two streams increases. This phenomenon is parameterized by the **convective Mach number**, $M_c$:
$$ M_c = \frac{|U_1 - U_2|}{a_1 + a_2} $$
where $(U_1, a_1)$ and $(U_2, a_2)$ are the velocities and sound speeds of the two streams. Standard RANS models fail to predict this growth rate reduction. This led to the development of empirical correction factors, where the compressible growth rate is modeled as a fraction of the incompressible rate, $(d\theta/dx)_{\text{comp}} = \Pi_c(M_c) (d\theta/dx)_{\text{inc}}$. A typical functional form consistent with physical constraints is $\Pi_c(M_c) = (1 + \alpha M_c^2)^{-1}$ for some constant $\alpha$ . This provides a clear empirical target for more physics-based models.

**Shock-Turbulence Interaction (STI):** Perhaps the most dramatic failure of uncorrected RANS models occurs when turbulence passes through a shock wave. This is a problem of **rapid distortion**, where the mean flow is compressed over a timescale much shorter than the eddy turnover time. DNS and experiments show a moderate amplification of [turbulent kinetic energy](@entry_id:262712) across the shock. However, standard eddy-viscosity models predict a massive, unphysical spike in $k$ . This failure is traced to two primary sources:
1.  **Excessive Production:** The modeled production term, $P_k^{\text{model}}$, is proportional to the square of the mean strain rate, $S_{ij}S_{ij}$. Within the extremely thin, high-gradient region of a shock, this term becomes enormous and positive.
2.  **Missing Sinks:** The physical mechanisms that counteract this production in reality—namely, the pressure-dilatation correlation ($\overline{p'\theta'}  0$) and the [dilatational dissipation](@entry_id:748437) ($\epsilon_d$)—are absent from the standard model equations.

The model thus predicts a huge source of energy with no corresponding sink, leading to the erroneous spike in $k$.

#### Common Strategies for Compressibility Corrections

The goal of modern [compressibility corrections](@entry_id:747585) is to introduce models for the missing physical sink terms to balance the excessive production in regions of strong compression. Several prominent approaches exist:

*   **Sarkar-type Corrections:** Based on [asymptotic analysis](@entry_id:160416), these models introduce explicit terms to account for both pressure-dilatation and [dilatational dissipation](@entry_id:748437). The correction often takes the form of a sink term proportional to the production, $-P_k M_t^2$, and an additional dissipation term proportional to $\epsilon_s M_t^2$. By acting on both production and dissipation, this approach provides strong damping but can sometimes be too aggressive, over-damping turbulence in certain flows.

*   **Zeman-type Corrections:** These models focus primarily on modeling the [dilatational dissipation](@entry_id:748437), $\epsilon_d$, often based on a physical picture involving intermittent small-scale "shocklets" within the turbulence. The correction augments the [dissipation rate](@entry_id:748577) $\epsilon$ with a function of $M_t$.

*   **Wilcox-type Corrections:** Implemented within the robust $k-\omega$ framework, these corrections typically modify the [specific dissipation rate](@entry_id:755157) $\omega$. Crucially, they often include a **free-shear limiter**, a function that activates the correction in free-shear flows (like jets and mixing layers) but deactivates or weakens it in the [near-wall region](@entry_id:1128462) of boundary layers. This is a pragmatic approach to prevent the known issue of corrections degrading the prediction of high-speed boundary layers.

All of these models are designed to be consistent with the theoretical scaling that compressible effects are of order $O(M_t^2)$ for small $M_t$, ensuring they vanish smoothly in the incompressible limit .

### Broader Implications and Constraints

Finally, the development and application of [compressibility corrections](@entry_id:747585) must adhere to broader physical and mathematical principles.

#### Connection to Thermodynamic Fields

In [compressible flow](@entry_id:156141), the momentum and energy equations are coupled. However, the simple analogies that exist for [laminar flow](@entry_id:149458) often break down for turbulence. The classical **Crocco-Busemann relation**, for instance, provides a simple algebraic link between the temperature and velocity profiles in a laminar, zero-pressure-gradient boundary layer on an [adiabatic wall](@entry_id:147723). For a Prandtl number of unity, it shows that the total enthalpy is constant across the boundary layer. This elegant result does not hold for turbulent flows modeled with RANS . The reason is the presence of turbulent transport terms in the mean energy equation—specifically, the turbulent heat flux (e.g., $\overline{\rho}c_p\widetilde{v''T''}$)—and a [turbulent dissipation](@entry_id:261970) source term ($\overline{\rho}\epsilon$). The ratio of turbulent [momentum diffusivity](@entry_id:275614) to turbulent heat diffusivity, the **turbulent Prandtl number ($Pr_t$)**, is generally not equal to one. This breakdown of the simple analogy underscores the need for sophisticated modeling of the energy equation and [turbulent heat flux](@entry_id:151024), which are themselves affected by compressibility.

#### The Constraint of Realizability

Any [turbulence model](@entry_id:203176), including its corrections, must produce results that are physically possible. This constraint is known as **[realizability](@entry_id:193701)**. The Reynolds stress tensor $R_{ij}$ (or its Favre-averaged counterpart) is a covariance matrix and must therefore be symmetric and positive semidefinite. This mathematical property implies several physical constraints :
1.  **Positivity of Normal Stresses:** The diagonal components must be non-negative (e.g., $\overline{u'_1 u'_1} \ge 0$).
2.  **Positivity of TKE:** The turbulent kinetic energy $k = \frac{1}{2} R_{ii}$ must be non-negative.
3.  **Schwarz Inequality:** The magnitude of shear stresses is bounded by the normal stresses: $|R_{ij}| \le \sqrt{R_{ii} R_{jj}}$ for $i \neq j$.

Compressibility corrections, if improperly designed, can violate these conditions. For example, an overly aggressive pressure-dilatation model could act as an unbounded negative source in the $k$-equation, potentially driving $k$ to negative values in a numerical simulation. Similarly, a correction to the pressure-strain term in an RSM could predict an unphysical state of anisotropy, pushing the eigenvalues of the normalized Reynolds stress tensor outside their valid range (the "Lumley triangle"). Even simple linear eddy-viscosity models are not inherently realizable and can violate the Schwarz inequality in regions of high mean strain, a problem not automatically fixed by a scalar compressibility function. Therefore, ensuring a model is realizable across all [flow regimes](@entry_id:152820) is a critical and non-trivial aspect of developing robust [compressibility corrections](@entry_id:747585).