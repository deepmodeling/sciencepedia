## Introduction
In the quantum world of molecules, electrons occupy intricate energy states whose properties dictate the very nature of chemical bonds, molecular structure, and reactivity. To navigate this complexity, scientists use a powerful shorthand known as the **molecular term symbol**. This concise notation, inherited from atomic physics, distills the essential symmetry and angular momentum properties of an electronic state into a single expression. However, decoding and applying these symbols requires a firm grasp of fundamental quantum mechanical principles. This article bridges that gap by providing a comprehensive guide to molecular [term symbols](@entry_id:151575), primarily for [diatomic molecules](@entry_id:148655). The first chapter, **Principles and Mechanisms**, will systematically deconstruct the [term symbol](@entry_id:171918), explaining the physical meaning of each component. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these symbols are used to predict molecular properties, interpret complex spectra, and rationalize [chemical reactivity](@entry_id:141717). Finally, **Hands-On Practices** will offer guided problems to reinforce these concepts, solidifying your ability to translate electronic configurations into the language of [term symbols](@entry_id:151575).

## Principles and Mechanisms

The electronic structure of a molecule is a complex tapestry woven from the kinetic and potential energies of its constituent electrons and nuclei. Within the Born-Oppenheimer approximation, we can consider the [electronic states](@entry_id:171776) for a fixed nuclear geometry. A **molecular [term symbol](@entry_id:171918)** is a powerful and concise notation, inherited from [atomic spectroscopy](@entry_id:155968), that summarizes the essential angular momentum and symmetry properties of a given electronic state. Understanding these symbols is paramount to interpreting molecular spectra and comprehending the nature of chemical bonds. This chapter will deconstruct the molecular [term symbol](@entry_id:171918) for [diatomic molecules](@entry_id:148655), revealing the quantum mechanical principles that each component encodes.

### Decoding the Diatomic Term Symbol: $^{2S+1}\Lambda_{\Omega}^{\pm}(\mathrm{g/u})$

For a diatomic molecule, where the potential has [cylindrical symmetry](@entry_id:269179) about the internuclear axis, the electronic state is conventionally written as $^{2S+1}\Lambda_{\Omega}^{\pm}(\mathrm{g/u})$. Each part of this symbol represents a specific physical quantity or symmetry property of the electronic wavefunction. We will dissect each component, building a complete picture of the state it describes [@problem_id:2653019].

#### Total Electronic Spin and Multiplicity ($S$ and $2S+1$)

The superscript to the left of the main symbol represents the **spin multiplicity**. It is defined as $2S+1$, where $S$ is the **total electronic spin quantum number**. This number arises from the vector sum of the individual spin angular momenta of all electrons in the molecule.

*   If $S=0$, the multiplicity is 1, and the state is a **singlet**. This occurs when all electron spins are paired.
*   If $S=1/2$, the [multiplicity](@entry_id:136466) is 2, and the state is a **doublet**. This implies one unpaired electron.
*   If $S=1$, the multiplicity is 3, and the state is a **triplet**. This corresponds to two [unpaired electrons](@entry_id:137994) with parallel spins.

In general, for a [total spin](@entry_id:153335) $S$, the number of [unpaired electrons](@entry_id:137994) $n$ is given by $n = 2S$, assuming all other electrons are paired. For example, if a [spectroscopic analysis](@entry_id:755197) identifies a molecular state with the [term symbol](@entry_id:171918) $^4\Sigma_g^-$, the spin multiplicity is 4. From the relation $2S+1 = 4$, we find that the total spin [quantum number](@entry_id:148529) is $S = 3/2$. This indicates the presence of $n = 2S = 3$ unpaired electrons in the molecule [@problem_id:2004591].

#### Projection of Orbital Angular Momentum ($\Lambda$)

In the strong axial electric field of a [diatomic molecule](@entry_id:194513), the total electronic orbital angular momentum vector $\mathbf{L}$ is not conserved; it precesses rapidly around the internuclear axis (let's define this as the $z$-axis). Consequently, the quantum number $L$ is not a "good" [quantum number](@entry_id:148529). However, the projection of $\mathbf{L}$ onto this axis, $L_z$, *is* conserved. The [quantum number](@entry_id:148529) associated with this projection is $M_L = \sum_i m_{l,i}$, where the sum is over all electrons.

The energy of the electronic state depends on the magnitude of this axial angular momentum, but not on its direction (i.e., whether the electrons are circulating "clockwise" or "counter-clockwise"). Therefore, states with $M_L$ and $-M_L$ are degenerate (for $M_L \ne 0$). The [term symbol](@entry_id:171918) uses the quantum number $\Lambda$, which is the absolute value of the total projection:

$\Lambda = |M_L|$

By convention, numerical values of $\Lambda$ are represented by Greek capital letters, in analogy with the s, p, d, f notation for atomic orbitals:

*   $\Lambda = 0 \rightarrow \Sigma$ state
*   $\Lambda = 1 \rightarrow \Pi$ state
*   $\Lambda = 2 \rightarrow \Delta$ state
*   $\Lambda = 3 \rightarrow \Phi$ state

For instance, a state identified by the term symbol $^3\Delta_u$ is a [triplet state](@entry_id:156705) ($S=1$) and, from the symbol $\Delta$, must have a [total orbital angular momentum](@entry_id:265302) projection of $\Lambda=2$ [@problem_id:2004581]. For any molecule in a **closed-shell** configuration, where all molecular orbitals are fully occupied, the contributions to $M_L$ from individual electrons cancel out, resulting in $\Lambda=0$. Such molecules always have a $\Sigma$ ground state [@problem_id:2004578].

#### Symmetry Properties I: Inversion Parity (g/u)

For molecules that possess a [center of inversion](@entry_id:273028), such as all **homonuclear [diatomic molecules](@entry_id:148655)** (e.g., $N_2$, $O_2$), the electronic wavefunction must have a definite symmetry with respect to the inversion operation, $\hat{\mathcal{I}}$. This operator transforms the coordinates of every electron $\mathbf{r}_i$ to $-\mathbf{r}_i$ relative to the inversion center (the midpoint of the internuclear axis).

Since applying the inversion operator twice returns the original state ($\hat{\mathcal{I}}^2 = \hat{1}$), its eigenvalues must be either $+1$ or $-1$.
*   If $\hat{\mathcal{I}}\Psi_{el} = +\Psi_{el}$, the wavefunction is symmetric with respect to inversion. It is said to have [even parity](@entry_id:172953) and is labeled with a subscript **g** for **gerade** (German for "even").
*   If $\hat{\mathcal{I}}\Psi_{el} = -\Psi_{el}$, the wavefunction is antisymmetric. It has [odd parity](@entry_id:175830) and is labeled with a subscript **u** for **[ungerade](@entry_id:147965)** ("odd").

This g/u subscript is only used for [centrosymmetric molecules](@entry_id:166437). For [heteronuclear diatomics](@entry_id:150148) like CO or HCl, which lack an inversion center, this label is omitted.

The overall parity of a multi-electron state can be determined from the parities of the individual occupied molecular orbitals (MOs). The total parity is the product of the parities of each occupied orbital. This is often called the **product rule**. A key consequence of this rule is that any filled MO, regardless of its own parity, contributes a gerade ($+1$) factor to the total state parity. This is because a doubly occupied gerade orbital contributes $(+1) \times (+1) = +1$, and a doubly occupied ungerade orbital contributes $(-1) \times (-1) = +1$. Therefore, the overall parity of a state is determined solely by the product of the parities of the singly occupied orbitals. For example, a configuration with all orbitals doubly occupied except for one electron in a $\pi_u$ orbital and one in a $\sigma_g$ orbital will have an overall parity of $u \times g = u$ (since $(-1) \times (+1) = -1$) [@problem_id:2653038].

#### Symmetry Properties II: Reflection Symmetry ($\pm$)

For $\Sigma$ states ($\Lambda=0$), the [term symbol](@entry_id:171918) includes a superscript $+$ or $-$ to denote the symmetry of the electronic wavefunction upon reflection through *any* plane containing the internuclear axis (a $\sigma_v$ plane).
*   If the wavefunction is symmetric with respect to this reflection, it is labeled $\Sigma^+$.
*   If the wavefunction is antisymmetric, it is labeled $\Sigma^-$.

A crucial question is why this label is reserved exclusively for $\Sigma$ states. The reason lies in the degeneracy of states with $\Lambda > 0$ [@problem_id:2653027]. A state with $\Lambda > 0$ is doubly degenerate, corresponding to the two components with $M_L = +\Lambda$ and $M_L = -\Lambda$. A reflection operation $\hat{\sigma}_v$ does not leave these components unchanged; instead, it transforms one into the other. For example, acting on the state $|+\Lambda\rangle$, the reflection produces a state proportional to $|-\Lambda\rangle$. This means neither $|+\Lambda\rangle$ nor $|-\Lambda\rangle$ is an [eigenstate](@entry_id:202009) of the reflection operator. While one can form [linear combinations](@entry_id:154743) of these [degenerate states](@entry_id:274678) that *are* [eigenstates](@entry_id:149904) of a *specific* reflection plane, these combinations will not be [eigenstates](@entry_id:149904) for a reflection in a different plane. Since there is no unique, plane-independent reflection symmetry, the $\pm$ label is not meaningful for $\Pi, \Delta$, etc., states.

In contrast, $\Sigma$ states ($\Lambda=0$) are non-degenerate with respect to orbital angular momentum. The wavefunction for a $\Sigma$ state must therefore be an eigenfunction of the reflection operator for *any* vertical plane, with a consistent eigenvalue of $+1$ or $-1$.

A simple rule is that a closed-shell configuration is totally symmetric under all operations, so its [term symbol](@entry_id:171918) is always $^1\Sigma^+$ (or $^1\Sigma_g^+$ for homonuclear diatomics) [@problem_id:2004578]. For open-shell configurations, the symmetry must be explicitly determined. For example, consider a state arising from a $(\pi)^2$ configuration where the two electrons have parallel spins. The Pauli exclusion principle requires that the spatial part of the wavefunction be antisymmetric. This [antisymmetry](@entry_id:261893) leads to the state being antisymmetric upon reflection, resulting in a $^3\Sigma^-$ term [@problem_id:2004567].

### Coupling of Angular Momenta and Fine Structure

The various electronic angular momenta—spin and orbital—can couple to one another, a phenomenon known as **[spin-orbit coupling](@entry_id:143520)**. This coupling splits a single term into multiple, closely-spaced energy levels, known as **[fine structure](@entry_id:140861)**. The way these momenta couple depends on the relative strengths of the interactions, described by **Hund's coupling cases**. The most common is Hund's case (a).

#### Hund's Case (a) and the Quantum Number $\Omega$

Hund's case (a) applies to most light [diatomic molecules](@entry_id:148655). In this scheme, the electronic orbital angular momentum $\mathbf{L}$ and the spin angular momentum $\mathbf{S}$ are strongly coupled to the internuclear axis, but only weakly coupled to each other. We have already defined the projection of $\mathbf{L}$ on the axis ($\Lambda$). Similarly, we can define $\Sigma$ (not to be confused with the symbol for a $\Lambda=0$ state) as the [quantum number](@entry_id:148529) for the projection of the [total spin](@entry_id:153335) $\mathbf{S}$ onto the internuclear axis. $\Sigma$ can take on the $2S+1$ integer or half-integer values from $-S$ to $+S$.

The projection of the *total* [electronic angular momentum](@entry_id:198934), $\mathbf{J}_e = \mathbf{L} + \mathbf{S}$, onto the internuclear axis is given by the [quantum number](@entry_id:148529) $M_J = \Lambda + \Sigma$. The [term symbol](@entry_id:171918) uses the [quantum number](@entry_id:148529) $\Omega$, which is the absolute value of this total projection:

$\Omega = |M_L + \Sigma|$

The different possible values of $\Omega$ for a given $\Lambda$ and $S$ correspond to the different fine-structure levels. As a concrete example, let's determine the possible values of $\Omega$ for a molecule in a $^2\Pi$ state [@problem_id:2004565].
1.  The superscript 2 indicates a doublet state, so $2S+1=2$, which gives $S=1/2$.
2.  The possible values for the [spin projection](@entry_id:184359) are $\Sigma = -1/2, +1/2$.
3.  The symbol $\Pi$ indicates that $\Lambda=1$. This corresponds to [degenerate states](@entry_id:274678) with $M_L = +1$ and $M_L = -1$.
4.  We calculate the possible values of $M_L + \Sigma$:
    *   For $M_L = +1$: $1 + 1/2 = 3/2$ and $1 - 1/2 = 1/2$.
    *   For $M_L = -1$: $-1 + 1/2 = -1/2$ and $-1 - 1/2 = -3/2$.
5.  The possible values of $\Omega = |M_L + \Sigma|$ are therefore $1/2$ and $3/2$. This means the $^2\Pi$ term splits into two fine-structure levels, which are denoted $^2\Pi_{1/2}$ and $^2\Pi_{3/2}$.

### From Electron Configurations to Term Symbols

One of the most important applications of this formalism is predicting the [electronic states](@entry_id:171776) that arise from a given electron configuration and identifying the ground state among them.

#### Hund's Rules for Molecules

When an open-shell configuration gives rise to multiple electronic terms, their relative energies can be predicted by a set of empirical rules known as **Hund's rules**, adapted for molecules.

1.  **Rule 1 (Maximum Multiplicity):** The term with the highest spin multiplicity ($2S+1$) has the lowest energy.
2.  **Rule 2 (Maximum Orbital Angular Momentum):** For terms with the same multiplicity, the one with the highest value of $\Lambda$ has the lowest energy.

Let's apply these rules to a common and important example: the $(\pi_g)^2$ configuration, found in the $O_2$ molecule. This configuration gives rise to three distinct terms: $^1\Sigma_g^+$, $^3\Sigma_g^-$, and $^1\Delta_g$ [@problem_id:1994555].

*   Applying Rule 1: The spin multiplicities are 1, 3, and 1. The highest multiplicity is 3, corresponding to the $^3\Sigma_g^-$ term. Therefore, $^3\Sigma_g^-$ is the ground state.
*   Applying Rule 2: To order the remaining two singlet states, we compare their $\Lambda$ values. For $^1\Sigma_g^+$, $\Lambda=0$. For $^1\Delta_g$, $\Lambda=2$. Since $2 > 0$, the $^1\Delta_g$ state is lower in energy than the $^1\Sigma_g^+$.

The predicted energy ordering for the states from the $(\pi_g)^2$ configuration is thus $E(^3\Sigma_g^-) \lt E(^1\Delta_g) \lt E(^1\Sigma_g^+)$, which is experimentally confirmed.

### Beyond Hund's Case (a): Strong Spin-Orbit Coupling

The framework described so far, Hund's case (a), assumes that spin-orbit coupling is weak compared to the electrostatic interactions that couple $\mathbf{L}$ and $\mathbf{S}$ to the internuclear axis. For molecules containing heavy atoms (e.g., $Bi_2$), this assumption breaks down. The interaction between an electron's spin and its own [orbital motion](@entry_id:162856) can become so strong that it is more important to consider the [total angular momentum](@entry_id:155748) of each individual electron first. This leads to **Hund's case (c)**.

In this regime, $\Lambda$ and $S$ are no longer [good quantum numbers](@entry_id:262514) because the spin-orbit interaction mixes states with different $\Lambda$ and $S$. Instead, we define a quantum number for the projection of each *individual* electron's [total angular momentum](@entry_id:155748) ($\mathbf{j}_i = \mathbf{l}_i + \mathbf{s}_i$) onto the internuclear axis. This is denoted by $\omega_i = \lambda_i + \sigma_i$. The total projection for the molecule, $\Omega$, is then the sum of these individual projections, $\Omega = |\sum_i \omega_i|$.

The primary consequence is a different pattern of energy levels. For example, consider an excited configuration $(\pi_g)^1(\sigma_u)^1$ in a heavy diatomic molecule [@problem_id:2004564].
*   For the $\pi$ electron, $\lambda = \pm 1$ and $\sigma = \pm 1/2$. The possible $\omega$ values are $\pm 3/2$ and $\pm 1/2$. Due to strong [spin-orbit coupling](@entry_id:143520), the states with $|\omega|=3/2$ and $|\omega|=1/2$ have significantly different energies.
*   For the $\sigma$ electron, $\lambda=0$ and $\sigma = \pm 1/2$, so $\omega = \pm 1/2$.

Coupling these one-electron states gives the possible total $|\Omega|$ values. Combining the $|\omega_\pi|=3/2$ manifold with $|\omega_\sigma|=1/2$ gives rise to states with $|\Omega|=1$ and $|\Omega|=2$. Combining the $|\omega_\pi|=1/2$ manifold with $|\omega_\sigma|=1/2$ gives states with $|\Omega|=0$ and $|\Omega|=1$. Note that we obtain two distinct states with $|\Omega|=1$. Furthermore, for homonuclear molecules, states with $\Omega=0$ split into two levels, $0^+$ and $0^-$, based on reflection symmetry. In total, this configuration yields five distinct energy levels ($|\Omega|=2$, two distinct $|\Omega|=1$ levels, and the $0^+$ and $0^-$ levels), a richer structure than would be predicted by a simple Hund's case (a) analysis. This illustrates how the term symbol formalism adapts to different physical regimes, providing an indispensable tool for deciphering the intricate world of molecular electronic structure.