## Introduction
Open-shell systems—molecules and materials with one or more unpaired electrons—are central to vast areas of modern science, from [coordination chemistry](@entry_id:153771) and catalysis to [molecular magnetism](@entry_id:191279) and materials science. Their unique reactivity, spectroscopic signatures, and magnetic properties are dictated by the intricate quantum mechanics of electron spin. The concept of [spin symmetry](@entry_id:197993) provides the theoretical language and framework for describing these complex systems. However, correctly capturing spin effects within the practical constraints of computational chemistry presents a significant challenge. The widespread use of approximate methods often leads to a "[spin symmetry](@entry_id:197993) dilemma," where achieving energetic accuracy may require sacrificing the formal correctness of the wavefunction's spin state. This creates a critical knowledge gap for researchers who rely on these tools to predict and interpret molecular properties.

This article provides a comprehensive exploration of [spin symmetry](@entry_id:197993) in [open-shell systems](@entry_id:168723), designed for graduate-level students and researchers in quantum chemistry. We begin in the **Principles and Mechanisms** chapter by establishing the formal quantum mechanical description of many-electron spin, detailing the construction of spin-adapted wavefunctions, and examining how [spin symmetry](@entry_id:197993) is treated—and often broken—within foundational methods like Hartree-Fock and Density Functional Theory. Following this, the **Applications and Interdisciplinary Connections** chapter bridges theory and practice, showcasing how [spin symmetry](@entry_id:197993) principles are applied to understand molecular structure, model [magnetic exchange coupling](@entry_id:172004) in [polynuclear complexes](@entry_id:156104), interpret spectroscopic data, and engineer novel molecular electronic devices. Finally, the **Hands-On Practices** section offers targeted computational exercises to reinforce the theoretical concepts and provide practical experience with the methods discussed. Through this structured approach, readers will gain a deep and functional understanding of the theory, application, and computational nuances of spin in open-shell chemistry.

## Principles and Mechanisms

In the nonrelativistic quantum theory of electronic structure, where the Hamiltonian is independent of spin coordinates, the total electron spin emerges as a fundamental symmetry of the system. This chapter delineates the principles governing this symmetry and the mechanisms by which it is described, enforced, or sometimes broken in approximate theoretical models. We will begin by establishing the quantum mechanical algebra of many-electron spin, proceed to the systematic construction of wavefunctions with well-defined spin, explore the implications for widely used computational methods, and conclude by examining the physical limits of the [spin symmetry](@entry_id:197993) concept itself.

### The Quantum Mechanical Description of Many-Electron Spin

While an individual electron possesses an intrinsic and immutable spin quantum number $s = \frac{1}{2}$, the collective spin of a many-electron system is a variable and dynamically crucial property. Its description requires moving from single-particle operators to total [spin operators](@entry_id:155419).

#### Total Spin Operators and Their Algebra

For an $N$-electron system, the total spin vector operator, $\hat{\mathbf{S}}$, is defined as the vector sum of the individual one-electron [spin operators](@entry_id:155419), $\hat{\mathbf{s}}_i$:
$$
\hat{\mathbf{S}} = \sum_{i=1}^{N} \hat{\mathbf{s}}_i
$$
The components of this total operator are simply the sums of the individual components: $\hat{S}_x = \sum_i \hat{s}_{ix}$, $\hat{S}_y = \sum_i \hat{s}_{iy}$, and $\hat{S}_z = \sum_i \hat{s}_{iz}$.

A key result is that because the [spin operators](@entry_id:155419) of different electrons commute (i.e., $[\hat{s}_{i\alpha}, \hat{s}_{j\beta}] = 0$ for $i \neq j$), the [total spin](@entry_id:153335) components obey the same fundamental [commutation relations](@entry_id:136780) as a single-particle [angular momentum operator](@entry_id:155961):
$$
[\hat{S}_x, \hat{S}_y] = \mathrm{i}\hbar \hat{S}_z \quad \text{(and cyclic permutations)}
$$
This algebraic structure is of paramount importance, as it implies that the entire well-developed quantum theory of angular momentum can be applied to the total spin of a many-electron system.

The operator corresponding to the square of the total spin magnitude is $\hat{S}^2 = \hat{\mathbf{S}} \cdot \hat{\mathbf{S}}$. Expanding this definition reveals a crucial feature of spin coupling [@problem_id:2911649]:
$$
\hat{S}^2 = \left(\sum_{i=1}^{N} \hat{\mathbf{s}}_i\right) \cdot \left(\sum_{j=1}^{N} \hat{\mathbf{s}}_j\right) = \sum_{i=1}^{N} \hat{\mathbf{s}}_i^2 + \sum_{i \neq j} \hat{\mathbf{s}}_i \cdot \hat{\mathbf{s}}_j
$$
The operator $\hat{S}^2$ is not merely the sum of the individual $\hat{\mathbf{s}}_i^2$ operators. It also contains the two-electron cross-terms, $\hat{\mathbf{s}}_i \cdot \hat{\mathbf{s}}_j$, which represent the coupling between the spins of different electrons. While the eigenvalue of each $\hat{\mathbf{s}}_i^2$ is fixed at $s(s+1)\hbar^2 = \frac{3}{4}\hbar^2$, the eigenvalue of $\hat{S}^2$ depends on the collective orientation of all the electron spins, as governed by the cross-terms. This coupling is what allows a many-electron system to adopt various total spin states.

#### Spin Eigenstates and Quantum Numbers

Since the total [spin operators](@entry_id:155419) $\hat{\mathbf{S}}$ follow the canonical [angular momentum algebra](@entry_id:178952), it follows that $\hat{S}^2$ commutes with each of its components, for instance, $[\hat{S}^2, \hat{S}_z] = 0$ [@problem_id:2911649]. According to a fundamental postulate of quantum mechanics, this allows us to find a set of simultaneous eigenfunctions for both operators. These states, often called pure [spin states](@entry_id:149436), are labeled by two quantum numbers: the total [spin quantum number](@entry_id:142550) $S$ and the magnetic [spin quantum number](@entry_id:142550) $M_S$.

For a pure spin state $|\Psi_{S, M_S}\rangle$, the following [eigenvalue equations](@entry_id:192306) hold [@problem_id:2911649]:
$$
\hat{S}^2 |\Psi_{S, M_S}\rangle = S(S+1)\hbar^2 |\Psi_{S, M_S}\rangle
$$
$$
\hat{S}_z |\Psi_{S, M_S}\rangle = M_S\hbar |\Psi_{S, M_S}\rangle
$$
The total spin $S$ can take on half-integer or integer values, starting from a minimum value that depends on the number of electrons, up to a maximum of $N/2$. For a given $S$, the projection quantum number $M_S$ can take on $2S+1$ possible values: $M_S = -S, -S+1, \dots, S-1, S$.

It is essential to distinguish between the quantum number $S$, which characterizes the magnitude of the total spin, and $M_S$, which describes its projection onto a chosen axis. A state with a definite number of spin-$\alpha$ electrons ($N_\alpha$) and spin-$\beta$ electrons ($N_\beta$) is an eigenstate of $\hat{S}_z$ with $M_S = \frac{1}{2}(N_\alpha - N_\beta)$, but it is not necessarily an [eigenfunction](@entry_id:149030) of $\hat{S}^2$ [@problem_id:2911649]. The correct relationship is that for any state, the [total spin](@entry_id:153335) must be at least as large as the magnitude of its projection: $S \ge |M_S|$.

#### Spin Multiplicity

The quantity $2S+1$, which counts the number of possible $M_S$ projections for a given [total spin](@entry_id:153335) $S$, is called the **spin multiplicity** [@problem_id:2911681]. It represents the degeneracy of a spin state in the absence of interactions that break the [rotational symmetry](@entry_id:137077) in spin space, such as external magnetic fields or spin-orbit coupling. States are commonly referred to by their [multiplicity](@entry_id:136466):

*   $S=0$: Multiplicity $1$, **singlet** state.
*   $S=1/2$: Multiplicity $2$, **doublet** state.
*   $S=1$: Multiplicity $3$, **triplet** state.
*   $S=3/2$: Multiplicity $4$, **quartet** state.

And so on. For a system with an even number of electrons, the [total spin](@entry_id:153335) $S$ must be an integer, resulting in odd multiplicities (singlet, triplet, etc.). For a system with an odd number of electrons, $S$ must be a half-integer, leading to even multiplicities (doublet, quartet, etc.) [@problem_id:2911681].

For many chemical systems, particularly those in their highest possible spin state, there is a simple empirical relationship between the [multiplicity](@entry_id:136466) and the number of [unpaired electrons](@entry_id:137994), $n_u$. In such a high-spin configuration, where all [unpaired electrons](@entry_id:137994) have parallel spins, the total spin is $S = n_u/2$. The spin multiplicity is therefore $2S+1 = 2(n_u/2) + 1 = n_u+1$. For example, a system with two [unpaired electrons](@entry_id:137994) in a high-spin arrangement ($n_u=2$) has $S=1$ and a multiplicity of $3$ (a triplet).

### Constructing Spin-Adapted Wavefunctions

A central task in the theory of [open-shell systems](@entry_id:168723) is the construction of many-electron wavefunctions that are proper eigenfunctions of $\hat{S}^2$. These are known as **spin-adapted** wavefunctions.

#### The Two-Electron Case: Singlet and Triplet States

The simplest non-trivial system is that of two electrons. Each electron has spin $s=1/2$, so the [total spin](@entry_id:153335) can be $S = |\frac{1}{2}-\frac{1}{2}|, \dots, \frac{1}{2}+\frac{1}{2}$, giving $S=0$ (singlet) and $S=1$ (triplet) [@problem_id:2911681]. These states can be constructed systematically from the product basis of one-electron spin functions, $\{|\alpha\alpha\rangle, |\alpha\beta\rangle, |\beta\alpha\rangle, |\beta\beta\rangle\}$.

The state with the highest $M_S$ value, $|\alpha\alpha\rangle$ with $M_S=+1$, must belong to the highest possible [spin manifold](@entry_id:159034), which is the triplet ($S=1$). It is thus identified as the $|S=1, M_S=+1\rangle$ eigenstate. The other members of the triplet manifold can be generated by applying the total spin lowering operator, $\hat{S}_{-} = \hat{s}_{1-} + \hat{s}_{2-}$ [@problem_id:2911647]. This procedure yields the three normalized triplet states, which are symmetric with respect to the exchange of the two electrons' spin labels:
$$
|1, +1\rangle = |\alpha\alpha\rangle
$$
$$
|1, 0\rangle = \frac{1}{\sqrt{2}}(|\alpha\beta\rangle + |\beta\alpha\rangle)
$$
$$
|1, -1\rangle = |\beta\beta\rangle
$$
The remaining state must be the singlet, with $S=0$ and $M_S=0$. It can be found by constructing a combination of the $M_S=0$ product states that is orthogonal to the triplet $|1, 0\rangle$. This state is antisymmetric with respect to spin label exchange:
$$
|0, 0\rangle = \frac{1}{\sqrt{2}}(|\alpha\beta\rangle - |\beta\alpha\rangle)
$$
By applying the operator identity $\hat{S}^2 = \hat{S}_-\hat{S}_+ + \hat{S}_z^2 + \hbar \hat{S}_z$ (or its counterpart), one can rigorously verify that these four states are indeed [eigenfunctions](@entry_id:154705) of $\hat{S}^2$ with eigenvalues $1(2)\hbar^2=2\hbar^2$ for the triplet and $0(1)\hbar^2=0$ for the singlet [@problem_id:2911647].

#### The N-Electron Case and Spin Coupling

As the number of electrons grows, the complexity of spin coupling increases. For three electrons, coupling the spins $s_1=1/2$, $s_2=1/2$, and $s_3=1/2$ sequentially gives rise to one **quartet** manifold ($S=3/2$) and two distinct **doublet** manifolds ($S=1/2$) [@problem_id:2911656]. The total number of [spin states](@entry_id:149436) is $4 + 2\times2 = 8 = 2^3$, as expected.

The spin-adapted functions for these manifolds can be constructed using the same ladder operator approach. One starts with the highest-weight state of the highest [spin manifold](@entry_id:159034), $|3/2, 3/2\rangle = |\alpha\alpha\alpha\rangle$, and applies $\hat{S}_-$ repeatedly to generate the other three members of the quartet. The remaining states, which must be orthogonal to the quartet states, form the basis for the two doublet manifolds. For example, the $M_S=1/2$ spin space is spanned by $\{|\beta\alpha\alpha\rangle, |\alpha\beta\alpha\rangle, |\alpha\alpha\beta\rangle\}$. One [linear combination](@entry_id:155091) of these forms the $|3/2, 1/2\rangle$ state, while two other orthogonal combinations form the two distinct $|1/2, 1/2\rangle$ states [@problem_id:2911656]. This systematic construction ensures that the resulting functions are, by design, [eigenfunctions](@entry_id:154705) of $\hat{S}^2$.

#### Configuration State Functions (CSFs)

The Pauli exclusion principle requires that a total electronic wavefunction be antisymmetric with respect to the exchange of any two electrons. This is most commonly enforced by writing the wavefunction as a Slater determinant. However, a single Slater determinant is, in general, **not** an [eigenfunction](@entry_id:149030) of $\hat{S}^2$.

A crucial exception is a **high-spin determinant**, where all singly occupied orbitals have spin-$\alpha$ (or all have spin-$\beta$). Such a determinant corresponds to the highest possible $M_S$ value for a given number of unpaired electrons and can be proven to be a pure spin state. Applying the raising operator $\hat{S}_+$ to such a determinant yields zero, as there are no $\beta$ spins to raise. This identifies it as a "highest-weight" state with $S = |M_S|$, and it is therefore an eigenfunction of $\hat{S}^2$ [@problem_id:2911693] [@problem_id:2911614].

In contrast, a low-spin open-shell determinant, such as one representing an $M_S=0$ configuration with singly occupied orbitals $p\alpha$ and $q\beta$, is not an eigenfunction of $\hat{S}^2$. Applying $\hat{S}^2$ to this state produces a [linear combination](@entry_id:155091) of the original determinant and another determinant where the spins on orbitals $p$ and $q$ are swapped. Since the result is not proportional to the original state, the state is not an [eigenfunction](@entry_id:149030); it is a mixture of different spin states (in this case, singlet and triplet) [@problem_id:2911693].

To guarantee [spin purity](@entry_id:178603), one must work with **Configuration State Functions (CSFs)**. A CSF is a specific [linear combination](@entry_id:155091) of Slater [determinants](@entry_id:276593) constructed to be an [eigenfunction](@entry_id:149030) of $\hat{S}^2$ [@problem_id:2911614]. For example, in the CAS(2,2) space (two electrons in two orbitals, $a$ and $b$), the $M_S=0$ component of the open-shell triplet is the CSF $|^3\!(ab)\rangle = \frac{1}{\sqrt{2}}(|a\alpha, b\beta\rangle + |a\beta, b\alpha\rangle)$, while the open-shell singlet is $|^1\!(ab)\rangle = \frac{1}{\sqrt{2}}(|a\alpha, b\beta\rangle - |a\beta, b\alpha\rangle)$. When a Configuration Interaction (CI) calculation is performed in a basis of CSFs, the Hamiltonian matrix becomes block-diagonal with respect to the total spin $S$. Diagonalizing a block for a specific $S$ guarantees that the resulting CI eigenvectors are spin-pure.

### Spin Symmetry in Mean-Field Theories

Mean-field methods like Hartree-Fock (HF) approximate the [many-electron wavefunction](@entry_id:174975) as a single Slater determinant. This simplification has profound consequences for the treatment of [spin symmetry](@entry_id:197993) in [open-shell systems](@entry_id:168723).

#### The Problem of Spin Contamination

An ideal wavefunction for a nonrelativistic system should be an eigenfunction of $\hat{S}^2$. If an approximate wavefunction $\Psi_{approx}$ is not, it is said to be **spin-contaminated**. The degree of contamination is quantified by the deviation of the [expectation value](@entry_id:150961) $\langle\hat{S}^2\rangle = \langle\Psi_{approx}|\hat{S}^2|\Psi_{approx}\rangle$ from the desired eigenvalue $S(S+1)\hbar^2$. A state $\Psi_{approx}$ that is not an [eigenfunction](@entry_id:149030) of $\hat{S}^2$ can be viewed as a mixture of the desired spin state with contaminating contributions from states of other multiplicities. For a calculation targeting a doublet state ($S=1/2$), the contaminating states will be those with higher spin (quartets, sextets, etc.), as required by the condition $S' \ge |M_S|$ [@problem_id:2911631].

#### Unrestricted Hartree-Fock (UHF) and Spin-Symmetry Breaking

The **Unrestricted Hartree-Fock (UHF)** method allows the spatial orbitals for $\alpha$ and $\beta$ electrons to be different ($\phi_i^\alpha \neq \phi_i^\beta$). This flexibility gives the [variational principle](@entry_id:145218) more freedom to lower the total energy. However, this comes at the cost of breaking [spin symmetry](@entry_id:197993). A UHF determinant is an [eigenfunction](@entry_id:149030) of $\hat{S}_z$ but generally not of $\hat{S}^2$.

The formal reason for this is that the effective one-electron UHF Fock operator is spin-dependent ($\hat{F}^\alpha \neq \hat{F}^\beta$) and does not commute with the total [spin operator](@entry_id:149715) $\hat{S}^2$ [@problem_id:2911631]. Consequently, its [eigenfunctions](@entry_id:154705) (the UHF orbitals) and the determinant built from them do not respect the full [spin symmetry](@entry_id:197993) of the true Hamiltonian. For a single UHF determinant with $N_\alpha$ spin-$\alpha$ electrons and $N_\beta$ spin-$\beta$ electrons, the expectation value of $\hat{S}^2$ is given by (in [atomic units](@entry_id:166762), $\hbar=1$):
$$
\langle \hat{S}^2 \rangle = M_S(M_S+1) + N_\beta - \sum_{i=1}^{N_\alpha} \sum_{j=1}^{N_\beta} |\langle \phi_i^\alpha | \phi_j^\beta \rangle|^2
$$
where $M_S = (N_\alpha - N_\beta)/2$. For a two-electron system ($N_\alpha=1, N_\beta=1$) intended to be a singlet ($S=0, M_S=0$), the UHF determinant is $|a\alpha, b\beta\rangle$. The formula gives $\langle \hat{S}^2 \rangle = 0(1) + 1 - |\langle a|b \rangle|^2 = 1 - |s|^2$, where $s$ is the spatial overlap. The contamination is $1-|s|^2$. The state is a pure singlet ($\langle \hat{S}^2 \rangle = 0$) only if the orbitals are identical ($|s|=1$, the restricted RHF case). Conversely, in the limit where the orbitals become orthogonal ($s \to 0$), such as in [bond dissociation](@entry_id:275459), the expectation value approaches $\langle \hat{S}^2 \rangle \to 1$, indicating a 50/50 mixture of singlet and triplet character. For any intermediate case ($0  |s|  1$), the state is spin-contaminated [@problem_id:2911631].

#### Restricted Open-Shell Hartree-Fock (ROHF)

The **Restricted Open-Shell Hartree-Fock (ROHF)** method provides a way to retain a mean-field picture while rigorously preserving [spin symmetry](@entry_id:197993). The ROHF ansatz partitions the spatial orbitals into three subspaces: a **core** of doubly occupied orbitals, an **open-shell** space of singly occupied orbitals that determine the net spin, and a **virtual** space of unoccupied orbitals [@problem_id:2911606].

The crucial constraint in ROHF is that for every doubly occupied core orbital, the spatial part is identical for both the $\alpha$ and $\beta$ electrons. This ensures that the closed-shell core is a pure spin singlet ($S=0$) and does not contribute to spin contamination [@problem_id:2911606]. The [total spin](@entry_id:153335) of the molecule is therefore determined entirely by the electrons in the open-shell space.

For the highest possible [spin multiplicity](@entry_id:263865) (e.g., a high-spin doublet, triplet, etc.), the ROHF wavefunction can be represented by a single Slater determinant which is a pure spin state. For lower [multiplicity](@entry_id:136466) open-shell states (e.g., a low-spin doublet arising from three open-shell electrons), a single determinant is insufficient. In these cases, the ROHF reference state must be constructed as a specific, fixed linear combination of determinants—a CSF—to ensure it is an [eigenfunction](@entry_id:149030) of $\hat{S}^2$ [@problem_id:2911606]. The ROHF orbital optimization procedure then minimizes the energy of this spin-adapted CSF.

### Spin Symmetry and Electron Correlation

The choice between spin-restricted and spin-unrestricted descriptions is deeply intertwined with the problem of electron correlation, particularly the distinction between dynamic and static correlation.

#### The Role of Static Correlation

**Static (or nondynamical) correlation** becomes important in systems with two or more nearly degenerate electronic configurations. Classic examples include molecules with stretched or broken bonds, biradicals, and many [transition metal complexes](@entry_id:144856). In these cases, a single-determinant description is qualitatively incorrect. For the dissociation of $\text{H}_2$, the ground state at large separation is a perfect 50/50 mixture of two [determinants](@entry_id:276593). A restricted wavefunction, forced to doubly occupy a single molecular orbital, incorrectly includes unphysical ionic ($H^+ \cdots H^-$) character and gives a dramatically incorrect [dissociation energy](@entry_id:272940).

#### Broken Symmetry in Density Functional Theory (DFT)

This problem extends to Kohn-Sham Density Functional Theory (KS-DFT). While the exact exchange-correlation (xc) functional would yield the correct spin-pure ground state density (e.g., $n_\alpha(\mathbf{r}) = n_\beta(\mathbf{r})$ for a singlet) [@problem_id:2911660], common approximate functionals (LDAs, GGAs, and even some hybrids) struggle with [static correlation](@entry_id:195411).

In such cases, a spin-unrestricted (UKS) calculation can often find a **broken-symmetry solution** that is lower in energy than the spin-restricted (RKS) one. For singlet $\text{H}_2$ at large separation, the UKS calculation will yield a solution where the $\alpha$ electron localizes on one H atom and the $\beta$ electron on the other. This state has a non-zero [spin density](@entry_id:267742) ($n_\alpha \neq n_\beta$) and significant [spin contamination](@entry_id:268792) ($\langle \hat{S}^2 \rangle \approx 1$). While formally incorrect from a symmetry standpoint, this broken-symmetry solution provides a much better description of the energy by correctly describing two neutral atoms and eliminating the unphysical ionic terms that plague the RKS solution [@problem_id:2911660]. This behavior is a useful artifact of approximate DFT, where breaking [spin symmetry](@entry_id:197993) allows the method to mimic the effects of [static correlation](@entry_id:195411). This propensity for symmetry breaking is driven by the reduction of [self-interaction error](@entry_id:139981), which is exaggerated when two electrons are forced into the same spatial orbital [@problem_id:2911660]. As the [electronic coupling](@entry_id:192828) between the radical centers increases (e.g., at shorter bond lengths), the static correlation diminishes, and the spin-symmetric RKS solution correctly becomes the ground state.

#### High-Spin vs. Low-Spin States

The ultimate spin state of a molecule is determined by the energetic balance between one-electron [orbital energies](@entry_id:182840) and two-electron repulsion and exchange effects. A simple model can be constructed where electrons occupy orbitals split by an energy gap $\Delta$. Placing two electrons in the same low-lying orbital costs a large Coulomb repulsion energy $U$. Placing them in different orbitals costs the orbital promotion energy $\Delta$ plus a smaller repulsion $V$. The high-spin (triplet) arrangement is further stabilized by an exchange energy $K$. The low-spin (singlet) state is favored if the orbital gap is large, while the [high-spin state](@entry_id:155923) is favored if the pairing energy $P = U-V$ and exchange energy $K$ are dominant. The condition for the [high-spin state](@entry_id:155923) to be the ground state is approximately $\Delta  P + K$ [@problem_id:2911681]. This energetic competition dictates whether a system will have an open-shell or closed-shell ground state.

### The Limits of Spin Symmetry: Spin-Orbit Coupling

The entire theoretical framework discussed thus far rests on a fundamental assumption: that the electronic Hamiltonian is independent of spin. This is a nonrelativistic approximation. When [relativistic effects](@entry_id:150245) are considered, this assumption breaks down.

#### When Spin is Not Conserved

The most significant relativistic effect in this context is **spin-orbit coupling (SOC)**, which describes the interaction between an electron's [spin magnetic moment](@entry_id:272337) and the magnetic field generated by its [orbital motion](@entry_id:162856) around the nuclei. The SOC operator explicitly couples the spin and spatial degrees of freedom. Consequently, the full relativistic Hamiltonian, $\hat{H}_{rel} = \hat{H}_{nonrel} + \hat{H}_{SOC}$, no longer commutes with $\hat{S}^2$ or the orbital [angular momentum operator](@entry_id:155961) $\hat{L}^2$.
$$
[\hat{H}_{rel}, \hat{S}^2] \neq 0
$$
This means that $S$ is no longer a "good" quantum number. The true [stationary states](@entry_id:137260) of the system are not pure singlets, doublets, or triplets. Instead, they are mixtures of states with different spin (and orbital) angular momentum. The only conserved quantity is the total [electronic angular momentum](@entry_id:198934), $\hat{\mathbf{J}} = \hat{\mathbf{L}} + \hat{\mathbf{S}}$.

#### A Model System

This mixing can be demonstrated with a simple model Hamiltonian for two coupled spin-1/2 centers that includes an effective SOC term, the Dzyaloshinskii-Moriya (DM) interaction [@problem_id:2911694]:
$$
\hat{H} = J\,\hat{\mathbf{S}}_{1}\cdot\hat{\mathbf{S}}_{2} + D_{z}\,\big(\hat{S}_{1}^{x}\hat{S}_{2}^{y} - \hat{S}_{1}^{y}\hat{S}_{2}^{x}\big)
$$
The first term is the standard Heisenberg exchange, which is diagonal in the basis of total spin eigenstates $\{|S\rangle, |T_0\rangle\}$. The second term, representing the DM interaction, can be shown to have non-zero matrix elements coupling the [singlet and triplet states](@entry_id:148894). The resulting Hamiltonian matrix in this basis is not diagonal, and its commutator with the [matrix representation](@entry_id:143451) of $\hat{S}^2$ is non-zero when $D_z \neq 0$. This explicitly proves that the [eigenstates](@entry_id:149904) of this Hamiltonian are [linear combinations](@entry_id:154743) of the pure [singlet and triplet states](@entry_id:148894), and that total spin is not conserved.

#### Implications for Spin Projection

The non-conservation of spin has serious implications for methods that rely on [spin symmetry](@entry_id:197993), such as the spin-projection techniques used to "correct" the energy of broken-symmetry UHF or UKS solutions. These [projection methods](@entry_id:147401) rely on the assumption that the contaminated state is a simple mixture of pure spin states that are degenerate in the absence of exchange. When SOC is present, this assumption is violated because the Hamiltonian itself mixes spin states. Different [spin projection](@entry_id:184359) formalisms, which are equivalent when spin is conserved, can yield different energies when it is not [@problem_id:2911694]. This highlights that in the presence of significant [relativistic effects](@entry_id:150245), the very concept of assigning a single [spin multiplicity](@entry_id:263865) $S$ to an electronic state becomes an approximation, and a more rigorous treatment in terms of the total angular momentum $J$ is required.