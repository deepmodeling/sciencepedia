## Introduction
Dirac and Weyl [semimetals](@entry_id:152277) represent a fascinating class of topological materials that have reshaped our understanding of electronic states in solids. Functioning as three-dimensional analogues to graphene, they host quasiparticles that mimic relativistic fermions, governed by principles bridging condensed matter and high-energy physics. These materials are defined by unique points in their band structure—Dirac or Weyl points—where conduction and valence bands touch, leading to a host of exotic physical phenomena. The central question this article addresses is how these topological nodes emerge from underlying crystalline symmetries and what distinct, measurable signatures they produce.

This article provides a comprehensive journey into the world of Dirac and Weyl [semimetals](@entry_id:152277), structured to build a robust theoretical and practical understanding. The exploration is divided into three main chapters:

*   **Principles and Mechanisms:** This chapter delves into the core theory, explaining how Weyl points are generated from Dirac points through the breaking of time-reversal or inversion symmetry. It meticulously examines the resulting electronic structure, including [dispersion relations](@entry_id:140395), the density of states, the celebrated Fermi arc [surface states](@entry_id:137922), and key transport signatures like the [chiral anomaly](@entry_id:142077) and anomalous Hall effect.

*   **Applications and Interdisciplinary Connections:** Building on the theoretical foundation, this section explores the experimental realization of these materials and their observable properties. It highlights how concepts like the Berry phase and [chiral anomaly](@entry_id:142077) are measured in real systems and discusses how topological phases can be engineered. Furthermore, it illuminates the profound connections to other fields, including [mesoscopic physics](@entry_id:138415), superconductivity, and quantum field theory, through phenomena such as the Witten effect and the Casimir effect.

*   **Hands-On Practices:** To solidify the concepts discussed, this final chapter presents a set of practical problems. These exercises offer readers the opportunity to apply their knowledge by calculating fundamental properties like the [electronic specific heat](@entry_id:144099), Landau levels in a magnetic field, and the conditions for interaction-driven phase transitions.

By progressing through these sections, the reader will gain a deep appreciation for the principles, experimental manifestations, and far-reaching implications of Dirac and Weyl semimetals.

## Principles and Mechanisms

The conceptual framework of Dirac and Weyl [semimetals](@entry_id:152277) rests upon the profound interplay between [relativistic quantum mechanics](@entry_id:148643), crystalline symmetries, and [band structure](@entry_id:139379) topology. While the preceding introduction has outlined the historical and physical context, this chapter delves into the core principles and mechanisms that govern the emergence and unique physical manifestations of these topological states of matter. We will systematically dissect how Weyl points arise from their more symmetric Dirac counterparts, explore their characteristic spectral features, and elucidate the remarkable transport phenomena they engender.

### From Dirac to Weyl Semimetals: The Role of Symmetry

The foundation of our discussion is the **Dirac point**, a singular point in the Brillouin zone where four [electronic bands](@entry_id:175335) (two conduction and two valence, each with spin degeneracy) touch. These points are the three-dimensional analogue of the single Dirac cone in graphene. Such a four-fold degeneracy is not accidental; it is robustly protected by the combined action of fundamental crystalline symmetries, namely [time-reversal symmetry](@entry_id:138094) (TRS) and spatial [inversion symmetry](@entry_id:269948) (IS). A low-energy effective Hamiltonian describing a Dirac point can generally be written in a $4 \times 4$ basis that combines spin and another two-level degree of freedom (often termed [pseudospin](@entry_id:147053), representing orbital or sublattice quantum numbers).

The transition from a Dirac semimetal to a Weyl semimetal is induced by breaking one of these protecting symmetries. When either TRS or IS is broken, the four-fold degenerate Dirac point typically splits into a pair of two-fold degenerate **Weyl points**. Each Weyl point acts as a topologically protected node where two bands cross with a linear dispersion. These Weyl points are distinct from Dirac points in a crucial way: they are topologically non-trivial monopoles of Berry curvature in momentum space. Each Weyl point is characterized by an integer [topological charge](@entry_id:142322), its **[chirality](@entry_id:144105)** $\chi = \pm 1$, which determines whether it is a source ($\chi=+1$) or a sink ($\chi=-1$) of Berry curvature.

Let us examine the two primary mechanisms for generating Weyl points from a parent Dirac semimetal.

#### Breaking Time-Reversal Symmetry

Time-reversal symmetry can be broken by external magnetic fields or by intrinsic [magnetic ordering](@entry_id:143206) within a material. The Zeeman effect, which couples an external magnetic field to the electron spin, provides a canonical example of this mechanism.

Consider a model for a Dirac semimetal whose low-energy excitations near a Dirac point at $\mathbf{k}=0$ are described by the Hamiltonian $H_0(\mathbf{k})$. Now, let us introduce a TRS-breaking perturbation in the form of a Zeeman term, $H_Z = -b_z(\sigma_z \otimes \mathbb{I}_\tau)$, where $b_z$ is the Zeeman energy, $\sigma_z$ is a Pauli matrix for spin, and $\mathbb{I}_\tau$ is the identity in the [pseudospin](@entry_id:147053) space. The total Hamiltonian becomes $H(\mathbf{k}) = H_0(\mathbf{k}) + H_Z$.

To see the effect of this term, we can consider a specific Dirac Hamiltonian given by $H_0(\mathbf{k}) = \hbar \sum_{i=x,y,z} v_i k_i \Gamma_i$, where the $\Gamma_i$ matrices are constructed as $\Gamma_1=\sigma_x\otimes\tau_x$, $\Gamma_2=\sigma_y\otimes\tau_x$, and $\Gamma_3=\sigma_z\otimes\tau_x$. The total Hamiltonian is then:
$H(\mathbf{k}) = \hbar(v_x k_x\sigma_x + v_y k_y\sigma_y + v_z k_z\sigma_z) \otimes \tau_x - b_z(\sigma_z \otimes \mathbb{I}_\tau)$.

By working in the basis where the [pseudospin](@entry_id:147053) matrix $\tau_x$ is diagonal (with eigenvalues $\lambda_\tau = \pm 1$), the $4 \times 4$ Hamiltonian decouples into two $2 \times 2$ blocks. Each block is a Weyl Hamiltonian:
$H_{\lambda_\tau = \pm 1}(\mathbf{k}) = \pm \hbar(v_x k_x\sigma_x + v_y k_y\sigma_y + v_z k_z\sigma_z) - b_z \sigma_z$.

A Weyl point is a gapless point in the spectrum, occurring where the [energy bands](@entry_id:146576) touch. For the block $H_{+1}$, the [energy eigenvalues](@entry_id:144381) are $\pm \sqrt{(\hbar v_x k_x)^2 + (\hbar v_y k_y)^2 + (\hbar v_z k_z - b_z)^2}$. The gap closes when $k_x=k_y=0$ and $\hbar v_z k_z = b_z$. For the block $H_{-1}$, the eigenvalues are $\pm \sqrt{(\hbar v_x k_x)^2 + (\hbar v_y k_y)^2 + (\hbar v_z k_z + b_z)^2}$, and the gap closes when $k_x=k_y=0$ and $\hbar v_z k_z = -b_z$.

Thus, the single Dirac point at $\mathbf{k}=0$ has split into a pair of Weyl points located at $\mathbf{k}_{W\pm} = (0, 0, \pm \frac{b_z}{\hbar v_z})$. These two nodes possess opposite chirality ($\chi=-1$ at $-\frac{b_z}{\hbar v_z}$ and $\chi=+1$ at $+\frac{b_z}{\hbar v_z}$). The momentum-space separation of the Weyl points is directly proportional to the strength of the TRS-breaking field. In more complex models that include a "tilt" term in the dispersion, such as $H_{tilt} = (\mathbf{t} \cdot \mathbf{k}) \mathbb{I}_{4 \times 4}$, this splitting in momentum space can also lead to a splitting in energy [@problem_id:1239179]. Specifically, if the tilt is described by a vector $\mathbf{t}=(t_x, t_y, t_z)$, the two Weyl points appear at energies $E_{W\pm} = \mathbf{t} \cdot \mathbf{k}_{W\pm}$, resulting in an energy difference of $\Delta E = \frac{2 b_z t_z}{\hbar v_z}$.

#### Breaking Inversion Symmetry

Alternatively, Weyl points can be generated by breaking inversion symmetry in a crystal that lacks a center of symmetry (i.e., is [non-centrosymmetric](@entry_id:157488)), even while preserving TRS.

Let us illustrate this with a simple model for a Dirac semimetal where the inversion operator is $P = \mathbb{I}_\sigma \otimes \tau_x$. An inversion-symmetric Hamiltonian $H_0(\mathbf{k})$ must satisfy $P H_0(\mathbf{k}) P^{-1} = H_0(-\mathbf{k})$. An IS-breaking term $H_{IB}$ is one that violates this condition. Consider the case where $H_0(\mathbf{k}) = v_f (\mathbf{k} \cdot \boldsymbol{\sigma}) \otimes \mathbb{I}_\tau$ and an IS-breaking perturbation is introduced of the form $H_{IB} = (\mathbf{b} \cdot \boldsymbol{\sigma}) \otimes \tau_z$, where $\mathbf{b}$ is a constant vector related to the spin-orbit interaction in a non-centrosymmetric lattice [@problem_id:1239185].

The total Hamiltonian $H(\mathbf{k}) = H_0(\mathbf{k}) + H_{IB}$ can be block-diagonalized in the basis of $\tau_z$ (eigenvalues $\lambda_\tau = \pm 1$):
$H(\mathbf{k}) = \begin{pmatrix} v_f(\mathbf{k}\cdot\boldsymbol{\sigma}) + (\mathbf{b}\cdot\boldsymbol{\sigma}) & 0 \\ 0 & v_f(\mathbf{k}\cdot\boldsymbol{\sigma}) - (\mathbf{b}\cdot\boldsymbol{\sigma}) \end{pmatrix} = \begin{pmatrix} H_+(\mathbf{k}) & 0 \\ 0 & H_-(\mathbf{k}) \end{pmatrix}$.

Each block is a Weyl Hamiltonian, $H_\pm(\mathbf{k}) = \boldsymbol{\sigma} \cdot (v_f \mathbf{k} \pm \mathbf{b})$. The nodes are located where the vector coefficient of $\boldsymbol{\sigma}$ vanishes. This gives two Weyl points at positions $\mathbf{k}_{\pm} = \mp \frac{\mathbf{b}}{v_f}$. The original Dirac point at $\mathbf{k}=0$ is thus split into two Weyl points separated in momentum by the vector $\Delta\mathbf{k} = \mathbf{k}_- - \mathbf{k}_+ = \frac{2\mathbf{b}}{v_f}$. In this case, TRS is preserved. TRS requires that for every Weyl point with chirality $\chi$ at momentum $\mathbf{k}$, there must exist another point with [chirality](@entry_id:144105) $-\chi$ at momentum $-\mathbf{k}$. The pair we found at $\pm\mathbf{b}/v_f$ may have the same [chirality](@entry_id:144105), implying the existence of another pair with opposite chirality elsewhere in the Brillouin zone to satisfy the constraint imposed by TRS.

#### Merging Weyl Points: Topological Phase Transitions

Just as Weyl points can be created by breaking symmetries, they can be annihilated or merged by tuning system parameters. Such a merger represents a [topological phase transition](@entry_id:137214). For instance, a system can transition from a Weyl semimetal to a Dirac semimetal, or to a trivial or topological insulator.

Consider a system described by a Hamiltonian that contains both a TRS-breaking term proportional to a parameter $\delta$ and an IS-breaking term $m$ [@problem_id:1239156]. In such a case, a pair of Weyl points may exist, for example, on the $k_z$ axis at positions $k_z = \pm \frac{\sqrt{\delta^2 - m^2}}{v_z}$. The existence of these real-valued solutions for $k_z$ requires that $|\delta| > |m|$. The separation of the nodes is $2\frac{\sqrt{\delta^2-m^2}}{v_z}$.

If an external parameter, such as [hydrostatic pressure](@entry_id:141627) $P$, can tune the value of the mass term, for instance via a linear relation $m(P) = m_0 - \alpha P$, it becomes possible to control the node separation. As pressure is increased, $|m(P)|$ can be made to approach $|\delta|$. The Weyl points will move closer to each other, and at a critical pressure $P_c$ where $|m(P_c)| = |\delta|$, the separation vanishes. At this point, the two Weyl points merge at the $\Gamma$ point ($\mathbf{k}=0$), annihilating each other and forming a single, four-fold degenerate Dirac point. This marks a [topological phase transition](@entry_id:137214) from a Weyl semimetal to a Dirac semimetal. Increasing the pressure further such that $|m(P)| > |\delta|$ can open a full band gap, transitioning the system into an insulating state.

### Electronic and Spectral Properties of Weyl Semimetals

The unique band structure of Weyl semimetals gives rise to a host of distinctive spectral features, both in the bulk and on the surface.

#### Dispersion and Density of States

The defining feature of a Weyl point is the linear dispersion of energy with momentum. For a single, isotropic **type-I** Weyl node at $E=0, \mathbf{k}=0$, the [dispersion relation](@entry_id:138513) for the two touching bands is $E_\pm(\mathbf{k}) = \pm \hbar v_F |\mathbf{k}|$, where $v_F$ is the Fermi velocity. This linear dispersion has a direct consequence on the **density of states (DOS)**, which is the number of available [electronic states](@entry_id:171776) per unit energy per unit volume.

The number of states within a sphere of radius $k$ in [momentum space](@entry_id:148936) is $N(k) = \frac{1}{(2\pi)^3} \frac{4}{3}\pi k^3$ (accounting for a single two-fold degenerate cone). Using the [dispersion relation](@entry_id:138513) $k = |E|/(\hbar v_F)$, we find the number of states with energy less than $|E|$ is $N(E) = \frac{E^3}{6\pi^2(\hbar v_F)^3}$. The DOS is then given by $g(E) = \frac{dN}{dE}$, which yields:
$g(E) = \frac{E^2}{2\pi^2(\hbar v_F)^3}$.
This quadratic dependence of the DOS on energy, vanishing at the nodal point, is a hallmark of type-I Weyl semimetals.

In many real materials, the Weyl cone is not isotropic but is "tilted" along a certain direction. A tilt is described by an additional term in the Hamiltonian, $H_{tilt} = \hbar (\mathbf{w} \cdot \mathbf{k}) \mathbb{I}_2$. For a tilt along the $z$-direction with velocity $w_z$, the dispersion becomes $E_\pm(\mathbf{k}) = \hbar w_z k_z \pm \hbar v_F |\mathbf{k}|$. The cone is classified as type-I if the tilt is "subluminal" ($|w_z|  v_F$), ensuring the constant-energy surfaces are closed ellipsoids. If the tilt is "superluminal" ($|w_z| > v_F$), the constant-energy surfaces become open hyperboloids, defining a **type-II** Weyl semimetal with drastically different properties, including a finite DOS at the nodal energy. For a type-I cone, the tilt modifies the DOS, enhancing it by a factor that depends on the tilt velocity [@problem_id:1239196]. The DOS for a single tilted cone becomes:
$g(E) = \frac{E^2}{2\pi^2(\hbar v_F)^3(1 - w_z^2/v_F^2)^2}$.

The concept can be further generalized to **multi-Weyl [semimetals](@entry_id:152277)**, where the dispersion around the node is linear in one direction but anisotropic and of higher order in the perpendicular plane. For instance, a hypothetical isotropic double-Weyl node ($C=\pm2$) with a quadratic dispersion $E(\mathbf{k}) = \pm \alpha k^2$ would exhibit a completely different DOS, scaling as $g(E) \propto \sqrt{E}$ [@problem_id:1239092]. This illustrates the sensitive dependence of thermodynamic properties on the precise form of the band dispersion.

#### The Bulk-Boundary Correspondence: Fermi Arc Surface States

Perhaps the most celebrated feature of Weyl semimetals is the manifestation of their non-trivial bulk topology at their surfaces. The **bulk-boundary correspondence** dictates that at the interface between a WSM and a topologically trivial material (such as vacuum or a normal insulator), there must exist protected metallic surface states.

These states are known as **Fermi arcs**. Unlike the closed Fermi surfaces of conventional metals, Fermi arcs are open segments in the surface Brillouin zone that connect the projections of bulk Weyl points of opposite [chirality](@entry_id:144105). They are a direct consequence of the chiral nature of the Weyl nodes and cannot be removed without closing the bulk band gap.

The wavefunctions of these [surface states](@entry_id:137922) are localized at the boundary and decay exponentially into the bulk. We can calculate the [characteristic decay length](@entry_id:183295), or **[penetration depth](@entry_id:136478)** $\xi$, of these states. For a semi-infinite sample occupying the region $x > 0$, we look for zero-energy solutions of the Hamiltonian where the momentum component $k_x$ is replaced by the operator $-i\partial_x$. Assuming a solution of the form $\psi(x) \propto e^{-\kappa x}$ (where $\kappa = 1/\xi$), we replace $k_x$ with an imaginary momentum $i\kappa$. Solving the condition for a zero-energy state, $\det(H(i\kappa, k_y, k_z)) = 0$, allows us to determine $\kappa$ as a function of the surface momenta $(k_y, k_z)$ [@problem_id:1239085, @problem_id:1239120]. For example, in a simple model described by $H = v(k_x\sigma_x + k_y\sigma_y) + (m-tk_z^2)\sigma_z$, the [penetration depth](@entry_id:136478) at a specific point on the Fermi arc can be found to be $\xi = \frac{3v}{2m}$ [@problem_id:1239085]. The [penetration depth](@entry_id:136478) is generally dependent on the position along the arc, diverging as the surface momentum approaches the projection of a bulk Weyl node.

### Topological Response and Transport Signatures

The unique topological and electronic structure of Weyl semimetals gives rise to a set of extraordinary transport phenomena that serve as their experimental fingerprints.

#### The Chiral Anomaly and Charge Pumping

In [high-energy physics](@entry_id:181260), the **[chiral anomaly](@entry_id:142077)** refers to the quantum-mechanical breakdown of the classical conservation law for chiral charge. In a WSM, this phenomenon manifests as a transfer of electrons between Weyl nodes of opposite [chirality](@entry_id:144105) under the application of parallel electric ($\mathbf{E}$) and magnetic ($\mathbf{B}$) fields. This process is often called **chiral charge pumping**.

When a magnetic field $\mathbf{B}=B\hat{z}$ is applied, the electronic spectrum quantizes into Landau levels. A special feature of Weyl nodes is the existence of a **zeroth Landau level (ZLL)** that is chiral and has a linear dispersion only along the direction of the magnetic field, $E_0^\chi(k_z) \propto \chi k_z$. These ZLLs act as one-dimensional, perfectly transmitting channels for chiral fermions. An electric field $\mathbf{E}=E\hat{z}$ applied parallel to $\mathbf{B}$ accelerates electrons along these 1D channels according to the semiclassical [equation of motion](@entry_id:264286) $\hbar \dot{k}_z = -eE$.

For the node with chirality $\chi=+1$, electrons are pumped in one direction along $k_z$, while for the node with $\chi=-1$, they are pumped in the opposite direction. The result is a continuous flow of electrons from the valence band of one Weyl cone to the conduction band of the other, leading to a net generation of chiral charge $Q_5 = N_+ - N_-$. The number of available states in each ZLL per unit area is given by the Landau level degeneracy, $g = B/\Phi_0 = eB/(2\pi\hbar)$, where $\Phi_0$ is the [magnetic flux quantum](@entry_id:136429). Combining the rate of change of momentum with the density of states in $k$-space gives the net rate of chiral charge generation per unit volume [@problem_id:1239155]:
$\frac{1}{V}\frac{dQ_5}{dt} = \frac{e^2}{2\pi^2\hbar^2} \mathbf{E} \cdot \mathbf{B}$.
This anomalous charge pumping leads to a large [negative longitudinal magnetoresistance](@entry_id:146729), a key experimental signature of the [chiral anomaly](@entry_id:142077) in WSMs.

#### Anomalous Hall Effect and Axion Electrodynamics

In WSMs where [time-reversal symmetry](@entry_id:138094) is broken, the momentum-space separation of Weyl nodes acts as a source of net Berry curvature flux. This intrinsic Berry curvature endows electrons with an [anomalous velocity](@entry_id:146502) component transverse to an applied electric field, resulting in an **anomalous Hall effect (AHE)** even in the absence of a magnetic field.

The intrinsic anomalous Hall conductivity (AHC) is a topological quantity directly proportional to the momentum-space separation of the Weyl nodes. For a pair of nodes located at $\mathbf{k}_{W,1}$ and $\mathbf{k}_{W,2}$, the [conductivity tensor](@entry_id:155827) component $\sigma_{xy}$ is given by:
$\sigma_{xy} = \frac{e^2}{h} \frac{(\mathbf{k}_{W,2} - \mathbf{k}_{W,1})_z}{2\pi} = \frac{e^2}{4\pi^2\hbar} (\Delta k_z)$.
This formula provides a direct link between a macroscopic transport measurement and the microscopic separation of the topological charges in the Brillouin zone [@problem_id:1239201]. The magnitude of the AHC can be calculated from any low-energy model by first finding the locations of the Weyl points.

This phenomenology is part of a broader theoretical framework known as **[axion electrodynamics](@entry_id:144423)**. In this description, the electromagnetic response of the material is modified by a topological term involving a dynamical [axion](@entry_id:156508) field $\theta(\mathbf{x}, t)$. In a WSM, the spatial and temporal variations of $\theta$ are determined by the separation of Weyl nodes in momentum and energy:
$\nabla \theta = \sum_i \chi_i \mathbf{k}_i \equiv \mathbf{Q}$
$\frac{\partial \theta}{\partial t} = -\frac{1}{\hbar} \sum_i \chi_i E_i$.
The vector $\mathbf{Q}$, known as the axion vector, represents the momentum-space dipole moment of the chiral charges and is directly related to the AHC [@problem_id:1239205]. The time-dependent part is related to the [chiral anomaly](@entry_id:142077).

#### Quantum Interference Effects: Weak Antilocalization

The topology of a Weyl cone is also imprinted on quantum interference effects in transport. When an electron traverses a closed path in momentum space enclosing a Weyl node, its wavefunction acquires a geometric phase known as the **Berry phase**. For any closed loop on the Fermi surface surrounding a Weyl node, this Berry phase is equal to $\pi$.

This non-trivial phase has a profound impact on [quantum interference](@entry_id:139127) between time-reversed scattering paths. In conventional [disordered metals](@entry_id:145011), [constructive interference](@entry_id:276464) between such paths leads to enhanced backscattering, an effect called weak localization (WL). In a WSM, the additional $\pi$ Berry phase turns this interference destructive. This suppresses backscattering, thereby increasing conductivity. This phenomenon is termed **[weak antilocalization](@entry_id:144949) (WAL)**.

Applying an external magnetic field breaks the time-reversal symmetry of the interfering paths, quenching the WAL effect and causing the conductivity to decrease. This results in a characteristic negative magnetoconductivity. In a quasi-2D thin film subjected to a perpendicular magnetic field $B$, the correction to the conductivity $\Delta\sigma(B)$ can be described by the Hikami-Larkin-Nagaoka formula. In the low-field limit, this theory predicts a quadratic dependence on the magnetic field, $\Delta\sigma(B) \approx C B^2$. The coefficient $C$ is negative and depends on material parameters like the diffusion constant $D$ and phase coherence time $\tau_\phi$. A detailed analysis of the theory confirms this quadratic behavior and allows for the extraction of the coefficient $C$, providing a distinct experimental signature of the $\pi$ Berry phase associated with Weyl fermions [@problem_id:1239123].