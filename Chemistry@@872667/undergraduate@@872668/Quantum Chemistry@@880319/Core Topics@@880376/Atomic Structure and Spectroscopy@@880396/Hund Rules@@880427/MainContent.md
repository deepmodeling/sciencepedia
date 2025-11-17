## Introduction
While an electron configuration like $1s^2 2s^2 2p^2$ tells us which orbitals electrons occupy, it is an incomplete picture of an atom's electronic structure. For atoms with partially filled subshells, electrons can be arranged in [degenerate orbitals](@entry_id:154323) in multiple ways, creating numerous distinct electronic "microstates." Due to [electron-electron repulsion](@entry_id:154978), these microstates are not equal in energy. The fundamental challenge is to identify the true ground state—the specific arrangement with the lowest possible energy—which dictates the atom's chemical and physical properties.

This is the knowledge gap that Hund's rules address. Developed by Friedrich Hund, these empirical rules provide a systematic, quantum-mechanically grounded method for identifying the [ground state term](@entry_id:272039) of an atom or ion. By prioritizing the most significant electronic interactions, the rules allow us to predict the total spin, orbital, and angular momenta that define the most stable electronic state.

In this article, you will gain a deep understanding of this cornerstone of quantum chemistry. The first chapter, "Principles and Mechanisms," will unpack the quantum mechanical basis for the rules, including the critical roles of Coulomb repulsion and exchange energy. Following this, "Applications and Interdisciplinary Connections" will demonstrate the remarkable power of Hund's rules to explain observable phenomena in chemistry, [solid-state physics](@entry_id:142261), and spectroscopy. Finally, in "Hands-On Practices," you will have the opportunity to apply these concepts to solve concrete problems, solidifying your knowledge.

## Principles and Mechanisms

The [electronic configuration](@entry_id:272104) of an atom, such as $1s^2 2s^2 2p^2$ for carbon, provides a foundational description of how electrons occupy atomic orbitals. However, this notation is an incomplete representation of the atom's electronic state. For atoms with partially filled subshells, the [degenerate orbitals](@entry_id:154323) offer multiple possible arrangements for the valence electrons. Each specific assignment of quantum numbers ($m_l$ for orbital and $m_s$ for spin) to each electron defines a unique **microstate**. Due to electron-electron repulsion, these numerous microstates are not energetically equivalent. The electrostatic and magnetic interactions among electrons lift this degeneracy, splitting a single configuration into a hierarchy of distinct energy states. The task of identifying the true ground state—the [microstate](@entry_id:156003) or collection of microstates with the lowest possible energy—is central to understanding [atomic spectroscopy](@entry_id:155968), magnetism, and [chemical reactivity](@entry_id:141717).

Hund's rules are a set of empirical guidelines, grounded in quantum mechanics, that provide a robust framework for identifying the [ground state energy](@entry_id:146823) level of an atom or ion. These rules prioritize the [fundamental interactions](@entry_id:749649) that govern electron behavior: electrostatic repulsion and spin-orbit coupling. By applying them sequentially, one can determine the [total spin](@entry_id:153335), orbital, and total angular momenta that characterize the atom's lowest energy state.

### The Quantum Mechanical Basis of Energy Splitting: Coulomb and Exchange Integrals

The primary source of energy differences among the microstates of a given configuration is the electrostatic repulsion between electrons. A rigorous quantum mechanical treatment of a multi-electron atom reveals that the energy of a particular state is determined by a delicate balance of several factors. For a simplified two-electron system, the energy contribution from [electron-electron repulsion](@entry_id:154978) can be understood through two fundamental types of integrals.

The **Coulomb integral**, denoted $J_{ij}$, represents the classical [electrostatic potential energy](@entry_id:204009) of repulsion between the charge distributions of electron $i$ and electron $j$. If electron $i$ is in spatial orbital $\phi_i$ and electron $j$ is in orbital $\phi_j$, this integral quantifies the energetic cost of their mutual repulsion. A larger value of $J_{ij}$ implies stronger repulsion and a higher energy. Intuitively, the Coulomb repulsion is greatest when two electrons occupy the same spatial orbital (e.g., $J_{aa}$) and is reduced when they occupy different orbitals (e.g., $J_{ab}$), as they are on average farther apart in the latter case.

The **[exchange integral](@entry_id:177036)**, denoted $K_{ij}$, is a purely quantum mechanical effect with no classical counterpart. It arises directly from the [antisymmetry](@entry_id:261893) requirement imposed on the total electronic wavefunction by the Pauli Exclusion Principle. This integral contributes to the energy expression with a negative sign (i.e., as $-K_{ij}$), representing an energetic stabilization known as **exchange energy**. A crucial property of the [exchange integral](@entry_id:177036) is that it is non-zero only for electrons that have the same spin (parallel spins). It effectively reduces the total energy of the system, making states with parallel-spin electrons more stable than they would otherwise be. This stabilization can be thought of as arising from the "Pauli repulsion" between same-spin electrons, which creates a "Fermi hole" around each electron, a region where the probability of finding another electron with the same spin is significantly reduced. This enforced separation lowers the effective Coulomb repulsion, a stabilization captured by the term $K_{ij}$.

For a two-electron system, the total energy can be approximated as:
$E = I_1 + I_2 + J_{12} - \delta_{\sigma_1, \sigma_2} K_{12}$
Here, $I_1$ and $I_2$ are the one-electron energies (kinetic energy plus nucleus-electron attraction) for the two electrons. $J_{12}$ is the Coulomb integral. The term $-\delta_{\sigma_1, \sigma_2} K_{12}$ represents the [exchange energy](@entry_id:137069), where $K_{12}$ is the [exchange integral](@entry_id:177036) and the Kronecker delta $\delta_{\sigma_1, \sigma_2}$ is 1 if the electron spins $\sigma_1$ and $\sigma_2$ are parallel, and 0 if they are antiparallel.

### Hund's First Rule: The Rule of Maximum Multiplicity

Hund's first rule addresses the most significant energy contribution: the minimization of electron-electron repulsion by maximizing the total spin.

**Rule 1: For a given [electron configuration](@entry_id:147395), the electronic term with the maximum total [spin [quantum numbe](@entry_id:142550)r](@entry_id:148529) ($S$), and thus the maximum [spin multiplicity](@entry_id:263865) ($2S+1$), has the lowest energy.**

The physical origin of this rule is a direct consequence of the interplay between the Pauli principle and [electron repulsion](@entry_id:260827), as captured by the Coulomb and exchange integrals. To achieve a state of maximum [total spin](@entry_id:153335), electrons must have their individual spins aligned in parallel. According to the Pauli Exclusion Principle, no two electrons can have the same set of four [quantum numbers](@entry_id:145558). Therefore, if two electrons have the same [spin quantum number](@entry_id:142550) ($m_s$), they must occupy different spatial orbitals (i.e., have different $m_l$ values).

Consider the example of a neutral carbon atom with the configuration $1s^2 2s^2 2p^2$ [@problem_id:1373278]. We are concerned with the two electrons in the degenerate $2p$ subshell.
- One possible arrangement is to place both electrons in the same $2p$ orbital (e.g., $2p_x$) with opposite spins. This is a [singlet state](@entry_id:154728) with total spin $S=0$. The repulsion energy is dominated by the large Coulomb integral $J_{xx}$.
- Another arrangement is to place the electrons in two different orbitals (e.g., $2p_x$ and $2p_y$) with parallel spins. This is a [triplet state](@entry_id:156705) with total spin $S=1$.

The [triplet state](@entry_id:156705) is the ground state. The reason is twofold. First, by occupying different spatial orbitals, the electrons are on average farther apart, which significantly reduces their Coulombic repulsion ($J_{xy} \lt J_{xx}$). Second, because their spins are parallel, they benefit from the stabilizing [exchange energy](@entry_id:137069) (the $-K_{xy}$ term), which further lowers the energy. The arrangement with paired spins in a single orbital receives no such exchange stabilization.

A quantitative analysis confirms this. For the $p^2$ configuration, the energy separation between the lowest-lying [singlet state](@entry_id:154728) ($^1D$) and the lowest-lying triplet state ($^3P$) can be calculated. This difference, $\Delta E = E(^1D) - E(^3P)$, is found to be a positive quantity that is a multiple of a parameter related to the [exchange integral](@entry_id:177036), demonstrating that the triplet state is indeed lower in energy [@problem_id:1985075].

This rule is widely applied in predicting the magnetic properties of atoms and ions. For instance, a gaseous manganese(II) ion, Mn$^{2+}$, has an [electron configuration](@entry_id:147395) of $[\text{Ar}]\,3d^5$. To achieve the ground state, the five $d$-electrons will occupy the five degenerate $3d$ orbitals singly with their spins parallel. This maximizes the [total spin](@entry_id:153335), giving $S = 5 \times (1/2) = 5/2$. The corresponding **[spin multiplicity](@entry_id:263865)**, defined as $2S+1$, is $2(5/2) + 1 = 6$. This [high-spin state](@entry_id:155923) is known as a sextet and is responsible for the strong paramagnetic properties of Mn$^{2+}$ compounds [@problem_id:1985051].

### Hund's Second Rule: Maximizing Total Orbital Angular Momentum

After applying the first rule to identify the spin multiplicity of the ground state, there may still be several possible terms with this same [multiplicity](@entry_id:136466). Hund's second rule provides the criterion for distinguishing among them.

**Rule 2: For a given spin multiplicity, the term with the largest total orbital angular momentum quantum number ($L$) has the lowest energy.**

The total orbital angular momentum [quantum number](@entry_id:148529), $L$, is determined by the vector sum of the individual orbital angular momenta ($l_i$) of the valence electrons. States with different $L$ values are denoted by spectroscopic [term symbols](@entry_id:151575): S ($L=0$), P ($L=1$), D ($L=2$), F ($L=3$), G ($L=4$), and so on.

The physical reasoning behind this rule is more subtle than the first. A classical analogy suggests that when electrons orbit the nucleus in the same direction (correlating their motion), they can more effectively stay apart from one another, thus reducing their mutual repulsion. In quantum mechanics, a state with a higher value of $L$ corresponds to a [many-electron wavefunction](@entry_id:174975) that has nodes positioned in a way that minimizes [electron-electron repulsion](@entry_id:154978).

For example, a gaseous vanadium(III) ion ($V^{3+}$) has a $d^2$ configuration. The terms with the maximum spin multiplicity are found to be $^3F$ (a triplet F term) and $^3P$ (a triplet P term). Both have $S=1$. The $F$ term corresponds to $L=3$, while the $P$ term corresponds to $L=1$. According to Hund's second rule, the $^3F$ term, having the larger $L$ value, is lower in energy and is therefore the ground term [@problem_id:1373311].

Similarly, for the $p^2$ configuration of carbon, the Pauli principle allows for three terms: $^3P$, $^1D$, and $^1S$ [@problem_id:1985053]. Hund's first rule immediately identifies the $^3P$ term ($S=1$) as the ground term. However, we can also use the second rule to order the two singlet terms, $^1D$ ($S=0, L=2$) and $^1S$ ($S=0, L=0$). The rule predicts that the $^1D$ term is lower in energy than the $^1S$ term. Quantum mechanical calculations confirm this, showing that the energy difference $E(^1S) - E(^1D)$ is a positive quantity proportional to a parameter called the Slater-Condon integral $F_2$, which quantifies aspects of [electron repulsion](@entry_id:260827) [@problem_id:1373341].

### Hund's Third Rule: Spin-Orbit Coupling and Total Angular Momentum

The first two rules deal with [electrostatic interactions](@entry_id:166363), which split a configuration into distinct **terms** ($^{2S+1}L$). However, a weaker, relativistic effect known as **spin-orbit coupling** causes these terms to split further into fine-structure **levels**. This interaction arises from the coupling of each electron's intrinsic magnetic moment (due to its spin) with the magnetic field generated by its orbital motion around the charged nucleus.

As a result of this coupling, the total orbital angular momentum ($L$) and [total spin angular momentum](@entry_id:175552) ($S$) of the atom are no longer independently [conserved quantities](@entry_id:148503). Instead, they combine to form a new conserved quantity, the **[total angular momentum](@entry_id:155748)**, denoted by the [quantum number](@entry_id:148529) $J$. The possible values of $J$ for a given term are determined by the vector coupling of $L$ and $S$:
$J = L+S, L+S-1, \dots, |L-S|$

Each of these $J$ values represents a distinct energy level, and Hund's third rule specifies their energy ordering.

**Rule 3: For a given term, the ordering of the $J$ levels depends on the filling of the subshell.**
- **For subshells that are less than half-filled, the level with the minimum value of $J$ has the lowest energy.** Such a multiplet is called **normal**.
- **For subshells that are more than half-filled, the level with the maximum value of $J$ has the lowest energy.** Such a multiplet is called **inverted**.
- For a half-filled subshell, the ground term always has $L=0$, so $J=S$, resulting in only a single level.

This behavior is governed by the sign of the [spin-orbit coupling](@entry_id:143520) constant, $\zeta$. For less-than-half-filled shells, $\zeta$ is positive, and for more-than-half-filled shells, it is negative. The energy shift of a level $J$ is approximately proportional to $\zeta [J(J+1) - L(L+1) - S(S+1)]$.

Let's apply this to determine the complete ground state of carbon. From the first two rules, we identified its ground term as $^3P$, for which $L=1$ and $S=1$. The possible $J$ values are $1+1=2$, $1$, and $|1-1|=0$. The $2p$ subshell can hold $2(2\cdot1+1)=6$ electrons. With only two electrons, carbon's $2p$ subshell is less than half-filled. Therefore, the level with the minimum $J$ value, $J=0$, is the lowest in energy. The complete description of the carbon ground state is given by the [term symbol](@entry_id:171918) $^{2S+1}L_J$, which is $^3P_0$ [@problem_id:1985069] [@problem_id:1373346].

Now consider oxygen, with configuration $1s^2 2s^2 2p^4$. The $2p^4$ subshell can be viewed as having two "holes" compared to a filled shell. This **[electron-hole equivalence](@entry_id:187515)** dictates that a configuration of $k$ holes (like $p^4$) will give rise to the same set of terms as a configuration of $k$ electrons (like $p^2$). Thus, oxygen's ground term is also $^3P$. However, with four electrons, the subshell is more than half-filled. Hund's third rule now dictates that the level with the maximum $J$ value, $J=2$, has the lowest energy. The ground state of oxygen is therefore $^3P_2$. The multiplet splitting is inverted compared to carbon, a direct result of the spin-orbit coupling constant $\zeta$ being negative for more-than-half-filled shells [@problem_id:1985060]. The concept of [electron-hole equivalence](@entry_id:187515) is quite general; for example, the set of [spectroscopic terms](@entry_id:175979) for an $f^3$ configuration is identical to that for an $f^{11}$ configuration, as the latter has $14-11=3$ holes [@problem_id:1373305].

### Summary: A Systematic Approach to Finding the Ground State

Hund's rules provide a clear, hierarchical procedure for determining the ground-state [term symbol](@entry_id:171918) of an atom or ion.

1.  **Determine the electron configuration** and identify the partially filled valence subshell.
2.  **Apply Rule 1 (Maximize Spin):** Distribute the electrons among the orbitals of the subshell to achieve the maximum number of parallel spins. This gives the total spin $S$ and the spin multiplicity $2S+1$.
3.  **Apply Rule 2 (Maximize Orbital Angular Momentum):** With the spins fixed from step 2, distribute the electrons among the available magnetic quantum numbers ($m_l$) to maximize the sum $M_L = \sum m_l$. This maximum value of $M_L$ is equal to the ground term's total orbital angular momentum quantum number, $L$. This identifies the ground term $^{2S+1}L$.
4.  **Apply Rule 3 (Find Total Angular Momentum):** Determine the total angular momentum [quantum number](@entry_id:148529) $J$ for the lowest energy level.
    - If the subshell is less than half-filled, select the minimum possible value: $J = |L-S|$.
    - If the subshell is more than half-filled, select the maximum possible value: $J = L+S$.

Following this procedure provides the complete [ground state term symbol](@entry_id:153508) $^{2S+1}L_J$, a compact and powerful descriptor of the atom's fundamental electronic structure. For instance, for the Neodymium(III) ion (Nd$^{3+}$) with an $f^3$ configuration:
1.  The $4f$ subshell is partially filled.
2.  To maximize spin with 3 electrons, we have $S = 1/2+1/2+1/2 = 3/2$. The multiplicity is 4 (a quartet).
3.  The $f$ orbitals have $l=3$, so $m_l = \{-3, -2, -1, 0, 1, 2, 3\}$. To maximize $M_L$, we place the three electrons in the orbitals with $m_l=3, 2, 1$. This gives $M_L = 3+2+1=6$. Thus, $L=6$ (an $I$ term). The ground term is $^4I$.
4.  The $f$ subshell holds 14 electrons; with 3 electrons, it is less than half-filled. The ground state level has $J = |L-S| = |6 - 3/2| = 9/2$.

The complete ground state for Nd$^{3+}$ is therefore $^4I_{9/2}$ [@problem_id:1373305].