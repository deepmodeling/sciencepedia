## Introduction
The performance, lifespan, and safety of modern batteries are critically dependent on the complex and dynamic evolution of electrode microstructures. Uncontrolled morphological changes, such as the growth of [lithium dendrites](@entry_id:159084), can lead to capacity loss, short circuits, and catastrophic failure. Predicting and controlling these phenomena requires a modeling tool capable of capturing the intricate interplay between thermodynamics, chemical reactions, and [mass transport](@entry_id:151908) across evolving interfaces. Traditional modeling approaches that explicitly track sharp boundaries often face insurmountable computational challenges, creating a significant gap in our ability to design more reliable energy storage systems.

This article introduces [phase-field modeling](@entry_id:169811), a powerful continuum framework that elegantly overcomes these challenges. Instead of tracking sharp interfaces, this method describes the entire multiphase system using continuous fields, with their evolution governed by fundamental thermodynamic principles. Over the course of three chapters, you will gain a deep understanding of this versatile technique. The first chapter, **Principles and Mechanisms**, will lay the thermodynamic foundation, deriving the core Allen-Cahn and Cahn-Hilliard equations from a [free energy functional](@entry_id:184428) and explaining how they capture phenomena like nucleation and [anisotropic growth](@entry_id:153833). The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how to apply these principles to concrete material systems, coupling them with electrochemistry and transport phenomena to model complex processes like SEI formation and integrate them into multiscale design workflows. Finally, **Hands-On Practices** will provide opportunities to apply these theoretical concepts to solve practical problems in electrochemistry and stability analysis. We begin by exploring the fundamental principles that form the cornerstone of the phase-field method.

## Principles and Mechanisms

Phase-field models provide a powerful and versatile continuum framework for simulating the complex evolution of [electrode morphology](@entry_id:1124286). Bypassing the computational challenges of explicitly tracking sharp interfaces, these models represent the distinct phases (e.g., solid electrode and liquid electrolyte) and the boundaries between them using one or more continuous [scalar fields](@entry_id:151443) known as **order parameters**. The dynamics of these fields, and thus the evolution of the entire microstructure, are governed by a unified set of partial differential equations derived from the principles of non-equilibrium thermodynamics. This chapter elucidates the fundamental principles and mechanisms underpinning this approach, from the construction of the free energy functional to the derivation of the governing equations of motion and their application to electrochemical phenomena such as deposition, nucleation, and [dendritic growth](@entry_id:155385).

### The Free Energy Functional: The Thermodynamic Foundation

The cornerstone of any phase-field model is the **[free energy functional](@entry_id:184428)**, a mathematical expression that assigns a total free energy, $F$, to any given state of the system described by its fields. For a two-phase system, such as a lithium metal electrode in an electrolyte, the state can be described by an order parameter field, $\phi(\mathbf{x}, t)$, and a concentration field, $c(\mathbf{x}, t)$, representing the concentration of mobile ions. The total free energy is the [volume integral](@entry_id:265381) of a local free energy density, $f$, over the entire domain $\Omega$:

$F[\phi, c] = \int_{\Omega} f(\phi, c, \nabla\phi, \nabla c) \, dV$

This functional is not arbitrary; its components are carefully constructed to represent the essential physics of the multiphase system. A common form for the free energy density in electrochemical systems is a sum of three principal contributions :

$f(\phi, c, \nabla\phi) = W(\phi) + \frac{\kappa}{2}|\nabla\phi|^2 + f_{\text{chem}}(c, \phi)$

Each term has a distinct physical role in defining the thermodynamic landscape of the system.

#### The Order Parameter and the Double-Well Potential

The **order parameter**, $\phi$, serves to distinguish the phases. By convention, it takes on distinct constant values in the bulk of each phase. For instance, in modeling lithium [electrodeposition](@entry_id:160510), we might set $\phi=1$ to represent the solid metallic lithium phase and $\phi=0$ (or $\phi=-1$) for the liquid electrolyte phase. In the narrow region of the interface, $\phi$ varies smoothly between these values.

The thermodynamic stability of these bulk phases is enforced by the **local free energy density** or **double-well potential**, $W(\phi)$. This function is constructed to have local minima at the values of $\phi$ corresponding to the bulk phases. A mathematically simple and widely used form is the symmetric double-well potential :

$W(\phi) = \frac{\lambda}{4}(\phi^2 - 1)^2$

Here, $\lambda > 0$ is a parameter that controls the height of the energy barrier between the wells. The minima of this potential occur at $\phi = +1$ and $\phi = -1$, defining the two equilibrium bulk phases. Any value of $\phi$ between $-1$ and $+1$ corresponds to a higher local energy, which is characteristic of an interfacial region.

#### The Gradient Energy and the Diffuse Interface

While the double-well potential defines the bulk phases, it does not, on its own, prevent the formation of infinitely sharp interfaces, which are physically unrealistic. The **[gradient energy](@entry_id:1125718) term**, $\frac{\kappa}{2}|\nabla\phi|^2$, resolves this by adding an energy penalty proportional to the square of the gradient of the order parameter. The coefficient $\kappa > 0$ is the **gradient energy coefficient**. Because this term increases the system's energy wherever $\phi$ changes rapidly, it energetically favors gradual transitions between phases. The competition between the double-well potential, which favors pure phases, and the gradient energy, which penalizes sharp transitions, results in the formation of a **diffuse interface** with a finite, characteristic thickness and a positive [interfacial free energy](@entry_id:183036), or surface tension.

#### Deriving Macroscopic Properties: Interfacial Profile, Width, and Energy

The interplay between $W(\phi)$ and the gradient energy gives rise to macroscopic interfacial properties. We can derive these by analyzing the equilibrium structure of a one-dimensional planar interface. The equilibrium profile, $\phi(x)$, is the one that minimizes the total free energy functional. Using the calculus of variations, this minimizing profile is found to satisfy the Euler-Lagrange equation. For the [free energy functional](@entry_id:184428) with the potentials described above, the solution for an interface centered at $x=0$ is a hyperbolic tangent function :

$\phi(x) = \tanh\left(x \sqrt{\frac{\lambda}{2\kappa}}\right)$

This explicit solution reveals how the model's microscopic parameters, $\kappa$ and $\lambda$, determine macroscopic features. The **interface width**, $l$, can be defined from the characteristic length scale in the argument of the $\tanh$ function, which shows that it scales as:

$l \propto \sqrt{\frac{\kappa}{\lambda}}$

This relationship provides physical intuition: the interface becomes wider as the penalty for gradients ($\kappa$) increases, and narrower as the energy barrier between the bulk phases ($\lambda$) increases.

Furthermore, the excess free energy associated with this interface, known as the **interfacial energy**, $\gamma$, can be calculated by integrating the free energy density of the equilibrium profile. This calculation yields a direct relationship between the macroscopic surface tension and the phase-field parameters :

$\gamma = \int_{-\infty}^{\infty} \left[ W(\phi(x)) + \frac{\kappa}{2}\left(\frac{d\phi}{dx}\right)^2 \right] dx = \frac{2\sqrt{2}}{3}\sqrt{\kappa\lambda}$
(Note: The solution from  of $\frac{4}{3}\sqrt{\kappa\lambda}$ is based on a different free energy form $\kappa(\partial_x\phi)^2+W(\phi)$ instead of $\frac{\kappa}{2}(\partial_x\phi)^2+W(\phi)$. For the latter form used here, the result is $\frac{2\sqrt{2}}{3}\sqrt{\kappa\lambda}$.)

This ability to relate fundamental model parameters to measurable thermodynamic properties is a key strength of the phase-field method.

#### The Chemical Free Energy

The final component, $f_{\text{chem}}(c, \phi)$, couples the order parameter to the concentration of the mobile species, $c$. This term describes how the chemical free energy depends on both composition and phase. For example, the equilibrium concentration and activity of lithium ions are different in the electrolyte versus the solid electrode. A common model for the chemical free energy density of a [binary mixture](@entry_id:174561) is the **[regular solution model](@entry_id:138095)**, which includes both an ideal entropy of mixing and an enthalpic interaction term :

$f_{\text{chem}}(c) = RT\left[c\ln(c) + (1-c)\ln(1-c)\right] + \Omega c(1-c)$

Here, $R$ is the gas constant, $T$ is temperature, and $\Omega$ is the [interaction parameter](@entry_id:195108). The driving force for diffusion is the **chemical potential**, $\mu_c$, which is derived from this free energy density:

$\mu_c = \frac{\partial f_{\text{chem}}}{\partial c} = RT\ln\left(\frac{c}{1-c}\right) + \Omega(1-2c)$

This chemical potential is a crucial input for the dynamic equations that govern mass transport in the system.

### Equations of Motion: From Thermodynamics to Dynamics

A system not in equilibrium will evolve over time to reduce its total free energy. The [phase-field method](@entry_id:191689) models this evolution using thermodynamically consistent equations of motion. The mathematical form of these equations depends critically on whether the field variable represents a conserved or a non-conserved quantity .

#### Non-Conserved Dynamics: The Allen-Cahn Equation

An order parameter $\phi$ that describes a phase transformation (e.g., solidification) is typically a **non-conserved** quantity. The transformation from liquid to solid is a local change of state; the "amount" of solid, $\int \phi \, dV$, is not conserved but is created from the liquid phase. The evolution of a [non-conserved order parameter](@entry_id:1128777) is described by the **Allen-Cahn equation** (also known as the time-dependent Ginzburg-Landau equation):

$\frac{\partial \phi}{\partial t} = -L_{\phi} \frac{\delta F}{\delta \phi}$

Here, $L_{\phi}$ is a positive kinetic coefficient or mobility that sets the timescale of the relaxation, and $\frac{\delta F}{\delta \phi}$ is the variational derivative of the [free energy functional](@entry_id:184428) with respect to $\phi$. This derivative represents the thermodynamic driving force. The equation dictates that $\phi$ evolves locally to decrease the free energy, describing processes like [interface motion](@entry_id:1126592) and coarsening driven by curvature reduction.

#### Conserved Dynamics: The Cahn-Hilliard Equation

In contrast, the concentration $c$ of a chemical species is a **conserved** quantity. The total amount of the species in a closed system, $\int c \, dV$, can only change via fluxes across the system's boundaries. Its local evolution must obey a continuity equation:

$\frac{\partial c}{\partial t} = -\nabla \cdot \mathbf{J}_c$

where $\mathbf{J}_c$ is the flux of the species. In the context of phase-field models, this flux is driven by gradients in the chemical potential, $\mu_c = \delta F / \delta c$. The resulting evolution equation is the **Cahn-Hilliard equation**:

$\frac{\partial c}{\partial t} = \nabla \cdot \left( M_c \nabla \mu_c \right) = \nabla \cdot \left( M_c \nabla \frac{\delta F}{\delta c} \right)$

where $M_c$ is a mobility coefficient. This equation describes processes like [spinodal decomposition](@entry_id:144859) and diffusion, where matter is redistributed within the domain to lower the total free energy.

#### Model Selection and Interpretation

The distinction between Allen-Cahn and Cahn-Hilliard dynamics is fundamental . Applying Allen-Cahn dynamics to a field describes local relaxation or reaction, making it suitable for reaction-limited processes. Applying Cahn-Hilliard dynamics describes long-range transport and redistribution, making it the natural choice for diffusion-limited processes. The two models predict fundamentally different late-stage [coarsening dynamics](@entry_id:1122587): Allen-Cahn [coarsening](@entry_id:137440) typically scales with time as $t^{1/2}$, while Cahn-Hilliard coarsening scales as $t^{1/3}$. Using a non-conserved Allen-Cahn model for a process that is physically governed by conserved [mass transport](@entry_id:151908) (e.g., [diffusion-limited growth](@entry_id:1123701)) can lead to unphysical results, such as over-predicting dendrite tip velocities, because it neglects the long-range constraints imposed by diffusion .

### Modeling Electrochemical Phenomena

To model [electrodeposition](@entry_id:160510), we must couple the phase change at the electrode-electrolyte interface with the transport and consumption of ions. This is achieved by combining the Allen-Cahn and Cahn-Hilliard frameworks and introducing a reaction term that links them via electrochemical principles.

#### Coupling Phase, Concentration, and Electrochemistry

In a typical model for lithium plating, the phase field $\phi$ (solid/liquid) is treated as non-conserved, while the lithium ion concentration $c$ is treated as conserved. The electrochemical reaction at the interface consumes ions from the electrolyte (decreasing $c$) to create the solid phase (increasing $\phi$). This coupling is accomplished by adding a **reaction source/sink term**, $S_{rxn}$, to both [evolution equations](@entry_id:268137)  :

$\frac{\partial \phi}{\partial t} = -L_{\phi} \frac{\delta F}{\delta \phi} + S_{rxn}$

$\frac{\partial c}{\partial t} = \nabla \cdot \left( M_c \nabla \mu_c \right) - S_{rxn}$

The source term $S_{rxn}$ is non-zero only in the interfacial region and represents the local volumetric rate of the [phase transformation](@entry_id:146960).

#### The Reaction Source Term and Butler-Volmer Kinetics

The magnitude of the reaction term $S_{rxn}$ is not arbitrary; it is determined by the local [electrochemical kinetics](@entry_id:155032) and is directly proportional to the local **Faradaic current density**, $j$, via Faraday's law. For a monovalent species like lithium ($z=1$), the relationship is:

$S_{rxn} = \frac{j}{F}$

where $F$ is the Faraday constant. The current density $j$ itself is a function of the local conditions at the interface, most importantly the **overpotential**, $\eta$, which is the deviation of the [electrode potential](@entry_id:158928) from its equilibrium value. The relationship between current density and overpotential is often described by the **Butler-Volmer equation** :

$j = j_0 \left[ \exp\left(\frac{\alpha_a F \eta}{RT}\right) - \exp\left(-\frac{\alpha_c F \eta}{RT}\right) \right]$

where $j_0$ is the exchange current density and $\alpha_a, \alpha_c$ are transfer coefficients. By combining these equations, the phase-field model directly links the thermodynamic driving forces for [morphology](@entry_id:273085) evolution to the applied electrochemical conditions (e.g., applied current or voltage) that determine the overpotential.

#### Nucleation and the Role of Driving Force

Phase-field models can also capture kinetically limited phenomena like nucleation. The thermodynamic driving force for creating a new phase, $\Delta g$, can be incorporated into the free energy by adding a "tilting" term. For a symmetric double-well potential, this can be a simple linear term, $-h\phi$, where $h$ is proportional to the driving force . This term breaks the symmetry of the potential, making one phase (e.g., $\phi=+1$) energetically more favorable than the other ($\phi=-1$). The bulk free energy difference becomes $\Delta g = f_{bulk}(-1) - f_{bulk}(+1) = 2h$.

Remarkably, the phase-field framework can quantitatively reproduce results from [classical nucleation theory](@entry_id:147866). The classical nucleation barrier, $\Delta G_c$, for forming a spherical nucleus is given by:

$\Delta G_c = \frac{16\pi\gamma^3}{3(\Delta g)^2}$

By substituting the expressions for the [interfacial energy](@entry_id:198323) $\gamma$ and the driving force $\Delta g$ derived from the phase-field parameters ($\kappa, \lambda, h$), we can express this classical thermodynamic barrier entirely in terms of the underlying [phase-field model](@entry_id:178606) parameters. This demonstrates the model's capacity to bridge microscopic parameters and macroscopic kinetic events .

### Advanced Topic: Incorporating Anisotropy

Real [crystalline materials](@entry_id:157810) exhibit anisotropy, meaning their properties depend on direction. This is crucial for correctly predicting morphological features like dendrites, which have distinct crystallographic orientations.

#### Anisotropic Interfacial Energy

The primary source of anisotropy in many crystal growth phenomena is the [interfacial energy](@entry_id:198323). In the phase-field model, this is elegantly incorporated by promoting the scalar [gradient energy](@entry_id:1125718) coefficient $\kappa$ to a second-order tensor, $\kappa_{ij}$ . The gradient energy term becomes:

$f_{\text{grad}} = \frac{1}{2} (\partial_i \phi) \kappa_{ij} (\partial_j \phi)$

With this modification, the interfacial energy $\gamma$ is no longer a constant but depends on the orientation of the interface, given by its [unit normal vector](@entry_id:178851) $\mathbf{n}$. The orientation-dependent interfacial energy can be shown to scale as:

$\gamma(\mathbf{n}) \propto \sqrt{n_i \kappa_{ij} n_j}$

#### Anisotropy and Morphological Selection

This anisotropy in [interfacial energy](@entry_id:198323) has profound consequences for [morphology](@entry_id:273085) evolution. During [diffusion-limited growth](@entry_id:1123701), an initially flat interface is unstable to perturbations (the Mullins-Sekerka instability). However, the [interfacial energy](@entry_id:198323) provides a stabilizing effect (the Gibbs-Thomson effect), which penalizes the formation of highly curved regions. The strength of this "capillary stabilization" is proportional to the [interfacial energy](@entry_id:198323).

In an anisotropic system, [dendritic growth](@entry_id:155385) proceeds fastest in the directions where this capillary stabilization is weakest. Since $\gamma(\mathbf{n})$ is smallest for the directions $\mathbf{n}$ that minimize the quadratic form $n_i \kappa_{ij} n_j$, these become the preferred growth directions for the dendrite tips. The resulting [morphology](@entry_id:273085), with its characteristic arms and branches, is a direct reflection of the underlying [crystallographic anisotropy](@entry_id:1123263) encoded in the tensor $\kappa_{ij}$ . This illustrates how the phase-field method can capture the intricate relationship between atomic-scale crystal structure and macroscopic [morphology](@entry_id:273085) in a computationally tractable manner.