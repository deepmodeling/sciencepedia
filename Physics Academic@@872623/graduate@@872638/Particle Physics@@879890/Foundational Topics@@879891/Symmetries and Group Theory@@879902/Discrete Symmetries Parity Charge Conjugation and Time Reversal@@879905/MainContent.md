## Introduction
In the quest to understand the fundamental laws of nature, symmetry principles serve as our most profound guides. Beyond the continuous symmetries of spacetime that lead to the conservation of energy and momentum, particle physics is governed by a set of [discrete symmetries](@entry_id:158714): Parity (P), the mirror-image reflection; Charge Conjugation (C), the exchange of particles and [antiparticles](@entry_id:155666); and Time Reversal (T), the reversal of motion. Initially presumed to be exact symmetries of nature, the discovery that some are violated shattered old paradigms and provided deep new insights into the structure of the Standard Model. This violation is not a flaw but a crucial feature of our universe, explaining phenomena from [particle decay](@entry_id:159938) patterns to the very existence of matter.

This article provides a comprehensive exploration of these three fundamental symmetries. It is structured to build a complete picture from first principles to real-world applications.
-   **Principles and Mechanisms** will delve into the theoretical framework of P, C, and T transformations in quantum [field theory](@entry_id:155241), examining how fields and physical observables behave and establishing the mathematical basis for their conservation or violation.
-   **Applications and Interdisciplinary Connections** will demonstrate how these principles are applied as powerful tools to set [selection rules](@entry_id:140784) in particle decays, probe the internal structure of hadrons, understand the phenomenon of CP violation, and connect particle physics to cosmology and [condensed matter](@entry_id:747660).
-   **Hands-On Practices** will offer a series of guided problems, allowing you to apply your understanding to concrete physical scenarios, from determining the fate of particle reactions to verifying the symmetry of interaction Lagrangians.

## Principles and Mechanisms

In our exploration of the fundamental constituents of nature, we find that the laws governing their interactions are constrained by profound symmetries. Beyond the continuous spacetime symmetries of the Poincaré group, which give rise to [conservation of energy](@entry_id:140514), momentum, and angular momentum, there exist [discrete symmetries](@entry_id:158714) whose study has revealed deep insights into the structure of the Standard Model and the universe itself. These are the symmetries of **Parity (P)**, or mirror reflection; **Charge Conjugation (C)**, the exchange of particles with [antiparticles](@entry_id:155666); and **Time Reversal (T)**, the reversal of the direction of motion. This chapter will systematically investigate the principles and mechanisms of these three fundamental discrete transformations.

### Parity: The Symmetry of Mirror Reflection

The **[parity transformation](@entry_id:159187)**, denoted by $\mathcal{P}$, is the inversion of all three spatial coordinates: $\vec{x} \to -\vec{x}$. It is the quantum mechanical equivalent of a mirror reflection combined with a 180-degree rotation. The spacetime [coordinate transformation](@entry_id:138577) is $x^\mu = (x^0, \vec{x}) \to x_P^\mu = (x^0, -\vec{x})$. A physical law is said to be parity-invariant if its form is unchanged by this transformation; the mirror-image of an experiment should be a possible experiment.

#### Transformation of Fields and Observables

How [physical quantities](@entry_id:177395) and the fields that describe them behave under parity determines whether an interaction conserves this symmetry. A scalar quantity, like mass, is unchanged. A classical vector like momentum $\vec{p}$ is odd under parity, $\vec{p} \to -\vec{p}$, since it is the derivative of position with respect to time. In contrast, [orbital angular momentum](@entry_id:191303), $\vec{L} = \vec{r} \times \vec{p}$, is even under parity: $\vec{L} \to (-\vec{r}) \times (-\vec{p}) = +\vec{L}$. This distinction gives rise to two classes of vector-like quantities.

*   **Polar vectors (or simply vectors)** transform like the [position vector](@entry_id:168381): $\vec{V} \to -\vec{V}$. Examples include position, momentum, and the electric field.
*   **Axial vectors (or pseudovectors)** transform like angular momentum: $\vec{A} \to +\vec{A}$. Examples include torque and the magnetic field.

In quantum [field theory](@entry_id:155241), fields are classified by their transformation properties. A [scalar field](@entry_id:154310) $\phi(x)$ transforms to $\phi(x_P)$, while a **pseudoscalar field** $\phi'(x)$ transforms to $-\phi(x_P)$. The distinction between vector and axial-vector fields is similarly crucial.

For Dirac fermions, described by the field $\psi(x)$, the [parity transformation](@entry_id:159187) is represented by a matrix acting on the spinor indices:
$$
\mathcal{P} \psi(t, \vec{x}) \mathcal{P}^{-1} = \eta_P \gamma^0 \psi(t, -\vec{x})
$$
where $\gamma^0$ is the time-like gamma matrix and $\eta_P$ is the **[intrinsic parity](@entry_id:157995)** of the fermion, a phase factor which can be chosen to be $+1$ by convention for leptons and quarks. The transformation of the adjoint spinor $\bar{\psi}(x) = \psi^\dagger(x) \gamma^0$ follows as $\mathcal{P} \bar{\psi}(x) \mathcal{P}^{-1} = \eta_P^* \bar{\psi}(x_P) \gamma^0$.

From these fundamental transformations, we can determine the parity of various fermion bilinears which form the currents of interactions.
*   Scalar: $\bar{\psi}\psi \xrightarrow{\mathcal{P}} \bar{\psi}(x_P)\gamma^0\gamma^0\psi(x_P) = \bar{\psi}(x_P)\psi(x_P)$ (even)
*   Pseudoscalar: $\bar{\psi}\gamma^5\psi \xrightarrow{\mathcal{P}} \bar{\psi}(x_P)\gamma^0\gamma^5\gamma^0\psi(x_P) = -\bar{\psi}(x_P)\gamma^5\psi(x_P)$ (odd)
*   Vector current: $\bar{\psi}\gamma^\mu\psi$. The time component $\bar{\psi}\gamma^0\psi = \psi^\dagger\psi$ is a [scalar density](@entry_id:161438) and is even. The spatial components $\bar{\psi}\gamma^i\psi$ are odd. This is the characteristic transformation of a [four-vector](@entry_id:160261).
*   Axial-vector current: $\bar{\psi}\gamma^\mu\gamma^5\psi$. The time component $\bar{\psi}\gamma^0\gamma^5\psi$ is odd, while the spatial components $\bar{\psi}\gamma^i\gamma^5\psi$ are even. This constitutes an axial [four-vector](@entry_id:160261).

A concrete example illustrates the difference between vector and axial-vector operators constructed from fermion fields [@problem_id:175718]. The spatial part of the fermion [spin operator](@entry_id:149715), $\vec{A}_S = \int d^3x \, \psi^\dagger \frac{\vec{\Sigma}}{2} \psi$, transforms as an [axial vector](@entry_id:191829) under parity. In contrast, the momentum operator, $\vec{V}_P = \int d^3x \, \psi^\dagger (\frac{1}{i}\vec{\nabla}) \psi$, transforms as a [polar vector](@entry_id:184542). The different behaviors stem from how the operators $\vec{\Sigma}$ and $\vec{\nabla}$ act under spatial inversion. The gradient $\vec{\nabla}$ flips sign, making $\vec{V}_P$ a [true vector](@entry_id:190731), while the spin matrices $\vec{\Sigma}$ commute with $\gamma^0$ and are invariant, making $\vec{A}_S$ an [axial vector](@entry_id:191829). A physical system whose dynamics are described by a [scalar product](@entry_id:175289) of a vector and an [axial vector](@entry_id:191829), such as $\vec{V}_P \cdot \vec{A}_S$, would necessarily violate parity, as the Lagrangian would acquire a minus sign under the transformation.

#### Parity Conservation and Violation

A theory is parity-conserving if its Lagrangian density $\mathcal{L}(x)$ transforms as a true scalar, i.e., $\mathcal{L}(x) \xrightarrow{\mathcal{P}} \mathcal{L}(x_P)$. This ensures the action $S = \int d^4x \, \mathcal{L}(x)$ is invariant. Electromagnetic and strong interactions conserve parity. However, the weak interaction famously violates it.

We can use the requirement of [parity conservation](@entry_id:160454) to constrain the structure of hypothetical theories. Consider an interaction between a fermion $\psi$ and a new [antisymmetric tensor](@entry_id:191090) field $B_{\mu\nu}$, described by $\mathcal{L}_{int} = g \, \bar{\psi}(x) \sigma^{\mu\nu} \psi(x) B_{\mu\nu}(x)$, where $\sigma^{\mu\nu} = \frac{i}{2}[\gamma^\mu, \gamma^\nu]$ [@problem_id:175727]. To check for parity invariance, we transform each piece. The fermion bilinear transforms as:
$$
\bar{\psi}(x) \sigma^{\mu\nu} \psi(x) \xrightarrow{\mathcal{P}} \bar{\psi}(x_P) \gamma^0 \sigma^{\mu\nu} \gamma^0 \psi(x_P)
$$
Using the identity $\gamma^0 \gamma^\mu \gamma^0 = (\Lambda_P)_\alpha^\mu \gamma^\alpha$, where $(\Lambda_P)_\mu^\nu = \text{diag}(1, -1, -1, -1)$, one can show that $\gamma^0\sigma^{\mu\nu}\gamma^0 = (\Lambda_P)_\alpha^\mu (\Lambda_P)_\beta^\nu \sigma^{\alpha\beta}$. The tensor field $B_{\mu\nu}$ transforms as $B_{\mu\nu}(x) \xrightarrow{\mathcal{P}} \eta_B (\Lambda_P)_\mu^\rho (\Lambda_P)_\nu^\sigma B_{\rho\sigma}(x_P)$, where $\eta_B$ is its [intrinsic parity](@entry_id:157995). The full Lagrangian density then transforms into:
$$
\mathcal{L}_{int}(x) \xrightarrow{\mathcal{P}} g \, \left[ \bar{\psi}(x_P) (\Lambda_P)_\alpha^\mu (\Lambda_P)_\beta^\nu \sigma^{\alpha\beta} \psi(x_P) \right] \left[ \eta_B (\Lambda_P)_\mu^\rho (\Lambda_P)_\nu^\sigma B_{\rho\sigma}(x_P) \right]
$$
Using the property $(\Lambda_P)_\alpha^\mu (\Lambda_P)_\mu^\rho = \delta_\alpha^\rho$, the Lorentz indices contract to give:
$$
\mathcal{L}_{int}(x) \xrightarrow{\mathcal{P}} \eta_B \, g \, \bar{\psi}(x_P) \sigma^{\rho\sigma} \psi(x_P) B_{\rho\sigma}(x_P) = \eta_B \, \mathcal{L}_{int}(x_P)
$$
For the action to be invariant, we require $\eta_B = +1$. This demonstrates how imposing a symmetry principle dictates the fundamental properties, such as [intrinsic parity](@entry_id:157995), of the fields involved.

### Charge Conjugation: The Symmetry of Antimatter

**Charge conjugation**, denoted by $\mathcal{C}$, is an operation that reverses all internal additive [quantum numbers](@entry_id:145558), such as electric charge, [baryon number](@entry_id:157941), and lepton number, without affecting spacetime coordinates or momentum. A particle is transformed into its corresponding [antiparticle](@entry_id:193607).

The action of $\mathcal{C}$ on fields that carry charge is non-trivial. The photon field $A_\mu$, sourced by the electric current, must flip its sign: $\mathcal{C} A_\mu(x) \mathcal{C}^{-1} = -A_\mu(x)$. For a Dirac fermion field $\psi$, the transformation is:
$$
\mathcal{C} \psi(x) \mathcal{C}^{-1} = \eta_C C \bar{\psi}^T(x) \quad \text{and} \quad \mathcal{C} \bar{\psi}(x) \mathcal{C}^{-1} = -\eta_C^* \psi^T(x) C^{-1}
$$
where $C$ is the [charge conjugation](@entry_id:158278) matrix satisfying $C^{-1}\gamma^\mu C = -(\gamma^\mu)^T$, and $\eta_C$ is a phase factor, usually set to one.

The QED interaction Lagrangian, $\mathcal{L}_{\text{int}} = e \bar{\psi} \gamma^\mu \psi A_\mu$, provides a crucial test of C-invariance. Under [charge conjugation](@entry_id:158278), the electromagnetic field, being sourced by the charge current, must flip its sign: $\mathcal{C} A_\mu(x) \mathcal{C}^{-1} = -A_\mu(x)$. The fermion vector current $j^\mu = \bar{\psi} \gamma^\mu \psi$ also transforms. Using the transformation rules for the fermion fields, one can show that the current flips sign:
$$
\mathcal{C} j^\mu(x) \mathcal{C}^{-1} = \mathcal{C} (\bar{\psi}\gamma^\mu\psi)(x) \mathcal{C}^{-1} = -\bar{\psi}\gamma^\mu\psi(x) = -j^\mu(x)
$$
This sign change is a subtle but essential consequence of the anti-commuting nature of fermion fields. When transforming the fields and reordering them back into the original form, an extra minus sign is generated. Therefore, the full Lagrangian density transforms as:
$$
\mathcal{C} \mathcal{L}_{\text{int}} \mathcal{C}^{-1} = e (\mathcal{C} \bar{\psi}\gamma^\mu\psi \mathcal{C}^{-1}) (\mathcal{C} A_\mu \mathcal{C}^{-1}) = e (- \bar{\psi}\gamma^\mu\psi) (-A_\mu) = e \bar{\psi}\gamma^\mu\psi A_\mu = \mathcal{L}_{\text{int}}
$$
The Lagrangian is invariant. This confirms that QED is C-conserving. Hypothetical theories involving "commuting [spinors](@entry_id:158054)" would not possess this invariance, highlighting the fundamental role of fermion statistics [@problem_id:175717].

In contrast, the [weak interaction](@entry_id:152942) is not C-invariant; it is maximally C-violating. The weak force couples to **chiral currents**. A left-chiral current is $J_L^\mu = \bar{\psi}_L \gamma^\mu \psi_L$. Using the projector $P_L = \frac{1}{2}(1 - \gamma^5)$, we can decompose this into vector and axial-vector parts: $J_L^\mu = \frac{1}{2}(\bar{\psi}\gamma^\mu\psi - \bar{\psi}\gamma^\mu\gamma^5\psi)$. Under [charge conjugation](@entry_id:158278), the vector current is odd ($V \to -V$) but the axial-vector current is even ($A \to +A$). Applying this to the left-chiral current gives [@problem_id:175704]:
$$
(J_L^\mu)^C = \frac{1}{2} \left( -(\bar{\psi}\gamma^\mu\psi) - (+\bar{\psi}\gamma^\mu\gamma^5\psi) \right) = -\frac{1}{2}(\bar{\psi}\gamma^\mu\psi + \bar{\psi}\gamma^\mu\gamma^5\psi) = -J_R^\mu
$$
Charge conjugation transforms a left-chiral current into a right-chiral current. Since the [weak interaction](@entry_id:152942) couples only to left-chiral fermions (and right-chiral anti-fermions), the C-transformed world, which would feature weak interactions for right-chiral fermions, does not exist. The symmetry is broken in the most extreme way possible.

### Time Reversal: Reversing the Flow of Causality

**Time reversal**, denoted by $\mathcal{T}$, reverses the direction of [time evolution](@entry_id:153943): $t \to -t, \vec{x} \to \vec{x}$. Classically, this reverses momentum ($\vec{p} \to -\vec{p}$) and angular momentum ($\vec{L} \to -\vec{L}$) but leaves position ($\vec{r} \to \vec{r}$) unchanged. In quantum mechanics, for the Schrödinger equation $i\hbar \frac{\partial}{\partial t}|\psi\rangle = H|\psi\rangle$ to be covariant under [time reversal](@entry_id:159918), the operator $\mathcal{T}$ must be **anti-unitary**. This means it involves [complex conjugation](@entry_id:174690): $\mathcal{T} c \mathcal{T}^{-1} = c^*$ for any complex number $c$. This ensures that $i\hbar \to -i\hbar$, which combines with $\frac{\partial}{\partial t} \to -\frac{\partial}{\partial t}$ to leave the equation's structure intact if the Hamiltonian is T-invariant, $[H, \mathcal{T}]=0$.

The anti-unitary nature of $\mathcal{T}$ has direct consequences for [observables](@entry_id:267133). For the orbital [angular momentum operator](@entry_id:155961) $\vec{L} = \vec{r} \times \vec{p}$, its transformation is [@problem_id:175712]:
$$
\mathcal{T} \vec{L} \mathcal{T}^{-1} = \mathcal{T} (\vec{r} \times \vec{p}) \mathcal{T}^{-1} = (\mathcal{T}\vec{r}\mathcal{T}^{-1}) \times (\mathcal{T}\vec{p}\mathcal{T}^{-1}) = (+\vec{r}) \times (-\vec{p}) = -\vec{L}
$$
The transformation correctly reproduces the classical expectation that angular momentum is odd under [time reversal](@entry_id:159918). Similarly, spin $\vec{S}$ is also T-odd. In contrast, the electric field $\vec{E}$ is T-even, while the magnetic field $\vec{B}$ is T-odd.

The possible existence of a permanent **electric dipole moment (EDM)** for a fundamental particle like an electron or a neutron is a powerful probe for T-violation. A particle's EDM must be aligned with its spin, $\vec{d} \propto \vec{S}$. The interaction energy of an EDM with an electric field is $-\vec{d} \cdot \vec{E}$. If this term were in the Hamiltonian, it would transform under T as:
$$
H_{EDM} = -\vec{d} \cdot \vec{E} \propto -\vec{S} \cdot \vec{E} \xrightarrow{\mathcal{T}} -(-\vec{S}) \cdot (+\vec{E}) = +\vec{S} \cdot \vec{E} = -H_{EDM}
$$
A Hamiltonian containing such a term cannot be T-invariant. In QFT, this interaction is described by a Lagrangian term $\mathcal{L}_{\text{EDM}} = -i \frac{d}{2} \bar{\psi} \sigma^{\mu\nu}\gamma^5\psi F_{\mu\nu}$ [@problem_id:175729]. Under time reversal, the anti-unitary nature of $\mathcal{T}$ conjugates the explicit factor of $i$, turning $-i$ to $+i$. The fermion bilinear $\bar{\psi} \sigma^{\mu\nu}\gamma^5\psi$ and the [field tensor](@entry_id:186486) $F_{\mu\nu}$ have components that transform in a coordinated way such that their contraction $\bar{\psi} \sigma^{\mu\nu}\gamma^5\psi F_{\mu\nu}$ is even under T. The net effect is that the Lagrangian density flips its sign: $\mathcal{L}'_{\text{EDM}}(x') = - \mathcal{L}_{\text{EDM}}(x)$. This demonstrates explicitly that an EDM violates [time-reversal symmetry](@entry_id:138094).

A remarkable consequence of [time-reversal invariance](@entry_id:152159) in systems with a half-integer [total spin](@entry_id:153335) (i.e., an odd number of fermions) is **Kramers' degeneracy**. For such systems, the time-reversal operator has the property $\mathcal{T}^2 = -1$. If $|\psi\rangle$ is an energy [eigenstate](@entry_id:202009) of a T-invariant Hamiltonian $H$, then so is $|\mathcal{T}\psi\rangle$ with the same energy. Furthermore, these two states are necessarily orthogonal. We can show this using the properties of the [anti-unitary operator](@entry_id:149378) $\mathcal{T}$. For a system where $\mathcal{T}^2=-1$, we have $\mathcal{T}^{-1} = -\mathcal{T}$. Using the defining property of an [anti-unitary operator](@entry_id:149378), $\langle\phi | \mathcal{T}\psi \rangle = \langle \mathcal{T}^{-1}\phi | \psi \rangle^*$, we can prove orthogonality as follows:
$$
\langle\psi | \mathcal{T}\psi \rangle = \langle \mathcal{T}^{-1}\psi | \psi \rangle^* = \langle -\mathcal{T}\psi | \psi \rangle^* = - \langle \mathcal{T}\psi | \psi \rangle^*
$$
We also know that for any inner product, $\langle \mathcal{T}\psi | \psi \rangle = \langle \psi | \mathcal{T}\psi \rangle^*$. Substituting this into the previous equation gives:
$$
\langle\psi | \mathcal{T}\psi \rangle = - (\langle \psi | \mathcal{T}\psi \rangle^*)^* = - \langle \psi | \mathcal{T}\psi \rangle
$$
This implies $2 \langle \psi | \mathcal{T}\psi \rangle = 0$, and thus $\langle \psi | \mathcal{T}\psi \rangle = 0$.
Therefore, $|\psi\rangle$ and $|\mathcal{T}\psi\rangle$ are distinct, orthogonal states with the same energy. Every energy level in such a system must be at least doubly degenerate. This **Kramers' degeneracy** is a robust prediction, exemplified in the electronic structure of atoms and materials with unpaired electrons in the absence of a magnetic field [@problem_id:175730].

### Combined Symmetries: CP and CPT

While P and C are individually violated by the weak interaction, it was initially thought that their combination, **CP**, might be an exact symmetry. CP transforms a particle into its [antiparticle](@entry_id:193607) and takes the mirror image. This symmetry is also violated, albeit at a much smaller level, as first observed in the decay of [neutral kaons](@entry_id:159316).

The Standard Model contains a possible source of CP violation in the strong sector, known as the QCD theta-term, $\mathcal{L}_{\theta} \propto \theta G_{\mu\nu}^a \tilde{G}^{a, \mu\nu}$, where $\tilde{G}$ is the dual [field strength tensor](@entry_id:159746) [@problem_id:175706]. The operator $\mathcal{O} = G_{\mu\nu}^a \tilde{G}^{a, \mu\nu}$ is a product of the [gluon](@entry_id:159508) field strength and its dual. Under parity, one can show that $G$ transforms into a tensor of the same rank, but the Levi-Civita tensor in the definition of the dual, $\tilde{G}$, picks up a factor of $\det(\Lambda_P)=-1$. This makes the operator $\mathcal{O}$ a [pseudoscalar](@entry_id:196696): $\mathcal{P}[\mathcal{O}](x) = -\mathcal{O}(x_P)$. Under [charge conjugation](@entry_id:158278), the gluon fields $G_{\mu\nu}^a$ are in the adjoint representation and are their own [antiparticles](@entry_id:155666), transforming like photons, $C[G_{\mu\nu}^a] = -G_{\mu\nu}^a$. The operator $\mathcal{O}$, being bilinear in $G$, is therefore C-even: $C[\mathcal{O}](x) = +\mathcal{O}(x)$. Combining these, we see the theta-term is CP-odd: $(CP)[\mathcal{O}](x) = -\mathcal{O}(x_P)$. A non-zero value of the parameter $\theta$ would signal strong CP violation, which is experimentally constrained to be extremely small, leading to the "strong CP problem."
The transformation properties of other bilinears under combined symmetries can also be determined. For instance, the fermionic tensor current $J^{\mu\nu} = \bar{\psi} \sigma^{\mu\nu} \psi$ is P-even (transforming as a [rank-2 tensor](@entry_id:187697)) but C-odd, making it CP-odd [@problem_id:175742].

#### The CPT Theorem

The most resilient of all [discrete symmetries](@entry_id:158714) is the combination of all three: **CPT**. The **CPT theorem**, a cornerstone of quantum field theory, states that any Lorentz-invariant, local QFT with a Hermitian Hamiltonian must be invariant under the combined transformation of C, P, and T. This is not an empirical law that might be broken, but a mathematical consequence of the axioms of QFT.

CPT invariance has profound physical consequences.
1.  **Equality of Particle-Antiparticle Properties:** A particle and its antiparticle must have exactly the same mass and total decay width (and thus the same lifetime). This holds even if C, P, T, and any of their pairings are violated. For a decay process $F \to f^- S^+$, even with complex couplings that violate symmetries, CPT invariance guarantees that the total decay rate is identical to that of the antiparticle process $\bar{F} \to f^+ S^-$ [@problem_id:175739]. Any observed difference in mass or lifetime between a particle and its antiparticle would shatter the foundations of local quantum [field theory](@entry_id:155241).

2.  **Relation Between Scattering Cross Sections:** CPT invariance relates the matrix element for a process $A+B \to C+D$ to its CPT-conjugate process, $\bar{C}+\bar{D} \to \bar{A}+\bar{B}$. The theorem states that their polarized amplitudes are equal (up to a phase) if one also reverses the spin projections. When calculating total unpolarized cross sections, one must sum over final spins and average over initial spins. This leads to a relationship between the cross sections that is not equality, but is fixed by spin and kinematic factors [@problem_id:175676]. For a $2 \to 2$ process at a given [center-of-mass energy](@entry_id:265852) squared $s$, the ratio of the cross sections is:
$$
\frac{\sigma_{tot}(A+B \to C+D)}{\sigma_{tot}(\bar{C}+\bar{D} \to \bar{A}+\bar{B})} = \frac{(2S_C+1)(2S_D+1)}{(2S_A+1)(2S_B+1)} \frac{|\vec{p}_{CD}|^2}{|\vec{p}_{AB}|^2}
$$
where $g_i = 2S_i+1$ are the spin degeneracy factors and $|\vec{p}_{ij}|$ are the magnitudes of the momenta in the CM frame. This precise relationship provides another stringent test of the CPT theorem.

The observed CP violation in the universe, coupled with the assumption of CPT invariance, implies that there must also be T violation. The study of these [discrete symmetries](@entry_id:158714), their conservation and violation, thus continues to be a crucial frontier in our quest to understand the fundamental laws of nature.