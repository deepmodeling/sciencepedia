## Introduction
Turbulent combustion, the engine of [power generation](@entry_id:146388) and propulsion systems, is governed by a complex interplay of fluid dynamics, chemical kinetics, and heat transfer. Accurately predicting these [reacting flows](@entry_id:1130631) is a central challenge in [computational combustion](@entry_id:1122776). While simpler turbulence models are widely used, they often fail to capture the highly anisotropic and non-equilibrium turbulence characteristic of practical combustors with strong swirl and density variations. This knowledge gap necessitates a more physically comprehensive approach. Reynolds Stress Transport Models (RSTMs) offer such a framework by directly solving for the transport of the individual Reynolds stresses, providing a higher-fidelity representation of [turbulence physics](@entry_id:756228).

This article serves as a comprehensive guide to understanding and applying RSTMs in combustion. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, exploring the derivation of the RSTM equations and the modeling of their unclosed terms. Following this, **Applications and Interdisciplinary Connections** will demonstrate how RSTM is used to analyze complex flame phenomena and wall-bounded flows, highlighting its connection to computational science. Finally, **Hands-On Practices** will offer practical exercises to reinforce these concepts. We begin by examining the fundamental principles that distinguish RSTMs from simpler closures.

## Principles and Mechanisms

The accurate prediction of turbulent reacting flows, which lie at the heart of [combustion science](@entry_id:187056), hinges on our ability to model the complex interplay between fluid motion, chemical reactions, and heat release. While simpler turbulence models provide valuable insights, they often fall short in flows characterized by strong anisotropy, swirl, and significant [body forces](@entry_id:174230)—all common features of practical combustors. Reynolds Stress Transport Models (RSTMs) represent a more advanced, physically grounded approach by abandoning the simplifying assumptions of [isotropic turbulence](@entry_id:199323) and instead solving transport equations for the individual components of the Reynolds stress tensor. This chapter delineates the fundamental principles and mechanisms that underpin the RSTM framework, with a particular focus on its application to variable-density reacting flows.

### From Reynolds Averaging to the Closure Problem

The foundation of most turbulence modeling lies in the decomposition of instantaneous flow quantities into mean and fluctuating components. The classical **Reynolds decomposition** for a velocity field $u_i(\mathbf{x}, t)$ is expressed as:

$u_i = \overline{u_i} + u_i'$

Here, $\overline{u_i}$ represents the [mean velocity](@entry_id:150038), obtained through an averaging process (e.g., ensemble or long-time averaging), and $u_i'$ is the turbulent fluctuation around that mean. A direct consequence of this definition is that the average of the fluctuation is zero, i.e., $\overline{u_i'} = 0$ . When this decomposition is applied to the nonlinear convective term $u_i u_j$ in the Navier-Stokes equations, and the result is averaged, a new term emerges:

$\overline{u_i u_j} = \overline{(\overline{u_i} + u_i')(\overline{u_j} + u_j')} = \overline{u_i}\overline{u_j} + \overline{u_i'u_j'}$

The term $\overline{u_i'u_j'}$ is the **kinematic Reynolds stress tensor**, often denoted $R_{ij}$. This [symmetric tensor](@entry_id:144567) ($R_{ij} = R_{ji}$) represents the average transport of momentum due to turbulent fluctuations. Physically, it acts as an additional stress on the mean flow. It possesses units of velocity squared ($[L^2]/[T^2]$), and its trace, $R_{kk} = \overline{u_k'u_k'}$, is equal to twice the [turbulent kinetic energy](@entry_id:262712) per unit mass, $k = \frac{1}{2}\overline{u_l'u_l'}$. The appearance of this unknown tensor in the averaged momentum equations gives rise to the fundamental **closure problem** of turbulence: the averaged equations contain more unknowns ($R_{ij}$) than equations.

It is crucial to distinguish the Reynolds stress tensor, a dynamical quantity representing turbulent [momentum flux](@entry_id:199796), from the **mean strain-rate tensor**, $S_{ij}$, a purely kinematic quantity describing the rate of deformation of the mean flow :

$S_{ij} = \frac{1}{2} \left( \frac{\partial \overline{u_i}}{\partial x_j} + \frac{\partial \overline{u_j}}{\partial x_i} \right)$

$S_{ij}$ has units of inverse time ($[1]/[T]$) and is dimensionally and conceptually distinct from $R_{ij}$. Turbulence models aim to provide a "closure," which is a model equation relating the unknown Reynolds stresses to the known mean flow quantities.

### The Challenge of Variable Density: Favre Averaging

In combustion, large heat release causes substantial variations in fluid density, $\rho$. Applying standard Reynolds averaging to the governing equations in this context introduces a plethora of new, complex correlation terms involving density fluctuations (e.g., $\overline{\rho'u_i'}$, $\overline{\rho'u_i'u_j'}$) . This hopelessly complicates the closure problem.

To circumvent this, **Favre (or density-weighted) averaging** is almost universally employed. A quantity $\phi$ is decomposed as $\phi = \tilde{\phi} + \phi''$, where the Favre average is $\tilde{\phi} = \overline{\rho \phi} / \overline{\rho}$ and $\phi''$ is the Favre fluctuation. The key property of this decomposition is that the density-weighted average of the fluctuation is zero, $\overline{\rho \phi''} = 0$, though the unweighted average $\overline{\phi''}$ is generally non-zero.

The principal advantage of Favre averaging is the simplification of the mean [conservation equations](@entry_id:1122898). For instance, the mean convective momentum flux becomes :

$\overline{\rho u_i u_j} = \overline{\rho} \tilde{u}_i \tilde{u}_j + \overline{\rho u_i'' u_j''}$

This form is structurally analogous to the constant-density case, with the unclosed term now being the **Favre-averaged Reynolds stress tensor**, $\overline{\rho u_i'' u_j''}$. This simplification makes the development of tractable closure models feasible. In the limit of constant density, $\rho' = 0$, Favre and Reynolds averages become identical ($\tilde{\phi} = \overline{\phi}$), and the corresponding stress tensors are directly related ($\overline{\rho u_i'' u_j''} = \rho \overline{u_i' u_j'}$) . Throughout the remainder of this chapter, we will primarily consider the Favre-averaged framework, denoting the Favre Reynolds stress per unit mass as $\tilde{R}_{ij} = \widetilde{u_i'' u_j''} = \overline{\rho u_i'' u_j''} / \overline{\rho}$.

### Limitations of Eddy-Viscosity Models and the Motivation for RSTM

The most common approach to closing the RANS equations is to invoke the **Boussinesq hypothesis**. This hypothesis postulates a linear analogy between the turbulent stresses and the mean strain, modeling the anisotropic part of the Reynolds stress tensor as being proportional to the mean strain-rate tensor :

$\tilde{R}_{ij} - \frac{2}{3}k\delta_{ij} = -2\nu_t \left( \tilde{S}_{ij} - \frac{1}{3}\tilde{S}_{kk}\delta_{ij} \right)$

Here, $\nu_t$ is the turbulent "eddy" viscosity, which itself must be modeled (e.g., using the $k$-$\epsilon$ model). While computationally efficient, this [linear eddy-viscosity model](@entry_id:751307) (LEVM) has severe structural limitations. Because the [deviatoric stress tensor](@entry_id:267642) is assumed to be linearly proportional to the deviatoric strain-rate tensor, the model enforces that their principal axes must be aligned. However, experiments and direct numerical simulations (DNS) of complex flows, particularly combusting shear layers, show significant **stress-strain misalignment**. Furthermore, in a simple shear flow, the Boussinesq hypothesis incorrectly predicts that the normal stresses are equal, failing to capture the strong **anisotropy** that is physically present.

Reynolds Stress Transport Models (RSTMs) provide a direct remedy to these failings. Instead of postulating an algebraic stress-strain relationship, RSTMs solve a separate transport equation for each of the six unique components of the Reynolds stress tensor, $\tilde{R}_{ij}$. By doing so, they can naturally account for the complex physics that generate [turbulence anisotropy](@entry_id:756224) and non-equilibrium effects, making them far more suitable for the challenging conditions encountered in combustion .

### The Reynolds Stress Transport Equation (RSTE)

The exact transport equation for the Reynolds stress tensor is derived by taking the momentum equation for the velocity fluctuation $u_i'$, multiplying by $u_j'$, adding the symmetric counterpart, and averaging. The resulting equation can be written schematically as:

$\frac{D \tilde{R}_{ij}}{Dt} = \mathcal{P}_{ij} + \Phi_{ij} - \mathcal{E}_{ij} + \mathcal{D}_{ij} + \text{other terms}$

Here, $\frac{D}{Dt} = \frac{\partial}{\partial t} + \tilde{u}_k \frac{\partial}{\partial x_k}$ is the [material derivative](@entry_id:266939) following the mean flow. Each term on the right-hand side represents a distinct physical process that acts as a source or sink for the Reynolds stresses . Let us examine the key terms in their Favre-averaged form, which are central to RSTM development.

#### Production by Mean Shear ($P_{ij}$)
The production tensor, typically denoted by its density-multiplied form in the RSTE for $\overline{\rho}\tilde{R}_{ij}$, represents the rate at which kinetic energy is extracted from the mean flow and converted into turbulent fluctuations. It arises from the interaction of the Reynolds stresses with the mean [velocity gradient](@entry_id:261686). This term is exact and does not require modeling:

$P_{ij} = -\overline{\rho}\left(\tilde{R}_{ik} \frac{\partial \tilde{u}_j}{\partial x_k} + \tilde{R}_{jk} \frac{\partial \tilde{u}_i}{\partial x_k}\right)$

The structure of this term is the primary source of anisotropy in turbulence. For instance, in a [simple shear flow](@entry_id:1131665), it generates the streamwise normal stress component but not the others, directly driving the turbulence away from an isotropic state .

#### Dissipation ($\varepsilon_{ij}$)
The dissipation tensor represents the destruction of Reynolds stresses due to viscous action, which converts [turbulent kinetic energy](@entry_id:262712) into internal energy (heat). For a constant-viscosity flow, it is defined as:

$\varepsilon_{ij} = 2\nu \overline{ \frac{\partial u_i'}{\partial x_k} \frac{\partial u_j'}{\partial x_k} }$

This term involves correlations of small-scale velocity gradients and is therefore **unclosed**. A widely used modeling assumption, justified by Kolmogorov's theory of local isotropy at high Reynolds numbers, is that the small-scale dissipative motions are isotropic. This allows the dissipation tensor to be modeled as :

$\varepsilon_{ij} \approx \frac{2}{3} \varepsilon \delta_{ij}$

where $\varepsilon$ is the [scalar dissipation](@entry_id:1131248) rate of TKE. This approximation is valid far from walls and in regions where the small-scale turbulence is not significantly perturbed by effects like strong shear or heat release.

#### Pressure-Strain and Pressure-Dilatation ($\Phi_{ij}$)
The [pressure-strain correlation](@entry_id:753711) tensor, $\Phi_{ij} = \overline{p'(\partial_j u_i'' + \partial_i u_j'')}$, is arguably the most complex and critical term in the RSTE. It arises from correlations between fluctuating pressure and fluctuating velocity gradients. This term is unclosed and models for it are central to the performance of any RSTM. Its physical role is twofold, especially in the context of combustion .

The tensor can be decomposed into a trace-free (deviatoric) part, $\phi_{ij}$, and a trace (isotropic) part:
$\Phi_{ij} = \phi_{ij} + \frac{1}{3}\Phi_{kk}\delta_{ij}$

1.  **Redistribution**: The deviatoric part, $\phi_{ij}$, is the **pressure-strain redistribution tensor**. It does not create or destroy total TKE (its trace is zero by definition), but it shuffles energy among the normal stress components ($R_{11}, R_{22}, R_{33}$). It is the mechanism that counters the anisotropy generated by the production term, tending to drive the turbulence towards an isotropic state. This is the key physical process that is missing from LEVMs . Modeling this term is essential for correctly predicting anisotropic stresses. A classic approach is the **linear [return-to-isotropy](@entry_id:754321) model** (Rotta model) for the "slow" part of this term, which assumes the rate of redistribution is proportional to the current anisotropy :
    $\phi_{ij}^{(\text{slow})} \propto - \frac{\varepsilon}{k} (\tilde{R}_{ij} - \frac{2}{3}k\delta_{ij})$

2.  **Dilatational Effects**: The trace of the tensor, $\Phi_{kk} = 2\overline{p'(\partial_k u_k'')}$, is directly related to the **pressure-dilatation** correlation. In an incompressible flow, the velocity field is divergence-free, so $\Phi_{kk}=0$. In [compressible flows](@entry_id:747589), however, $\Phi_{kk}$ is non-zero and represents a source or sink of TKE through the work done by pressure fluctuations on dilating fluid elements. In low-Mach-number combustion, even without significant acoustic effects, the strong [thermal expansion](@entry_id:137427) due to heat release creates large velocity divergence fluctuations ($\theta'' = \partial_k u_k''$). This makes the pressure-dilatation correlation a [dominant term](@entry_id:167418) in the TKE budget, often acting as a major source of [turbulence production](@entry_id:189980) [@problem_id:4058927, @problem_id:4058938]. A model for $\Phi_{ij}$ in reacting flows must therefore account for both redistribution and these critical dilatational effects.

#### Turbulent and Diffusive Transport
The RSTE also contains terms representing the spatial transport of Reynolds stresses by velocity fluctuations (turbulent transport, e.g., $-\partial_k \overline{\rho u_i''u_j''u_k''}$) and by molecular and pressure effects (diffusion). These terms are also unclosed and are typically modeled using a [gradient-diffusion hypothesis](@entry_id:156064), assuming that the stresses are transported down their own gradients .

### Practical Implementation: The Realizability Constraint

A critical requirement for any [turbulence model](@entry_id:203176) is **[realizability](@entry_id:193701)**. This mathematical constraint demands that the model must not predict physically impossible states. For the Reynolds stress tensor, this means it must remain positive semi-definite at all times. This implies, among other things, that the [normal stresses](@entry_id:260622) must be non-negative ($R_{ii} \ge 0$) and that the shear stresses must satisfy the Schwarz inequality ($R_{ij}^2 \le R_{ii}R_{jj}$).

In the intense and complex environment of a combustor, standard RSTM closures can sometimes violate this condition. For example, a strong negative production term $P_{22}$ (which can occur in regions of rapid expansion) might drive the corresponding [normal stress](@entry_id:184326) $R_{22}$ towards a negative value over a computational time step. To prevent this, [realizability constraints](@entry_id:1130703) are enforced within the numerical implementation. A common strategy involves modifying the model coefficients on-the-fly. For instance, if a time step update predicts $R_{22}^{n+1}  0$, the coefficient of the rapid pressure-strain term, $C_r$, can be dynamically increased to counteract the unphysical tendency and ensure that $R_{22}^{n+1}$ is clipped at or above zero . This ensures the mathematical and physical integrity of the simulation, a necessary step for robustly applying RSTMs to challenging combustion problems.