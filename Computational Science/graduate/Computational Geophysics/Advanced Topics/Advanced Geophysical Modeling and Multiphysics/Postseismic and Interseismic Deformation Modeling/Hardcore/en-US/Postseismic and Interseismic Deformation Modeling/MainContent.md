## Introduction
The Earth's surface is in constant, albeit slow, motion, driven by the relentless movement of tectonic plates. This motion culminates in earthquakes, which abruptly release accumulated strain, but the story does not end there. Understanding the full [earthquake cycle](@entry_id:748775)—from the quiet interseismic period of strain build-up to the complex, transient postseismic relaxation—is fundamental to modern [geophysics](@entry_id:147342) and [seismic hazard](@entry_id:754639) assessment. However, the deep crustal and mantle processes that govern this cycle are hidden from direct view. The primary challenge lies in bridging the gap between what we can observe at the surface with geodetic instruments and the underlying physics of fault behavior and [rock mechanics](@entry_id:754400) at depth.

This article provides a comprehensive guide to the principles and applications of postseismic and [interseismic deformation](@entry_id:750780) modeling. It is structured to build your understanding from foundational concepts to advanced applications. In **Principles and Mechanisms**, we will dissect the core physical laws, from the elastic response to fault slip to the distinct signatures of afterslip, [viscoelastic relaxation](@entry_id:756531), and poroelastic rebound. Next, **Applications and Interdisciplinary Connections** will demonstrate how these models are used to solve real-world problems, such as assessing time-dependent seismic hazards, optimizing geodetic networks, and exploring the Earth's global dynamic response to great earthquakes. Finally, **Hands-On Practices** will offer practical exercises to implement and explore these models computationally, solidifying the theoretical knowledge you have gained.

## Principles and Mechanisms

The deformation of the Earth's lithosphere throughout the seismic cycle—from the slow, interseismic accumulation of strain to the rapid release in an earthquake and the subsequent transient relaxation—can be described by a set of fundamental physical principles. This chapter outlines the core mechanisms that govern these processes, providing a theoretical foundation for the computational models used to interpret geodetic observations. We will explore the elastic framework for crustal deformation, the kinematic and physical models of interseismic strain, the distinct mechanisms of postseismic transients, and the mathematical tools used to unify these concepts and invert for Earth properties.

### The Elastic Framework for Crustal Deformation

On the timescales of human observation and for the majority of the [earthquake cycle](@entry_id:748775), the Earth's upper crust behaves as an elastic solid. This approximation allows us to employ the powerful mathematical framework of continuum mechanics to relate internal processes, such as fault slip, to observable surface deformation.

#### The Volterra Dislocation: A Model for Fault Slip

The primary source of tectonic deformation is slip on a fault. In [continuum mechanics](@entry_id:155125), this is elegantly represented as a **Volterra dislocation**. A Volterra dislocation is defined by a prescribed displacement discontinuity, or jump, $\llbracket \mathbf{u} \rrbracket$, across an internal surface $S$ (the fault plane). This jump is precisely the fault slip vector $\mathbf{s}$. Everywhere else in the elastic medium, the displacement field is continuous and satisfies the governing equations of elastostatic equilibrium. A critical condition for [mechanical equilibrium](@entry_id:148830) is that the traction (force per unit area) must be continuous across the dislocation surface; otherwise, infinite accelerations would occur.

The Volterra dislocation is a specialized case of a more general concept known as **[eigenstrain](@entry_id:198120)**, $\epsilon_{ij}^*$. Eigenstrain represents any non-elastic, stress-free strain, such as that caused by thermal expansion, phase changes, or [aseismic creep](@entry_id:746526). In a constrained elastic body, [eigenstrain](@entry_id:198120) induces stress and elastic deformation. A dislocation can be mathematically represented as an eigenstrain distribution that is concentrated on the fault surface using a Dirac delta function. While dislocations are formally a subset of [eigenstrain](@entry_id:198120), in practice, we treat fault slip as a surface source (dislocation) and distributed inelastic processes like ductile flow as volumetric sources (eigenstrain) .

#### From Fault Slip to Surface Displacement: Green's Functions

To model the deformation caused by fault slip, we need a method to map the displacement discontinuity on the fault surface $S$ to the resulting displacement field $\mathbf{u}$ at any point $\mathbf{x}$ in the medium, particularly at the Earth's surface. This mapping is accomplished through **Green's functions**. A Green's function is the fundamental response of the medium to a point source. For a given fault geometry and elastic structure, the total displacement is found by integrating the slip over the fault area, weighted by the appropriate Green's functions.

For many applications in [geophysics](@entry_id:147342), the Earth can be reasonably approximated as a homogeneous, isotropic, linear [elastic half-space](@entry_id:194631). The analytical solutions for the Green's functions in such a medium were famously derived by Okada in 1985 and remain a cornerstone of crustal deformation modeling. These solutions provide the displacement, strain, and tilt fields at the surface due to a finite rectangular dislocation source at depth.

A crucial and sometimes counter-intuitive property of these solutions arises from the structure of the governing elastic equations. For a problem where the slip (a displacement boundary condition) is prescribed, the resulting [displacement field](@entry_id:141476) $\mathbf{u}$ depends on the geometry of the fault and the medium's **Poisson's ratio** ($\nu$), but it is independent of the **shear modulus** ($\mu$). Conversely, the stress field, which is calculated from the displacement field via Hooke's law ($\sigma_{ij} = C_{ijkl}\epsilon_{kl}$), is directly proportional to the shear modulus $\mu$. This means that inverting surface displacement data for fault slip does not, in a simple elastic model, constrain the rock's stiffness, but inverting for stress changes does .

### Interseismic Period: The Accumulation of Tectonic Strain

Between large earthquakes, [tectonic plates](@entry_id:755829) continue to move, and strain accumulates on locked portions of faults, setting the stage for the next rupture. Modeling this slow loading process is key to assessing seismic hazards.

#### The Back-Slip Model

A simple yet powerful tool for calculating the surface velocities during the interseismic period is the **back-slip model**, developed by Savage and Burford. This model is based on the principle of superposition in linear elasticity. Consider a long strike-slip fault where the shallow portion (to a depth $D$, the **locking depth**) is locked, while the deeper portion creeps steadily at the long-term plate rate $V$.

The interseismic surface velocity field can be constructed by superimposing two elastic solutions:
1.  **Steady Tectonic Loading:** A hypothetical scenario where the fault slips at the full plate rate $V$ along its entire depth. This produces rigid block motion, with a step-like [velocity profile](@entry_id:266404) at the surface: $u_{tectonic}(x) = \frac{V}{2}\mathrm{sgn}(x)$.
2.  **Fictitious Back-Slip:** To enforce the "locked" condition on the shallow segment (from depth 0 to $D$), we superimpose the elastic field caused by a fictitious fault slipping in the opposite direction at a rate of $-V$ on this segment.

The sum of these two fields cancels the slip on the shallow locked portion while leaving the deep creep intact. The resulting surface velocity profile across the fault (at a [perpendicular distance](@entry_id:176279) $x$) is given by the classic arctangent function :
$$
u(x) = \frac{V}{\pi} \arctan\left(\frac{x}{D}\right)
$$
In this model, the far-field plate rate $V$ sets the amplitude of the velocity difference across the fault, while the locking depth $D$ controls the width of the deformation zone. A deeper locking depth results in a broader region of surface strain. As $D \to 0$ (no locking), the profile approaches a sharp step function, and as $D \to \infty$ (infinitely strong fault), the surface velocity becomes zero everywhere.

#### Fault Coupling and Geodetic Moment Deficit

The simple binary view of a fault being either fully locked or fully creeping can be generalized to a spatially variable **interseismic [coupling coefficient](@entry_id:273384)**, $\Phi(x)$, which ranges from 0 (fully creeping) to 1 (fully locked). This dimensionless coefficient represents the fraction of the long-term relative plate velocity that is *not* accommodated by [aseismic creep](@entry_id:746526) on the fault interface but is instead stored as elastic strain in the surrounding crust. The portion of slip that is stored is known as the **slip deficit rate**.

Geodetic measurements, such as those from the Global Navigation Satellite System (GNSS), can be used to invert for maps of this [coupling coefficient](@entry_id:273384) on major faults, particularly subduction zone megathrusts. These "locking maps" are powerful tools for hazard assessment. Regions of high coupling ($\Phi \approx 1$) are accumulating stress and are considered more likely to rupture in future earthquakes.

Furthermore, we can quantify the rate at which seismic potential is accumulating. By analogy with the seismic moment of an earthquake ($M_0 = \mu A s$), we can define the **geodetic moment deficit rate**, $\dot{M}_0$, by integrating the slip deficit rate over the fault area $A$, weighted by the shear modulus $\mu$:
$$
\dot{M}_0 = \iint_A \mu \cdot \Phi(\mathbf{x}) \cdot V_{pl}(\mathbf{x}) \,dA
$$
where $V_{pl}(\mathbf{x})$ is the local plate convergence rate. This quantity represents the rate at which moment is being stored on the fault, which will eventually be released in earthquakes. For a fault divided into segments with uniform properties, this integral becomes a sum over the segments .

### Postseismic Period: Mechanisms of Transient Deformation

Immediately following a large earthquake, the crust and upper mantle do not simply return to a state of steady interseismic loading. Instead, they undergo a period of transient deformation that can last for days to decades. This postseismic relaxation is driven by several distinct physical mechanisms.

#### Afterslip

**Afterslip** is the process of continued, aseismic slip on the fault plane after a mainshock. It typically occurs on portions of the fault that did not rupture coseismically, often in deeper, downdip regions or in patches surrounding the main rupture area.

The governing physics of afterslip is rooted in rock friction. Laboratory experiments have shown that fault friction is not constant but depends on the slip rate and the history of slip, a behavior captured by **[rate-and-state friction](@entry_id:203352) laws**. Afterslip is thought to occur on parts of the fault that exhibit **velocity-strengthening** behavior, where the frictional resistance increases with slip velocity. This property inhibits the unstable acceleration that leads to earthquakes and instead promotes stable, slow slip. The relationship, often described by the Dieterich-Ruina law, can be written as :
$$
\tau = \sigma_{\mathrm{eff}} \left[ \mu_{0} + a \ln \left( \frac{V}{V_{0}} \right) + b \ln \left( \frac{\theta V_{0}}{D_{c}} \right) \right]
$$
where $\tau$ is shear stress, $\sigma_{\mathrm{eff}}$ is effective normal stress, $V$ is slip rate, and $\theta$ is a state variable representing the maturity of frictional contacts. For velocity-strengthening friction, the parameter difference $(a-b)$ is positive. The coseismic stress changes from the earthquake drive slip on these patches, resulting in a slip rate that decays approximately as $\dot{u} \propto 1/t$. When integrated over time, this produces a surface displacement that grows logarithmically: $u(t) \propto \ln(1+t/t_0)$ . Because the source is slip on the fault, the resulting surface deformation pattern is spatially localized near the fault, with gradients decaying over a distance comparable to the depth of the afterslip.

#### Viscoelastic Relaxation

While afterslip is a process on a fault surface, **[viscoelastic relaxation](@entry_id:756531)** is a volumetric process that occurs within the hot, ductile lower crust and upper mantle. The coseismic stress change is not confined to the elastic upper crust but also loads the underlying viscoelastic layers. Over time, these stresses relax through ductile flow.

This behavior can be conceptualized using simple spring-and-dashpot models. The most fundamental of these is the **Maxwell model**, which consists of a linear elastic spring (representing instantaneous elastic response) and a linear viscous dashpot (representing slow, ductile flow) connected in series. For a given stress $\sigma$ and strain $\epsilon$, its behavior is described by the [constitutive relation](@entry_id:268485) :
$$
\dot{\epsilon} = \frac{\dot{\sigma}}{\mu} + \frac{\sigma}{\eta}
$$
Here, $\mu$ is the [shear modulus](@entry_id:167228) and $\eta$ is the viscosity. This model is characterized by a single relaxation timescale, the **Maxwell time**, $\tau_M = \eta/\mu$. In response to a step-change in stress from an earthquake, a Maxwell body will exhibit an exponentially decaying [strain rate](@entry_id:154778). More complex rheologies, such as the **Burgers model** (a Maxwell element in series with a Kelvin-Voigt element), can be used to represent materials with both transient and [steady-state creep](@entry_id:161740) behavior, introducing multiple relaxation timescales .

The key phenomenological signatures of [viscoelastic relaxation](@entry_id:756531) are a surface deformation that decays roughly **exponentially** in time and a spatial pattern that is broad and long-wavelength, affecting regions hundreds of kilometers from the fault .

#### Poroelastic Rebound

A third mechanism, **poroelastic rebound**, involves the flow of fluids (like water) within the pore spaces of the crust. An earthquake suddenly changes the stress field, which in turn causes an instantaneous change in the pressure of the pore fluid. This initial response is **undrained**, as the fluid has no time to move. The magnitude of the initial [pore pressure](@entry_id:188528) change $\Delta p$ is related to the change in mean total stress $\Delta \sigma_m$ by **Skempton's coefficient** $B$: $\Delta p = B \Delta \sigma_m$.

The deformation of the porous rock skeleton is governed by the **[effective stress](@entry_id:198048)**, $\sigma'$, defined by Terzaghi's principle as modified by Biot: $\sigma'_{ij} = \sigma_{ij} - \alpha p \delta_{ij}$, where $\alpha$ is the **Biot coefficient** that couples the [fluid pressure](@entry_id:270067) to the solid matrix.

Following the initial [undrained response](@entry_id:756307), the induced pressure gradients drive fluid flow, and the system slowly evolves towards a **drained** state where the excess pore pressure has dissipated. This diffusion process causes [time-dependent deformation](@entry_id:755974). The timescale of the rebound is diffusive, scaling as $\tau \sim L^2/c$, where $L$ is a [characteristic length](@entry_id:265857) scale and $c$ is the [hydraulic diffusivity](@entry_id:750440). The total amplitude of the rebound deformation scales with the product $\alpha B$. Whether this transient results in uplift or subsidence depends on the sign of the coseismic stress change: regions that were compressed $(\Delta \sigma_m > 0)$ will experience postseismic subsidence as fluid drains out, while regions that were dilated $(\Delta \sigma_m  0)$ will experience uplift as fluid flows in .

### Unifying Observations and Models

The principles outlined above provide the basis for constructing quantitative models to analyze geodetic data and infer properties of the Earth's interior.

#### Deconstructing Geodetic Time Series

A continuous GNSS time series recording the displacement of a point on the Earth's surface following an earthquake is a composite of the various physical mechanisms at play. A common functional model used to fit such a time series is :
$$
u(t) = \underbrace{s_0 H(t-t_c)}_{\text{Coseismic}} + \underbrace{\sum_{i=1}^N A_i e^{-(t-t_c)/\tau_i}}_{\text{Viscoelastic}} + \underbrace{B \ln\left(1+\frac{t-t_c}{t_0}\right)}_{\text{Afterslip}} + \underbrace{V t}_{\text{Interseismic}} + \epsilon(t)
$$
Each term has a direct physical interpretation:
-   $s_0 H(t-t_c)$: The instantaneous coseismic offset at the time of the earthquake $t_c$, modeled by a Heaviside step function.
-   $\sum A_i e^{-(t-t_c)/\tau_i}$: A sum of exponential decay terms representing the relaxation of different viscoelastic modes in the lower crust and mantle.
-   $B \ln(1+\dots)$: A logarithmic term representing the integrated effect of afterslip on the fault.
-   $V t$: A linear term representing the steady, long-term secular velocity of the station due to [plate tectonics](@entry_id:169572).
-   $\epsilon(t)$: A [stochastic noise](@entry_id:204235) term, which in reality is often temporally correlated ([colored noise](@entry_id:265434)) .

#### Inverse Modeling and Regularization

The ultimate goal is often to use surface displacement data to solve an **inverse problem**: to infer the [spatial distribution](@entry_id:188271) of unknown physical properties, such as afterslip on a fault or viscosity variations in the mantle. This typically takes the form of a linear system $d = Gx$, where $d$ is the data vector, $x$ is the vector of model parameters, and $G$ is the Green's function matrix derived from the physical principles discussed earlier.

These [inverse problems](@entry_id:143129) are frequently ill-posed, meaning that small errors in the data can lead to large, unphysical oscillations in the solution. To obtain a stable and physically meaningful solution, we employ **regularization**. A common method is **Tikhonov regularization**, which involves minimizing a weighted sum of the [data misfit](@entry_id:748209) and a penalty term that measures the "roughness" or complexity of the model:
$$
\min_x \left( \|Gx-d\|_2^2 + \lambda^2 \|Lx\|_2^2 \right)
$$
This can be interpreted within a Bayesian framework as finding the **Maximum A Posteriori (MAP)** estimate, where the [data misfit](@entry_id:748209) corresponds to the likelihood and the regularization term corresponds to a [prior belief](@entry_id:264565) about the model's properties. The [regularization parameter](@entry_id:162917) $\lambda$ controls the trade-off between fitting the data and satisfying the prior constraint. The operator $L$ encodes our [prior belief](@entry_id:264565) about the model's structure :
-   **Zeroth-order** ($L=I$): Penalizes the magnitude of the model parameters, shrinking them towards zero.
-   **First-order** ($L \approx \nabla$): Penalizes the gradient of the model, favoring solutions that are piecewise-constant or "flat".
-   **Second-order** ($L \approx \nabla^2$): Penalizes the curvature of the model, favoring smooth solutions.

#### The Complete Cycle: A Unified View

The interseismic loading process and postseismic relaxation are two facets of the same underlying mechanical system. We can unify them by considering the evolution of stress in a viscoelastic medium that is subject to a constant long-term loading rate. A simple 1D Maxwell model subjected to a kinematic loading rate $S(x)$ (representing interseismic backslip) and a periodic coseismic stress drop provides a powerful insight  .

The solution to the governing stress evolution equation shows that after a disturbance, the system relaxes back towards a **steady state**. In this steady state, the stress becomes constant, and all the long-term deformation is accommodated by the viscous component. Crucially, the steady-state viscous strain rate becomes equal to the imposed tectonic loading rate, $\dot{\gamma}_{v,ss}(x) = S(x)$. This means the steady-state deformation rate is *independent* of the viscosity $\eta$. The viscosity only controls the timescale of the transient relaxation back to this steady state. This result underscores a fundamental principle: to constrain the rheological properties of the lithosphere and asthenosphere, we must observe the time-dependent, transient parts of the deformation cycle. Steady-state interseismic velocities alone are insufficient.