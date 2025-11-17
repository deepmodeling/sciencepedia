## Introduction
Standard [turbulence models](@entry_id:190404), foundational to [computational fluid dynamics](@entry_id:142614) (CFD), were developed primarily for incompressible flows where fluid density remains constant. However, in critical applications like high-speed aerospace, [turbomachinery](@entry_id:276962), and [combustion](@entry_id:146700), this assumption fails, leading to significant prediction errors. This discrepancy highlights a crucial knowledge gap: how to adapt [turbulence models](@entry_id:190404) to account for the unique physics of compressible flow. This article addresses this challenge by providing a comprehensive overview of [compressibility corrections](@entry_id:747585) for [turbulence models](@entry_id:190404).

The first chapter, **Principles and Mechanisms**, delves into the fundamental theory, identifying the turbulent Mach number as the key parameter and explaining new physical phenomena like [dilatational dissipation](@entry_id:748437) and pressure-dilatation. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the practical impact of these corrections across diverse fields, from predicting [shock-induced separation](@entry_id:196064) in aerodynamics to modeling star formation in astrophysics. Finally, the **Hands-On Practices** chapter provides practical exercises to solidify understanding, guiding the reader through model development, validation, and implementation. By navigating these sections, readers will gain a deep, functional understanding of why, how, and where [compressibility corrections](@entry_id:747585) are essential for modern fluid dynamics simulation.

## Principles and Mechanisms

Standard turbulence models, particularly those in the Reynolds-Averaged Navier–Stokes (RANS) framework, were historically developed for incompressible flows. In such flows, density is constant, and the velocity field is solenoidal ([divergence-free](@entry_id:190991)). However, in many engineering and scientific applications—from aerospace and [turbomachinery](@entry_id:276962) to astrophysics and [combustion](@entry_id:146700)—the effects of fluid [compressibility](@entry_id:144559) are significant. Applying incompressible [turbulence models](@entry_id:190404) directly to these regimes can lead to substantial inaccuracies. This chapter elucidates the fundamental principles governing the influence of compressibility on turbulence and details the mechanisms through which these effects are incorporated into [turbulence models](@entry_id:190404).

### The Governing Parameter: The Turbulent Mach Number

A common point of confusion in compressible turbulence is identifying the parameter that dictates the need for corrections. One might intuitively assume that the mean flow Mach number, $M_{\infty}$, is the sole determinant. While a high $M_{\infty}$ certainly indicates a compressible mean flow, it does not necessarily mean that the turbulence *dynamics* are significantly altered by compressibility. The crucial parameter governing the intrinsic compressibility of the turbulent fluctuations themselves is the **turbulent Mach number**, $M_t$.

From [dimensional analysis](@entry_id:140259), we can establish the fundamental [dimensionless groups](@entry_id:156314) that govern a homogeneous compressible [turbulent flow](@entry_id:151300). Given a set of relevant [physical quantities](@entry_id:177395)—[turbulent kinetic energy](@entry_id:262712) ($k$), dissipation rate ($\epsilon$), density ($\rho$), viscosity ($\mu$), speed of sound ($a$), and a [characteristic length](@entry_id:265857) scale ($L$)—two key parameters emerge: the turbulent Reynolds number, $Re_t$, and a Mach number based on turbulent quantities ([@problem_id:3302855]).

The turbulent Mach number is formally defined as the ratio of a characteristic turbulent velocity fluctuation to the local mean speed of sound. The characteristic velocity is taken as the root-mean-square (rms) of the velocity fluctuations, $u'_{\mathrm{rms}} = \sqrt{\overline{u_i' u_i'}}$. Given the standard definition of [turbulent kinetic energy](@entry_id:262712) (TKE) per unit mass, $k = \frac{1}{2}\overline{u_i' u_i'}$, the rms velocity is $u'_{\mathrm{rms}} = \sqrt{2k}$. Therefore, the turbulent Mach number is given by:

$$
M_t = \frac{\sqrt{2k}}{a}
$$

where $a$ is the local mean speed of sound ([@problem_id:3302800]). This parameter quantifies the [compressibility](@entry_id:144559) of the turbulent eddies themselves. If the eddies are moving relative to each other at speeds approaching the speed of sound, they can generate significant [density fluctuations](@entry_id:143540) and compressive motions, altering the energy cascade and dissipation processes.

The distinction between $M_{\infty}$ and $M_t$ is critical ([@problem_id:3302800]). Consider two hypothetical flows:
1.  A supersonic boundary layer with $M_{\infty} = 2.0$, where the turbulence intensity is low, resulting in a local $M_t \approx 0.02$.
2.  A low-speed, highly [turbulent jet](@entry_id:271164) with $M_{\infty} = 0.25$, but with intense velocity fluctuations in a cold region, leading to a local $M_t \approx 0.33$.

In the first case, although the mean flow is highly compressible, the turbulence itself is not. The [turbulent eddies](@entry_id:266898) are moving at speeds far below the local speed of sound. In the second case, despite a nominally incompressible mean flow, the turbulence is intrinsically compressible. This demonstrates that $M_t$, not $M_{\infty}$, is the primary indicator for whether specific corrections to the *turbulence model closure* are necessary.

### Morkovin's Hypothesis: The Incompressible Limit

The observation that low-$M_t$ turbulence behaves similarly to incompressible turbulence is formalized by **Morkovin's Hypothesis**. This hypothesis, based on extensive experimental data, posits that for non-hypersonic, attached turbulent shear flows without strong shocks, the essential dynamics of the turbulence are unaffected by [compressibility](@entry_id:144559) as long as the density fluctuations are small compared to the mean density ([@problem_id:3302813]).

The theoretical basis for this hypothesis lies in the scaling of [compressibility](@entry_id:144559) effects with $M_t$. Through an analysis of the linearized equations for fluctuating quantities, one can show that for small-amplitude, locally isentropic fluctuations, both the relative [density fluctuations](@entry_id:143540) and the dilatational (compressive) component of the [turbulent kinetic energy](@entry_id:262712) scale with the square of the turbulent Mach number:

$$
\frac{\rho'_{\mathrm{rms}}}{\bar{\rho}} \sim O(M_t^2) \quad \text{and} \quad \frac{k_d}{k} \sim O(M_t^2)
$$

Here, $\rho'_{\mathrm{rms}}$ is the root-mean-square of [density fluctuations](@entry_id:143540), $\bar{\rho}$ is the mean density, $k$ is the total [turbulent kinetic energy](@entry_id:262712), and $k_d$ is the portion of TKE associated with dilatational velocity fluctuations ([@problem_id:3302813]).

These [scaling laws](@entry_id:139947) imply that if $M_t$ is small (a common threshold is $M_t \lesssim 0.3$), the [density fluctuations](@entry_id:143540) are of second-order smallness and the kinetic energy is overwhelmingly contained in the solenoidal (incompressible, vortical) part of the [velocity field](@entry_id:271461). The direct dynamical impact of compressibility on the turbulence structure—such as energy transfer via compression—is negligible. In this regime, the primary effect of compressibility is on the *mean* flow properties (the "variable property" effect). The mean density, temperature, and viscosity vary throughout the flow, and these variations must be accounted for. However, the turbulence closure models themselves, which describe the Reynolds stresses and dissipation, can often be used without explicit [compressibility corrections](@entry_id:747585) ([@problem_id:3302796]). This is a powerful simplification, but one must always verify that the condition of small $M_t$ holds.

### New Physics in Compressible Turbulence

When $M_t$ becomes significant, Morkovin's hypothesis breaks down, and several new physical mechanisms, absent in incompressible flow, become important. To properly account for these, the mathematical framework of [turbulence modeling](@entry_id:151192) must be adapted.

#### Favre (Mass-Weighted) Averaging

The first adaptation is the use of **Favre (mass-weighted) averaging** for variable-density flows. In standard Reynolds averaging, a quantity $\phi$ is decomposed into a mean $\bar{\phi}$ and a fluctuation $\phi'$. Averaging the continuity equation, $\partial_t \rho + \nabla \cdot (\rho \mathbf{u}) = 0$, results in a mean equation containing the unclosed turbulent mass flux term, $\overline{\rho' \mathbf{u}'}$.

Favre averaging circumvents this issue. A quantity $\phi$ is decomposed into a Favre mean $\tilde{\phi} = \overline{\rho \phi} / \bar{\rho}$ and a Favre fluctuation $\phi'' = \phi - \tilde{\phi}$. A key property is that $\overline{\rho \phi''} = 0$. Applying this to the continuity equation yields $\partial_t \bar{\rho} + \nabla \cdot (\bar{\rho} \tilde{\mathbf{u}}) = 0$. This mean [continuity equation](@entry_id:145242) has the same form as the instantaneous one and contains no unclosed terms. This simplification propagates to the momentum and energy equations, making Favre averaging the standard choice for compressible RANS modeling ([@problem_id:3382029]).

#### New Terms in the Turbulent Kinetic Energy Budget

With Favre averaging, the [transport equation](@entry_id:174281) for [turbulent kinetic energy](@entry_id:262712), $k = \frac{1}{2} \widetilde{u_i'' u_i''}$, can be derived. Compared to its incompressible counterpart, the exact TKE budget reveals new terms that represent distinct physical processes ([@problem_id:3302807]). The simplified budget for a statistically stationary, homogeneous flow is:

$$
P_k = \bar{\rho} \epsilon + \Pi
$$

Here, $P_k = -\overline{\rho u_i'' u_j''} \partial_j \tilde{u}_i$ is the production rate, $\bar{\rho} \epsilon$ is the viscous dissipation rate, and $\Pi$ is the pressure-dilatation. The total dissipation rate $\epsilon$ itself is composed of two parts: $\epsilon = \epsilon_s + \epsilon_d$. The two new terms are thus **[dilatational dissipation](@entry_id:748437) ($\epsilon_d$)** and **pressure-dilatation ($\Pi$)**.

**Dilatational Dissipation, $\epsilon_d$**
This term represents the irreversible conversion of turbulent kinetic energy into internal energy (heat) by viscous stresses acting on compressive motions. Its [exact form](@entry_id:273346) is $\bar{\rho} \epsilon_d = \overline{\tau'_{ij} \partial_j u_i' |_d}$, where the subscript $d$ denotes the dilatational part. Because it is a dissipative process driven by viscosity, it is always a sink for TKE ($\epsilon_d \ge 0$) and contributes to [entropy production](@entry_id:141771).

**Pressure-Dilatation, $\Pi$**
This term, defined as $\Pi = \overline{p' (\nabla \cdot \mathbf{u}')}$, represents the rate of work done by fluctuating pressure on the fluctuating [volumetric strain rate](@entry_id:272471) (dilatation) of fluid parcels. It acts as an exchange mechanism between turbulent kinetic energy and internal energy. Unlike dissipation, this process is, in principle, reversible and does not directly generate entropy. Its sign depends on the correlation between pressure and dilatation fluctuations. In many flows, such as decaying or shear-driven turbulence, high pressure tends to be correlated with compression ($\nabla \cdot \mathbf{u}'  0$), making $\Pi$ a net sink for TKE.

A more rigorous view emerges from the [transport equation](@entry_id:174281) for the Favre-averaged Reynolds stress tensor, $R_{ij} = \overline{\rho u_i'' u_j''}$ ([@problem_id:3302830]). Here, the pressure-velocity correlation term is decomposed into a trace-free **pressure-strain tensor**, which redistributes TKE among its components, and its trace, which is precisely the pressure-dilatation. This highlights that pressure-dilatation is the compressible component of the pressure-strain interaction, directly affecting the total TKE budget.

### Modeling Strategies for Compressibility Corrections

Since $\epsilon_d$ and $\Pi$ are zero in incompressible flows, standard [turbulence models](@entry_id:190404) do not account for them. Compressibility corrections are essentially models for these new terms.

#### Models for Dilatational Dissipation and Pressure-Dilatation

There are two main philosophies for correcting [two-equation models](@entry_id:271436) like the $k-\epsilon$ model ([@problem_id:3302849]).

1.  **Sarkar-type Corrections**: This approach focuses on modeling the **pressure-dilatation** term, $\Pi$. The model, often derived from [asymptotic analysis](@entry_id:160416), typically takes the form $\Pi \propto M_t^2 P_k$ or $\Pi \propto M_t^2 \bar{\rho}\epsilon$. This modeled term is then added as an extra sink in the $k$-equation. This effectively reduces the net production of turbulence at high $M_t$ ([@problem_id:3382029]).

2.  **Zeman-type Corrections**: This approach focuses on modeling the **[dilatational dissipation](@entry_id:748437)**, $\epsilon_d$. The total dissipation is now $\epsilon = \epsilon_s + \epsilon_d$. A model is proposed for $\epsilon_d$, often incorporating a threshold $M_t$ for activation. The [transport equation](@entry_id:174281) for the dissipation rate ($\epsilon$-equation) is then modified to account for the production and destruction of this new compressible part of the dissipation. This increases the total dissipation at high $M_t$.

A common algebraic model for [dilatational dissipation](@entry_id:748437), based on the work of Sarkar, relates it directly to the solenoidal dissipation $\epsilon_s$ and the turbulent Mach number ([@problem_id:578323]):
$$
\epsilon_d = C_d M_t^2 \epsilon_s
$$
where $C_d$ is a model constant. This explicitly shows the $M_t^2$ scaling and provides a simple way to augment the total dissipation. Both the Sarkar and Zeman approaches are designed to reduce to the standard incompressible model as $M_t \to 0$ ([@problem_id:3302849]).

#### Implicit Corrections in Eddy-Viscosity Models

Beyond explicit source terms, compressibility effects can also appear implicitly through the [constitutive relation](@entry_id:268485) for the Reynolds stresses. In the Boussinesq eddy-viscosity model, the compressible form of the Reynolds stress tensor is:

$$
-\overline{\rho u_i'' u_j''} = 2 \mu_t \left( \tilde{S}_{ij} - \frac{1}{3} (\nabla \cdot \tilde{\mathbf{U}}) \delta_{ij} \right) - \frac{2}{3} \bar{\rho} k \delta_{ij}
$$

When this is substituted into the definition of TKE production, $P_k$, an additional term arises from the isotropic part of the stress tensor: $P_k^{\text{iso}} = -\frac{2}{3} \bar{\rho} k (\nabla \cdot \tilde{\mathbf{U}})$ ([@problem_id:3384740]). This term acts as a source of TKE in regions of mean compression ($\nabla \cdot \tilde{\mathbf{U}}  0$), such as across a shock wave, and a sink in regions of mean expansion ($\nabla \cdot \tilde{\mathbf{U}} > 0$), such as in a nozzle or a flow with strong heat release. This is a distinct physical effect tied to the mean flow dilatation and is automatically included when using a compressible eddy-viscosity formulation.

#### Corrections for Turbulent Heat and Scalar Transport

Compressibility also affects the transport of scalars like temperature. In many models, the [turbulent heat flux](@entry_id:151024) is modeled using a [gradient-diffusion hypothesis](@entry_id:156064) involving a turbulent thermal diffusivity, $\alpha_t$. The ratio of turbulent viscosity to [thermal diffusivity](@entry_id:144337) is the **turbulent Prandtl number**, $Pr_t = \nu_t / \alpha_t$.

While often assumed constant ($Pr_t \approx 0.85-0.9$) in incompressible flows, this assumption becomes questionable at high Mach numbers. The dilatational fluctuations that contribute to TKE dissipation can also enhance the mixing and decorrelation of scalar fluctuations. This suggests that the [thermal diffusivity](@entry_id:144337) $\alpha_t$ might be enhanced relative to the [momentum diffusivity](@entry_id:275614) $\nu_t$. A time-scale analysis suggests that the scalar decorrelation rate gains a dilatational contribution proportional to $M_t^2$. This leads to a model where the turbulent Prandtl number increases with the turbulent Mach number ([@problem_id:3302824]):

$$
Pr_t(M_t) = Pr_{t0} (1 + \beta M_t^2)
$$

where $Pr_{t0}$ is the incompressible value and $\beta$ is a model constant. Ignoring this effect can lead to errors in predicting wall heat transfer and temperature distributions in high-speed flows.

In summary, correcting [turbulence models](@entry_id:190404) for [compressibility](@entry_id:144559) is a multi-faceted task. It requires identifying the relevant physical parameter ($M_t$), understanding the new physical mechanisms that emerge at high $M_t$ (pressure-dilatation and [dilatational dissipation](@entry_id:748437)), and implementing physically-based models for these effects. These models, which typically scale with $M_t^2$, can be added as explicit corrections to the [transport equations](@entry_id:756133) or may arise implicitly from the fundamental closure assumptions, impacting not only [momentum transport](@entry_id:139628) but [scalar transport](@entry_id:150360) as well.