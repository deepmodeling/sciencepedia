## Introduction
Predicting the behavior of materials, from the strength of a metal alloy to the efficiency of a battery, requires understanding phenomena that span an immense range of length and time scales. While the fundamental laws of quantum mechanics govern atomic bonding, these are computationally intractable for simulating the deformation of an entire engineering component. This scale-separation problem presents a significant challenge in materials science, which no single computational method can overcome. The solution lies in the [hierarchy of materials modeling](@entry_id:1126051), a powerful paradigm that systematically links a suite of simulation techniques, each tailored to a specific scale.

This article provides a comprehensive overview of this hierarchical approach. The journey begins in the **Principles and Mechanisms** chapter, where we will dissect the foundational theories and computational methods at each level of the hierarchy, from [electronic structure calculations](@entry_id:748901) to continuum mechanics. We will then explore how these individual models are put into action in the **Applications and Interdisciplinary Connections** chapter, showcasing integrated workflows that predict complex real-world phenomena in materials science, engineering, and even biology. Finally, the **Hands-On Practices** chapter will offer practical exercises to solidify your understanding of key concepts like coarse-graining and homogenization, bridging theory with application.

## Principles and Mechanisms

Materials behavior is governed by physical laws acting across a vast spectrum of length and time scales, from the quantum dance of electrons that determines [chemical bonding](@entry_id:138216) (angstroms, femtoseconds) to the macroscopic deformation of engineering components (meters, seconds). No single computational model can span this entire range. Instead, the field of [multiscale materials simulation](@entry_id:1128334) relies on a hierarchy of methods, each tailored to a specific window of scale, with principles and mechanisms for passing information between them. This chapter elucidates the foundational methods at each level of this hierarchy and the overarching principles that ensure the physical and mathematical consistency of the multiscale enterprise.

### The Multiscale Hierarchy: A Conceptual Overview

The [hierarchy of materials modeling](@entry_id:1126051) can be envisioned as a ladder, where each rung represents a class of simulation methods characterized by its fundamental **degrees of freedom** (the variables being tracked), the **governing equations** that describe their evolution, and the characteristic **length and time scales** over which they are applicable. Ascending the ladder involves a process of **coarse-graining**, where fine-scale details are systematically averaged or integrated out to produce a simpler, more computationally tractable model that is valid at a larger scale.

A canonical progression of methods, from the most detailed to the most coarse-grained, serves to illustrate this concept . The journey begins with quantum mechanics and ends with continuum [engineering mechanics](@entry_id:178422):

1.  **Density Functional Theory (DFT)**: This is a quantum mechanical method that solves for the ground-state electronic structure. Its degrees of freedom are the electron density, $n(\mathbf{r})$, and it solves the time-independent Kohn-Sham equations. It operates at the scale of atomic bonds ($\sim 10^{-10}\,\mathrm{m}$) and describes phenomena on electronic timescales ($\sim 10^{-15}\,\mathrm{s}$).

2.  **Ab Initio Molecular Dynamics (AIMD)**: This method adds dynamics to the electronic scale. The degrees of freedom are the atomic positions and momenta, $\{\mathbf{R}_i, \mathbf{P}_i\}$. It evolves these according to Newton's laws of motion, but with the crucial feature that the forces on the atoms are calculated "from first principles" using DFT at every timestep. This restricts AIMD to small systems (hundreds of atoms) and short times (picoseconds).

3.  **Classical Molecular Dynamics (MD)**: To access larger systems and longer times, MD replaces the expensive quantum force calculation with [empirical interatomic potentials](@entry_id:136487) (force fields). The degrees of freedom remain atomic positions and momenta, and the governing equations are still Newton's laws. This coarse-graining of the forces allows MD to simulate millions of atoms for up to microseconds.

4.  **Kinetic Monte Carlo (KMC)**: Many material processes, like diffusion or phase transformations, are dominated by rare, thermally activated events. MD spends most of its computational effort simulating atomic vibrations between these events. KMC coarse-grains these vibrations away. Its degrees of freedom are discrete configurational states, $\{\alpha\}$, and it models the system as a Markovian process, jumping between states with predefined rates. This allows it to reach experimental timescales of seconds or longer.

5.  **Phase-Field (PF) Modeling**: This method moves from a discrete, atomistic description to a continuous one. The degrees of freedom are continuous fields, or **order parameters**, $\phi(\mathbf{x}, t)$, that represent average properties like local composition or crystalline order. The governing equations are partial differential equations (PDEs) that describe the relaxation of these fields toward a state of lower free energy. It is a mesoscale method, bridging atomistics to the continuum.

6.  **Finite Element Method (FEM)**: At the top of the hierarchy is the continuum scale, where the material is treated as a homogeneous or heterogeneous medium without resolving its atomic nature. FEM is a powerful numerical technique for solving the PDEs of continuum mechanics (e.g., for displacement $\mathbf{u}(\mathbf{x}, t)$ and stress $\boldsymbol{\sigma}(\mathbf{x}, t)$). The material's specific behavior is encapsulated in a **[constitutive model](@entry_id:747751)**, which is often informed by the lower-scale methods. This enables simulation at the engineering scale of meters and seconds .

### Level I: The Electronic Scale

The foundation of the hierarchy rests on quantum mechanics, which describes the behavior of electrons and their role in forming chemical bonds. The ultimate governing law is the many-body Schrödinger equation. However, solving this equation exactly is intractable for all but the simplest systems. The Born-Oppenheimer approximation, which assumes that the light electrons instantaneously adjust to the motion of the much heavier nuclei, is the first crucial simplification. Within this framework, we seek the electronic ground state for a fixed configuration of nuclei.

#### Density Functional Theory

For decades, the primary variable in quantum calculations was the [many-electron wavefunction](@entry_id:174975), $\Psi(\mathbf{r}_1, ..., \mathbf{r}_N)$, a highly complex object in a $3N$-dimensional space. **Density Functional Theory (DFT)** revolutionized the field by re-casting the problem in terms of a much simpler quantity: the electron density $n(\mathbf{r})$, a function in 3D space. The Hohenberg-Kohn theorems provide the formal foundation, proving that the ground-state electron density of a system uniquely determines all its properties, including its energy.

In practice, DFT is implemented through the **Kohn-Sham (KS) construction**. This brilliantly maps the intractable problem of interacting electrons onto a fictitious system of non-interacting electrons that, by design, has the exact same ground-state density $n(\mathbf{r})$ as the real system. The KS approach leads to a set of effective single-particle Schrödinger-like equations. The price of this simplification is that all the complex many-body effects of exchange (from Pauli exclusion) and correlation (from electrons avoiding each other) are bundled into a single term known as the **exchange-correlation (XC) functional**, $E_{\text{xc}}[n]$. The [exact form](@entry_id:273346) of $E_{\text{xc}}[n]$ is unknown and must be approximated .

The choice of approximation for $E_{\text{xc}}[n]$ is a central aspect of DFT and defines a "Jacob's Ladder" of functionals with increasing accuracy and complexity.
-   The **Local Density Approximation (LDA)** assumes the exchange-correlation energy at a point $\mathbf{r}$ is the same as that of a [uniform electron gas](@entry_id:163911) with density $n(\mathbf{r})$.
-   The **Generalized Gradient Approximation (GGA)** improves upon this by also including the local gradient of the density, $|\nabla n(\mathbf{r})|$, making it more accurate for the inhomogeneous electron densities found in real materials.

The choice of XC functional directly affects the predicted total energies, forces, and stresses. Consequently, properties derived from these quantities—such as [elastic moduli](@entry_id:171361), which are critical inputs for higher-scale continuum models—are sensitive to the DFT approximation used at the hierarchy's base .

#### Contrast with Wavefunction-Based Methods

It is crucial to distinguish DFT from traditional wavefunction-based methods. In **Hartree-Fock (HF) theory**, the fundamental variable is the [many-electron wavefunction](@entry_id:174975), which is approximated as a single Slater determinant. This ansatz exactly accounts for electron exchange but completely neglects electron correlation. **Post-Hartree-Fock** methods, such as Møller-Plesset [perturbation theory](@entry_id:138766) (MP2) or Coupled Cluster (CCSD), systematically improve upon the HF solution by including contributions from excited [determinants](@entry_id:276593) to recover the missing [correlation energy](@entry_id:144432). These methods are generally more accurate than standard DFT approximations but exhibit much steeper computational scaling with system size, limiting their application to smaller molecules and systems .

### Level II: The Atomistic Scale

At this level, we abstract away the electronic details and treat atoms as the fundamental particles. The motion of these atoms is governed by the laws of classical mechanics, with their interactions described by an [effective potential energy](@entry_id:171609) surface.

#### Classical Molecular Dynamics

**Molecular Dynamics (MD)** simulates the evolution of a system of atoms by numerically integrating Newton's equations of motion, $\mathbf{F}_i = m_i \ddot{\mathbf{R}}_i$. In a [conservative system](@entry_id:165522), the forces are the negative gradient of a potential energy function, $\mathbf{F}_i = -\nabla_{\mathbf{R}_i} U(\{\mathbf{R}_j\})$. This is equivalent to a Hamiltonian system, described by a Hamiltonian $H(q,p) = T(p) + U(q)$, where $q$ and $p$ are the generalized positions and momenta of the atoms.

The exact, continuous-time evolution of such a system has a profound property described by **Liouville's theorem**: the flow in phase space has zero divergence, meaning phase-space volume is exactly conserved . This property is a hallmark of Hamiltonian mechanics. To capture the correct long-time statistical mechanics of the system, it is highly desirable for the numerical integrator used in MD to preserve as much of this geometric structure as possible.

This leads to the use of **[symplectic integrators](@entry_id:146553)**, such as the widely used **velocity-Verlet algorithm**. A symplectic integrator is a numerical map that, for any finite timestep $\Delta t$, exactly preserves phase-space volume and is time-reversible. While these integrators do *not* exactly conserve the original Hamiltonian $H(q,p)$, they have an even more remarkable property: they exactly conserve a nearby "shadow" Hamiltonian, $\tilde{H}_{\Delta t}$, which differs from the true Hamiltonian by terms of order $\mathcal{O}(\Delta t^2)$. This exact conservation of a modified Hamiltonian means that the energy of the true system, $H(q,p)$, exhibits bounded oscillations over extremely long simulation times, with no systematic drift. This excellent long-term [energy stability](@entry_id:748991) is the primary reason for their ubiquitous use in MD simulations .

#### Interatomic Potentials: The Force Calculation

The accuracy of an MD simulation is fundamentally limited by the quality of the [interatomic potential](@entry_id:155887), $U(\{\mathbf{R}_j\})$, which replaces the computationally prohibitive quantum mechanical calculation of forces. The development of these potentials, or force fields, is a central activity in materials simulation. They can be broadly classified by the physics they aim to capture .

-   **Pairwise Additive Potentials**: The simplest models assume the total energy is a sum of interactions between pairs of atoms, $E = \frac{1}{2} \sum_{i \neq j} V(r_{ij})$. The classic **Lennard-Jones (LJ) potential** is of this form, with a repulsive $r^{-12}$ term modeling Pauli exclusion and an attractive $r^{-6}$ term modeling London [dispersion forces](@entry_id:153203) . While useful for [noble gases](@entry_id:141583) and simple molecular systems, pairwise central-force potentials are fundamentally inadequate for many condensed matter systems. For example, in cubic crystals, they enforce the **Cauchy relation** ($C_{12} = C_{44}$ for the [elastic constants](@entry_id:146207)), which is strongly violated by most metals due to the non-pairwise nature of [metallic bonding](@entry_id:141961).

-   **Many-Body Potentials for Metals**: To overcome the limitations of pair potentials, the **Embedded-Atom Method (EAM)** was developed. In EAM, the energy of an atom depends not only on its pairwise interactions but also on the "electron density" it is embedded in, which is a superposition of contributions from all its neighbors. This non-linear, environment-dependent "embedding energy" makes EAM a true [many-body potential](@entry_id:197751) and allows it to correctly capture trends in cohesion and surface energies that depend on an atom's coordination number .

-   **Many-Body Potentials for Covalent Systems**: Covalent bonds, as in silicon or carbon, are highly directional. **Tersoff-type bond-order potentials** capture this by modulating the strength of each pairwise bond with a "bond-order" term. This term explicitly depends on the local environment, including the angles between bonds. This allows the potential to distinguish between different hybridizations (e.g., $sp^2$ vs. $sp^3$) and accurately model the directional nature of [covalent bonding](@entry_id:141465), which is essential for describing mechanical properties and [brittle fracture](@entry_id:158949) .

-   **Reactive Potentials**: To simulate chemical reactions involving [bond formation](@entry_id:149227) and breaking, even more sophisticated potentials are needed. The **Reactive Force Field (ReaxFF)** family extends the bond-order concept by incorporating a dynamic [charge equilibration](@entry_id:189639) scheme. At every timestep, [partial atomic charges](@entry_id:753184) are recalculated to respond to the changing local chemical environment. This allows ReaxFF to model complex reactive processes like combustion, catalysis, and oxidation, where [charge transfer](@entry_id:150374) plays a pivotal role .

### Level III: The Mesoscale

The mesoscale bridges the atomistic world and the macroscopic continuum. Methods at this level coarse-grain atomic degrees of freedom to model the collective behavior of defects and the evolution of microstructure over length scales of nanometers to micrometers and time scales of microseconds to seconds.

#### Kinetic Monte Carlo

**Kinetic Monte Carlo (KMC)** is an event-based, stochastic method designed to simulate systems where the dynamics are dominated by rare, thermally activated events. It operates under the crucial assumption of a **separation of time scales**: the system rapidly equilibrates within a potential energy basin (a "state") and only infrequently jumps over an energy barrier to a new state. The rates, $k_i$, for all possible events are assumed to be known, often calculated from lower-scale methods like DFT using Transition State Theory.

The KMC algorithm does not track the detailed trajectory of atoms. Instead, it models the system's evolution as a **continuous-time Markov process**. In each step, it performs two actions:
1.  It determines the waiting time, $\tau$, until the next event occurs. This time is drawn from an [exponential distribution](@entry_id:273894) whose rate is the sum of all possible event rates, $K = \sum_i k_i$.
2.  It selects which event occurs. The probability of selecting event $j$ is proportional to its rate, $p_j = k_j / K$.

This procedure advances the simulation time in variable, stochastically determined steps, allowing it to efficiently bypass the vibrational motions and reach experimentally relevant timescales .

KMC methods can be categorized by how they represent the system's state:
-   **Lattice KMC** defines the state on a fixed crystal lattice. Atoms or defects occupy discrete sites, and the events consist of hopping between these sites or reacting with neighbors. An "event catalog" containing all possible local configurations and their associated rates is pre-computed. This makes it extremely efficient and well-suited for phenomena on well-defined crystalline surfaces, such as catalysis and [epitaxial growth](@entry_id:157792).
-   **Off-Lattice KMC** treats atomic coordinates as continuous variables. Events are transitions between local energy minima on the potential energy surface. Identifying these events and their pathways often requires computationally expensive saddle-point searches "on the fly". This approach is necessary for systems without a fixed lattice structure, such as [amorphous materials](@entry_id:143499), or for modeling complex [morphological evolution](@entry_id:175809) where the catalog of possible events is not known in advance [@problem_id:3815427, @problem_id:3815434].

#### Phase-Field Modeling

The **Phase-Field (PF)** method takes a different approach to coarse-graining, replacing discrete atoms with continuous **order parameter** fields. These fields, such as composition $c(\mathbf{x},t)$ or a structural parameter $\eta(\mathbf{x},t)$, represent local, averaged properties of the material. The state of the system is described by a **Ginzburg-Landau [free energy functional](@entry_id:184428)**, which typically has two parts: a bulk energy density, $f_{\text{bulk}}$, which describes the energy of uniform phases, and a gradient energy term, $\frac{\kappa}{2} |\nabla \phi|^2$, which penalizes spatial variations and assigns a finite energy and thickness to interfaces between phases .

The dynamics of the system are assumed to be purely dissipative, meaning the system evolves to monotonically decrease its total free energy, consistent with the Second Law of Thermodynamics. The form of the governing evolution equation depends critically on whether the order parameter is a conserved quantity.

-   **Non-conserved Order Parameters**: A quantity like crystalline orientation, $\eta$, is not conserved; it can appear or disappear locally as a region crystallizes or melts. Its evolution follows a path of steepest descent on the free energy landscape. This leads to the **Allen-Cahn equation**:
    $$ \frac{\partial \eta}{\partial t} = - L_\eta \frac{\delta F}{\delta \eta} $$
    where $L_\eta$ is a kinetic coefficient and $\delta F/\delta \eta$ is the thermodynamic driving force, defined as the functional derivative of the free energy $F$.

-   **Conserved Order Parameters**: A quantity like atomic composition, $c$, is conserved; it cannot be created or destroyed locally but must be transported via diffusion. Its dynamics must obey a continuity equation, $\partial_t c + \nabla \cdot \mathbf{J}_c = 0$. Assuming a linear relationship between the [diffusive flux](@entry_id:748422) $\mathbf{J}_c$ and the gradient of the chemical potential $\mu_c = \delta F/\delta c$, we arrive at the **Cahn-Hilliard equation**:
    $$ \frac{\partial c}{\partial t} = \nabla \cdot \left( M_c \nabla \frac{\delta F}{\delta c} \right) $$
    where $M_c$ is the mobility. This equation describes processes like spinodal decomposition, where a homogeneous alloy separates into distinct phases .

### Level IV: The Continuum Scale

At the highest level of the hierarchy, the material is viewed as a continuum, and its internal atomic or microstructural details are subsumed into effective constitutive properties. The **Finite Element Method (FEM)** is the workhorse for solving the governing equations of continuum mechanics, such as the [balance of linear momentum](@entry_id:193575), $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$, for a body in [static equilibrium](@entry_id:163498). The critical input for any continuum simulation is the **constitutive model**, which relates stress to strain and captures the specific mechanical response of the material.

The choice of [constitutive model](@entry_id:747751) depends on the expected material behavior :
-   **Elasticity**: Describes reversible deformation where the material returns to its original shape upon unloading. The stress is a function of the current strain, often derived from a stored energy potential, $\boldsymbol{\sigma} = \partial \psi / \partial \boldsymbol{\varepsilon}$.
-   **Plasticity**: Describes permanent, irreversible deformation that occurs when the stress exceeds a critical value defined by a **[yield surface](@entry_id:175331)**. The evolution of plastic strain is history-dependent and is tracked using **[internal state variables](@entry_id:750754)**. The process is inherently dissipative, as energy is expended to create defects and move them through the material.
-   **Viscoelasticity**: Describes materials that exhibit both energy storage (elastic) and [energy dissipation](@entry_id:147406) (viscous) characteristics, leading to a time- and rate-dependent response. This behavior is often modeled using [hereditary integrals](@entry_id:186265) based on the Boltzmann [superposition principle](@entry_id:144649).

#### Crystal Plasticity: A Microstructure-Informed Model

**Crystal Plasticity (CP)** is a sophisticated [constitutive model](@entry_id:747751) that resides at the interface between the mesoscale and the continuum. It describes the [plastic deformation](@entry_id:139726) of [crystalline materials](@entry_id:157810) by explicitly accounting for the underlying mechanism of dislocation slip on specific crystallographic planes.

At its core, CP is based on the **[multiplicative decomposition](@entry_id:199514)** of the deformation gradient into elastic and plastic parts, $\mathbf{F} = \mathbf{F}^e \mathbf{F}^p$. The plastic flow, represented by the plastic [velocity gradient](@entry_id:261686) $\mathbf{L}^p = \dot{\mathbf{F}}^p (\mathbf{F}^p)^{-1}$, is assumed to be the sum of shearing rates on all active [slip systems](@entry_id:136401):
$$ \mathbf{L}^p = \sum_{\alpha} \dot{\gamma}^\alpha (\mathbf{s}^\alpha \otimes \mathbf{m}^\alpha) $$
Here, each slip system $\alpha$ is defined by its slip [direction vector](@entry_id:169562) $\mathbf{s}^\alpha$ and slip plane normal $\mathbf{m}^\alpha$. The rate of slip, $\dot{\gamma}^\alpha$, is driven by the **[resolved shear stress](@entry_id:201022)** $\tau^\alpha$ on that system—the projection of the macroscopic stress onto the slip plane in the slip direction. By explicitly incorporating the geometry and orientation of the crystal lattice through the set of available [slip systems](@entry_id:136401), CP naturally captures the profound [plastic anisotropy](@entry_id:203119) of single crystals and the collective response of polycrystalline aggregates .

### Principles of Information Transfer and Model Validity

A successful [multiscale simulation](@entry_id:752335) is more than just a collection of individual models; it requires a principled framework for linking scales and for understanding the validity and uncertainty of its predictions.

#### Strategies for Linking Scales

Two primary strategies exist for exchanging information between different levels of the modeling hierarchy.

-   **Hierarchical Parameter Passing**: This is a sequential, one-way information flow. A high-fidelity, lower-scale simulation is performed first on a small, representative system to compute effective properties or parameters. These parameters (e.g., [elastic constants](@entry_id:146207) from DFT, diffusion rates from MD) are then used as fixed input for a larger, higher-scale model that is run independently. There is no feedback from the upper scale to the lower scale during the simulation .

-   **Concurrent Coupling**: In this more complex approach, models for different scales are run simultaneously and are coupled within a single simulation, allowing for bidirectional information flow. This is necessary when the behavior in one region requires high fidelity while being strongly influenced by the larger-scale environment, such as at a crack tip. Concurrent methods typically formulate a single total energy functional for the entire system and solve for a [global equilibrium](@entry_id:148976). Examples include :
    -   **Quantum Mechanics/Molecular Mechanics (QM/MM)**, which treats a small, chemically active region with QM and the surrounding environment with a classical MM force field.
    -   The **Quasicontinuum (QC)** method, which seamlessly couples a fully atomistic region with a continuum region whose energy is determined by the local deformation via the Cauchy-Born rule.
    -   The **Arlequin** method, which provides a general framework for blending different models in overlapping domains, enforcing compatibility with constraints.
    A key challenge in concurrent [atomistic-continuum coupling](@entry_id:746567) is the potential for spurious "[ghost forces](@entry_id:192947)" at the interface due to inconsistencies between the two models. Ensuring that the coupled method passes a **patch test**—the ability to exactly reproduce a uniform strain field with zero net forces on unconstrained atoms—is a crucial diagnostic for consistency .

#### Principles of Coarse-Graining

The process of deriving a higher-scale model from a lower-scale one is known as coarse-graining. Formally, this involves defining a mapping from the high-dimensional microscopic degrees of freedom to a reduced set of coarse variables. The goal is to find an effective potential for these coarse variables that reproduces certain properties of the original system. Different methods arise from different choices of what property to match :

-   **Structural Matching**: Seeks an [effective potential](@entry_id:142581) that reproduces the structural [correlation functions](@entry_id:146839) of the atomistic system, such as the radial distribution function $g(r)$. This is equivalent to matching the [potential of mean force](@entry_id:137947) (PMF) of the coarse variables.
-   **Force Matching**: Constructs the [effective potential](@entry_id:142581) by minimizing the difference between its gradient (the coarse-grained force) and the ensemble-averaged force from the underlying [atomistic simulation](@entry_id:187707) projected onto the coarse degrees of freedom.
-   **Thermodynamic Matching**: Aims to directly reproduce bulk thermodynamic properties like pressure or compressibility. It is important to note that a potential derived from structural matching alone is not guaranteed to reproduce thermodynamic properties, a problem known as a lack of "[thermodynamic consistency](@entry_id:138886)" .

#### Representativity and Transferability

For a hierarchical model to be predictive, it must satisfy two crucial criteria: representativity and transferability.

-   **Representativity**: The lower-scale simulations used to parameterize the model must be performed on a simulation volume that is large enough to be statistically representative of the true [material microstructure](@entry_id:202606). The size of this **Representative Volume Element (RVE)**, $L$, must be much larger than the characteristic [correlation length](@entry_id:143364) of the microstructure, $\ell_c$. As $L$ increases, the variance of the computed effective properties should decay, indicating convergence to the true [ensemble average](@entry_id:154225) .

-   **Transferability**: The trained model must be able to provide accurate and physically meaningful predictions for conditions (e.g., loading paths, boundary conditions) beyond those it was trained on. This requires not only that the model is a good fit to the training data, but also that it respects fundamental physical laws. A key diagnostic for transferability is to check for thermodynamic consistency. For an [isothermal process](@entry_id:143096), the model must not violate the Second Law of Thermodynamics, meaning the predicted dissipation rate, $\mathcal{D}(t) = \mathbf{S}(t) : \dot{\mathbf{E}}(t) - \dot{\psi}(t)$, must remain non-negative for any admissible history. A prediction of negative dissipation is an unambiguous sign of model failure .

#### Uncertainty in the Hierarchy

Every model in the hierarchy is an approximation of reality, and it is essential to understand and quantify the uncertainty in its predictions. Uncertainty in multiscale modeling can be decomposed into two fundamental types .

-   **Aleatoric Uncertainty**: This is the inherent variability or randomness in a system that persists even if the model and its parameters were known perfectly. It is often called "irreducible uncertainty".
-   **Epistemic Uncertainty**: This is uncertainty due to a lack of knowledge. It stems from simplifications in the model form, or from errors in the model parameters. It is, in principle, "reducible" with more data or better models.

These two types of uncertainty manifest at every level of the multiscale hierarchy :
-   At the **electronic scale**, the choice of an approximate XC functional in DFT is a major source of epistemic uncertainty. The thermal vibrations of nuclei at finite temperature introduce aleatoric uncertainty in the energy.
-   At the **atomistic scale**, uncertainty in the functional form and fitted parameters of an interatomic potential is epistemic. The stochastic nature of trajectories within a thermodynamic ensemble in an MD simulation is aleatoric.
-   At the **mesoscale**, the choice of free-energy functional in a PF model or the set of included events in a KMC model is epistemic. The stochastic event selection in KMC and the thermal noise terms in Langevin-based PF models are aleatoric.
-   At the **continuum scale**, the choice of constitutive model (e.g., linear elastic vs. plastic) is epistemic. The inherent [spatial variability](@entry_id:755146) of material properties in a real component (e.g., random grain structure) is aleatoric.

A rigorous multiscale simulation workflow must not only pass information up the chain of scales but must also propagate and quantify these uncertainties to provide a complete and honest assessment of the confidence in its final predictions.