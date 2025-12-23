## Introduction
Advanced [phase-field models](@entry_id:202885) are a powerful computational tool for simulating the intricate evolution of microstructures in materials. Their ability to handle complex geometries and multi-physics interactions makes them indispensable for understanding and designing next-generation materials, particularly compositionally complex systems like high-entropy alloys (HEAs). However, accurately capturing the interplay between chemistry, [phase transformations](@entry_id:200819), and mechanical stress in multicomponent, multiphase alloys presents a significant theoretical challenge. This article provides a comprehensive framework to bridge this gap, detailing how to construct and apply physically rigorous, chemo-mechanically coupled [phase-field models](@entry_id:202885).

Across three chapters, you will gain a deep, graduate-level understanding of this framework. The "Principles and Mechanisms" chapter will lay out the thermodynamic and kinetic foundations, from constructing free-energy functionals to deriving the governing Allen-Cahn and Cahn-Hilliard equations. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate the model's predictive power in the context of HEAs and explore its integration with solid mechanics, plasticity, and electrochemistry. Finally, a series of "Hands-On Practices" will provide opportunities to engage with the core theoretical and computational concepts. This journey begins with a deep dive into the fundamental principles that form the bedrock of advanced materials simulation.

## Principles and Mechanisms

Phase-field models offer a powerful and versatile framework for simulating microstructural evolution in complex materials by describing the system's state through a set of continuous field variables. The dynamics of these fields are governed by a total free-energy functional, which acts as a thermodynamic potential, and a set of kinetic equations consistent with the principles of [irreversible thermodynamics](@entry_id:142664). This chapter elucidates the fundamental principles and mechanisms underlying advanced, chemo-mechanically coupled, multi-phase phase-field models, with a particular focus on their application to high-entropy alloys (HEAs).

### The Thermodynamic Foundation: The Free-Energy Functional

At the heart of any phase-field model lies the **free-energy functional**, typically a Helmholtz-type energy $F$, which maps the state of the system—defined by its composition, phase distribution, and mechanical state—to a scalar value. The system evolves in a manner that continuously decreases this total free energy, seeking a state of [thermodynamic equilibrium](@entry_id:141660). The functional is constructed as an integral of a local free-energy density, $f$, over the entire domain $\Omega$:

$F = \int_{\Omega} f(\{c_{\alpha}\}, \{\phi_{i}\}, \boldsymbol{\varepsilon}, \nabla c_{\alpha}, \nabla \phi_{i}, T) \, \mathrm{d}V$

The density $f$ is a [composite function](@entry_id:151451), encapsulating the various contributions to the system's energy. A typical construction includes chemical, interfacial, and mechanical contributions .

#### Bulk Chemical Free Energy

The **bulk chemical free-energy density**, $f_{\mathrm{chem}}(\{c_{\alpha}\}, \{\phi_{i}\}, T)$, represents the free energy of a hypothetical homogeneous material point with local composition $\{c_{\alpha}\}$ and phase fractions $\{\phi_i\}$ at a given temperature $T$. Its dependence on temperature is fundamental, accounting for all entropic effects, most notably the [configurational entropy](@entry_id:147820) of mixing, which is a defining characteristic of HEAs. This term is constructed by interpolating the free-energy densities of the individual, constituent phases, denoted $f_i(\{c_{\alpha}\})$. For a multiphase system, a common approach is to write:

$f_{\mathrm{chem}} = \sum_{i=1}^{N} h_i(\{\phi_j\}) f_i(\{c_{\alpha}\}) + W g(\{\phi_j\})$

Here, $h_i(\{\phi_j\})$ are **interpolation functions** that transition smoothly between phases, and $W g(\{\phi_j\})$ is a **multi-well potential** that penalizes mixed-phase states, thus creating an energetic preference for pure phases. The precise form of these functions is critical and will be detailed in a subsequent section .

#### Gradient Energy and the Diffuse Interface

A defining feature of [phase-field models](@entry_id:202885) is the representation of interfaces not as sharp, zero-thickness boundaries, but as diffuse regions of finite width over which field variables change smoothly. This is achieved by introducing **[gradient energy](@entry_id:1125718) terms** into the functional. These terms penalize spatial variations in the field variables:

$f_{\mathrm{grad}} = \sum_{i=1}^{N} \frac{\kappa_{\phi,i}}{2} |\nabla \phi_i|^2 + \sum_{\alpha=1}^{M} \frac{\kappa_{c,\alpha}}{2} |\nabla c_\alpha|^2$

The positive coefficients $\kappa_{\phi,i}$ and $\kappa_{c,\alpha}$ are known as **[gradient energy](@entry_id:1125718) coefficients**. The inclusion of these terms, which represent the energetic cost of creating gradients, ensures that the free energy of an infinitely sharp interface would be infinite, thus regularizing the problem and leading to a diffuse interface with a characteristic thickness and a finite [interfacial energy](@entry_id:198323) .

The properties of the interface are determined by the competition between the bulk potential, which seeks to separate the domain into pure phases, and the gradient energy, which opposes sharp changes. For a simple one-dimensional planar interface between two phases ($\alpha$ and $\beta$), this relationship can be quantified analytically. Let's consider an effective two-phase system described by a single order parameter $\phi$ (where $\phi=1$ in phase $\alpha$ and $\phi=0$ in phase $\beta$) and a simplified free-energy density containing only the essential interfacial terms: $f = A \phi^2 (1-\phi)^2 + \frac{\kappa_g}{2} |\nabla \phi|^2$. Here, $A$ represents the height parameter of the double-well potential, and $\kappa_g$ is the effective gradient coefficient across the interface. By minimizing the total [free energy functional](@entry_id:184428), we can solve for the equilibrium interface profile and derive expressions for the interfacial energy per unit area, $\gamma$, and the interface width, $W$. The equilibrium condition dictates an equipartition between the potential and gradient energy contributions, leading to the results :

$\gamma = \frac{\sqrt{A \kappa_g}}{6}$

$W \sim \sqrt{\frac{\kappa_g}{A}}$

These relationships are fundamental, as they connect the abstract parameters of the phase-field model ($A$, $\kappa_g$) to measurable physical properties of the interface ($\gamma$, $W$).

### Order Parameters: Describing the Material State

The power of phase-field models lies in their ability to describe complex microstructures using a variety of continuous fields, or **order parameters**. It is crucial to distinguish between the different types of order parameters based on the physical quantities they represent and whether those quantities are conserved.

#### Phase Fields as Non-Conserved Phase Indicators

A **phase field**, $\phi_i(\mathbf{x}, t)$, is a [non-conserved order parameter](@entry_id:1128777) that identifies the presence and volume fraction of a particular phase at a point in space and time. For a system with $N$ phases, we typically employ a set of phase fields $\{\phi_i\}_{i=1}^N$ subject to the constraints $\phi_i \ge 0$ and $\sum_{i=1}^N \phi_i = 1$. In this construction, the pure phase $k$ corresponds to the state $\phi_k = 1$ and $\phi_{j\neq k}=0$. Regions where $0 \lt \phi_i \lt 1$ represent diffuse interfaces.

In the so-called [sharp-interface limit](@entry_id:1131545), achieved by taking the interface thickness parameter $\varepsilon$ to zero in a potential of the form $\frac{1}{\varepsilon}W(\phi) + \varepsilon |\nabla \phi|^2$, the [minimizers](@entry_id:897258) of the free energy converge to fields where $\phi_i$ takes a value of either 0 or 1 almost everywhere. The domain $\Omega$ is partitioned into disjoint regions $\Omega_i$, and $\phi_i$ becomes the characteristic (or indicator) function for the region occupied by phase $i$. In this limit, the volume of phase $i$ is precisely $\int_\Omega \phi_i \, \mathrm{d}V$ .

It is essential to distinguish these phase-indicating fields from **structural order parameters**, which describe variations of properties *within* a single phase. Examples include an orientation field $\mathbf{Q}(\mathbf{x}) \in SO(3)$ representing the local crystal lattice orientation in a polycrystalline solid, or a [scalar field](@entry_id:154310) $\eta(\mathbf{x})$ describing the degree of long-range [chemical order](@entry_id:260645) in an [order-disorder transition](@entry_id:140999). Unlike phase fields, these parameters are not subject to a sum-to-one constraint and can vary smoothly inside a region where a single phase field $\phi_i$ is equal to 1 .

#### Composition Fields as Conserved Quantities

In contrast to phase fields, **composition fields**, $c_\alpha(\mathbf{x}, t)$, represent the [local concentration](@entry_id:193372) of a chemical species $\alpha$. In a [substitutional alloy](@entry_id:139785), these fields are subject to the constraint $\sum_\alpha c_\alpha = 1$. Crucially, composition is a **conserved quantity**. The total amount of each species in an isolated system must remain constant. This conservation law has profound implications for the kinetic equations governing the evolution of $c_\alpha$, as will be discussed later .

### Constructing the Potential Landscape

The predictive power of a phase-field model is critically dependent on the careful construction of its free-energy landscape. This involves choosing appropriate functional forms for the interpolation functions and the multi-well potential.

#### Two-Phase Models: The Role of Interpolation Functions

For a two-phase system ($\phi=0,1$), the bulk free energy is typically interpolated as $f_{\mathrm{chem}} = h(\phi) f_\alpha(c) + (1-h(\phi)) f_\beta(c)$, and other properties like the [elastic stiffness tensor](@entry_id:196425) $\mathbb{C}$ may be interpolated similarly. The choice of the interpolation function $h(\phi)$ is not arbitrary. A simple linear interpolation, $h(\phi) = \phi$, while intuitive, introduces a critical artifact. The thermodynamic driving force for phase evolution includes a term proportional to $h'(\phi)$. For $h(\phi)=\phi$, $h'(\phi)=1$ everywhere, which means that even in a pure bulk phase (where $\phi=0$ or $\phi=1$), a spurious driving force can exist if the properties of the two phases differ (e.g., if their elastic energies are unequal). This unphysical force can destabilize the pure phases.

To eliminate this artifact, the interpolation function must satisfy the conditions $h'(0)=0$ and $h'(1)=0$, in addition to $h(0)=0$ and $h(1)=1$. A common choice that satisfies these requirements is the [quintic polynomial](@entry_id:753983) $h(\phi) = \phi^3(10 - 15\phi + 6\phi^2)$ or the simpler cubic form $h(\phi) = \phi^2(3-2\phi)$. By ensuring the derivative of the interpolation function vanishes in the bulk phases, we guarantee that no artificial driving forces arise from the interpolation itself in homogeneous regions .

#### Multi-Phase Models: The Gibbs Simplex and Multi-Obstacle Potentials

Extending the model to $N \ge 3$ phases requires a more sophisticated potential structure. The state of the system, described by the vector $\boldsymbol{\phi} = (\phi_1, \dots, \phi_N)$, is constrained to lie on the **Gibbs [simplex](@entry_id:270623)**: $\Delta_N = \{\boldsymbol{\phi} \in \mathbb{R}^N | \sum_i \phi_i = 1, \phi_i \ge 0\}$. The potential $W(\boldsymbol{\phi})$ must be constructed to have degenerate global minima at the vertices of this simplex (the pure-phase states) and positive energy everywhere else.

A robust construction for such a **multi-obstacle potential** combines a sum of double-well potentials for each phase with a sum of cross-interaction terms that penalize the coexistence of multiple phases. A standard form is :

$W(\{\phi_i\}) = a \sum_{i=1}^N \phi_i^2 (1 - \phi_i)^2 + b \sum_{1 \le i  j \le N} \phi_i^2 \phi_j^2$

where $a>0$ and $b>0$. The first term, a sum of double-wells, ensures that for each component $i$, the states $\phi_i=0$ and $\phi_i=1$ are energetically favored. The second term, the "multi-obstacle" part, creates an energy barrier for any state where two or more phases, say $\phi_i$ and $\phi_j$, are simultaneously non-zero. This term is crucial for controlling the energies of multi-phase junctions and for suppressing unphysical "[wetting](@entry_id:147044)" artifacts where a third phase spontaneously appears at the interface between two other phases .

### The Engine of Evolution: Kinetics and Driving Forces

The free-energy functional defines the thermodynamic landscape, but the evolution of the system across this landscape is governed by kinetic equations. These equations relate the rate of change of the field variables to the thermodynamic driving forces, which are defined by variational derivatives of the total free energy.

#### Conserved vs. Non-Conserved Dynamics

The fundamental distinction between conserved and non-conserved quantities leads to two different classes of kinetic equations.

For a **non-conserved** order parameter, such as a phase field $\phi_i$, its local value is not constrained by a conservation law. It can relax towards a lower energy state locally. Assuming a linear relationship between the rate of change and the thermodynamic driving force (a common assumption in near-equilibrium systems), the evolution follows an **Allen-Cahn equation**, which describes a simple [gradient flow](@entry_id:173722):

$\frac{\partial \phi_i}{\partial t} = -L_i \frac{\delta F}{\delta \phi_i}$

Here, $L_i$ is a kinetic coefficient or mobility, and $\frac{\delta F}{\delta \phi_i}$ is the variational derivative of the free energy, which acts as the driving force for phase transformation.

For a **conserved** quantity like composition $c_\alpha$, its evolution must obey the continuity equation: $\frac{\partial c_\alpha}{\partial t} + \nabla \cdot \mathbf{J}_\alpha = 0$, where $\mathbf{J}_\alpha$ is the diffusive flux of species $\alpha$. According to linear non-equilibrium thermodynamics, the flux is proportional to the gradient of a thermodynamic potential. For [multicomponent diffusion](@entry_id:149036), the driving force is the gradient of the **chemical potential**, $\mu_\alpha = \frac{\delta F}{\delta c_\alpha}$. This leads to the **Cahn-Hilliard equation**. For a multicomponent system, this takes the form :

$\frac{\partial c_\alpha}{\partial t} = \nabla \cdot \left( \sum_{\beta=1}^M M_{\alpha\beta} \nabla \mu_\beta \right)$

where $M_{\alpha\beta}$ is the **[mobility matrix](@entry_id:1127994)**. This equation's structure, with the divergence operator acting on a flux term, mathematically guarantees that the total amount of each species, $\int_\Omega c_\alpha \, \mathrm{d}V$, is conserved over time, provided no-[flux boundary conditions](@entry_id:749481) are imposed.

#### The Multicomponent Mobility Matrix

In multicomponent systems, the diffusion of one species is influenced by the presence and movement of all others. This cross-coupling is captured by the [mobility matrix](@entry_id:1127994) $M_{\alpha\beta}$. The principles of [irreversible thermodynamics](@entry_id:142664), specifically **Onsager's reciprocal relations**, impose strict conditions on this matrix. For systems without external magnetic fields or time-reversal-odd variables, the matrix must be symmetric: $M_{\alpha\beta} = M_{\beta\alpha}$. Furthermore, the Second Law of Thermodynamics, which requires that [entropy production](@entry_id:141771) must always be non-negative, dictates that the matrix must be **positive semi-definite** .

For substitutional alloys, where atoms occupy a common lattice, there is an additional constraint: the net diffusive flux must be zero, $\sum_\alpha \mathbf{J}_\alpha = \mathbf{0}$. This imposes the condition that the rows and columns of the mobility matrix must sum to zero: $\sum_\alpha M_{\alpha\beta} = 0$ and $\sum_\beta M_{\alpha\beta} = 0$. A common and physically consistent model for the [mobility matrix](@entry_id:1127994) that satisfies all these properties is given by :

$M_{\alpha\beta} = m(\{c\}, T) c_\alpha (\delta_{\alpha\beta} - c_\beta)$

where $m(\{c\}, T)$ is a scalar mobility function and $\delta_{\alpha\beta}$ is the Kronecker delta.

### Coupling Mechanisms: The Role of Mechanics

In [crystalline solids](@entry_id:140223), phase transformations and compositional inhomogeneities are almost always accompanied by mechanical stresses and strains. These mechanical effects can, in turn, profoundly influence the thermodynamics and kinetics of the evolution.

#### Eigenstrain and Elastic Energy

The coupling between chemistry, phase, and mechanics is introduced through the **elastic energy density**, $f_{\mathrm{el}}$. A standard formulation based on [linear elasticity](@entry_id:166983) is :

$f_{\mathrm{el}} = \frac{1}{2} (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^0) : \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^0)$

Here, $\boldsymbol{\varepsilon}$ is the total strain tensor, $\mathbb{C}$ is the [elastic stiffness tensor](@entry_id:196425), and $\boldsymbol{\varepsilon}^0$ is the **eigenstrain** or stress-free transformation strain. The [eigenstrain](@entry_id:198120) represents the strain that a small volume of material would undergo due to a change in its composition or phase if it were not constrained by the surrounding material. It is a function of the local composition and phase fields, e.g., $\boldsymbol{\varepsilon}^0(\{c_\alpha\}, \{\phi_i\})$. A common example is Vegard's law, where the [lattice parameter](@entry_id:160045), and thus the eigenstrain, varies linearly with composition. The [stiffness tensor](@entry_id:176588) $\mathbb{C}$ can also be phase-dependent.

A spatially varying eigenstrain field that is geometrically **incompatible** (i.e., it cannot be derived from a single-valued displacement field) will inevitably generate internal stresses, even in the absence of external loads. These stresses store elastic energy in the system and are a primary driver for many microstructural patterning phenomena .

#### Stress-Assisted Diffusion and Phase Transformation

The stored elastic energy is part of the total free energy and thus influences all thermodynamic driving forces. By taking the variational derivative of the total free energy, we find that the mechanical state couples back into the [evolution equations](@entry_id:268137) for composition and phase.

The most direct coupling to diffusion is through the elastic contribution to the chemical potential. By applying the [variational principle](@entry_id:145218) while enforcing [mechanical equilibrium](@entry_id:148830) ($\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$), one can derive the following key result for the elastic part of the chemical potential :

$\mu_\alpha^{\mathrm{el}} = \frac{\partial f_{\mathrm{el}}}{\partial c_\alpha} \bigg|_{\boldsymbol{\varepsilon}} = -\boldsymbol{\sigma} : \frac{\partial \boldsymbol{\varepsilon}^0}{\partial c_\alpha}$

This equation shows that the chemical potential of species $\alpha$ is modified by a term proportional to the local stress tensor $\boldsymbol{\sigma}$. Consequently, gradients in stress can create gradients in chemical potential, driving a diffusive flux. This phenomenon is known as **[stress-assisted diffusion](@entry_id:184392)** or [stress migration](@entry_id:1132524). For instance, in a material under hydrostatic stress $\sigma_h = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$ with a simple isotropic [eigenstrain](@entry_id:198120) $\boldsymbol{\varepsilon}^0 = \beta_\alpha c_\alpha \mathbf{I}$, this contribution simplifies to $\mu_\alpha^{\mathrm{el}} = -3 \beta_\alpha \sigma_h$. Species with a positive expansion coefficient $\beta_\alpha$ will be driven out of regions of high tensile stress (positive $\sigma_h$) and into regions of high compressive stress.

Similarly, the elastic energy contributes to the driving force for [phase transformation](@entry_id:146960), $\delta F / \delta \phi_i$. This term often dictates the shape and orientation of new phases nucleating within a solid matrix, favoring morphologies that minimize the elastic strain energy.

### Advanced Formulations: The Kim-Kim-Suzuki (KKS) Model

For multicomponent, multiphase systems, a crucial choice in model formulation is how to treat the composition fields within the diffuse interfaces. The simplest approach, often called a WBM-type model, uses a single overall composition field $c(\mathbf{x}, t)$ and interpolates the bulk free energies $f_\alpha(c)$ and $f_\beta(c)$. This method, however, suffers from a significant physical inconsistency. It treats the interface as a new material whose free energy is an average of the parent phase energies, creating an artificial free energy barrier that is not present in the real system. This leads to unphysical [solute trapping](@entry_id:1131938) effects that depend on the numerical interface width.

The **Kim-Kim-Suzuki (KKS) model** provides a more physically rigorous solution to this problem. Instead of a single composition field, the KKS model introduces separate composition fields for each phase, $c_\alpha(\mathbf{x}, t)$ and $c_\beta(\mathbf{x}, t)$, which are defined throughout the entire domain. The overall composition $c$ is then defined as a mixture: $c = h(\phi) c_\alpha + (1-h(\phi)) c_\beta$. The key feature of the KKS model is the enforcement of **[local thermodynamic equilibrium](@entry_id:139579)** within the interface. This is achieved by requiring that the chemical potentials of the individual phases be equal to a single, common chemical potential $\mu$ at every point:

$\mu = \frac{\partial f_\alpha(c_\alpha)}{\partial c_\alpha} = \frac{\partial f_\beta(c_\beta)}{\partial c_\beta}$ (in the absence of stress)

This constraint ensures that the system's energy follows the [common-tangent construction](@entry_id:187353) of bulk thermodynamics, thereby eliminating the artificial energy barrier of the mixture model. The benefits of this approach are profound :

1.  **Physical Interface Thermodynamics**: It correctly reproduces the [solute partitioning](@entry_id:1131936) that occurs within an interface in [local equilibrium](@entry_id:156295).
2.  **Elimination of Artifacts**: It removes spurious free energy barriers and the associated interface-width-dependent [solute trapping](@entry_id:1131938).
3.  **Consistent Chemo-Mechanical Coupling**: It allows phase-specific properties like eigenstrain to be defined as functions of the physically meaningful phase compositions ($c_\alpha, c_\beta$), suppressing spurious elastic forces that arise in mixture models.
4.  **Robustness in Multiphase Systems**: In systems with three or more phases, it prevents the spurious stabilization of a third "ghost" phase at a binary interface, a known artifact of simpler interpolation schemes.

While computationally more demanding due to the increased number of fields, the KKS formulation provides a far more accurate and physically consistent framework for modeling complex chemo-mechanical processes in multicomponent, multiphase materials like HEAs.