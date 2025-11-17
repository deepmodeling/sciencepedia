## Introduction
The intricate [electronic states of diatomic molecules](@entry_id:185408) are elegantly captured by a compact notation known as the molecular term symbol. This powerful shorthand, based on quantum mechanics and [molecular symmetry](@entry_id:142855), is the language spectroscopists and chemists use to describe and differentiate the myriad energy levels a molecule can possess. Without a systematic framework, interpreting the dense [line spectra](@entry_id:144909) of molecules or predicting their fundamental properties like magnetism would be an insurmountable task. Molecular [term symbols](@entry_id:151575) provide this essential framework, bridging the gap between abstract quantum theory and tangible experimental observation.

This article will guide you through the complete landscape of [molecular term symbols](@entry_id:167434). In **Principles and Mechanisms**, we will deconstruct the term symbol piece by piece, exploring the quantum mechanical origins of each label. Following this, **Applications and Interdisciplinary Connections** will demonstrate how these symbols are used to predict chemical properties, interpret spectra, and connect to fields like [statistical thermodynamics](@entry_id:147111) and computational chemistry. Finally, **Hands-On Practices** will offer a chance to apply these principles to concrete examples, solidifying your understanding.

## Principles and Mechanisms

The electronic structure of [diatomic molecules](@entry_id:148655) is elegantly summarized by a compact notation known as the **molecular term symbol**. This symbol, in its complete form $^{2S+1}\Lambda_{\Omega}^{\pm}(\mathrm{g/u})$, encodes the essential angular momentum and symmetry properties of a given electronic state. Understanding the principles and mechanisms that give rise to each component of this symbol is fundamental to interpreting molecular spectra and understanding chemical bonding. This chapter deconstructs the term symbol, exploring the quantum mechanical origins of each label from first principles.

### The Quantum Numbers of the Internuclear Axis

In a diatomic molecule, the two nuclei define a unique axis in space. The [electrostatic potential](@entry_id:140313) experienced by the electrons is not spherically symmetric, as in an atom, but possesses [cylindrical symmetry](@entry_id:269179) about this internuclear axis. This has a profound consequence: the total electronic orbital [angular momentum operator](@entry_id:155961), $\mathbf{L}$, does not commute with the electronic Hamiltonian. Therefore, its magnitude (characterized by the quantum number $L$) is not a conserved quantity, or a "good" quantum number. However, the component of the orbital angular momentum along the internuclear axis, conventionally designated as the $z$-axis, *is* conserved.

For each individual electron $i$, we can define a quantum number $\lambda_i$ that represents the projection of its orbital angular momentum, $\mathbf{l}_i$, onto the internuclear axis (in units of $\hbar$). The requirement that the electronic wavefunction must be single-valued upon a full $2\pi$ rotation about the axis constrains these $\lambda_i$ values to be integers ($\lambda_i = 0, \pm 1, \pm 2, \dots$). The total projection of the orbital angular momentum for the multi-electron state is the sum of these individual contributions, $M_L = \sum_i \lambda_i$.

The energy of the electronic state in the absence of external fields depends on the magnitude of this total projection, but not on its sign (i.e., whether the electrons are orbiting clockwise or counter-clockwise). We therefore define the primary [quantum number](@entry_id:148529) for the [term symbol](@entry_id:171918), $\Lambda$, as the absolute value of the total projection: $\Lambda = |M_L|$. By convention, the numerical values of $\Lambda$ are denoted by Greek capital letters:

*   $\Lambda = 0$: a $\Sigma$ state
*   $\Lambda = 1$: a $\Pi$ state
*   $\Lambda = 2$: a $\Delta$ state
*   $\Lambda = 3$: a $\Phi$ state
...and so on alphabetically. States with $\Lambda > 0$ are doubly degenerate, corresponding to the two possibilities $M_L = +\Lambda$ and $M_L = -\Lambda$. States with $\Lambda = 0$ are non-degenerate in this respect. [@problem_id:2653019] [@problem_id:2653022]

To illustrate how $\Lambda$ is determined from an electronic configuration, consider a hypothetical state where one electron occupies a $\pi$ molecular orbital ($|\lambda_1|=1$) and a second electron occupies a $\delta$ molecular orbital ($|\lambda_2|=2$). The possible values for the total projection $M_L$ are derived from all combinations of the individual projections: $M_L = \lambda_1 + \lambda_2$. This gives $M_L = (+1)+(+2)=+3$, $(+1)+(-2)=-1$, $(-1)+(+2)=+1$, and $(-1)+(-2)=-3$. The possible magnitudes are therefore $\Lambda = |M_L| = 1$ and $3$. This configuration would give rise to both $\Pi$ and $\Phi$ [electronic states](@entry_id:171776). [@problem_id:2653022]

### Electron Spin and Multiplicity

The next component of the [term symbol](@entry_id:171918), the superscript, describes the total [electron spin](@entry_id:137016). For a multi-electron system, the individual electron spins $\mathbf{s}_i$ (each with quantum number $s=1/2$) couple to form a total electron [spin angular momentum](@entry_id:149719) $\mathbf{S}$. The magnitude of this [total spin](@entry_id:153335) is characterized by the [quantum number](@entry_id:148529) $S$.

For a configuration with $n$ unpaired electrons, each residing in a distinct spatial molecular orbital, the possible values of the total spin [quantum number](@entry_id:148529) $S$ can be found by applying the rules of [angular momentum addition](@entry_id:156081). Starting with one electron ($S=1/2$), and sequentially adding the spin of the next, one finds that the possible values for the [total spin](@entry_id:153335) $S$ range from a maximum of $S_{max} = n/2$ (all spins aligned) down to a minimum of $S_{min} = 1/2$ (if $n$ is odd) or $S_{min} = 0$ (if $n$ is even), in integer steps. The total number of distinct spin states that can be formed is given by the expression $\lfloor n/2 \rfloor + 1$. [@problem_id:2653000]

The [term symbol](@entry_id:171918) does not report $S$ directly, but rather the **spin multiplicity**, defined as $2S+1$. This value represents the number of possible projections of the total spin vector $\mathbf{S}$ onto an axis.
*   $S=0$: Multiplicity = 1 (**singlet** state)
*   $S=1/2$: Multiplicity = 2 (**doublet** state)
*   $S=1$: Multiplicity = 3 (**triplet** state)

The spin multiplicity is written as a pre-superscript, as in ${}^3\Pi$ for a triplet Pi state. [@problem_id:2653019]

The relative energies of terms arising from the same [electronic configuration](@entry_id:272104) are governed primarily by electron-electron Coulomb repulsion, a principle codified in **Hund's Rules**. Hund's first rule states that for a given configuration, the term with the highest spin multiplicity is lowest in energy. The quantum mechanical origin of this rule lies in the Pauli exclusion principle, which requires the total wavefunction of a system of electrons to be antisymmetric with respect to the exchange of any two electrons.

Since the Hamiltonian is spin-independent (in this approximation), the total wavefunction can be written as a product of a spatial part and a spin part. For the total product to be antisymmetric, a symmetric spin function must be paired with an antisymmetric spatial function, and vice versa. A [high-spin state](@entry_id:155923) (like a triplet, $S=1$) has a symmetric spin function. Consequently, its spatial wavefunction must be antisymmetric. An antisymmetric spatial wavefunction vanishes whenever two electrons are at the same point in space, creating what is known as a **Fermi hole**. This enforced separation keeps the electrons further apart on average, reducing their mutual Coulombic repulsion and thus lowering the energy of the state. Conversely, a [low-spin state](@entry_id:149561) (like a singlet, $S=0$) has an antisymmetric spin function, requiring a symmetric spatial function, which allows electrons to be closer together, increasing their repulsion energy.

A classic example is the $\pi_g^2$ configuration, found in the ground state of the O$_2$ molecule. This configuration gives rise to three terms: ${}^3\Sigma_g^{-}$, ${}^1\Delta_g$, and ${}^1\Sigma_g^{+}$. The term with the highest multiplicity is the triplet, ${}^3\Sigma_g^{-}$. According to Hund's rule, this is correctly predicted to be the ground electronic state. [@problem_id:2653047]

### Symmetry Properties of the Electronic Wavefunction

The remaining labels on the [term symbol](@entry_id:171918), the g/u subscript and the $\pm$ superscript, describe how the total electronic wavefunction transforms under specific symmetry operations of the molecular framework.

#### Inversion Symmetry: Gerade and Ungerade Parity

For **homonuclear [diatomic molecules](@entry_id:148655)** (e.g., N$_2$, O$_2$), the two nuclei are identical. This confers an additional element of symmetry: a center of inversion, $i$, located at the midpoint of the internuclear bond. The [molecular point group](@entry_id:191277) is $D_{\infty h}$. The electronic Hamiltonian is invariant under the inversion operation, $\hat{\mathcal{I}}$, which transforms the coordinates of every electron $\mathbf{r}_i$ to $-\mathbf{r}_i$. As a result, electronic wavefunctions can be classified by their behavior under this operation. Since applying the inversion operator twice returns the original state ($\hat{\mathcal{I}}^2 = \hat{1}$), the eigenvalues of $\hat{\mathcal{I}}$ must be either $+1$ or $-1$.

*   If $\hat{\mathcal{I}}\Psi = +\Psi$, the wavefunction is symmetric with respect to inversion and is labeled **gerade** (German for "even"), denoted by a subscript **g**.
*   If $\hat{\mathcal{I}}\Psi = -\Psi$, the wavefunction is antisymmetric with respect to inversion and is labeled **ungerade** (German for "odd"), denoted by a subscript **u**.

This g/u parity label is applicable to all [electronic states](@entry_id:171776) ($\Sigma, \Pi, \Delta$, etc.) of a homonuclear diatomic. **Heteronuclear [diatomic molecules](@entry_id:148655)** (e.g., CO, HCl), which belong to the $C_{\infty v}$ point group, lack a [center of inversion](@entry_id:273028), and thus their [term symbols](@entry_id:151575) do not carry a g/u label. [@problem_id:2653028]

The overall parity of a multi-electron state is determined by the parities of the individual molecular orbitals (MOs) occupied by the electrons. The rule is that the total parity is the product of the parities of all occupied orbitals. A key consequence of this rule is that any filled MO, or **closed shell**, contributes a factor of $(p_{MO})^2$ to the total parity. Since both $(+1)^2=1$ and $(-1)^2=1$, any closed shell, whether composed of g or u orbitals, always has an overall gerade parity. Therefore, the total parity of a state is determined solely by the product of the parities of the electrons in the partially filled (open-shell) orbitals. For instance, a configuration with open shells $(\pi_u)^1(\sigma_g)^1$ would have a total parity of $u \times g = u$, resulting in an [ungerade](@entry_id:147965) state. [@problem_id:2653038]

#### Reflection Symmetry: The $\pm$ Label for $\Sigma$ States

All [linear molecules](@entry_id:166760), both homonuclear and heteronuclear, possess an infinite number of reflection planes, $\sigma_v$, that contain the internuclear axis. The term symbol can include a superscript, $+$ or $-$, that describes the wavefunction's behavior upon reflection through one of these planes. However, this label is exclusively applied to $\Sigma$ states ($\Lambda=0$). [@problem_id:2653019]

The reason for this exclusivity is rooted in the transformation properties of the wavefunctions. A reflection $\hat{\sigma}_v$ transforms the azimuthal angle as $\phi \to -\phi$ (for a plane at $\phi=0$).

*   For a **$\Sigma$ state** ($\Lambda=0$), the electronic wavefunction is non-degenerate and its azimuthal dependence is constant. It must therefore be an eigenfunction of the reflection operator. Crucially, its eigenvalue ($+1$ for symmetric, $-1$ for antisymmetric) is the same regardless of which $\sigma_v$ plane is chosen for the reflection. This plane-independent eigenvalue makes the $\pm$ label a well-defined, [good quantum number](@entry_id:263156). We denote these states as $\Sigma^+$ and $\Sigma^-$. [@problem_id:2653027]

*   For states with **$\Lambda > 0$** ($\Pi, \Delta$, etc.), the situation is different. These states are doubly degenerate, spanned by components with [orbital angular momentum](@entry_id:191303) projections of $+\Lambda$ and $-\Lambda$ (e.g., corresponding to azimuthal dependencies of $e^{i\Lambda\phi}$ and $e^{-i\Lambda\phi}$). The reflection operator $\hat{\sigma}_v$ does not return these basis functions to themselves, but rather interchanges them: $\hat{\sigma}_v| \Lambda \rangle \propto |-\Lambda \rangle$. While it is possible to form linear combinations that are [eigenfunctions](@entry_id:154705) of reflection through one *specific* plane, these combinations are not eigenfunctions for reflection through any other plane. Since there is no plane-independent eigenvalue, no unambiguous $\pm$ label can be assigned, and it is omitted from the [term symbol](@entry_id:171918) for all states with $\Lambda > 0$. [@problem_id:2653027]

### The Group-Theoretical Foundation of Term Symbols

The classification scheme of [molecular term symbols](@entry_id:167434) finds its most rigorous expression in the language of group theory. The [electronic term symbols](@entry_id:192560) are, in fact, labels for the **[irreducible representations](@entry_id:138184) (irreps)** of the molecule's symmetry [point group](@entry_id:145002). For a homonuclear diatomic, this is the $D_{\infty h}$ group.

The quantum number $\Lambda$ directly relates to the character of the rotation operation $C_{\phi}$.
*   For $\Sigma$ states ($\Lambda=0$), which are one-dimensional, the wavefunction is invariant to rotation about the axis, so the character is $\chi(C_{\phi}) = 1$.
*   For $\Pi, \Delta, \dots$ states ($\Lambda>0$), which are two-dimensional, the character is given by $\chi(C_{\phi}) = 2\cos(\Lambda\phi)$.

The $\pm$ superscript for $\Sigma$ states corresponds to the character of the reflection operation, $\sigma_v$.
*   For $\Sigma^+$ states, the character is $\chi(\sigma_v) = +1$.
*   For $\Sigma^-$ states, the character is $\chi(\sigma_v) = -1$.
*   For all two-dimensional irreps ($\Lambda>0$), the reflection operation interchanges the basis functions, resulting in a [matrix representation](@entry_id:143451) with a trace of zero. Thus, for $\Pi, \Delta, \dots$ states, $\chi(\sigma_v) = 0$.

Finally, the g/u subscript corresponds to the character of the inversion operation, $i$. For g-states $\chi(i)=+1$ and for u-states $\chi(i)=-1$. This group-theoretical framework provides the ultimate justification for the rules and labels described in the previous sections. [@problem_id:2653009]

### Spin-Orbit Coupling and Total Electronic Angular Momentum

So far, we have treated orbital and spin angular momenta as independent. In reality, they interact via **spin-orbit coupling (SOC)**, a relativistic effect that couples the [spin magnetic moment](@entry_id:272337) with the magnetic field generated by the orbital motion of electrons. In the **Hund's case (a)** coupling scheme, which is common for many molecules, both orbital and spin angular momenta are strongly coupled to the internuclear axis.

We define $\Sigma$ as the quantum number for the projection of the [total spin](@entry_id:153335) $\mathbf{S}$ onto the internuclear axis; $\Sigma$ can take any integer or half-integer value from $-S$ to $+S$. The total [electronic angular momentum](@entry_id:198934) projection on the axis is then given by the quantum number $\Omega$, defined as:

$\Omega = |\Lambda + \Sigma|$

Spin-orbit coupling lifts the degeneracy of states that have the same $\Lambda$ and $S$ but different values of $\Omega$. This results in a splitting of a single term into several closely spaced **[fine structure](@entry_id:140861)** components, each labeled by its value of $\Omega$. The $\Omega$ value is appended as a subscript to the term symbol, as in ${}^{2S+1}\Lambda_\Omega$.

For example, let us determine the spin-orbit components for a ${}^{7}\Delta$ term. From the symbol, we deduce the spin multiplicity is $7$, so $2S+1=7 \Rightarrow S=3$. The symbol $\Delta$ means $\Lambda=2$. The possible values for the [spin projection](@entry_id:184359) are $\Sigma \in \{-3, -2, -1, 0, 1, 2, 3\}$. We can now calculate the possible values for $\Omega = |\Lambda + \Sigma| = |2 + \Sigma|$:
*   $\Sigma = -3 \Rightarrow \Omega = |2-3| = 1$
*   $\Sigma = -2 \Rightarrow \Omega = |2-2| = 0$
*   $\Sigma = -1 \Rightarrow \Omega = |2-1| = 1$
*   $\Sigma = 0 \Rightarrow \Omega = |2+0| = 2$
*   $\Sigma = 1 \Rightarrow \Omega = |2+1| = 3$
*   $\Sigma = 2 \Rightarrow \Omega = |2+2| = 4$
*   $\Sigma = 3 \Rightarrow \Omega = |2+3| = 5$

The set of unique $\Omega$ values is $\{0, 1, 2, 3, 4, 5\}$. Thus, the ${}^{7}\Delta$ term splits into six distinct fine-structure components: ${}^{7}\Delta_0$, ${}^{7}\Delta_1$, ${}^{7}\Delta_2$, ${}^{7}\Delta_3$, ${}^{7}\Delta_4$, and ${}^{7}\Delta_5$. [@problem_id:2653029]

### Coupling with Molecular Rotation: Hund's Cases

The electronic [term symbol](@entry_id:171918) provides the foundation for describing the full energy state of the molecule, which also includes rotation. The way electronic angular momenta couple with the end-over-end rotation of the molecule is described by **Hund's coupling cases**. The two most important limiting cases are determined by the relative strength of spin-orbit coupling versus the interaction of the electronic motion with the [molecular rotation](@entry_id:263843).

*   **Hund's Case (a)**: This limit applies when spin-orbit coupling is strong. Both $\mathbf{L}$ and $\mathbf{S}$ are strongly coupled to the internuclear axis, making their projections $\Lambda$ and $\Sigma$ (and thus $\Omega$) [good quantum numbers](@entry_id:262514). The [total angular momentum](@entry_id:155748) of the molecule, $\mathbf{J}$, is formed by the coupling of the [molecular rotation](@entry_id:263843) with $\Omega$. The electronic state is written with the $\Omega$ subscript, e.g., ${}^{2S+1}\Lambda_{\Omega}$.

*   **Hund's Case (b)**: This limit applies when [spin-orbit coupling](@entry_id:143520) is weak (common in light molecules). The spin $\mathbf{S}$ decouples from the internuclear axis and instead couples to the total angular momentum excluding spin, denoted $N$. Here, $\Lambda$ and $N$ are [good quantum numbers](@entry_id:262514), but $\Sigma$ and $\Omega$ are not. The electronic [term symbol](@entry_id:171918) is written without an $\Omega$ subscript, e.g., ${}^{2S+1}\Lambda$. The rotational levels, labeled by $N$, are then split into a multiplet of total angular momentum states $J$ by the weak [spin-rotation coupling](@entry_id:195667).

These coupling cases illustrate how the electronic [term symbol](@entry_id:171918) is the essential starting point for building a complete picture of a molecule's rovibronic energy levels. [@problem_id:2653023]