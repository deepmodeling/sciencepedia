## Introduction
The electronic structure of [many-electron atoms](@entry_id:178999) presents a complex quantum mechanical problem, where electron-electron repulsions and spin-orbit interactions create a dense manifold of energy states. To navigate this complexity, a systematic labeling and ordering system is essential. This article introduces [atomic term symbols](@entry_id:173554) and Hund's rules, the fundamental framework for understanding and predicting the [electronic states](@entry_id:171776) of atoms. We will begin in the **Principles and Mechanisms** section by deriving [term symbols](@entry_id:151575) from first principles using the Russell-Saunders coupling scheme and detailing the physical basis of Hund's rules. The **Applications and Interdisciplinary Connections** section will demonstrate the predictive power of this formalism in interpreting [atomic spectra](@entry_id:143136), explaining magnetism, and forming a bridge to the electronic structure of molecules. Finally, the **Hands-On Practices** will provide targeted exercises to solidify these theoretical concepts. This journey will equip you with the tools to decode the intricate language of atomic structure.

## Principles and Mechanisms

This chapter delves into the fundamental principles that govern the electronic structure of [many-electron atoms](@entry_id:178999), leading to the formalism of [atomic term symbols](@entry_id:173554) and the predictive power of Hund's rules. We will construct this framework from first principles, beginning with the hierarchy of interactions within an atom and culminating in a detailed understanding of how to label and order [atomic energy levels](@entry_id:148255).

### The Physical Basis: The Russell-Saunders Coupling Approximation

In a [many-electron atom](@entry_id:182912), the behavior of its electrons is dictated by a complex Hamiltonian that includes kinetic energy, electron-nucleus attraction, electron-electron repulsion, and more subtle [relativistic effects](@entry_id:150245). To make this problem tractable, we employ a perturbative approach grounded in the relative magnitudes of these interactions. For light atoms (those with a relatively low nuclear charge $Z$), the dominant interactions can be organized into a clear hierarchy. The total Hamiltonian, $\hat{H}$, can be expressed as:

$ \hat{H} = \hat{H}_{\mathrm{Coulomb}} + \hat{H}_{\mathrm{SO}} + \hat{H}_{\mathrm{Zeeman}} + \dots $

Here, $\hat{H}_{\mathrm{Coulomb}}$ encompasses the dominant kinetic energy terms and the [electrostatic potential energy](@entry_id:204009), including both the strong attraction to the nucleus and the repulsion between electrons. $\hat{H}_{\mathrm{SO}}$ represents the spin-orbit interaction, a relativistic effect that couples an electron's spin with its orbital motion. $\hat{H}_{\mathrm{Zeeman}}$ describes the interaction with an external magnetic field.

The **Russell-Saunders coupling scheme** (or **LS coupling**) is founded on the observation that for light atoms, these terms represent vastly different [energy scales](@entry_id:196201) [@problem_id:2874680]. A typical hierarchy of energy scales is:

$ E_{\mathrm{Coulomb}} \gg E_{\mathrm{SO}} \gg E_{\mathrm{Zeeman}} $

For instance, the energy splittings between different electronic configurations are on the order of several electron-volts (eV). Within a single configuration, the splittings between different arrangements of orbital and spin angular momenta (which we will soon define as **terms**) due to [electron-electron repulsion](@entry_id:154978) are typically in the range of $0.1-1$ eV. The fine-structure splittings caused by [spin-orbit coupling](@entry_id:143520) are smaller, often $10^{-3}-10^{-1}$ eV. Finally, the Zeeman splitting in a typical laboratory magnetic field of $1$ Tesla is on the order of $10^{-4}$ eV [@problem_id:2874680]. This distinct separation of scales justifies treating $\hat{H}_{\mathrm{SO}}$ and $\hat{H}_{\mathrm{Zeeman}}$ as successive perturbations to the eigenstates of $\hat{H}_{\mathrm{Coulomb}}$.

Crucially, the dominant Hamiltonian, $\hat{H}_{\mathrm{Coulomb}}$, is rotationally invariant in both spatial coordinates and the abstract spin space. This means it commutes with the operators for the square of the [total orbital angular momentum](@entry_id:265302), $\hat{L}^2$, and the square of the [total spin angular momentum](@entry_id:175552), $\hat{S}^2$.

$ [\hat{H}_{\mathrm{Coulomb}}, \hat{L}^2] = 0 \quad \text{and} \quad [\hat{H}_{\mathrm{Coulomb}}, \hat{S}^2] = 0 $

As a consequence, the eigenstates of $\hat{H}_{\mathrm{Coulomb}}$ can be chosen to be [simultaneous eigenstates](@entry_id:149152) of $\hat{L}^2$ and $\hat{S}^2$. This means that in the LS coupling approximation, the total orbital angular momentum quantum number $L$ and the total spin angular momentum quantum number $S$ are "good" quantum numbers. They provide an excellent basis for labeling the energy manifolds, which we call **atomic terms**.

### The Language of Atomic States: Term Symbols

To label these energy manifolds, we use a compact notation known as the **[atomic term symbol](@entry_id:191170)**, which takes the form $^{2S+1}L_J$. Each component of this symbol has a precise physical meaning derived from the principles of [angular momentum coupling](@entry_id:145967) [@problem_id:2624398].

*   **Total Spin Angular Momentum ($S$):** The individual [spin angular momentum](@entry_id:149719) vectors $\mathbf{s}_i$ of all electrons are vectorially summed to give the [total spin angular momentum](@entry_id:175552) vector $\mathbf{S} = \sum_i \mathbf{s}_i$. The quantum number $S$ characterizes the magnitude of this vector. The quantity $2S+1$ is called the **[spin multiplicity](@entry_id:263865)** and indicates the number of possible projections of the [total spin](@entry_id:153335) vector onto a chosen axis ($M_S = S, S-1, \dots, -S$). A [multiplicity](@entry_id:136466) of 1 is a **singlet**, 2 is a **doublet**, 3 is a **triplet**, and so on.

*   **Total Orbital Angular Momentum ($L$):** Similarly, the individual orbital angular momentum vectors $\mathbf{l}_i$ are summed to give the [total orbital angular momentum](@entry_id:265302) vector $\mathbf{L} = \sum_i \mathbf{l}_i$. The integer [quantum number](@entry_id:148529) $L$ characterizes its magnitude. By historical convention, the value of $L$ is encoded by a capital letter:
    *   $L=0 \rightarrow S$ (Sharp)
    *   $L=1 \rightarrow P$ (Principal)
    *   $L=2 \rightarrow D$ (Diffuse)
    *   $L=3 \rightarrow F$ (Fundamental)
    *   $L=4 \rightarrow G$, and alphabetically thereafter (omitting J).

*   **Total Angular Momentum ($J$):** The weaker [spin-orbit interaction](@entry_id:143481), $\hat{H}_{\mathrm{SO}}$, couples the total orbital and total spin angular momenta. This means that $\mathbf{L}$ and $\mathbf{S}$ precess around a resultant [total angular momentum](@entry_id:155748) vector, $\mathbf{J} = \mathbf{L} + \mathbf{S}$. The quantum number $J$ characterizes the magnitude of this [total angular momentum](@entry_id:155748). According to the rules of quantum mechanical [angular momentum addition](@entry_id:156081), for a given $L$ and $S$, the allowed values of $J$ are integers or half-integers in the range:
    $ J = |L-S|, |L-S|+1, \dots, L+S $
    Each specific value of $J$ corresponds to a distinct energy **level** within the term, giving rise to the [fine structure](@entry_id:140861) observed in atomic spectra.

### Coupling of Angular Momenta

The rule for determining the possible values of a total [angular momentum quantum number](@entry_id:172069) from its constituents is a cornerstone of quantum mechanics. Let's derive the rule for combining two orbital angular momenta, $l_1$ and $l_2$, to form a total $L$ [@problem_id:2624453].

We consider two electrons with quantum numbers $(l_1, m_{l1})$ and $(l_2, m_{l2})$. The total space is a [tensor product](@entry_id:140694) of the individual state spaces, of dimension $(2l_1+1)(2l_2+1)$. The projection of the [total angular momentum](@entry_id:155748) is simply the sum of individual projections, $M_L = m_{l1} + m_{l2}$.

The maximum possible value of $M_L$ is $l_1 + l_2$, which occurs for the unique "stretched state" where $m_{l1} = l_1$ and $m_{l2} = l_2$. This state must be the highest-weight state of a multiplet, meaning it corresponds to a total angular momentum quantum number $L = l_1 + l_2$. This establishes the maximum possible value of $L$.

Now, consider the subspace with $M_L = l_1 + l_2 - 1$. It is spanned by two basis states: one where $m_{l1} = l_1-1, m_{l2} = l_2$, and another where $m_{l1} = l_1, m_{l2} = l_2-1$. One [linear combination](@entry_id:155091) of these two states belongs to the $L = l_1 + l_2$ multiplet (it can be generated by applying the lowering operator $L_-$ to the stretched state). The other, orthogonal linear combination must be the highest-weight state of a *new* multiplet. Since its $M_L$ value is $l_1 + l_2 - 1$, this new multiplet must have $L = l_1 + l_2 - 1$.

This inductive process continues. At each step, we find a new multiplet with an $L$ value one unit smaller, until we reach the minimum possible value, $L = |l_1 - l_2|$. The final result is the Clebsch-Gordan series: the set of allowed [total angular momentum](@entry_id:155748) quantum numbers $L$ obtained by coupling $l_1$ and $l_2$ is:

$ L \in \{ |l_1 - l_2|, |l_1 - l_2| + 1, \dots, l_1 + l_2 \} $

This same rule applies to the coupling of any two angular momenta, such as $\mathbf{S}_1$ and $\mathbf{S}_2$ to form $\mathbf{S}$, or $\mathbf{L}$ and $\mathbf{S}$ to form $\mathbf{J}$. For example, for two non-[equivalent electrons](@entry_id:201572) in a $p$ orbital ($l_1=1$) and a $d$ orbital ($l_2=2$), the possible $L$ values are $|1-2|, \dots, 1+2$, so $L \in \{1, 2, 3\}$. The total number of states in the [coupled basis](@entry_id:136812), $\sum_L (2L+1)$, must equal the total number of states in the [uncoupled basis](@entry_id:156676), $(2l_1+1)(2l_2+1)$. For our example, $(2(1)+1) + (2(2)+1) + (2(3)+1) = 3+5+7 = 15$, which matches $(2(1)+1)(2(2)+1) = 3 \times 5 = 15$ [@problem_id:2624453].

### The Pauli Principle and Equivalent Electrons

The situation becomes more subtle when we consider **[equivalent electrons](@entry_id:201572)**—electrons that share the same principal ($n$) and orbital ($l$) quantum numbers. The Pauli exclusion principle dictates that the total wavefunction of a system of fermions must be antisymmetric with respect to the exchange of any two particles. The total wavefunction can be approximated as a product of a spatial part and a spin part: $\Psi = \Phi_{\text{spatial}} \chi_{\text{spin}}$. For $\Psi$ to be antisymmetric, if the spin part is symmetric upon exchange, the spatial part must be antisymmetric, and vice versa.

For a two-electron system, the [total spin](@entry_id:153335) $S$ can be $S=1$ (triplet) or $S=0$ (singlet).
*   The $S=1$ triplet spin functions are **symmetric** under [particle exchange](@entry_id:154910).
*   The $S=0$ singlet spin function is **antisymmetric** under [particle exchange](@entry_id:154910).

For the spatial part of two [equivalent electrons](@entry_id:201572), it is a known result from the theory of angular momentum that the symmetry of the coupled spatial function depends on the total [orbital quantum number](@entry_id:164193) $L$:
*   If $L$ is **even**, the spatial function is **symmetric**.
*   If $L$ is **odd**, the spatial function is **antisymmetric**.

Combining these requirements to ensure an overall [antisymmetric wavefunction](@entry_id:153813) leads to a powerful selection rule for two [equivalent electrons](@entry_id:201572):
*   If $S=1$ (symmetric spin), then $L$ must be odd (antisymmetric space).
*   If $S=0$ (antisymmetric spin), then $L$ must be even (symmetric space).
In short, for two [equivalent electrons](@entry_id:201572), the sum $L+S$ must be an even integer [@problem_id:2624412].

Let's apply this to the important case of a $p^2$ configuration, where two [equivalent electrons](@entry_id:201572) have $l=1$. Naively coupling the angular momenta gives $L \in \{0, 1, 2\}$ and $S \in \{0, 1\}$. This would suggest six possible terms: $^1S, ^3S, ^1P, ^3P, ^1D, ^3D$. However, the Pauli principle eliminates half of these:
*   For $S=1$ (triplet), $L$ must be odd. Only $L=1$ is allowed. So, $^3P$ is allowed, but $^3S$ ($L=0$) and $^3D$ ($L=2$) are forbidden.
*   For $S=0$ (singlet), $L$ must be even. $L=0$ and $L=2$ are allowed. So, $^1S$ and $^1D$ are allowed, but $^1P$ ($L=1$) is forbidden.

Thus, for the $p^2$ configuration, only the terms $^1S$, $^3P$, and $^1D$ are physically allowed [@problem_id:2624427]. This same principle can be applied to more complex cases, such as the $f^2$ configuration ($l=3$), where the allowed terms are $^1S, ^3P, ^1D, ^3F, ^1G, ^3H, ^1I$ [@problem_id:2624412].

### Hund's Rules: Ordering Electronic States by Energy

Now that we can identify the allowed terms for a given electron configuration, the next step is to predict their energy ordering. This is accomplished by a set of empirical but physically-grounded guidelines known as **Hund's rules**. These rules arise directly from the hierarchy of interactions in the LS coupling scheme.

#### Hund's First Rule: Maximizing Spin

**Rule 1: For a given [electron configuration](@entry_id:147395), the term with the maximum total spin quantum number $S$ (and thus the highest [spin multiplicity](@entry_id:263865) $2S+1$) has the lowest energy.**

The physical origin of this rule is the interplay between the Pauli principle and electrostatic repulsion. The Hamiltonian itself is spin-independent, but spin has a profound indirect effect. As discussed, a state with a higher [total spin](@entry_id:153335) $S$ requires a more antisymmetric spatial wavefunction. An antisymmetric spatial wavefunction, $\Phi(\mathbf{r}_1, \mathbf{r}_2) = -\Phi(\mathbf{r}_2, \mathbf{r}_1)$, must vanish when the electrons are at the same point in space ($\mathbf{r}_1 = \mathbf{r}_2$). This creates a "correlation hole" or "[exchange hole](@entry_id:148904)" around each electron, reducing the probability of finding another electron with parallel spin nearby. By keeping electrons with parallel spins farther apart on average, this effect significantly reduces their mutual Coulomb repulsion energy. This reduction in energy is quantified by the **[exchange integral](@entry_id:177036)**, $K$, which is a positive quantity. For each pair of parallel-spin electrons, the energy is lowered by an amount related to $K$. Therefore, maximizing the number of parallel spins—which is equivalent to maximizing the total spin $S$—maximizes this "exchange stabilization" and lowers the total energy [@problem_id:2624413].

For the $p^2$ configuration, the allowed terms are $^1S (S=0), ^1D (S=0)$, and $^3P (S=1)$. Hund's first rule predicts that the $^3P$ term will have the lowest energy.

#### Hund's Second Rule: Maximizing Orbital Angular Momentum

**Rule 2: For terms with the same maximum [total spin](@entry_id:153335) $S$, the term with the largest total [orbital angular momentum quantum number](@entry_id:167573) $L$ has the lowest energy.**

This rule also arises from minimizing electron-electron Coulomb repulsion, but it addresses the more subtle angular correlations in electron motion. The [electron-electron repulsion](@entry_id:154978) operator, $1/r_{ij}$, is not spherically symmetric; it depends on the relative positions of the electrons. A state with a high value of $L$ corresponds classically to a situation where the electrons are orbiting the nucleus in a correlated, co-rotating fashion. This correlated motion helps them to stay out of each other's way, maintaining a larger average separation and thus lowering their repulsion energy. Conversely, a low value of $L$ implies that the individual orbital angular momentum vectors are partially cancelling, corresponding to more frequent "head-on" approaches and higher average repulsion. Mathematically, the energy of the terms is expressed using Slater-Condon parameters, and for a fixed $S$, the coefficients of these positive-definite radial integrals are such that the energy is minimized for the largest possible $L$ [@problem_id:2624408].

For the $p^2$ configuration, we are left to order the $^1S (L=0)$ and $^1D (L=2)$ terms. Both have $S=0$. Hund's second rule predicts that the $^1D$ term is lower in energy than the $^1S$ term. Combining both rules, the energy ordering for the terms of $p^2$ is $E(^3P)  E(^1D)  E(^1S)$.

#### Hund's Third Rule: The Role of Spin-Orbit Coupling

**Rule 3: For a given term (fixed $S$ and $L$), the ordering of the fine-structure levels (different $J$ values) depends on the filling of the subshell.**
*   **For subshells that are less than half-filled, the level with the minimum [total angular momentum](@entry_id:155748) $J = |L-S|$ has the lowest energy.**
*   **For subshells that are more than half-filled, the level with the maximum [total angular momentum](@entry_id:155748) $J = L+S$ has the lowest energy.**

This rule is a direct consequence of the [spin-orbit interaction](@entry_id:143481), $\hat{H}_{\mathrm{SO}}$. Within a given term, the effect of this operator can be modeled as $\hat{H}_{\mathrm{SO}} = A \mathbf{L} \cdot \mathbf{S}$, where $A$ is an effective [spin-orbit coupling](@entry_id:143520) constant. The energy shift for a level with quantum number $J$ is then given by:

$ \Delta E_J = \langle A \mathbf{L} \cdot \mathbf{S} \rangle = \frac{A}{2} [J(J+1) - L(L+1) - S(S+1)] $

The sign of the constant $A$ determines the ordering. For subshells that are less than half-filled, detailed analysis shows that $A$ is positive. Since $J(J+1)$ increases with $J$, a positive $A$ means the energy increases with $J$. Therefore, the lowest energy level corresponds to the minimum possible value of $J$.

For subshells that are more than half-filled, we invoke the principle of **electron-hole symmetry**. A configuration of $n$ electrons in a subshell that can hold $N_{\text{max}}$ electrons can be viewed as a configuration of $h = N_{\text{max}} - n$ "holes" in an otherwise filled subshell. A filled subshell has $L=0$, $S=0$, and a [total spin](@entry_id:153335)-orbit energy of zero. This implies that the spin-orbit operator for the $n$-electron system is the negative of the operator for the corresponding $h$-hole system. Consequently, the effective [coupling constant](@entry_id:160679) reverses its sign: $A_{n\text{-electrons}} = -A_{h\text{-holes}}$. Since the $h$-hole system constitutes a less-than-half-filled subshell (for which $A_h > 0$), the constant for the more-than-half-filled electron system must be negative ($A_n  0$). With a negative $A$, the energy $\Delta E_J$ *decreases* as $J$ increases. The lowest energy level is therefore the one with the maximum possible value of $J$ [@problem_id:2624380].

As an example, consider the $f^2$ configuration ($L=5, S=1$ for the ground term $^3H$). This is less than half-filled ($2  7$). The possible $J$ values are $4, 5, 6$. The ground level is the one with minimum $J$, so the full ground state level is $^3H_4$ [@problem_id:2624412]. By [particle-hole symmetry](@entry_id:142469), the ground term of the $f^{12}$ configuration (12 electrons, or 2 holes) is also $^3H$. However, since this subshell is more than half-filled ($12 > 7$), the ordering of the $J$ levels is inverted. The ground level is the one with maximum $J$, which is $^3H_6$ [@problem_id:2624379].

### A Summary of Degeneracies

It is crucial to distinguish the hierarchical levels of description for an atomic state, each with its own associated degeneracy [@problem_id:2624427].

1.  **Configuration:** Specifies the occupation of subshells (e.g., $p^2$). Its total degeneracy is the number of ways to place the electrons into the available spin-orbitals, given by the binomial coefficient $\binom{g}{n}$, where $n$ is the number of electrons and $g=2(2l+1)$ is the number of states in the subshell. For $p^2$, $g=6$ and $n=2$, so the total degeneracy is $\binom{6}{2}=15$.

2.  **Term ($^{2S+1}L$):** A collection of states sharing the same $L$ and $S$. In the absence of spin-orbit coupling, these states are degenerate. The degeneracy is the product of the orbital and spin degeneracies: $(2L+1)(2S+1)$.

3.  **Level ($^{2S+1}L_J$):** A collection of states sharing the same $L, S$, and $J$. These are split by spin-orbit coupling but remain degenerate in the absence of external fields. The degeneracy is $(2J+1)$, corresponding to the possible values of the projection $M_J$.

4.  **State ($|L, S, J, M_J\rangle$):** A single, non-degenerate quantum state of the atom (a microstate).

The degeneracies must sum correctly up the hierarchy. For our $p^2$ example, the allowed terms are $^3P$, $^1D$, and $^1S$.
*   $^3P$: $L=1, S=1$. Term degeneracy = $(2(1)+1)(2(1)+1) = 3 \times 3 = 9$.
*   $^1D$: $L=2, S=0$. Term degeneracy = $(2(2)+1)(2(0)+1) = 5 \times 1 = 5$.
*   $^1S$: $L=0, S=0$. Term degeneracy = $(2(0)+1)(2(0)+1) = 1 \times 1 = 1$.
The sum of the term degeneracies is $9+5+1=15$, which correctly matches the total degeneracy of the $p^2$ configuration.

### The Limits of the Model: From LS to jj Coupling

The Russell-Saunders coupling scheme and Hund's rules provide an excellent description for light atoms, but their validity diminishes as the nuclear charge $Z$ increases. The reason lies in the different scaling of the electrostatic and spin-orbit interactions with $Z$ [@problem_id:2624399].

*   The electrostatic multiplet splittings, arising from electron-electron repulsion, scale approximately linearly with $Z$ ($E_{\text{Coulomb}} \propto Z$).
*   The one-electron [spin-orbit interaction](@entry_id:143481), which depends on the electron's motion in the steep potential near the nucleus, scales much more rapidly, approximately as the fourth power of $Z$ ($E_{\text{SO}} \propto Z^4$).

Consequently, the ratio of spin-orbit to electrostatic interaction strengths grows as $Z^3$. For light atoms, this ratio is small, justifying LS coupling. For very heavy atoms, this ratio becomes large, and the fundamental assumption of the LS scheme breaks down. The [spin-orbit interaction](@entry_id:143481) for each individual electron becomes stronger than the electrostatic coupling between electrons.

In this regime, a different coupling scheme, known as **[jj-coupling](@entry_id:140838)**, becomes more appropriate. Here, the spin $\mathbf{s}_i$ and orbital $\mathbf{l}_i$ momentum of each electron first couple to form an individual [total angular momentum](@entry_id:155748) $\mathbf{j}_i = \mathbf{l}_i + \mathbf{s}_i$. Then, these individual $\mathbf{j}_i$ vectors are coupled to form the [total angular momentum](@entry_id:155748) of the atom, $\mathbf{J} = \sum_i \mathbf{j}_i$.

Between the pure LS and pure [jj coupling](@entry_id:147317) extremes lies the realm of **[intermediate coupling](@entry_id:167774)**, where electrostatic and spin-orbit effects are of comparable magnitude. In this regime, neither $L$ and $S$ nor the individual $j_i$ are [good quantum numbers](@entry_id:262514). The true physical states are mixtures of pure LS or pure jj states, and calculations become significantly more complex. In practice, many heavy atoms are best described by [intermediate coupling](@entry_id:167774), with LS coupling providing a useful starting point for light atoms and [jj coupling](@entry_id:147317) for the heaviest elements.