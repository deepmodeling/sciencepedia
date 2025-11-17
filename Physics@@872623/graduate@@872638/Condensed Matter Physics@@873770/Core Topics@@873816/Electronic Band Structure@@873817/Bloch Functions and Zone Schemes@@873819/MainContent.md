## Introduction
Understanding the behavior of electrons in the [periodic potential](@entry_id:140652) of a crystal lattice is the central task of solid-state physics. The immense complexity of a solid, with its interacting electrons and ions, seems to present an intractable quantum mechanical problem. The key to simplifying this challenge lies in the crystal's defining feature: its translational symmetry. Bloch's theorem and the resulting framework of [electronic band theory](@entry_id:182196) provide the fundamental language for describing how this symmetry shapes the quantum states of electrons, ultimately determining whether a material is a metal, an insulator, or a semiconductor. This article delves into the core principles of Bloch functions and the various [zone schemes](@entry_id:147728) used to represent the [electronic band structure](@entry_id:136694).

This article addresses the fundamental gap between the abstract Schrödinger equation and the tangible electronic properties of materials. We will unpack how the seemingly simple constraint of lattice [periodicity](@entry_id:152486) leads to the rich and [complex structure](@entry_id:269128) of [electronic bands](@entry_id:175335), gaps, and momenta. The journey will begin in the first chapter, "Principles and Mechanisms," where we derive Bloch's theorem from first principles, introduce the crucial concept of the reciprocal lattice and Brillouin zones, and explore how band structures are formed and represented. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate how this theoretical framework is used to interpret experiments, engineer materials like [superlattices](@entry_id:200197), and understand advanced concepts such as Bloch oscillations and the modern [topological classification](@entry_id:154529) of matter. Finally, "Hands-On Practices" will offer a series of guided problems to build a working, quantitative command of these essential concepts.

## Principles and Mechanisms

### The Consequence of Lattice Periodicity: Bloch's Theorem

The defining characteristic of a crystalline solid is the spatial [periodicity](@entry_id:152486) of its atomic arrangement. This [periodicity](@entry_id:152486) is described by a **Bravais lattice**, which is the set of all vectors $\mathbf{R}$ of the form $\mathbf{R} = n_1 \mathbf{a}_1 + n_2 \mathbf{a}_2 + n_3 \mathbf{a}_3$, where $\mathbf{a}_i$ are the [primitive lattice vectors](@entry_id:270646) and $n_i$ are integers. In the single-particle approximation, an electron moves in an effective potential $V(\mathbf{r})$ that possesses the same periodicity as the lattice:
$$
V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r}) \quad \text{for all } \mathbf{R} \text{ in the Bravais lattice.}
$$
This discrete translational symmetry is the central principle from which the entire framework of [electronic band theory](@entry_id:182196) originates. The single-particle Hamiltonian, $\hat{H} = \frac{\hat{\mathbf{p}}^2}{2m} + V(\mathbf{r})$, is invariant under translation by any lattice vector $\mathbf{R}$. To see this, we introduce the **[translation operator](@entry_id:756122)** $\hat{T}_{\mathbf{R}}$, defined by its action on an arbitrary function $f(\mathbf{r})$ as $\hat{T}_{\mathbf{R}} f(\mathbf{r}) = f(\mathbf{r} + \mathbf{R})$. The kinetic energy operator $\hat{\mathbf{p}}^2$ commutes with all translation operators, and the potential energy operator $V(\mathbf{r})$ commutes with $\hat{T}_{\mathbf{R}}$ by definition of its periodicity. Therefore, the Hamiltonian commutes with the set of all lattice translation operators:
$$
[\hat{H}, \hat{T}_{\mathbf{R}}] = 0 \quad \text{for all } \mathbf{R}.
$$
Since all translation operators $\hat{T}_{\mathbf{R}}$ also commute with each other, it is possible to find a common set of eigenfunctions for $\hat{H}$ and all $\hat{T}_{\mathbf{R}}$. Let $\psi(\mathbf{r})$ be such an [eigenfunction](@entry_id:149030). Its [eigenvalue equation](@entry_id:272921) for the [translation operator](@entry_id:756122) is:
$$
\hat{T}_{\mathbf{R}} \psi(\mathbf{r}) = \psi(\mathbf{r} + \mathbf{R}) = C_{\mathbf{R}} \psi(\mathbf{r}).
$$
The eigenvalues $C_{\mathbf{R}}$ must satisfy the group property $C_{\mathbf{R}_1} C_{\mathbf{R}_2} = C_{\mathbf{R}_1 + \mathbf{R}_2}$. Combined with the unitarity of $\hat{T}_{\mathbf{R}}$ (which implies $|C_{\mathbf{R}}|=1$ for normalization), the only possible solution for the eigenvalues is $C_{\mathbf{R}} = \exp(i\mathbf{k} \cdot \mathbf{R})$ for some real vector $\mathbf{k}$. This leads to the first statement of **Bloch's theorem**: the [eigenfunctions](@entry_id:154705) of a periodic Hamiltonian can be chosen to satisfy
$$
\psi_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{i\mathbf{k} \cdot \mathbf{R}} \psi_{\mathbf{k}}(\mathbf{r}).
$$
The vector $\mathbf{k}$ is known as the **[crystal momentum](@entry_id:136369)** and serves as a quantum number labeling the state. From a group-theoretic perspective, the [crystal momentum](@entry_id:136369) $\mathbf{k}$ labels the one-dimensional [irreducible representations](@entry_id:138184) of the crystal's discrete translation group [@problem_id:2972358].

An equivalent and often more intuitive form of Bloch's theorem can be derived by defining a new function $u_{\mathbf{k}}(\mathbf{r}) = e^{-i\mathbf{k} \cdot \mathbf{r}} \psi_{\mathbf{k}}(\mathbf{r})$. Examining its behavior under a lattice translation, we find:
$$
u_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{-i\mathbf{k} \cdot (\mathbf{r}+\mathbf{R})} \psi_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{-i\mathbf{k} \cdot \mathbf{r}} e^{-i\mathbf{k} \cdot \mathbf{R}} \left( e^{i\mathbf{k} \cdot \mathbf{R}} \psi_{\mathbf{k}}(\mathbf{r}) \right) = e^{-i\mathbf{k} \cdot \mathbf{r}} \psi_{\mathbf{k}}(\mathbf{r}) = u_{\mathbf{k}}(\mathbf{r}).
$$
This shows that $u_{\mathbf{k}}(\mathbf{r})$ is a **cell-periodic function**, possessing the full [periodicity](@entry_id:152486) of the Bravais lattice. The eigenfunction can thus be expressed in the famous **Bloch form**:
$$
\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k} \cdot \mathbf{r}} u_{n\mathbf{k}}(\mathbf{r}).
$$
Here, we have added a **band index** $n$, which arises because for a given $\mathbf{k}$, there are generally many different solutions $u_{n\mathbf{k}}(\mathbf{r})$ corresponding to different [energy eigenvalues](@entry_id:144381) $E_n(\mathbf{k})$ [@problem_id:2972343].

It is crucial to distinguish crystal momentum $\hbar\mathbf{k}$ from the mechanical momentum of the electron, represented by the operator $\hat{\mathbf{p}} = -i\hbar\boldsymbol{\nabla}$. Applying $\hat{\mathbf{p}}$ to a Bloch function yields:
$$
\hat{\mathbf{p}} \psi_{n\mathbf{k}}(\mathbf{r}) = \hat{\mathbf{p}} \left( e^{i\mathbf{k} \cdot \mathbf{r}} u_{n\mathbf{k}}(\mathbf{r}) \right) = \hbar\mathbf{k} \psi_{n\mathbf{k}}(\mathbf{r}) + e^{i\mathbf{k} \cdot \mathbf{r}} (-i\hbar\boldsymbol{\nabla}) u_{n\mathbf{k}}(\mathbf{r}).
$$
A Bloch state is not an eigenstate of the [momentum operator](@entry_id:151743) unless the cell-periodic part $u_{n\mathbf{k}}(\mathbf{r})$ is a constant, which is only true for a free electron in the absence of a potential. The expectation value of the mechanical momentum, $\langle\psi_{n\mathbf{k}} | \hat{\mathbf{p}} | \psi_{n\mathbf{k}}\rangle$, is not generally equal to $\hbar\mathbf{k}$. This reflects the fact that in a [periodic potential](@entry_id:140652), continuous translational symmetry is broken, and thus mechanical momentum is not a conserved quantity. Crystal momentum, however, plays the role of the conserved quantity associated with the *discrete* [translational symmetry](@entry_id:171614) of the lattice [@problem_id:2972358].

### The Reciprocal Lattice and Brillouin Zones

The definition of crystal momentum $\mathbf{k}$ through the phase factor $\exp(i\mathbf{k} \cdot \mathbf{R})$ has a profound consequence: it is not uniquely defined. To see this, we introduce the **[reciprocal lattice](@entry_id:136718)**, which is the set of all vectors $\mathbf{G}$ satisfying the condition:
$$
e^{i\mathbf{G} \cdot \mathbf{R}} = 1 \quad \text{for all direct lattice vectors } \mathbf{R}.
$$
This condition is equivalent to $\mathbf{G} \cdot \mathbf{R} = 2\pi m$, where $m$ is an integer. The [reciprocal lattice](@entry_id:136718) is itself a Bravais lattice, generated by primitive reciprocal vectors $\mathbf{b}_j$ which are related to the [direct lattice](@entry_id:748468) [primitive vectors](@entry_id:142930) $\mathbf{a}_i$ by the relation $\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi \delta_{ij}$.

Now, consider replacing $\mathbf{k}$ with $\mathbf{k}' = \mathbf{k} + \mathbf{G}$, where $\mathbf{G}$ is any reciprocal lattice vector. The phase factor in Bloch's theorem becomes:
$$
e^{i\mathbf{k}' \cdot \mathbf{R}} = e^{i(\mathbf{k}+\mathbf{G}) \cdot \mathbf{R}} = e^{i\mathbf{k} \cdot \mathbf{R}} e^{i\mathbf{G} \cdot \mathbf{R}} = e^{i\mathbf{k} \cdot \mathbf{R}}.
$$
The phase factor is unchanged. This means that $\mathbf{k}$ and $\mathbf{k}+\mathbf{G}$ are equivalent labels for the translational properties of an eigenstate. All physically distinct states can therefore be described by restricting $\mathbf{k}$ to a single primitive cell of the reciprocal lattice. By convention, this [primitive cell](@entry_id:136497) is chosen as the Wigner-Seitz cell of the reciprocal lattice, which is known as the **first Brillouin zone (BZ)** [@problem_id:2972343].

To make these definitions concrete, let's derive the reciprocal lattice for a general two-dimensional Bravais lattice defined by $\mathbf{a}_1 = L_1 \hat{\mathbf{x}}$ and $\mathbf{a}_2 = L_2 (\cos\theta \hat{\mathbf{x}} + \sin\theta \hat{\mathbf{y}})$ [@problem_id:2972345]. The primitive reciprocal vectors $\mathbf{b}_1$ and $\mathbf{b}_2$ must satisfy $\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi\delta_{ij}$. By solving the system of linear equations, one finds:
$$
\mathbf{b}_1 = \frac{2\pi}{L_1 \sin\theta}(\sin\theta \hat{\mathbf{x}} - \cos\theta \hat{\mathbf{y}})
$$
$$
\mathbf{b}_2 = \frac{2\pi}{L_2 \sin\theta} \hat{\mathbf{y}}
$$
An interesting geometric property is that the angle $\varphi$ between the reciprocal vectors $\mathbf{b}_1$ and $\mathbf{b}_2$ is related to the angle $\theta$ between the direct [lattice vectors](@entry_id:161583) by $\varphi = \pi - \theta$. This inverse relationship between angles is a general feature of two-dimensional lattices.

### Band Structure and Zone Schemes

Substituting the Bloch form $\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k} \cdot \mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})$ into the Schrödinger equation yields an eigenvalue equation for the cell-periodic function $u_{n\mathbf{k}}(\mathbf{r})$:
$$
\left[ \frac{(\hat{\mathbf{p}} + \hbar\mathbf{k})^2}{2m} + V(\mathbf{r}) \right] u_{n\mathbf{k}}(\mathbf{r}) = E_n(\mathbf{k}) u_{n\mathbf{k}}(\mathbf{r}).
$$
The operator in the brackets, $H_{\mathbf{k}} = e^{-i\mathbf{k}\cdot\mathbf{r}} \hat{H} e^{i\mathbf{k}\cdot\mathbf{r}}$, is known as the **Bloch Hamiltonian**. For each fixed value of crystal momentum $\mathbf{k}$, $H_{\mathbf{k}}$ is a Hamiltonian acting on the space of cell-[periodic functions](@entry_id:139337), and its solution yields a [discrete spectrum](@entry_id:150970) of [energy eigenvalues](@entry_id:144381) $E_1(\mathbf{k}), E_2(\mathbf{k}), \ldots$. The functions $E_n(\mathbf{k})$ that trace the [energy eigenvalues](@entry_id:144381) as $\mathbf{k}$ is varied through the Brillouin zone form the **electronic band structure** of the material.

The equivalence of $\mathbf{k}$ and $\mathbf{k}+\mathbf{G}$ has a direct impact on the band structure. The Bloch Hamiltonians at these two wavevectors are unitarily related: $H_{\mathbf{k}+\mathbf{G}} = e^{-i\mathbf{G}\cdot\mathbf{r}} H_{\mathbf{k}} e^{i\mathbf{G}\cdot\mathbf{r}}$. Since a [unitary transformation](@entry_id:152599) preserves the eigenvalue spectrum, the set of [energy eigenvalues](@entry_id:144381) must be the same. This implies that the band structure is periodic in the reciprocal lattice:
$$
E_n(\mathbf{k}+\mathbf{G}) = E_n(\mathbf{k})
$$
Consequently, the **group velocity** of an electron in band $n$, defined by $\mathbf{v}_n(\mathbf{k}) = \frac{1}{\hbar}\boldsymbol{\nabla}_{\mathbf{k}} E_n(\mathbf{k})$, is also periodic with the reciprocal lattice: $\mathbf{v}_n(\mathbf{k}+\mathbf{G}) = \mathbf{v}_n(\mathbf{k})$ [@problem_id:2972350]. This [periodicity](@entry_id:152486) allows us to represent the band structure in several ways, known as **[zone schemes](@entry_id:147728)**.

A consistent convention for relating the Bloch functions themselves is to choose a gauge such that $\psi_{n, \mathbf{k}+\mathbf{G}}(\mathbf{r}) = \psi_{n\mathbf{k}}(\mathbf{r})$. This choice, which is always possible for an isolated, non-degenerate band, implies a specific transformation property for the cell-periodic part:
$$
e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}} u_{n, \mathbf{k}+\mathbf{G}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r}) \implies u_{n, \mathbf{k}+\mathbf{G}}(\mathbf{r}) = e^{-i\mathbf{G}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r}).
$$
This transformation rule is crucial for understanding the properties of Wannier functions and Berry curvature [@problem_id:2972343, @problem_id:2972350].

The three common [zone schemes](@entry_id:147728) are:
1.  **Extended Zone Scheme:** The energy $E_n(\mathbf{k})$ for each individual band $n$ is plotted over all of reciprocal space. This is physically intuitive in the limit of very weak potentials.
2.  **Repeated Zone Scheme:** The entire [band structure](@entry_id:139379) (all bands $n$) is plotted within each Brillouin zone, making the [periodicity](@entry_id:152486) explicit.
3.  **Reduced Zone Scheme:** This is the most common representation. All wavevectors $\mathbf{k}$ from the extended scheme are uniquely mapped into the first Brillouin zone by translation with an appropriate [reciprocal lattice vector](@entry_id:276906) $\mathbf{G}$: $\mathbf{k}' = \mathbf{k} - \mathbf{G}$. States that were distinct in the extended zone (e.g., from different regions of k-space) but map to the same $\mathbf{k}'$ must be distinguished by assigning them to different bands. This results in a multi-band structure within the first BZ [@problem_id:2972347].

A powerful pedagogical tool for understanding these schemes and the physical origin of band gaps is the **nearly-free electron (NFE) model**. In this model, we start with free electrons ($V(\mathbf{r})=0$), whose energy dispersion is a simple parabola $E^{(0)}(\mathbf{k}) = \frac{\hbar^2 |\mathbf{k}|^2}{2m}$. We then introduce a weak periodic potential $V(\mathbf{r})$ as a perturbation [@problem_id:2972309].

In the [extended zone scheme](@entry_id:200549), the free-electron states are plane waves $|\mathbf{k}\rangle$. The potential $V(\mathbf{r})$ has Fourier components $V_{\mathbf{G}}$ which couple [plane waves](@entry_id:189798) that differ by a [reciprocal lattice vector](@entry_id:276906): $\langle \mathbf{k}-\mathbf{G} | V | \mathbf{k} \rangle = V_{-\mathbf{G}}$. This coupling is weak unless the states are nearly degenerate in energy. The degeneracy condition $E^{(0)}(\mathbf{k}) \approx E^{(0)}(\mathbf{k-G})$ is met precisely at the Brillouin zone boundaries, for example, at $k = G/2$ in one dimension. At these points, [degenerate perturbation theory](@entry_id:143587) shows that the potential lifts the degeneracy, opening an **energy gap** of magnitude $\Delta E = 2|V_{\mathbf{G}}|$.

In the **[extended zone scheme](@entry_id:200549)**, this gap appears as a discontinuity in the energy parabola at each zone boundary $k = \pm n\pi/a$. In the **[reduced zone scheme](@entry_id:265307)**, the portions of the parabola from higher zones are "folded" back into the first BZ. For instance, the parabola centered at $G=2\pi/a$ is folded back to the first BZ. The gap at $k=\pi/a$ now manifests as an **avoided crossing** between the first and second bands at the zone boundary [@problem_id:2972309]. Both schemes describe the same physical states and energies; they are merely different representations of the same physics. Any physical observable, such as the density of states, is identical in both schemes [@problem_id:2972309].

The physical origin of this energy gap is the formation of **standing waves** at the zone boundary [@problem_id:2972369]. At $k=G/2$, the two degenerate free-electron waves $e^{i(G/2)x}$ and $e^{-i(G/2)x}$ combine to form two distinct standing waves. One combination, $\psi_- \propto \cos(Gx/2)$, concentrates electron charge density on the atomic nuclei (potential minima), lowering its energy. The other, $\psi_+ \propto \sin(Gx/2)$, concentrates charge between the nuclei (potential maxima), raising its energy. The energy difference between these two states is the band gap. A direct consequence is that the [group velocity](@entry_id:147686) $dE/dk$ becomes zero at the zone boundary, consistent with the non-propagating nature of [standing waves](@entry_id:148648) [@problem_id:2972369].

### Formal Properties of Bloch Functions

For a rigorous treatment of electronic properties, we must consider the formal mathematical properties of the set of Bloch functions $\{\psi_{n\mathbf{k}}\}$.

A key theoretical construct is the use of **Born-von Kármán (BvK) boundary conditions**. For a finite crystal containing $N = N_1 \times N_2 \times N_3$ primitive cells, we impose periodic boundary conditions on the wavefunction over a large "supercell" defined by the vectors $\mathbf{T}_i = N_i \mathbf{a}_i$. The condition $\psi(\mathbf{r} + \mathbf{T}_i) = \psi(\mathbf{r})$ applied to a Bloch function requires $e^{i\mathbf{k} \cdot \mathbf{T}_i} = 1$. This quantizes the allowed values of the [crystal momentum](@entry_id:136369) $\mathbf{k}$ into a discrete mesh:
$$
\mathbf{k} = \frac{\ell_1}{N_1} \mathbf{b}_1 + \frac{\ell_2}{N_2} \mathbf{b}_2 + \frac{\ell_3}{N_3} \mathbf{b}_3, \quad \text{where } \ell_i \text{ are integers.}
$$
This results in exactly $N$ distinct, uniformly spaced $\mathbf{k}$-vectors within the first Brillouin zone. In contrast, for a theoretically infinite crystal, $\mathbf{k}$ is a continuous variable. The BvK formalism is a mathematical tool that allows us to work with a discrete basis and normalizable wavefunctions, with the understanding that in the [thermodynamic limit](@entry_id:143061) ($N_i \to \infty$), sums over the discrete $\mathbf{k}$-mesh converge to integrals over the continuous BZ [@problem_id:2972360]:
$$
\frac{1}{V} \sum_{\mathbf{k}} \to \int_{\text{BZ}} \frac{d^3k}{(2\pi)^3} \quad \text{or} \quad \frac{1}{N} \sum_{\mathbf{k}} \to \frac{\Omega_c}{(2\pi)^3} \int_{\text{BZ}} d^3k,
$$
where $V = N\Omega_c$ is the total crystal volume and $\Omega_c$ is the [primitive cell](@entry_id:136497) volume.

The [spectral theorem](@entry_id:136620) of quantum mechanics guarantees that for a given Hamiltonian, the set of all its eigenfunctions forms a complete [orthonormal basis](@entry_id:147779) for the Hilbert space. For the periodic Hamiltonian, this means the set of all Bloch functions $\{\psi_{n\mathbf{k}}\}$ (with $n$ spanning all bands and $\mathbf{k}$ spanning the first BZ) is a complete basis [@problem_id:2972333]. Any arbitrary square-integrable state $\Psi(\mathbf{r})$ can be uniquely expanded in this basis.

For a finite crystal with BvK conditions, the expansion is a sum:
$$
\Psi(\mathbf{r}) = \sum_{n, \mathbf{k} \in \text{BZ}} c_{n\mathbf{k}} \psi_{n\mathbf{k}}(\mathbf{r}), \quad \text{with} \quad c_{n\mathbf{k}} = \int_{\Omega} \psi_{n\mathbf{k}}^*(\mathbf{r}) \Psi(\mathbf{r}) d^3r.
$$
The [completeness relation](@entry_id:139077) is $\sum_{n, \mathbf{k} \in \text{BZ}} |\psi_{n\mathbf{k}}\rangle\langle\psi_{n\mathbf{k}}| = I$.

In the infinite-volume limit, the sum becomes an integral, and the states are typically Dirac delta-normalized. The [completeness relation](@entry_id:139077) takes the form:
$$
\sum_n \int_{\text{BZ}} d^3k \, |\psi_{n\mathbf{k}}\rangle\langle\psi_{n\mathbf{k}}| = I,
$$
assuming the normalization convention $\langle\psi_{n\mathbf{k}} | \psi_{n'\mathbf{k}'}\rangle = \delta_{nn'} \delta^{(3)}(\mathbf{k}-\mathbf{k}')$ [@problem_id:2972333]. It is worth noting that the existence of topologically non-trivial bands (e.g., those with a non-zero Chern number) implies an obstruction to defining a smooth, periodic gauge for the Bloch functions over the entire BZ. However, this geometric property does not invalidate the completeness of the set of [eigenstates](@entry_id:149904) themselves [@problem_id:2972333].

### Beyond Perfect Periodicity: The Effect of Disorder

Real crystals are never perfectly periodic. They contain impurities, vacancies, and other defects which can be modeled by a static **disorder potential** $U(\mathbf{r})$ added to the periodic Hamiltonian: $\hat{H} = \hat{H}_{\text{per}} + U(\mathbf{r})$. For a single, specific realization of disorder, the potential $U(\mathbf{r})$ is not periodic, so the total Hamiltonian $\hat{H}$ does not commute with lattice translation operators. As a result, exact [translational symmetry](@entry_id:171614) is broken, and [crystal momentum](@entry_id:136369) $\mathbf{k}$ is no longer a [good quantum number](@entry_id:263156). The true [eigenstates](@entry_id:149904) of $\hat{H}$ are no longer Bloch waves [@problem_id:2972310].

However, the concept of [crystal momentum](@entry_id:136369) can be recovered in a statistical sense. We consider an ensemble of systems, where the disorder potential $U(\mathbf{r})$ is a random variable. A physically reasonable assumption is that the disorder is **statistically homogeneous**, meaning its statistical properties (e.g., its [correlation function](@entry_id:137198) $\langle U(\mathbf{r}) U(\mathbf{r}') \rangle$) are invariant under a lattice translation.

Under this assumption, while physical properties of a single sample are not translationally invariant, their **ensemble average** is. For instance, the averaged single-particle Green's function, which describes the propagation of an electron, regains [translational invariance](@entry_id:195885):
$$
\langle G(\mathbf{r}+\mathbf{a}, \mathbf{r}'+\mathbf{a}; \omega) \rangle = \langle G(\mathbf{r}, \mathbf{r}'; \omega) \rangle.
$$
This restored symmetry implies that in [reciprocal space](@entry_id:139921), the averaged Green's function, $\langle G(\mathbf{k}, \omega) \rangle$, and the corresponding [electron self-energy](@entry_id:148523), $\Sigma(\mathbf{k}, \omega)$, are diagonal in the crystal momentum index $\mathbf{k}$. This means that disorder does not, on average, mix different $\mathbf{k}$ states. Instead, it modifies the properties of each $\mathbf{k}$ state. The [self-energy](@entry_id:145608) $\Sigma(\mathbf{k}, \omega)$ is a complex quantity. Its real part shifts the energy of the state, while its imaginary part gives the state a finite lifetime due to scattering off the disorder.

Consequently, the **spectral function** $A(\mathbf{k}, \omega) = -\frac{1}{\pi}\text{Im}\langle G(\mathbf{k}, \omega)\rangle$, which for a clean system is a delta function at the band energy $E_n(\mathbf{k})$, becomes a broadened peak. The position of the peak still disperses with $\mathbf{k}$, but its finite width signifies that a state with a definite [crystal momentum](@entry_id:136369) is no longer a [stationary state](@entry_id:264752) but a "quasiparticle" that decays over time. Thus, even in the presence of weak disorder, crystal momentum remains an exceptionally useful concept for describing the averaged spectral and [transport properties](@entry_id:203130) of electrons in solids [@problem_id:2972310].