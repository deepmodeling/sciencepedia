## Introduction
In the [multiscale modeling of materials](@entry_id:752334), the ability to accurately describe the forces between atoms is paramount. Interatomic potentials provide the crucial link between the quantum mechanical world and large-scale simulations, but no single potential is universally applicable. A fundamental challenge lies in selecting a functional form that correctly captures the underlying physics of a specific interaction, be it a strong covalent bond or a weak nonbonded attraction. This article tackles this challenge by providing a deep dive into two of the most foundational and widely used pairwise potentials: the Buckingham and Morse potentials.

This guide is structured to build a comprehensive understanding from theory to practice. The first chapter, **Principles and Mechanisms**, establishes the theoretical framework of pairwise [central potentials](@entry_id:149020) and then meticulously deconstructs the Buckingham and Morse models, explaining the physical origins of their terms and their inherent limitations. Following this, the **Applications and Interdisciplinary Connections** chapter explores how these potentials are employed across materials science and chemistry to predict macroscopic properties, model chemical reactions, and serve as building blocks for complex force fields. Finally, the **Hands-On Practices** section offers practical exercises that challenge you to apply these concepts, from calculating [cohesive energy](@entry_id:139323) to addressing numerical instabilities, cementing your knowledge through direct engagement.

## Principles and Mechanisms

In the study of atomistic systems, the dynamics of constituent particles are governed by the forces they exert upon one another. For a vast range of materials and conditions, these forces can be derived from a [potential energy function](@entry_id:166231). This chapter delves into the principles and mechanisms of two widely used potential energy models—the Buckingham and Morse potentials—which serve as canonical examples of functions designed to represent distinct physical interaction regimes: nonbonded van der Waals forces and [covalent bonding](@entry_id:141465), respectively.

### The Foundation: Pairwise Central Potentials

In many computational models, the [total potential energy](@entry_id:185512), $U_{\text{total}}$, of a system of particles is approximated as a sum over all distinct pairs of interacting particles. This is the **[pairwise additivity](@entry_id:193420)** assumption. Furthermore, if the interaction between any two particles depends only on the scalar distance, $r$, separating them, the potential is known as a **pairwise [central potential](@entry_id:148563)**, denoted $U(r)$. The [total potential energy](@entry_id:185512) is then expressed as:

$$U_{\text{total}} = \sum_{i \lt j} U(r_{ij})$$

where $r_{ij} = |\mathbf{r}_i - \mathbf{r}_j|$ is the distance between particle $i$ at position $\mathbf{r}_i$ and particle $j$ at position $\mathbf{r}_j$.

A fundamental principle of mechanics states that a [conservative force](@entry_id:261070) is the negative gradient of a potential energy. For a pairwise [central potential](@entry_id:148563), the force $\mathbf{F}_{ij}$ exerted on particle $i$ by particle $j$ is derived from this principle:

$$\mathbf{F}_{ij} = - \nabla_{\mathbf{r}_i} U(r_{ij})$$

Applying the chain rule, this gradient becomes $\nabla_{\mathbf{r}_i} U(r_{ij}) = \frac{dU}{dr_{ij}} \nabla_{\mathbf{r}_i} r_{ij}$. The gradient of the scalar distance, $\nabla_{\mathbf{r}_i} r_{ij}$, is simply the unit vector pointing from particle $j$ to particle $i$, denoted $\hat{\mathbf{r}}_{ij} = \frac{\mathbf{r}_i - \mathbf{r}_j}{r_{ij}}$. This leads to the foundational equation for the force derived from any pairwise [central potential](@entry_id:148563) :

$$\mathbf{F}_{ij} = - \frac{dU}{dr} \bigg|_{r=r_{ij}} \hat{\mathbf{r}}_{ij}$$

This elegant relationship ensures two critical properties. First, the force is always directed along the line connecting the two particles, meaning there are no tangential components. Second, it guarantees that Newton's third law, the principle of action and reaction, is satisfied. Since $\hat{\mathbf{r}}_{ji} = -\hat{\mathbf{r}}_{ij}$ and $r_{ij} = r_{ji}$, it follows directly that $\mathbf{F}_{ji} = -\mathbf{F}_{ij}$ . The negative sign is of paramount physical importance: it ensures that a region where the potential energy slope $\frac{dU}{dr}$ is positive corresponds to an attractive force (pulling the particles together, opposite to $\hat{\mathbf{r}}_{ij}$), while a region where the slope is negative corresponds to a repulsive force (pushing the particles apart, along $\hat{\mathbf{r}}_{ij}$).

### The Buckingham Potential: Modeling Nonbonded Interactions

The Buckingham potential is a classic model designed to describe the interaction between neutral, closed-shell atoms or molecules, such as [noble gases](@entry_id:141583) or [nonpolar molecules](@entry_id:149614) in a condensed phase. These are typically referred to as **[nonbonded interactions](@entry_id:189647)**. The potential is constructed as a sum of two terms, each representing a distinct physical phenomenon :

$$U(r) = A e^{-Br} - \frac{C}{r^6}$$

This functional form is also known as the **exp-6 potential**.

#### Physical Origin of the Terms

The power of the Buckingham potential lies in the physical justification for each of its components.

The first term, $A e^{-Br}$, represents the strong **short-range repulsion** that occurs when the electron clouds of two atoms begin to overlap. According to the Pauli exclusion principle, two electrons with the same spin cannot occupy the same quantum state. As atoms are pushed together, this principle forces electrons into higher-energy, anti-[bonding orbitals](@entry_id:165952). This effect manifests as a sharp increase in the system's kinetic and potential energy, resulting in a powerful repulsive force. The electron density of an atom decays approximately exponentially with distance from the nucleus. The magnitude of this Pauli repulsion is proportional to the overlap of the electron wavefunctions, which itself decays exponentially with interatomic separation. Therefore, an exponential form $A e^{-Br}$ is a physically well-motivated model for this repulsion . This stands in contrast to the $r^{-12}$ repulsion used in the Lennard-Jones potential, which is chosen primarily for computational convenience rather than being derived from first principles .

The second term, $-C r^{-6}$, represents the long-range **dispersion attraction**, also known as the **London [dispersion force](@entry_id:748556)**. Even in a neutral, nonpolar atom, the electron distribution fluctuates quantum mechanically, creating an instantaneous, transient dipole moment. This temporary dipole generates an electric field that polarizes any nearby atom, inducing a correlated dipole moment in it. The interaction between the original [instantaneous dipole](@entry_id:139165) and the induced dipole results in a net attractive force. This is a purely quantum mechanical effect, derived from [second-order perturbation theory](@entry_id:192858). For two isotropic atoms in the non-retarded regime, this interaction energy scales as the inverse sixth power of the separation, hence the $-C r^{-6}$ form. The coefficient $C$, often denoted $C_6$, is the London dispersion coefficient and is related to the electronic properties of the interacting atoms, specifically their dynamic polarizabilities and characteristic ionization energies .

#### Parameters and Properties

From the requirement of [dimensional homogeneity](@entry_id:143574), the parameters of the Buckingham potential have distinct physical units. For $U(r)$ to have units of energy (e.g., electron-volts, eV), and the argument of the exponential, $Br$, to be dimensionless, the units must be as follows :
*   $A$: The repulsion amplitude, with units of **energy** (e.g., eV).
*   $B$: The repulsion hardness or inverse range, with units of **inverse length** (e.g., $\mathrm{\AA}^{-1}$).
*   $C$: The dispersion coefficient, with units of **energy $\times$ length$^6$** (e.g., $\mathrm{eV} \cdot \mathrm{\AA}^{6}$).

Typical values for [ionic solids](@entry_id:139048) or [noble gases](@entry_id:141583) might be $A \sim 10^3$–$10^5$ eV, $B \sim 1$–$5$ $\mathrm{\AA}^{-1}$, and $C \sim 10$–$200$ $\mathrm{eV} \cdot \mathrm{\AA}^{6}$ .

A key advantage of the Buckingham potential over the Lennard-Jones potential is its flexibility. A Lennard-Jones potential has only two parameters ($\epsilon$ and $\sigma$), which fixes the potential's shape. Specifically, the dimensionless curvature at the minimum, $U''(r_e) r_e^2 / \epsilon$, is a fixed constant ($72$ for the 12-6 form). The Buckingham potential has three parameters, which allows this curvature to be tuned independently of the well depth and position. This extra degree of freedom is crucial for fitting the potential to additional experimental data, such as elastic constants or [vibrational frequencies](@entry_id:199185), providing a more accurate representation of the material's properties .

#### A Critical Limitation: The Buckingham Catastrophe

Despite its physical basis, the standard Buckingham potential suffers from a severe flaw at very short distances. As $r \to 0$, the exponential repulsion term $A e^{-Br}$ approaches a finite value $A$, but the attractive dispersion term $-C r^{-6}$ diverges to negative infinity. Consequently, the potential unphysically plunges to $-\infty$ as $r \to 0$ . This "Buckingham catastrophe" can cause numerical blow-ups in [molecular dynamics simulations](@entry_id:160737) if particles undergo a high-energy collision and approach each other too closely. To circumvent this, practical implementations of the Buckingham potential must be modified. Common strategies include multiplying the attractive term by a damping function that goes to zero as $r \to 0$, or [splicing](@entry_id:261283) the potential to a purely repulsive function (like the Ziegler–Biersack–Littmark, ZBL, potential) below a certain cutoff distance .

### The Morse Potential: Modeling Covalent Bonds

The Morse potential is a phenomenological model developed specifically to describe the potential energy of a **diatomic [covalent bond](@entry_id:146178)**. Unlike the Buckingham potential, which is built from physically distinct nonbonded terms, the Morse potential is a single, unified function designed to reproduce the characteristic shape of a bound quantum state.

A common form of the Morse potential, with its minimum at $-D_e$, is:

$$U(r) = D_e \left( e^{-2a(r-r_e)} - 2e^{-a(r-r_e)} \right)$$

where:
*   $D_e$: The **[dissociation energy](@entry_id:272940)** or well depth, with units of energy. This is the energy required to break the bond.
*   $r_e$: The **equilibrium bond distance**, where the potential energy is at a minimum, with units of length.
*   $a$: A parameter with units of **inverse length** that controls the "width" or "stiffness" of the potential well.

This form is convenient because it sets the energy at infinite separation to zero, $U(\infty) = 0$, and the energy at the equilibrium distance to $U(r_e) = -D_e$ .

#### Key Features and Physical Realism

The Morse potential's success lies in its ability to capture two essential features of covalent bonds that simpler models, like the [harmonic potential](@entry_id:169618), fail to describe .

1.  **Finite Dissociation Energy:** A real [covalent bond](@entry_id:146178) has a finite strength; a specific amount of energy, $D_e$, is required to break it. The [harmonic potential](@entry_id:169618), $U(r) = \frac{1}{2}k(r-r_e)^2$, increases quadratically without limit, implying an infinite [bond strength](@entry_id:149044). The Morse potential, by virtue of its exponential terms, correctly flattens out to an asymptote ($U(\infty)=0$) as the bond is stretched, representing the [dissociation](@entry_id:144265) of the molecule into two separate, non-interacting atoms.

2.  **Anharmonicity:** A real bond potential is not a perfect parabola. The restoring force weakens as the bond is stretched. This is known as **anharmonicity**. The Morse potential is intrinsically anharmonic. Its curvature is not constant; by taking the second derivative, we find the curvature at the minimum is $k = U''(r_e) = 2D_e a^2$. This relates the "stiffness" parameter $a$ to the harmonic [vibrational frequency](@entry_id:266554), $\omega = \sqrt{k/\mu} = a\sqrt{2D_e/\mu}$, where $\mu$ is the [reduced mass](@entry_id:152420) of the [diatomic molecule](@entry_id:194513) . For any displacement from equilibrium, the curvature changes, leading to an asymmetric well. This asymmetry correctly predicts that the spacing between [vibrational energy levels](@entry_id:193001) decreases as the vibrational [quantum number](@entry_id:148529) increases, a hallmark of real molecular spectra.

The three parameters of the Morse potential ($D_e, r_e, a$) map directly to key experimental [observables](@entry_id:267133) of a bond ([dissociation energy](@entry_id:272940), [bond length](@entry_id:144592), and vibrational frequency), making it a powerful and intuitive tool.

### Choosing the Right Tool: Morse for Bonds, Buckingham for Nonbonds

The distinct physical origins and mathematical forms of the Morse and Buckingham potentials make them suited for different tasks. The choice between them is a critical decision in constructing a multiscale model.

*   The **Morse potential** is the superior choice for modeling **intramolecular [bonded interactions](@entry_id:746909)**. Its functional form is designed to capture the physics of a dissociating covalent bond: a finite [bond strength](@entry_id:149044), an equilibrium distance, and realistic [anharmonicity](@entry_id:137191). Its purely exponential form reflects the rapid decay of interactions governed by [orbital overlap](@entry_id:143431) in a chemical bond .

*   The **Buckingham potential** is the superior choice for modeling **intermolecular [nonbonded interactions](@entry_id:189647)** between closed-shell species. It correctly combines the two dominant physical effects in this regime: exponential Pauli repulsion at short range and $r^{-6}$ dispersion attraction at long range. Using a Buckingham potential to model a [covalent bond](@entry_id:146178) is physically inappropriate; its $r^{-6}$ attractive tail does not describe [bond dissociation](@entry_id:275459), and its unphysical behavior at $r \to 0$ is problematic .

While it is possible to *locally* match a Buckingham potential to a Morse potential by forcing their values and first two derivatives to be equal at the [equilibrium point](@entry_id:272705) $r_e$, their global behaviors are fundamentally different. Such a local fit does not change the fact that they represent different underlying physics .

### Beyond Pairwise Additivity: The Limits of the Models

A crucial, and often subtle, assumption in using potentials like Buckingham or Morse is that of **[pairwise additivity](@entry_id:193420)**—that the total energy is simply a sum of two-body terms. This is an approximation. In reality, the interaction energy between two particles can be influenced by the presence of a third.

The most famous example of such a **non-additive** interaction is the **Axilrod-Teller-Muto (ATM) three-body dispersion** term. Arising from third-order [quantum perturbation theory](@entry_id:171278), it describes how the correlated electronic fluctuations of three atoms are coupled. The resulting energy term, $E_{\text{ATM}}$, depends not only on the three pairwise distances ($r_{12}, r_{23}, r_{13}$) but also on the angles of the triangle they form. Its mathematical structure is fundamentally irreducible to a sum of pair potentials. Consequently, no pairwise [additive potential](@entry_id:264108), whether Buckingham, Morse, or Lennard-Jones, can ever capture this effect .

This omission is not always negligible. In dense systems where dispersion forces are important, such as condensed [noble gases](@entry_id:141583), the three-body ATM contribution can account for $5-15\%$ of the total [cohesive energy](@entry_id:139323). It is typically repulsive on average, meaning that pairwise models tend to overbind the system. Understanding this limitation is the first step toward employing more advanced many-body potentials, which are essential for achieving higher accuracy in multiscale simulations.