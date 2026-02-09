## Introduction
Bloch's theorem is the foundational principle of the quantum theory of solids, providing an elegant and powerful simplification for the otherwise intractable problem of describing electron behavior in a periodic crystal lattice. By exploiting the inherent translational symmetry of crystalline materials, the theorem transforms our understanding of electron states, revealing that they are not chaotic but are instead highly ordered, quasi-periodic waves propagating through the crystal. This conceptual breakthrough is the key that unlocks our ability to understand, predict, and ultimately engineer the vast array of electronic, optical, and transport properties that materials exhibit. The article addresses the fundamental question of how symmetry constrains quantum mechanics in a periodic system, bridging the gap between an abstract Hamiltonian and tangible material properties.

This exploration is structured to build a comprehensive understanding from first principles to cutting-edge applications. The first chapter, **Principles and Mechanisms**, will derive Bloch's theorem from symmetry considerations, introducing the essential concepts of crystal momentum, the Brillouin zone, energy bands, and the modern extensions involving spin, symmetry groups, and band topology. Following this, the chapter on **Applications and Interdisciplinary Connections** will demonstrate the theorem's profound impact, showing how it underpins computational materials science, explains electronic transport and spectroscopic measurements, and provides the language for the frontier of topological and engineered quantum materials. Finally, the **Hands-On Practices** section offers a set of computational problems designed to solidify these concepts, connecting the theoretical framework to the practical implementation used in modern research.

## Principles and Mechanisms

### Symmetry in Periodic Solids: The Foundation of Bloch's Theorem

The quantum mechanical description of an electron moving within a crystalline solid is governed by the time-independent Schrödinger equation, $H\psi(\mathbf{r}) = E\psi(\mathbf{r})$. The Hamiltonian operator, $H$, encapsulates the physics of the system. For a single, non-interacting electron of mass $m$ in a static potential $V(\mathbf{r})$, the Hamiltonian takes the form:

$$
H = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})
$$

Here, the first term represents the kinetic energy and the second term represents the potential energy of the electron interacting with the fixed ionic lattice. The defining characteristic of a perfect crystal is its discrete translational symmetry. The atomic arrangement is invariant under translation by any lattice vector $\mathbf{R}$ belonging to the crystal's Bravais lattice. This physical symmetry imposes a crucial constraint on the potential energy function:

$$
V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r}) \quad \text{for all lattice vectors } \mathbf{R}
$$

This periodicity of the potential is the cornerstone upon which the entire theory of electronic band structure is built. To understand its consequences, we must analyze the symmetries of the Hamiltonian operator itself. Let us define a **lattice translation operator**, $T_{\mathbf{R}}$, by its action on an arbitrary wavefunction $\psi(\mathbf{r})$:

$$
(T_{\mathbf{R}}\psi)(\mathbf{r}) = \psi(\mathbf{r} + \mathbf{R})
$$

We can now investigate whether the Hamiltonian $H$ commutes with this operator. The commutator is $[H, T_{\mathbf{R}}] = HT_{\mathbf{R}} - T_{\mathbf{R}}H$. We can analyze the kinetic and potential energy terms separately.

For the potential energy term, its commutation with $T_{\mathbf{R}}$ is a direct consequence of the potential's periodicity. Applying the commutator to a test function $\psi(\mathbf{r})$ gives:
$$
([V, T_{\mathbf{R}}]\psi)(\mathbf{r}) = V(\mathbf{r})(T_{\mathbf{R}}\psi)(\mathbf{r}) - T_{\mathbf{R}}(V(\mathbf{r})\psi(\mathbf{r})) = V(\mathbf{r})\psi(\mathbf{r}+\mathbf{R}) - V(\mathbf{r}+\mathbf{R})\psi(\mathbf{r}+\mathbf{R})
$$
Since $V(\mathbf{r}) = V(\mathbf{r}+\mathbf{R})$, the two terms are identical, and thus $[V, T_{\mathbf{R}}] = 0$.

For the kinetic energy term, $K = -\frac{\hbar^2}{2m}\nabla^2$, its commutation follows from the fact that the Laplacian operator $\nabla^2$ is invariant under a constant shift of coordinates. A derivative with respect to $\mathbf{r}$ is identical to a derivative with respect to a shifted coordinate $\mathbf{s} = \mathbf{r}+\mathbf{R}$. Therefore, the Laplacian of a shifted function is the same as the shifted Laplacian of the original function: $\nabla^2[\psi(\mathbf{r}+\mathbf{R})] = (\nabla^2\psi)(\mathbf{r}+\mathbf{R})$. This leads to:
$$
([K, T_{\mathbf{R}}]\psi)(\mathbf{r}) = K[\psi(\mathbf{r}+\mathbf{R})] - T_{\mathbf{R}}[K\psi(\mathbf{r})] = -\frac{\hbar^2}{2m}(\nabla^2\psi)(\mathbf{r}+\mathbf{R}) - \left(-\frac{\hbar^2}{2m}\nabla^2\psi\right)(\mathbf{r}+\mathbf{R}) = 0
$$
Since both the kinetic and potential parts of the Hamiltonian commute with the translation operator, the full Hamiltonian commutes as well:
$$
[H, T_{\mathbf{R}}] = 0 \quad \text{for all lattice vectors } \mathbf{R}
$$
This fundamental commutation relation is the mathematical expression of the fact that the Hamiltonian possesses the same translational symmetry as the crystal lattice [@problem_id:3792887]. A central theorem of quantum mechanics states that if a set of operators commute with each other, it is possible to find a basis of states that are simultaneous eigenstates of all of them. Since the Hamiltonian $H$ commutes with all translation operators $T_{\mathbf{R}}$, and since all translation operators commute with each other (as $T_{\mathbf{R}}T_{\mathbf{R}'} = T_{\mathbf{R}+\mathbf{R}'} = T_{\mathbf{R}'}T_{\mathbf{R}}$), we can find energy eigenstates that are also eigenstates of every lattice translation.

### The Structure of Electronic Eigenstates: Bloch's Theorem

Let $\psi(\mathbf{r})$ be a simultaneous eigenstate of $H$ and all $T_{\mathbf{R}}$. It must satisfy:
$$
H\psi(\mathbf{r}) = E\psi(\mathbf{r})
$$
$$
T_{\mathbf{R}}\psi(\mathbf{r}) = c(\mathbf{R})\psi(\mathbf{r})
$$
where $E$ is the energy eigenvalue and $c(\mathbf{R})$ is the eigenvalue of the translation operator $T_{\mathbf{R}}$. The properties of the translation operators impose strict constraints on the form of these eigenvalues. First, the operators $T_{\mathbf{R}}$ are unitary, which means their eigenvalues must be complex numbers of unit modulus, i.e., $|c(\mathbf{R})|=1$. Second, the group property $T_{\mathbf{R}+\mathbf{R}'} = T_{\mathbf{R}}T_{\mathbf{R}'}$ implies that the eigenvalues must satisfy the functional equation $c(\mathbf{R}+\mathbf{R}') = c(\mathbf{R})c(\mathbf{R}')$.

A function that satisfies both these conditions must be of the form $c(\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}$ for some real vector $\mathbf{k}$ [@problem_id:3792887]. This vector $\mathbf{k}$ is known as the **crystal momentum** or **Bloch vector**. It serves as a new quantum number that labels the irreducible representations of the lattice translation group.

The eigenvalue equation for the translation operator thus becomes a condition on the structure of the energy eigenstates:
$$
\psi(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}\psi(\mathbf{r})
$$
This identity is the first form of **Bloch's theorem**. It reveals that an energy eigenstate in a periodic potential is not itself periodic with the lattice; rather, it is quasi-periodic, acquiring a specific phase factor upon translation by a lattice vector.

A more common and insightful form of the theorem is obtained by defining a new function, $u_{\mathbf{k}}(\mathbf{r})$, such that $\psi_{\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}}u_{\mathbf{k}}(\mathbf{r})$. Let us examine the periodicity of this new function:
$$
u_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot(\mathbf{r}+\mathbf{R})} \psi_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot\mathbf{r}}e^{-i\mathbf{k}\cdot\mathbf{R}} \left( e^{i\mathbf{k}\cdot\mathbf{R}} \psi_{\mathbf{k}}(\mathbf{r}) \right) = e^{-i\mathbf{k}\cdot\mathbf{r}} \psi_{\mathbf{k}}(\mathbf{r}) = u_{\mathbf{k}}(\mathbf{r})
$$
The function $u_{\mathbf{k}}(\mathbf{r})$ is therefore truly periodic with the lattice, $u_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = u_{\mathbf{k}}(\mathbf{r})$. This leads to the canonical statement of Bloch's theorem: The energy eigenstates of a periodic Hamiltonian can be written as the product of a plane wave $e^{i\mathbf{k}\cdot\mathbf{r}}$ and a **cell-periodic function** $u_{n\mathbf{k}}(\mathbf{r})$ that has the same periodicity as the Bravais lattice.

The labels $n$ and $\mathbf{k}$ have been added to completely specify the state. For a fixed crystal momentum $\mathbf{k}$, the Schrödinger equation, when rewritten for the periodic function $u_{\mathbf{k}}(\mathbf{r})$, becomes an eigenvalue problem on the unit cell with $\mathbf{k}$-dependent boundary conditions. This equation yields a discrete spectrum of energy eigenvalues. The integer $n$ that enumerates these distinct energy levels for a given $\mathbf{k}$ is called the **band index** [@problem_id:3792931]. The full eigenstate is thus labeled $\psi_{n\mathbf{k}}(\mathbf{r})$.

### Reciprocal Space and the Brillouin Zone

The crystal momentum $\mathbf{k}$ is a central concept, but it is not uniquely defined. To see this, consider the phase factor $e^{i\mathbf{k}\cdot\mathbf{R}}$. If we add a special vector $\mathbf{G}$ to $\mathbf{k}$ such that $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$ for all lattice vectors $\mathbf{R}$, the phase factor remains unchanged:
$$
e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}
$$
This means that the crystal momenta $\mathbf{k}$ and $\mathbf{k}+\mathbf{G}$ describe the exact same translational symmetry and are therefore physically equivalent. The set of all such vectors $\mathbf{G}$ forms a lattice in its own right, known as the **reciprocal lattice**. Any two Bloch states whose crystal momenta differ by a reciprocal lattice vector are considered equivalent.

This redundancy implies that all unique electronic states can be described by restricting the crystal momentum $\mathbf{k}$ to a single primitive cell of the reciprocal lattice. By convention, this primitive cell is chosen to be the Wigner-Seitz cell of the reciprocal lattice, which is called the **First Brillouin Zone (BZ)**. The BZ contains all the unique crystal momenta needed to label the electronic states of the crystal [@problem_id:3792936].

As a concrete example, consider the face-centered cubic (FCC) lattice, which is the structure of many common metals like aluminum and copper. If the conventional cubic cell has a side length $a$, a set of primitive real-space vectors is $a_1 = \frac{a}{2}(\hat{y} + \hat{z})$, $a_2 = \frac{a}{2}(\hat{z} + \hat{x})$, and $a_3 = \frac{a}{2}(\hat{x} + \hat{y})$. The corresponding reciprocal lattice vectors can be shown to be the primitive vectors of a body-centered cubic (BCC) lattice. The First Brillouin Zone for the FCC lattice is therefore the Wigner-Seitz cell of the BCC lattice, which is a geometric shape known as a truncated octahedron. Important high-symmetry points in this BZ, such as the center ($\Gamma$ point at $(0,0,0)$), the center of a square face ($X$ point at $\frac{2\pi}{a}(1,0,0)$), and the center of a hexagonal face ($L$ point at $\frac{\pi}{a}(1,1,1)$), are used to plot and analyze the electronic band structure [@problem_id:3792890].

In an infinite crystal, $\mathbf{k}$ is a continuous variable. However, any real crystal is finite. The properties of a macroscopic crystal are typically modeled by imposing periodic (Born-von Kármán) boundary conditions on a large but finite system of $N$ unit cells. For a 1D chain of length $L=Na$, imposing the condition $\psi(x) = \psi(x+L)$ leads to the quantization of the wavevector:
$$
k = n \frac{2\pi}{Na}, \quad n \in \mathbb{Z}
$$
This means there are $N$ discrete, equally spaced allowed $\mathbf{k}$-values within the first Brillouin Zone. The spacing between them is $\Delta k = \frac{2\pi}{Na}$. As the size of the crystal $N \to \infty$, this spacing becomes infinitesimally small, $\Delta k \to 0$. The discrete set of $\mathbf{k}$-points merges into a continuum, justifying the treatment of $\mathbf{k}$ as a continuous variable and the replacement of sums over $\mathbf{k}$ with integrals in the thermodynamic limit [@problem_id:3792897].

### The Electronic Band Structure: Bands and Gaps

For each value of the band index $n$, the energy eigenvalue $E_{n}(\mathbf{k})$ is a continuous function of the crystal momentum $\mathbf{k}$ as it varies across the Brillouin zone. This function $E_{n}(\mathbf{k})$ is called an **energy band**. The collection of all energy bands for a given material, $E_{n}(\mathbf{k})$ for all $n$ and all $\mathbf{k} \in \text{BZ}$, is known as its **electronic band structure**.

Because the crystal momenta $\mathbf{k}$ and $\mathbf{k}+\mathbf{G}$ are physically equivalent, the energy bands must have the periodicity of the reciprocal lattice:
$$
E_{n}(\mathbf{k}) = E_{n}(\mathbf{k}+\mathbf{G})
$$
This periodicity is a fundamental property of the band structure and means that all information is contained within the first Brillouin Zone [@problem_id:3792936].

The interaction between the electron and the periodic potential of the lattice is what gives rise to the characteristic features of the band structure: continuous bands of allowed energies separated by forbidden energy ranges called **band gaps**. A simple but powerful illustration of this mechanism is provided by the nearly-free electron model. In this model, the periodic potential $V(\mathbf{r})$ is treated as a small perturbation to a free electron gas. The unperturbed states are plane waves with energies $E^{(0)}(\mathbf{k}) = \frac{\hbar^2k^2}{2m}$. At points in $\mathbf{k}$-space on the boundary of the Brillouin Zone, the Bragg condition is met, and states like $\mathbf{k}$ and $\mathbf{k}-\mathbf{G}$ can become degenerate, $E^{(0)}(\mathbf{k}) \approx E^{(0)}(\mathbf{k}-\mathbf{G})$. A non-zero Fourier component of the potential, $V_{\mathbf{G}}$, acts as a coupling term between these degenerate states. Applying degenerate perturbation theory shows that this coupling lifts the degeneracy and opens a gap in the energy spectrum. The size of this energy gap is precisely $2|V_{\mathbf{G}}|$ [@problem_id:3792935]. From an alternative, tight-binding perspective, bands arise from the hybridization of discrete atomic orbitals as atoms are brought together to form a crystal, and gaps represent the energy ranges between these hybridized bands [@problem_id:3792936].

The existence and size of a band gap between the highest occupied band (the **valence band**) and the lowest unoccupied band (the **conduction band**) determine a material's electronic properties. The nature of this gap is further classified as either direct or indirect. A material has a **direct band gap** if the maximum energy of the valence band and the minimum energy of the conduction band occur at the same $\mathbf{k}$-point in the Brillouin Zone. It has an **indirect band gap** if they occur at different $\mathbf{k}$-points [@problem_id:3792936]. This distinction is critical for optoelectronic applications, as electron-hole recombination in direct-gap materials can efficiently emit photons, while in indirect-gap materials it requires the assistance of a phonon to conserve momentum.

### A Formal View: The Bloch Hamiltonian and Direct Integral Decomposition

The structure implied by Bloch's theorem allows for a powerful mathematical reformulation of the Schrödinger equation. The full Hilbert space of wavefunctions on the entire crystal, $\mathcal{H} = L^2(\mathbb{R}^d)$, can be formally decomposed into a "direct integral" of smaller Hilbert spaces, one for each crystal momentum $\mathbf{k}$ in the Brillouin Zone:
$$
\mathcal{H} \cong \int_{\mathrm{BZ}}^{\oplus} \mathcal{H}_{\mathbf{k}} \, d\mathbf{k}
$$
In this picture, the Hamiltonian $H$, which acts on the entire space $\mathcal{H}$, is block-diagonalized. It does not mix states with different crystal momenta $\mathbf{k}$. This means that for each $\mathbf{k}$, we can solve an independent, smaller eigenvalue problem.

This is achieved by rewriting the Schrödinger equation for the cell-periodic part of the Bloch function, $u_{n\mathbf{k}}(\mathbf{r})$. Substituting $\psi_{n\mathbf{k}} = e^{i\mathbf{k}\cdot\mathbf{r}}u_{n\mathbf{k}}$ into the original equation $H\psi_{n\mathbf{k}} = E_{n}(\mathbf{k})\psi_{n\mathbf{k}}$ leads to an eigenvalue equation for $u_{n\mathbf{k}}$:
$$
H(\mathbf{k}) u_{n\mathbf{k}}(\mathbf{r}) = E_{n}(\mathbf{k}) u_{n\mathbf{k}}(\mathbf{r})
$$
where $H(\mathbf{k})$ is the **Bloch Hamiltonian**:
$$
H(\mathbf{k}) = e^{-i\mathbf{k}\cdot\mathbf{r}} H e^{i\mathbf{k}\cdot\mathbf{r}} = \frac{1}{2m}(-i\hbar\nabla + \hbar\mathbf{k})^2 + V(\mathbf{r})
$$
The Bloch Hamiltonian $H(\mathbf{k})$ acts only on the space of cell-periodic functions, which is a much smaller and more manageable space than the full Hilbert space $L^2(\mathbb{R}^d)$. This transformation effectively converts a single, immense eigenvalue problem into a continuous family of smaller, more tractable eigenvalue problems, one for each $\mathbf{k}$ in the Brillouin Zone [@problem_id:3792864].

### Beyond the Scalar Electron: Spin-Orbit Coupling and Symmetries

So far, we have neglected the intrinsic spin of the electron. In many materials, particularly those containing heavy elements, the interaction between the electron's spin and its orbital motion in the electric field of the crystal—**spin-orbit coupling (SOC)**—is significant. The Hamiltonian must then be modified to include an SOC term, for example:
$$
H_{\text{SOC}} = \frac{\hbar}{4m^2c^2} \boldsymbol{\sigma} \cdot (\nabla V(\mathbf{r}) \times \mathbf{p})
$$
where $\boldsymbol{\sigma}$ is the vector of Pauli matrices. With this term, the Hamiltonian now acts on two-component spinors.

Crucially, the SOC term, like the scalar potential $V(\mathbf{r})$, possesses the translational symmetry of the lattice. Therefore, the total Hamiltonian still commutes with all lattice translation operators, $[H, T_{\mathbf{R}}] = 0$. As a result, Bloch's theorem remains valid. The eigenstates are now **spinor Bloch functions**, which can be written in the form $\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})$, where $u_{n\mathbf{k}}(\mathbf{r})$ is a cell-periodic two-component spinor [@problem_id:3792873] [@problem_id:3792873].

The inclusion of spin has profound consequences for the classification of states using group theory. A rotation by $2\pi$ does not return a spinor to its original state; it multiplies it by $-1$. This means that the ordinary representations of the crystal's point group are no longer sufficient. One must instead use the representations of the corresponding **double group**, which treats a $2\pi$ rotation as a distinct operation from the identity. The labeling of bands and the determination of degeneracies at high-symmetry points in the BZ must be done using the irreducible representations of the appropriate double little group [@problem_id:3792873].

This formalism is essential for understanding symmetry-enforced degeneracies. In systems with time-reversal symmetry (TR), Kramers' theorem guarantees that $E_n(\mathbf{k}) = E_m(-\mathbf{k})$ for some bands $n, m$. If the crystal also has inversion symmetry, the combination of TR and inversion symmetry ensures that every energy band is at least two-fold degenerate (spin degeneracy) at every $\mathbf{k}$-point in the BZ. Furthermore, crystals with **nonsymmorphic symmetries** (glide planes or screw axes) can exhibit even higher-dimensional degeneracies at certain points on the BZ boundary, leading to a "sticking together" of bands that is protected by symmetry and robust even in the presence of strong SOC [@problem_id:3792873].

### The Geometric Phase and Topology of Bands

The formulation of Bloch's theorem, $\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}}u_{n\mathbf{k}}(\mathbf{r})$, contains a subtle ambiguity. For each $\mathbf{k}$, the phase of the cell-periodic part $u_{n\mathbf{k}}$ is not uniquely determined. We can multiply it by an arbitrary phase factor, $u_{n\mathbf{k}} \to e^{-i\phi_n(\mathbf{k})}u_{n\mathbf{k}}$, without changing any of the fundamental properties of the state. This is a **U(1) gauge freedom**. Physical observables that depend only on a single state at a single $\mathbf{k}$, such as the energy $E_n(\mathbf{k})$ or the probability density $|\psi_{n\mathbf{k}}(\mathbf{r})|^2$, are independent of this choice of phase; they are gauge-invariant [@problem_id:3792921].

However, quantities that involve derivatives with respect to $\mathbf{k}$ can be gauge-dependent. A prime example is the **Berry connection** (or Berry potential), defined for a given band $n$ as:
$$
\mathbf{A}_{n}(\mathbf{k}) = i \langle u_{n\mathbf{k}} | \nabla_{\mathbf{k}} u_{n\mathbf{k}} \rangle_{\text{cell}}
$$
where the inner product is taken over a single unit cell. Under a gauge transformation, the Berry connection transforms exactly like the vector potential in electromagnetism: $\mathbf{A}_{n}(\mathbf{k}) \to \mathbf{A}_{n}(\mathbf{k}) + \nabla_{\mathbf{k}}\phi_n(\mathbf{k})$. While the Berry connection itself is not gauge-invariant, its curl, the **Berry curvature**, is:
$$
\mathbf{\Omega}_{n}(\mathbf{k}) = \nabla_{\mathbf{k}} \times \mathbf{A}_{n}(\mathbf{k})
$$
The Berry curvature is a gauge-invariant, geometric property of the band structure, describing the "twist" of the Hilbert space of Bloch functions as $\mathbf{k}$ varies across the Brillouin Zone [@problem_id:3792921].

A natural question arises: is it possible to choose a "smooth gauge"—that is, a set of phases $\phi_n(\mathbf{k})$—such that the resulting cell-periodic functions $u_{n\mathbf{k}}(\mathbf{r})$ are smooth and periodic across the entire Brillouin Zone? The answer is not always yes, and the obstruction is topological. For a 2D material, the integral of the Berry curvature over the entire Brillouin Zone is a topological invariant known as the **first Chern number**, $C_1$.
$$
C_{1} = \frac{1}{2\pi} \iint_{\text{BZ}} \mathbf{\Omega}_{n}(\mathbf{k}) \cdot d\mathbf{S}
$$
This number must be an integer. If $C_1 \neq 0$, the band is said to be topologically non-trivial, and it is mathematically impossible to find a global, smooth, periodic gauge for $u_{n\mathbf{k}}$. A non-zero Chern number indicates a fundamental topological obstruction [@problem_id:3792891].

The physical origin of non-trivial topology is often the presence of **band degeneracies**. Points in $\mathbf{k}$-space where a band touches another act as sources or sinks of Berry curvature—analogous to magnetic monopoles in momentum space. The Berry phase acquired on a loop enclosing such a degeneracy is quantized, and the net flux of curvature from these "monopoles" determines the overall Chern number of the band [@problem_id:3792891]. Symmetries play a critical role; for instance, time-reversal symmetry forces the Berry curvature to be an odd function, $\mathbf{\Omega}_{n}(\mathbf{k}) = -\mathbf{\Omega}_{n}(-\mathbf{k})$, which constrains the Chern number of any single band to be zero. However, this same symmetry can give rise to a different class of topological materials, the $\mathbb{Z}_2$ topological insulators, characterized by a different invariant [@problem_id:3792891]. These modern concepts reveal that the band structure of solids is endowed not only with energetic and dynamic properties but also with a rich and robust topological structure.