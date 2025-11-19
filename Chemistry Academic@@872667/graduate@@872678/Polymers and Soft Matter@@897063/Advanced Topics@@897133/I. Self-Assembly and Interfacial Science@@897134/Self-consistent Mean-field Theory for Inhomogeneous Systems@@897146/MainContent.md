## Introduction
Self-Consistent Field Theory (SCFT) stands as a cornerstone of modern polymer science, providing a powerful theoretical framework to predict the equilibrium phase behavior and mesoscopic structure of complex polymer assemblies. The challenge in modeling these systems lies in the intractable nature of the [many-body interactions](@entry_id:751663) between long, flexible chains. SCFT elegantly circumvents this difficulty by replacing the detailed interactions with an effective, averaged potential or "mean field," which is then determined self-consistently with the resulting polymer conformations. This article provides a comprehensive exploration of this indispensable theory, from its statistical mechanical foundations to its practical applications.

The following chapters will guide you through the complete landscape of SCFT. The first chapter, **Principles and Mechanisms**, delves into the heart of the theory, constructing the formalism from the ground up by introducing the Flory-Huggins interaction model, the Gaussian chain, the Edwards [diffusion equation](@entry_id:145865), and the derivation of the core self-consistency equations. Next, **Applications and Interdisciplinary Connections** demonstrates the theory's remarkable utility in modeling real-world phenomena, including polymer interfaces, confined systems, [polyelectrolyte brushes](@entry_id:186992), and highlights its conceptual parallels in other scientific fields like quantum mechanics and [solid mechanics](@entry_id:164042). Finally, **Hands-On Practices** bridges theory and computation, outlining key numerical exercises for implementing an SCFT solver, a critical skill for applying the theory to novel research problems.

## Principles and Mechanisms

The Self-Consistent Field Theory (SCFT) provides a powerful and versatile mean-field framework for predicting the equilibrium phase behavior and structure of inhomogeneous polymer systems. Having introduced its general scope, this chapter delves into the fundamental principles and statistical mechanical machinery that underpin the theory. We will construct the SCFT formalism from the ground up, starting from microscopic interaction models, building the statistical description of polymer chains in a field, deriving the core self-consistency equations, and finally, examining the theoretical justification and limitations of the mean-field approximation itself.

### From Lattice Interactions to Continuum Fields

The heart of any theory of mixtures is the description of [intermolecular interactions](@entry_id:750749). SCFT typically employs a coarse-grained view, where interactions are not between individual atoms but between effective monomer segments. The formulation of this interaction can be approached from both a discrete lattice perspective and a continuous field-theoretic one.

#### The Flory-Huggins Interaction Parameter

The foundational model for polymer mixture thermodynamics is the Flory-Huggins [lattice theory](@entry_id:147950). Consider a binary blend of two homopolymers, A and B, on a three-dimensional lattice where each site has a volume $v_0$ and a coordination number $z$. Within the mean-field approximation, the local excess [free energy of mixing](@entry_id:185318) arises from the change in contact energies between neighboring segments. Let the free energy of a contact between species $i$ and $j$ be $\varepsilon_{ij}(T)$, which may depend on temperature $T$.

The local density of contacts of a given type is proportional to the product of the local volume fractions of the participating species. The local interaction free energy density, $f_{\text{int}}$, can be written by summing over all contact types:
$$
f_{\text{int}}(\mathbf{r}) = \frac{1}{v_0} \left( \frac{1}{2} z \varepsilon_{AA} \phi_A^2(\mathbf{r}) + \frac{1}{2} z \varepsilon_{BB} \phi_B^2(\mathbf{r}) + z \varepsilon_{AB} \phi_A(\mathbf{r})\phi_B(\mathbf{r}) \right)
$$
where the factor of $\frac{1}{2}$ for like-like contacts prevents [double counting](@entry_id:260790). The excess free energy density of mixing, $\Delta f_{\text{mix}}$, is the difference between this value and the free energy of the unmixed components at the same local composition. After some algebraic manipulation using the [incompressibility](@entry_id:274914) condition $\phi_A(\mathbf{r}) + \phi_B(\mathbf{r}) = 1$, we find a remarkably simple form:
$$
\Delta f_{\text{mix}}(\mathbf{r}) = \frac{z}{v_0} \left[ \varepsilon_{AB}(T) - \frac{\varepsilon_{AA}(T) + \varepsilon_{BB}(T)}{2} \right] \phi_A(\mathbf{r})\phi_B(\mathbf{r})
$$
This expression captures the essence of the [mean-field interaction](@entry_id:200557): the free energy penalty or reward for creating an A-B interface is proportional to the product of the local volume fractions. The entire energetic contribution is encapsulated in a single parameter. By convention, this is expressed in terms of the dimensionless **Flory-Huggins parameter**, $\chi$, defined by the relation $\Delta f_{\text{mix}} = \frac{k_B T}{v_0} \chi \phi_A \phi_B$. Equating the two expressions gives a microscopic definition of $\chi$:
$$
\chi(T) = \frac{z}{k_B T} \left[ \varepsilon_{AB}(T) - \frac{\varepsilon_{AA}(T) + \varepsilon_{BB}(T)}{2} \right]
$$
This relation reveals that a positive $\chi$, which promotes phase separation, corresponds to a situation where unlike contacts ($\varepsilon_{AB}$) are less favorable than the average of like contacts.

Furthermore, the contact free energies $\varepsilon_{ij}$ can be decomposed into enthalpic ($u_{ij}$) and non-combinatorial entropic ($s_{ij}$) contributions per contact, $\varepsilon_{ij}(T) = u_{ij} - T s_{ij}$. Substituting this into the definition of $\chi$ yields its common temperature dependence [@problem_id:2927257]:
$$
\chi(T) = \frac{A}{T} + B
$$
where the enthalpic part $A$ and entropic part $B$ are given by:
$$
A = \frac{z}{k_B} \left[ u_{AB} - \frac{u_{AA}+u_{BB}}{2} \right] \quad \text{and} \quad B = -\frac{z}{k_B} \left[ s_{AB} - \frac{s_{AA}+s_{BB}}{2} \right]
$$
The $A/T$ term represents the traditional enthalpic contribution, while the temperature-independent term $B$ captures excess entropic effects beyond simple mixing, such as those arising from local packing or orientation correlations.

#### Continuum Representation of Interactions

While the lattice model is intuitive, SCFT is a continuum theory. In this framework, [short-range interactions](@entry_id:145678) are typically modeled via a contact potential. For a [binary system](@entry_id:159110), the excess interaction free energy, $F_{\text{int}}$, is written as:
$$
\frac{F_{\mathrm{int}}}{k_{B} T} = v_{AB}\int d\mathbf{r}\, c_{A}(\mathbf{r})\,c_{B}(\mathbf{r})
$$
where $c_{\alpha}(\mathbf{r})$ is the local number density of segments of type $\alpha$, and $v_{AB}$ is a parameter with units of volume that quantifies the strength of the interaction between A and B segments.

A formal connection between the lattice and continuum descriptions can be established by comparing their low-density limits. The excess free energy density of a fluid mixture can be expanded in a virial series in the densities. To second order, the term involving unlike species is $2B_{AB} c_A c_B$, where $B_{AB}$ is the second virial coefficient between A and B. By comparing this general form with the expressions from both the Flory-Huggins and [continuum models](@entry_id:190374) (using the relation $\phi_{\alpha} = v_0 c_{\alpha}$), one can extract the effective $B_{AB}$ from each. Equating them provides a mapping between the parameters [@problem_id:2927290]:
$$
\chi = \frac{v_{AB}}{v_0}
$$
This simple but powerful relation allows the phenomenological $\chi$ parameter to be identified with a specific parameter in the [continuum field theory](@entry_id:154108), providing a bridge between the two formalisms.

### The Ideal Polymer Chain in a Mean Field

The second essential component of SCFT is the statistical model of the polymer chain. SCFT simplifies the complex conformations of a real polymer by modeling it as an ideal **Gaussian chain**.

#### The Gaussian Chain Model and Characteristic Length Scales

A real polymer chain has local stiffness due to fixed bond lengths and angles. The Gaussian chain model coarse-grains over these local details, representing the polymer as a random walk. The fundamental parameter of this model is the **statistical segment length** or **Kuhn length**, $b$. A real chain of contour length $L$ is replaced by an idealized chain of $N = L/b$ freely-jointed "Kuhn segments," each of length $b$. The value of $b$ is chosen such that the model chain has the same [mean-square end-to-end distance](@entry_id:177206), $\langle R^2 \rangle = N b^2$, as the real chain.

The Kuhn length $b$ is a measure of the chain's effective stiffness. For a semi-flexible chain described by the [worm-like chain model](@entry_id:162974), which has a characteristic **[persistence length](@entry_id:148195)** $l_p$ (the length scale over which tangent-vector correlations decay), the Kuhn length is given by $b = 2l_p$ in the long-chain limit. For flexible polymers like polystyrene, $b$ is typically a few nanometers, significantly larger than a single chemical bond. [@problem_id:2927278]

#### The Edwards Diffusion Equation

The statistical mechanics of a continuous Gaussian chain in the presence of an external potential field $w(\mathbf{r})$ (in units of $k_B T$) is elegantly described by the **Edwards diffusion equation**. This equation governs the evolution of the chain propagator, $q(\mathbf{r}, s)$, which represents the partition function of a chain fragment of contour length $s$ starting at the origin and ending at position $\mathbf{r}$. The equation is:
$$
\frac{\partial q(\mathbf{r},s)}{\partial s} = \frac{b^2}{6}\nabla^2 q(\mathbf{r},s) - w(\mathbf{r},s) q(\mathbf{r},s)
$$
This equation is formally identical to a [diffusion equation](@entry_id:145865) in an imaginary-time potential, where the contour variable $s$ plays the role of time and the "diffusion coefficient" is $D = b^2/6$.

In the absence of a field ($w(\mathbf{r})=0$), this equation describes an [ideal chain](@entry_id:196640). Its solution corresponds to a random walk, and from it, we can derive all the standard statistical properties. For example, the [mean-square displacement](@entry_id:136284) from the chain start is $\langle |\Delta \mathbf{r}(s)|^2 \rangle = s b^2$. A particularly important measure of overall coil size is the **[radius of gyration](@entry_id:154974)**, $R_g$, which for a linear [ideal chain](@entry_id:196640) is related to the total chain length $N$ by:
$$
\langle R_g^2 \rangle = \frac{N b^2}{6}
$$
The radius of gyration, $R_g$, is the natural [intrinsic length scale](@entry_id:750789) of the polymer. In SCFT, it sets the characteristic wavelength for spatial variations in composition. Any structural features that develop, such as interfaces or lamellar domains, will have a size comparable to $R_g$. This can be seen by non-dimensionalizing the Edwards equation, where the Laplacian term $\frac{b^2}{6}\nabla^2$ becomes proportional to $(R_g/L_{\text{char}})^2$, where $L_{\text{char}}$ is a characteristic length of the system. For this term to be of order unity, we must have $L_{\text{char}} \sim R_g$. [@problem_id:2927278]

### The SCFT Formalism: Partition Functions and Free Energy

SCFT replaces the intractable problem of a system of many interacting polymers with a more tractable problem: a single polymer chain interacting with a self-consistent [mean field](@entry_id:751816) that represents the averaged influence of all other chains. This requires constructing the many-body partition function from its single-chain counterpart.

#### Ensembles and Partition Functions

The starting point is the single-chain partition function, $Q[w]$, for a single polymer in a given external field $w(\mathbf{r})$. This is obtained by integrating the chain [propagator](@entry_id:139558) over all final positions and conformations: $Q[w] = \int d\mathbf{r} \, q(\mathbf{r}, N)$.

In the mean-field approximation, the $n$ chains in the system are treated as statistically independent, non-interacting particles moving in the common field $w(\mathbf{r})$. Because the chains are identical, they are also indistinguishable.
In the **canonical ensemble**, where the number of chains $n$ is fixed, the many-body partition function $Z_n[w]$ is constructed by taking the product of single-chain partition functions and dividing by the Gibbs factor $n!$ to correct for indistinguishability:
$$
Z_n[w] = \frac{1}{n!} \left(Q[w]\right)^n
$$
In the **grand-[canonical ensemble](@entry_id:143358)**, the system is in contact with a reservoir at a fixed chemical potential $\mu$ per chain. The [grand partition function](@entry_id:154455) $\Xi[w]$ is a sum over all possible numbers of chains:
$$
\Xi[w] = \sum_{n=0}^{\infty} Z_n[w] e^{\beta \mu n} = \sum_{n=0}^{\infty} \frac{1}{n!} \left(e^{\beta \mu} Q[w]\right)^n = \exp\left(e^{\beta \mu} Q[w]\right)
$$
where $\beta = 1/(k_B T)$. In this ensemble, the chemical potential $\mu$ controls the average number of chains in the system, $\langle n \rangle$, via the thermodynamic relation $\langle n \rangle = e^{\beta \mu} Q[w]$. This is particularly useful in SCFT calculations where $\mu$ can be used as a Lagrange multiplier to enforce a constraint on the total average density. [@problem_id:2927307]

#### The SCFT Free Energy Functional

The self-consistent fields are determined by minimizing a [free energy functional](@entry_id:184428). For an incompressible binary melt of A and B homopolymers, a standard form for the [free energy functional](@entry_id:184428) $F$ (in units of $k_B T$) is:
$$
\frac{F}{k_{B}T} = \int d\mathbf{r} \,\Big[\chi N\,\phi_{A}(\mathbf{r})\,\phi_{B}(\mathbf{r}) - \xi(\mathbf{r})\big(1-\phi_{A}(\mathbf{r})-\phi_{B}(\mathbf{r})\big) - w_{A}(\mathbf{r})\,\phi_{A}(\mathbf{r}) - w_{B}(\mathbf{r})\,\phi_{B}(\mathbf{r})\Big] - n_A \ln Q_{A}[w_{A}] - n_B \ln Q_{B}[w_{B}]
$$
This functional contains several key components:
1.  The Flory-Huggins interaction energy, $\int d\mathbf{r} \, \chi N \phi_A \phi_B$.
2.  The incompressibility constraint, $\phi_A(\mathbf{r}) + \phi_B(\mathbf{r}) = 1$, enforced via a Lagrange multiplier field $\xi(\mathbf{r})$, often called the "pressure field".
3.  The coupling between the local volume fractions $\phi_{\alpha}(\mathbf{r})$ and the conjugate potential fields $w_{\alpha}(\mathbf{r})$.
4.  The entropic contributions from the chain conformations, expressed via the single-chain partition functions $-n_{\alpha} \ln Q_{\alpha}[w_{\alpha}]$.

The [equilibrium state](@entry_id:270364) is found at the saddle point of this functional, where the fields $\phi_{\alpha}$, $w_{\alpha}$, and $\xi$ satisfy a set of coupled, self-consistent equations.

### The Self-Consistency Equations: Solutions and Symmetries

The equilibrium structure of the system is described by the set of fields that make the [free energy functional](@entry_id:184428) stationary. This leads to the core equations of SCFT.

#### Derivation of the Mean-Field Equations

The self-consistent equations are derived by taking functional derivatives of $F$ with respect to each field and setting them to zero. Variation with respect to the density fields $\phi_A$ and $\phi_B$ yields relations for the conjugate potential fields:
$$
w_{A}(\mathbf{r}) = \chi N \phi_{B}(\mathbf{r}) + \xi(\mathbf{r})
$$
$$
w_{B}(\mathbf{r}) = \chi N \phi_{A}(\mathbf{r}) + \xi(\mathbf{r})
$$
Variation with respect to the pressure field $\xi(\mathbf{r})$ recovers the incompressibility constraint:
$$
\phi_{A}(\mathbf{r}) + \phi_{B}(\mathbf{r}) = 1
$$
Finally, variation with respect to the potential fields $w_{\alpha}(\mathbf{r})$ yields expressions for the densities $\phi_{\alpha}(\mathbf{r})$ in terms of the chain [propagators](@entry_id:153170), closing the loop of [self-consistency](@entry_id:160889).

#### The Pressure Field and Gauge Invariance

The three algebraic equations above can be manipulated to find an explicit expression for the pressure field $\xi(\mathbf{r})$ in terms of the potential fields [@problem_id:2927301]:
$$
\xi(\mathbf{r}) = \frac{1}{2}\left(w_{A}(\mathbf{r}) + w_{B}(\mathbf{r}) - \chi N\right)
$$
This relation reveals an important **gauge invariance** in the theory. If we shift the pressure field and both potential fields by the same arbitrary constant $C$, such that $\xi' = \xi + C$, $w'_A = w_A + C$, and $w'_B = w_B + C$, all the self-consistent algebraic relations remain satisfied. This transformation does not affect the physical density profiles, $\phi_A$ and $\phi_B$. This can be shown rigorously by examining the Edwards [diffusion equation](@entry_id:145865). A constant shift $C$ to the potential $w_k(\mathbf{r})$ results in the [propagator](@entry_id:139558) acquiring a simple exponential factor, $q'_k(\mathbf{r}, s) = q_k(\mathbf{r}, s) \exp(-sC)$. When calculating the density profile, which involves a product of forward and backward [propagators](@entry_id:153170) normalized by the total partition function, these exponential factors precisely cancel out. Consequently, the [physical observables](@entry_id:154692) are invariant under this [gauge transformation](@entry_id:141321). This freedom is often exploited in [numerical algorithms](@entry_id:752770) to "pin" one of the fields at a certain point, which improves stability. [@problem_id:2927301]

#### Multiplicity and Symmetry of Solutions

The set of non-linear self-consistent equations can admit multiple solutions, each corresponding to a different stationary point of the [free energy functional](@entry_id:184428). In the phase-separated regime, there can be solutions corresponding to the two homogeneous bulk phases, as well as various inhomogeneous solutions representing interfaces or ordered morphologies (e.g., lamellae, cylinders, spheres).

For systems with [periodic boundary conditions](@entry_id:147809), [translational invariance](@entry_id:195885) of the [free energy functional](@entry_id:184428) has a profound consequence. If $\phi_0(\mathbf{r})$ is an inhomogeneous solution that breaks translational symmetry, then any rigidly shifted profile $\phi_0(\mathbf{r} - \mathbf{r}_0)$ is also a solution with the exact same free energy. This leads to a continuous family of degenerate solutions. This degeneracy manifests in the [linear stability analysis](@entry_id:154985) of the solution. The Hessian (second variation) operator, when evaluated at $\phi_0(\mathbf{r})$, will have a zero eigenvalue. The corresponding eigenfunction, known as a **Goldstone mode**, is proportional to the gradient of the profile, $\nabla \phi_0(\mathbf{r})$, reflecting the fact that an infinitesimal rigid shift costs no free energy. This continuous degeneracy is lifted if [translational symmetry](@entry_id:171614) is explicitly broken, for instance by imposing hard-[wall boundary conditions](@entry_id:756608) or by introducing a weak external pinning field. These considerations are critical for both the conceptual understanding of [ordered phases](@entry_id:202961) and the practical implementation of [numerical solvers](@entry_id:634411). [@problem_id:2927272]

### Advanced Topics: Extensions and Validity of SCFT

The SCFT framework is highly adaptable and can be extended to a wide variety of complex polymer systems. It is also important to understand its theoretical foundation and the conditions under which it is expected to be accurate.

#### Modeling Complex Systems: Compressibility and Electrostatics

**Compressible Melts:** The standard SCFT formalism assumes the system is incompressible. To model compressible systems, the strict constraint $\sum \phi_{\alpha}=1$ is relaxed. In one common formulation, a [quadratic penalty](@entry_id:637777) term is added to the Hamiltonian, controlled by a [compressibility](@entry_id:144559) parameter $\kappa$. For a Hamiltonian of the form $\mathcal{H}[\xi] = - \sum n_{\alpha} \ln Q_{\alpha}[\xi] - \int d\mathbf{r}\,\xi(\mathbf{r}) + \int d\mathbf{r}\,\frac{\xi(\mathbf{r})^{2}}{2\kappa}$, the saddle-point condition yields a simple local [equation of state](@entry_id:141675) relating the total density $\phi_{\text{tot}}(\mathbf{r})$ to the pressure field $\xi(\mathbf{r})$: $\phi_{\text{tot}}(\mathbf{r}) = 1 - \xi(\mathbf{r})/\kappa$. This implies a constant local [compressibility](@entry_id:144559), $\partial \phi_{\text{tot}}/\partial \xi = -1/\kappa$, demonstrating how thermodynamic properties can be incorporated into the theory. [@problem_id:2927249]

**Polyelectrolytes:** SCFT can be extended to include long-range [electrostatic interactions](@entry_id:166363), essential for modeling [polyelectrolytes](@entry_id:199364). This is achieved by coupling the local number density of charges, $\rho_e(\mathbf{r})$, to a dimensionless [electrostatic potential](@entry_id:140313), $\psi(\mathbf{r})$, via the **Poisson equation**:
$$
\nabla^2 \psi(\mathbf{r}) = - 4\pi \ell_B \rho_e(\mathbf{r})
$$
where $\ell_B = e^2/(\varepsilon k_B T)$ is the Bjerrum length. The potential $\psi(\mathbf{r})$ then acts as an additional field on all charged species (polymer segments and mobile counterions). Within this framework, one can analyze the collective behavior of the system. For instance, by linearizing the self-consistent equations around a homogeneous state (an approach known as the Random Phase Approximation or RPA), one can calculate the system's response to perturbations. This analysis reveals the phenomenon of [electrostatic screening](@entry_id:138995). For a salt-free solution of polymers with a charged fraction $f$ and mean monomer density $n_m$, the inverse screening length squared, $\kappa^2$, in the long-wavelength limit is given by:
$$
\kappa^2 = 4 \pi \ell_B f n_m (f+1)
$$
This result, analogous to the Debye-Hückel screening in simple electrolytes, demonstrates SCFT's ability to capture the fundamental physics of charged polymer systems. [@problem_id:2927271]

#### The Validity of the Mean-Field Approximation

A crucial question remains: under what conditions is the mean-field approximation valid? SCFT is, at its core, a [saddle-point approximation](@entry_id:144800) to a full field-theoretic functional integral. The validity of this approximation hinges on the magnitude of fluctuations around the saddle-point solution.

**The Thermodynamic Limit:** For dense polymer melts, the strength of fluctuations is controlled not by the chain length $N$ alone, but by the **invariant [degree of polymerization](@entry_id:160520)**, $\bar{N}$, which measures the number of overlapping chains within the volume of a single coil. In three dimensions, it is defined as $\bar{N} \equiv (\rho_0 a^3)^2 N$, where $\rho_0$ is the monomer [number density](@entry_id:268986) and $a$ is a microscopic segment length. A detailed [scaling analysis](@entry_id:153681) of the field-theoretic partition function reveals that the [effective action](@entry_id:145780) (the exponent in the functional integral) is proportional to $\sqrt{\bar{N}}$. According to the [method of steepest descent](@entry_id:147601), the width of fluctuations around the saddle point scales as the inverse square root of this large parameter. Therefore, fluctuations of the order parameter field scale as $\langle (\delta \phi)^2 \rangle^{1/2} \sim \bar{N}^{-1/2}$. In the [thermodynamic limit](@entry_id:143061) of high-molecular-weight polymers ($N \to \infty$), $\bar{N}$ becomes very large, and fluctuations around the mean-field solution are strongly suppressed. This provides the fundamental justification for why SCFT is so successful in describing dense, high-molecular-weight polymer systems. [@problem_id:2927282]

#### Fluctuation Corrections and Critical Phenomena

While fluctuations are suppressed in dense melts, they can become significant near a critical point or in systems of lower dimensionality. The effects of fluctuations can be studied by going beyond the [saddle-point approximation](@entry_id:144800) and calculating [loop corrections](@entry_id:150150). For a system described by a scalar $\phi^4$ theory (the universal form of the SCFT functional near a critical point), the one-loop (Gaussian) fluctuation correction to the free energy involves an integral over the bare [propagator](@entry_id:139558), $G_0(\mathbf{q}) = 1/(r + \kappa q^2)$, where $r$ measures the distance to the mean-field critical point.

The behavior of this integral depends strongly on the spatial dimension $d$ [@problem_id:2927260]:
-   In $d=3$, the fluctuation integral remains finite as $r \to 0^+$. The leading correction to the free energy is non-analytic, scaling as $\sqrt{r}$. Fluctuations are present but do not cause a catastrophic divergence at the mean-field critical point.
-   In $d=2$, the fluctuation integral diverges logarithmically, scaling as $\ln(1/r)$ as $r \to 0^+$. This indicates that fluctuations are much stronger and fundamentally alter the nature of the phase transition.

This dimensional dependence is crucial for understanding polymer thin films. A film of thickness $L$ with neutral boundaries effectively behaves as a 2D system when the bulk [correlation length](@entry_id:143364) $\xi = \sqrt{\kappa/r}$ exceeds $L$. In this regime, the system's behavior is dominated by the two-dimensional "zero mode" ($q_z = 0$) of fluctuations. This leads to an enhancement of fluctuation effects, which manifest as a 2D-like logarithmic divergence in thermodynamic properties. This phenomenon of **[dimensional reduction](@entry_id:197644)** highlights a key area where simple [mean-field theory](@entry_id:145338) breaks down and more sophisticated theories that account for fluctuations are required. [@problem_id:2927260]