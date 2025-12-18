## Introduction
While an [electron configuration](@entry_id:147395) like $1s^2 2s^2 2p^2$ for carbon provides a basic address for its electrons, it presents an incomplete picture. It fails to account for the complex electrostatic and magnetic interactions between electrons, which split a single configuration into a rich hierarchy of distinct energy states. To describe and differentiate these states, we use a more powerful and precise notation known as the **[atomic term symbol](@entry_id:191170)**. This notation is the language of [atomic spectroscopy](@entry_id:155968) and a cornerstone of understanding electronic structure beyond simple [orbital diagrams](@entry_id:144038). This article addresses the knowledge gap between rudimentary configurations and the true quantum states of [many-electron atoms](@entry_id:178999).

In the following sections, you will gain a comprehensive understanding of this essential concept. The first section, **Principles and Mechanisms**, will deconstruct the [term symbol](@entry_id:171918), teaching you how to derive the allowed terms for any configuration using the Pauli principle and how to order them in energy with Hund's rules. Next, **Applications and Interdisciplinary Connections** will demonstrate the immense practical utility of [term symbols](@entry_id:151575) in interpreting atomic spectra, predicting magnetic properties, and understanding the behavior of atoms in molecules and solids. Finally, **Hands-On Practices** will offer guided problems to reinforce your skills and build your confidence in applying these principles.

## Principles and Mechanisms

The simple assignment of an [electronic configuration](@entry_id:272104), such as $1s^2 2s^2 2p^2$ for a carbon atom, provides a foundational but incomplete picture of its electronic structure. This notation implies that all electrons within a given subshell are energetically equivalent. In reality, the electrostatic repulsion between electrons and the magnetic interactions between their orbital and spin motions lift this degeneracy, splitting a single configuration into a hierarchy of distinct energy states. To describe and classify these states, we employ a more sophisticated and powerful notation known as the **[atomic term symbol](@entry_id:191170)**. This chapter elucidates the principles behind deriving and interpreting these symbols, providing a systematic framework for understanding the complex electronic structure of [many-electron atoms](@entry_id:178999).

### Decoding the Atomic Term Symbol: ${}^{2S+1}L_J$

An [atomic term symbol](@entry_id:191170) provides a concise summary of the total angular momenta of an atom in a specific electronic state. It takes the general form ${}^{2S+1}L_J$, where each component represents a crucial quantum mechanical property.

-   **The Total Orbital Angular Momentum Quantum Number ($L$)**: Just as an individual electron possesses orbital angular momentum described by the [quantum number](@entry_id:148529) $l$, a [many-electron atom](@entry_id:182912) has a **total orbital angular momentum**, which is the vector sum of the individual momenta: $\vec{L} = \sum_i \vec{l}_i$. The quantum number $L$ specifies the magnitude of this total momentum. The value of $L$ is denoted by a letter code, analogous to the $s, p, d, f$ notation for individual orbitals:
    -   $L=0$ is an **S** term
    -   $L=1$ is a **P** term
    -   $L=2$ is a **D** term
    -   $L=3$ is an **F** term
    and so on alphabetically (G, H, I, ...). For a system with two electrons with orbital quantum numbers $l_1$ and $l_2$, the possible values of $L$ are given by the Clebsch-Gordan series: $L = |l_1 - l_2|, |l_1 - l_2| + 1, \dots, l_1 + l_2$.

-   **The Total Spin Angular Momentum Quantum Number ($S$)**: Similarly, the individual spin angular momenta of the electrons, $\vec{s}_i$, combine to produce a **[total spin angular momentum](@entry_id:175552)**, $\vec{S} = \sum_i \vec{s}_i$. The [quantum number](@entry_id:148529) $S$ specifies its magnitude. For a two-electron system, where each electron has $s_i = 1/2$, the total spin can be $S = 1/2 + 1/2 = 1$ (spins parallel) or $S = 1/2 - 1/2 = 0$ (spins paired).

-   **The Spin Multiplicity ($2S+1$)**: This value, written as a presuperscript, indicates the number of possible orientations (projections) of the [total spin](@entry_id:153335) vector $\vec{S}$. A state with $S=0$ has a multiplicity of $2(0)+1=1$ and is called a **singlet**. A state with $S=1$ has a multiplicity of $2(1)+1=3$ and is called a **triplet**. A state with $S=2$ has a multiplicity of $5$ and is a **quintet**, and so forth. The [multiplicity](@entry_id:136466) provides direct insight into the [spin alignment](@entry_id:140245) of the electrons.

-   **The Total Angular Momentum Quantum Number ($J$)**: In what is known as the **Russell-Saunders (LS) coupling** scheme, the total orbital angular momentum $\vec{L}$ and [total spin angular momentum](@entry_id:175552) $\vec{S}$ are assumed to couple to form the **total [electronic angular momentum](@entry_id:198934)**, $\vec{J} = \vec{L} + \vec{S}$. The [quantum number](@entry_id:148529) $J$, written as a subscript, specifies the magnitude of this final vector. For a given term defined by $L$ and $S$, $J$ can take on integer or half-integer values ranging from $|L-S|$ to $L+S$ in integer steps. The set of states with the same $L$ and $S$ but different $J$ are referred to as **fine-structure levels** of a given term.

For example, let us deconstruct the [term symbol](@entry_id:171918) ${}^5D_4$. The superscript, the spin multiplicity, is $2S+1 = 5$, which implies that the total spin quantum number is $S=2$. The letter code is D, which corresponds to a total [orbital angular momentum [quantum numbe](@entry_id:167573)r](@entry_id:148529) of $L=2$. The subscript gives the total [angular momentum quantum number](@entry_id:172069) as $J=4$. We can verify that this $J$ value is consistent with the coupling of $L=2$ and $S=2$, as the possible $J$ values are $|2-2|, \dots, 2+2$, which are $0, 1, 2, 3, 4$. In this case, $J=4$ represents the maximum possible value.

### Deriving Atomic Terms: The Microstate Method

A given [electronic configuration](@entry_id:272104), such as $p^2$ or $d^4$, encompasses a set of possible arrangements of electrons within the orbitals of the subshell. Each specific arrangement, defined by a unique set of magnetic orbital ($m_l$) and magnetic spin ($m_s$) quantum numbers for every electron, is called a **[microstate](@entry_id:156003)**. The complete set of [microstates](@entry_id:147392) for a configuration can be systematically grouped to determine the allowed atomic terms.

A [microstate](@entry_id:156003) is characterized by its total magnetic [orbital quantum number](@entry_id:164193), $M_L = \sum_i m_{l,i}$, and its total magnetic [spin quantum number](@entry_id:142550), $M_S = \sum_i m_{s,i}$. These are the projections of the total orbital and [total spin angular momentum](@entry_id:175552) vectors, respectively, onto the z-axis.

Consider a hypothetical [microstate](@entry_id:156003) of a $d^4$ configuration. The five $d$-orbitals correspond to $m_l = +2, +1, 0, -1, -2$. Let the four electrons be arranged as follows: two electrons in the $m_l = +2$ orbital, one spin-up electron ($m_s = +1/2$) in the $m_l = +1$ orbital, and one spin-up electron in the $m_l = -2$ orbital.
To find $M_L$ and $M_S$ for this microstate, we sum the contributions from each electron:
-   The two electrons in the $m_l=+2$ orbital must have opposite spins by the Pauli exclusion principle ($m_s = +1/2$ and $m_s = -1/2$). Their contribution to $M_L$ is $2+2=4$, and to $M_S$ is $(+1/2) + (-1/2) = 0$.
-   The electron in the $m_l=+1$ orbital contributes $+1$ to $M_L$ and $+1/2$ to $M_S$.
-   The electron in the $m_l=-2$ orbital contributes $-2$ to $M_L$ and $+1/2$ to $M_S$.

Summing these values gives the totals for the [microstate](@entry_id:156003):
$M_L = (2+2) + 1 + (-2) = 3$
$M_S = (1/2 - 1/2) + 1/2 + 1/2 = 1$
This microstate is therefore one of the many belonging to the $d^4$ configuration, specifically characterized by the pair $(M_L, M_S) = (3, 1)$.

A specific term, ${}^{2S+1}L$, represents a collection of $(2S+1)(2L+1)$ microstates. This collection includes all [microstates](@entry_id:147392) with $M_L$ values ranging from $-L$ to $+L$ and $M_S$ values from $-S$ to $+S$. By constructing a table of all possible microstates for a configuration and their corresponding $(M_L, M_S)$ values, one can deduce the allowed terms by systematically identifying the sets of microstates that correspond to each term.

### The Role of the Pauli Principle in Electron Coupling

The method of deriving terms depends critically on whether the interacting electrons are in the same subshell.

#### Non-Equivalent Electrons

When electrons are in different subshells, they are termed **non-equivalent**. For example, in the excited state of carbon with configuration $1s^2 2s^2 2p^1 3p^1$, the two valence electrons are non-equivalent because they have different principal [quantum numbers](@entry_id:145558) ($n=2$ and $n=3$). In this case, the Pauli exclusion principle does not impose any extra restrictions on the coupling of their angular momenta, as the electrons are already distinguished by their $n$ [quantum number](@entry_id:148529). All combinations of $L$ and $S$ obtained from [vector addition](@entry_id:155045) are allowed.

For the $2p^1 3p^1$ configuration, we have $l_1=1$ and $l_2=1$. The possible [total orbital angular momentum](@entry_id:265302) values are:
$L = |1-1|, \dots, 1+1 \implies L = 0, 1, 2$ (S, P, and D terms)

The two electrons each have $s=1/2$, so the possible [total spin](@entry_id:153335) values are:
$S = |1/2-1/2|, 1/2+1/2 \implies S = 0, 1$ (Singlet and Triplet states)

By combining every possible $L$ with every possible $S$, we obtain the full set of terms:
-   $S=0$ (Singlets): $^1S, ^1P, ^1D$
-   $S=1$ (Triplets): $^3S, ^3P, ^3D$

Each of these terms will further split into fine-structure levels determined by $J$. For instance, the ${}^3D$ term ($L=2, S=1$) will split into levels with $J=1, 2, 3$, giving rise to the levels ${}^3D_1, {}^3D_2, {}^3D_3$.

#### Equivalent Electrons

The situation is fundamentally different for **[equivalent electrons](@entry_id:201572)**, which share the same values of both $n$ and $l$, such as the two electrons in the $2p^2$ configuration of a ground-state carbon atom. Here, the **Pauli exclusion principle** dictates that the total electronic wavefunction must be antisymmetric with respect to the exchange of any two electrons.

The total wavefunction, $\Psi_{\text{total}}$, can be approximated as a product of a spatial part, $\psi_{\text{spatial}}$, and a spin part, $\sigma_{\text{spin}}$. For $\Psi_{\text{total}}$ to be antisymmetric, one of two conditions must be met:
1.  $\psi_{\text{spatial}}$ is symmetric and $\sigma_{\text{spin}}$ is antisymmetric.
2.  $\psi_{\text{spatial}}$ is antisymmetric and $\sigma_{\text{spin}}$ is symmetric.

The symmetry of the spin part is straightforward:
-   For $S=0$ (singlet states), the spin wavefunction is **antisymmetric**.
-   For $S=1$ (triplet states), the spin wavefunction is **symmetric**.

The symmetry of the spatial part for two [equivalent electrons](@entry_id:201572) with [orbital quantum number](@entry_id:164193) $l$ coupled to a total $L$ depends on the value of $L$:
-   For even values of $L$, the spatial wavefunction is **symmetric**.
-   For odd values of $L$, the spatial wavefunction is **antisymmetric**.

Combining these requirements leads to a powerful selection rule for [equivalent electrons](@entry_id:201572): a term is only allowed if it pairs a symmetric spatial part with an antisymmetric spin part, or vice-versa. This means for a term with [quantum numbers](@entry_id:145558) $L$ and $S$ to be allowed, the sum $L+S$ must be an even number.

Let's apply this to the $p^2$ configuration ($l_1=l_2=1$). The possible naive terms are $^1S, ^3S, ^1P, ^3P, ^1D, ^3D$. We now check the $L+S$ rule for each:
-   $^1S$: $L=0, S=0 \implies L+S = 0$ (even). **Allowed.**
-   $^3S$: $L=0, S=1 \implies L+S = 1$ (odd). Forbidden.
-   $^1P$: $L=1, S=0 \implies L+S = 1$ (odd). Forbidden.
-   $^3P$: $L=1, S=1 \implies L+S = 2$ (even). **Allowed.**
-   $^1D$: $L=2, S=0 \implies L+S = 2$ (even). **Allowed.**
-   $^3D$: $L=2, S=1 \implies L+S = 3$ (odd). **Forbidden.**

Therefore, the Pauli principle restricts the allowed terms for a $p^2$ configuration to only $^1S$, $^3P$, and $^1D$.

### Predicting Energy Ordering: Hund's Rules

Once the allowed terms for a configuration are determined, we can predict their relative energy ordering using a set of empirical rules known as **Hund's Rules**. These rules are primarily used to identify the [ground state term](@entry_id:272039) and level.

**Hund's First Rule: Maximize Spin Multiplicity.**
For a given electronic configuration, the term with the greatest [spin multiplicity](@entry_id:263865) (i.e., the largest value of $S$) has the lowest energy.
*Physical Basis*: Electrons with parallel spins (higher $S$) are forced by the Pauli principle to occupy different regions of space. This "exchange correlation" reduces their average [electrostatic repulsion](@entry_id:162128), leading to a more stable, lower-energy state. For the $p^4$ configuration of an oxygen atom, the allowed terms are ${}^1D, {}^3P, {}^1S$. The ${}^3P$ term has a [multiplicity](@entry_id:136466) of 3 ($S=1$), while the other two have a [multiplicity](@entry_id:136466) of 1 ($S=0$). According to the first rule, the ${}^3P$ term is the ground term, as it has the lowest energy.

**Hund's Second Rule: Maximize Orbital Angular Momentum.**
For terms having the same spin multiplicity, the term with the largest value of $L$ has the lowest energy.
*Physical Basis*: States with higher $L$ correspond to electrons orbiting in the same direction, which allows them to stay further apart, again reducing their [electrostatic repulsion](@entry_id:162128). For the $p^2$ configuration, the allowed terms are ${}^1S, {}^3P, {}^1D$. The first rule identifies ${}^3P$ as the ground term. Among the remaining singlet terms, ${}^1D$ ($L=2$) lies lower in energy than ${}^1S$ ($L=0$).

**Spin-Orbit Coupling and Fine Structure**
The effects considered so far arise from electron-electron repulsion. A weaker magnetic effect, **[spin-orbit coupling](@entry_id:143520)**, also influences the energies. This is an interaction between the magnetic moment associated with the electron's spin and the internal magnetic field generated by its orbital motion. This interaction splits a given term (defined by $L$ and $S$) into a set of closely spaced **fine-structure levels**, each identified by a unique value of the total [angular momentum [quantum numbe](@entry_id:172069)r](@entry_id:148529), $J$.

The total number of states within a term, or its **degeneracy**, is given by $(2S+1)(2L+1)$. This must equal the sum of the degeneracies of its fine-structure levels, where each $J$ level is $(2J+1)$-fold degenerate. For instance, a ${}^3D$ term ($L=2, S=1$) has a total degeneracy of $(2\cdot1+1)(2\cdot2+1) = 3 \times 5 = 15$. It splits into levels with $J=1, 2, 3$. The sum of their individual degeneracies is $(2\cdot1+1) + (2\cdot2+1) + (2\cdot3+1) = 3 + 5 + 7 = 15$, confirming the conservation of states.

**Hund's Third Rule: Ordering of J-levels.**
This rule predicts the energy ordering of the fine-structure levels within the ground term. The ordering depends on whether the subshell is less or more than half-filled.
-   For subshells that are **less than half-filled**, the level with the **lowest** value of $J$ is the most stable.
-   For subshells that are **more than half-filled**, the level with the **highest** value of $J$ is the most stable.
-   For a **half-filled** subshell, there is only one $J$ level ($L=0$, so $J=S$).

Consider the carbon atom, with a $p^2$ configuration. This is a less-than-half-filled subshell (2 out of 6 electrons). Its ground term is ${}^3P$ ($L=1, S=1$), which splits into levels with $J=0, 1, 2$. According to Hund's third rule, the level with the lowest $J$, which is ${}^3P_0$, is the ground state level. The energy ordering is $E({}^3P_0) \lt E({}^3P_1) \lt E({}^3P_2)$. In contrast, for oxygen ($p^4$), a more-than-half-filled subshell, the ordering would be reversed, with ${}^3P_2$ being the lowest in energy.

### The Limits of Russell-Saunders Coupling

The entire framework described thus far is based on the **Russell-Saunders (LS) coupling** scheme. This model is built on a crucial assumption: that the [electrostatic repulsion](@entry_id:162128) between electrons is much stronger than the spin-orbit coupling interaction ($E_{ee} \gg E_{so}$). This hierarchy allows us to first determine $L$ and $S$ by coupling the individual $l_i$ and $s_i$, and then treat [spin-orbit coupling](@entry_id:143520) as a smaller perturbation that couples $L$ and $S$ to form $J$.

This assumption holds well for light atoms. However, spin-orbit coupling strength increases rapidly with the nuclear charge, approximately as $Z^4$. For [heavy elements](@entry_id:272514), the [spin-orbit interaction](@entry_id:143481) can become comparable in magnitude to the electrostatic repulsion. In such cases, the LS coupling scheme breaks down. A hypothetical calculation for the lead atom (Pb, Z=82) with a $6p^2$ configuration might show that the characteristic energy of [spin-orbit coupling](@entry_id:143520) is a substantial fraction (e.g., ~0.2) of the electron-electron repulsion energy. When this ratio is not small, $L$ and $S$ cease to be [good quantum numbers](@entry_id:262514), meaning the states can no longer be accurately described by a single term symbol like ${}^3P$.

In this limit, an alternative model known as **[j-j coupling](@entry_id:152915)** becomes more appropriate. In [j-j coupling](@entry_id:152915), the [orbital and spin angular momentum](@entry_id:167026) of each individual electron are first coupled to form a total angular momentum for that electron, $\vec{j}_i = \vec{l}_i + \vec{s}_i$. Then, these individual $\vec{j}_i$ vectors are coupled to form the [total angular momentum](@entry_id:155748) of the atom, $\vec{J} = \sum_i \vec{j}_i$. For most real atoms, the physical reality lies somewhere between the pure LS and pure [j-j coupling](@entry_id:152915) limits, a situation referred to as **[intermediate coupling](@entry_id:167774)**. Nevertheless, for chemists, the LS coupling scheme and its associated [term symbols](@entry_id:151575) remain the indispensable language for describing the [electronic states](@entry_id:171776) of most elements encountered in typical chemical contexts.