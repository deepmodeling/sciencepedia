## Introduction
The intricate machinery of life, from the folding of a single protein to the complex [signaling networks](@entry_id:754820) within a cell, operates according to the fundamental laws of physics and chemistry. Understanding these processes at a molecular level requires a quantitative framework that can describe the forces, energies, and motions governing biological molecules. This is the domain of [biophysical chemistry](@entry_id:150393). The primary challenge lies in bridging the gap between the seemingly chaotic, dynamic cellular environment and the elegant, predictive power of physical principles. This article is designed to build that bridge, providing a rigorous yet accessible exploration of the [biophysical chemistry](@entry_id:150393) of biological molecules.

The journey begins with **Principles and Mechanisms**, where we will establish the theoretical bedrock, starting from the statistical mechanics of single molecules and progressing to the [thermodynamic potentials](@entry_id:140516) and kinetic theories that govern their stability, interactions, and reactions. Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, demonstrating how they provide mechanistic insights into diverse biological phenomena, including DNA stability, [gene regulation](@entry_id:143507), [enzyme catalysis](@entry_id:146161), and the unique properties of [biological membranes](@entry_id:167298). Finally, the **Hands-On Practices** section provides an opportunity to apply these concepts through targeted problems, reinforcing the connection between theory and practical analysis. By navigating these chapters, you will gain a deep appreciation for how the language of physics illuminates the logic of biology.

## Principles and Mechanisms

The function of biological molecules is governed by a delicate interplay of thermodynamic and kinetic principles. To understand how proteins fold, ligands bind, and enzymes catalyze reactions, we must first establish a rigorous framework rooted in the statistical nature of matter and the fundamental laws of energy and entropy. This chapter elucidates these core principles, beginning with their statistical mechanical foundations and progressing to their application in complex biological phenomena.

### From Microscopic States to Macroscopic Thermodynamics

At its heart, the behavior of a biological macromolecule is the result of its exploration of a vast number of possible microscopic configurations, or **microstates**. The theoretical framework for connecting this microscopic world to the macroscopic thermodynamic properties we observe is **statistical mechanics**.

A common and highly useful scenario considers a single macromolecule at a fixed volume $V$ held in thermal equilibrium with a large solvent bath at a constant temperature $T$. This setup, where the system of interest (the macromolecule) can exchange energy but not particles or volume with its surroundings, defines the **[canonical ensemble](@entry_id:143358)**. A foundational assumption is that the coupling between the macromolecule and its environment is weak, allowing the energy levels of the macromolecule, $E_i$, to be well-defined. Under these conditions, the probability $P_i$ of finding the macromolecule in a specific microstate $i$ with energy $E_i$ is given by the **Boltzmann distribution**:

$$ P_i = \frac{\exp(-\beta E_i)}{Z} $$

where $\beta = 1/(k_B T)$ is the inverse thermal energy, with $k_B$ being the Boltzmann constant. The denominator, $Z$, is the [normalization constant](@entry_id:190182) that ensures the sum of all probabilities is one. This crucial quantity is the **[canonical partition function](@entry_id:154330)**:

$$ Z = \sum_i \exp(-\beta E_i) $$

The sum is taken over all possible microstates of the macromolecule. If an energy level $E_i$ is accessible through $g_i$ distinct [microstates](@entry_id:147392) (i.e., it is $g_i$-fold **degenerate**), the partition function is more conveniently written as a sum over unique energy levels:

$$ Z = \sum_i g_i \exp(-\beta E_i) $$

The partition function is the central quantity in the [canonical ensemble](@entry_id:143358) because it contains all the thermodynamic information about the system. It serves as the bridge to macroscopic thermodynamics through its relationship with the **Helmholtz free energy**, $F$:

$$ F = -k_B T \ln Z $$

This relationship is a cornerstone of statistical mechanics and is valid for any finite system, including a single macromolecule, described by the canonical ensemble [@problem_id:2935850]. It is not restricted to the [thermodynamic limit](@entry_id:143061). Other [thermodynamic potentials](@entry_id:140516) correspond to different ensembles, such as the [grand potential](@entry_id:136286) for the [grand canonical ensemble](@entry_id:141562) where particle number can fluctuate.

In the classical limit, if the molecule's total energy can be separated into contributions from its center-of-mass translation and its internal conformational motions, the partition function factorizes: $Z = Z_{\text{trans}} Z_{\text{int}}$. The translational part for a single particle of mass $m$ is $Z_{\text{trans}} = V/\Lambda^3$, where $\Lambda = h/\sqrt{2\pi m k_B T}$ is the thermal de Broglie wavelength. The internal part, $Z_{\text{int}}$, involves an integral over all [internal coordinates](@entry_id:169764), weighted by the Boltzmann factor of the internal potential energy [@problem_id:2935850]. This factorization is a powerful concept that simplifies the analysis of molecular motion.

### Chemical Potential and Non-Ideality in the Cellular Milieu

While the Helmholtz free energy is the natural potential for the $(N, V, T)$ ensemble, most biological processes occur at constant temperature and pressure. The appropriate thermodynamic potential is then the **Gibbs free energy**, $G$. For a multi-component system, the key quantity that governs the direction of mass transfer and chemical reaction is the **chemical potential**, $\mu_i$, defined as the partial molar Gibbs free energy of species $i$:

$$ \mu_i = \left(\frac{\partial G}{\partial n_i}\right)_{T, P, n_{j \ne i}} $$

Spontaneous processes, such as diffusion across a membrane, always proceed from a region of higher chemical potential to a region of lower chemical potential. The chemical potential of a solute $i$ is related to its concentration through the expression:

$$ \mu_i = \mu_i^\circ + RT \ln a_i $$

Here, $\mu_i^\circ$ is the chemical potential in a defined standard state, $R$ is the gas constant, and $a_i$ is the **activity** of the species, a measure of its "effective concentration". In an ideal solution, activity is equal to concentration. However, biological environments like the cytosol are extremely crowded with macromolecules, leading to significant **non-ideal** behavior. In such cases, activity is related to the molar concentration $c_i$ by an **[activity coefficient](@entry_id:143301)**, $\gamma_i$:

$$ a_i = \gamma_i \frac{c_i}{c^\circ} $$

where $c^\circ$ is the standard state concentration (typically $1\,\mathrm{M}$). The activity coefficient $\gamma_i$ accounts for all deviations from ideality. In crowded environments, the dominant non-ideal contribution is often the **[excluded volume effect](@entry_id:147060)**: the physical volume occupied by [macromolecules](@entry_id:150543) is unavailable to other solutes, effectively increasing their concentration and chemical potential. This leads to [activity coefficients](@entry_id:148405) greater than one.

The distinction between concentration and activity is not merely academic; it has profound consequences. Consider a neutral metabolite $X$ in two compartments separated by a permeable membrane: a crowded "left" compartment and a dilute "right" one. Suppose the concentration on the right is higher ($c_X^{\text{right}} = 0.15\,\mathrm{M}$) than on the left ($c_X^{\text{left}} = 0.10\,\mathrm{M}$). Naively, one might expect a net flux from right to left. However, if crowding on the left leads to a large [activity coefficient](@entry_id:143301) (e.g., $\gamma_X^{\text{left}} = 3.0$) while the right side is near-ideal ($\gamma_X^{\text{right}} = 1.0$), the activities are $a_X^{\text{left}} = 3.0 \times 0.10 = 0.30$ and $a_X^{\text{right}} = 1.0 \times 0.15 = 0.15$. Since $a_X^{\text{left}} > a_X^{\text{right}}$, the chemical potential is higher on the left, and the net flux will spontaneously occur from left to right, *against* the concentration gradient [@problem_id:2935868]. This demonstrates that in non-ideal systems, activity, not concentration, dictates the direction of [spontaneous processes](@entry_id:137544). Equilibrium is reached not when concentrations are equal, but when chemical potentials—and thus activities—are equal.

### The Forces Shaping Biological Structures

The thermodynamic properties of biomolecules are determined by a complex balance of fundamental non-covalent interactions. The stability of these interactions is highly dependent on the aqueous environment.

#### Electrostatic Interactions and Screening

**Ionic interactions**, or [salt bridges](@entry_id:173473), are powerful, long-range Coulombic forces between charged groups. The energy of interaction between two [point charges](@entry_id:263616) $q_1$ and $q_2$ separated by a distance $r$ in a medium with [relative permittivity](@entry_id:267815) $\varepsilon_r$ is given by:

$$ U(r) = \frac{1}{4\pi\varepsilon_0\varepsilon_r} \frac{q_1 q_2}{r} $$

In vacuum ($\varepsilon_r = 1$), the interaction between a lysine ammonium group and an aspartate carboxylate group at a distance of $0.40\,\mathrm{nm}$ is strongly favorable, on the order of $-83\,\mathrm{kcal\,mol^{-1}}$. Water, however, has a high relative permittivity ($\varepsilon_r \approx 78.5$), which dramatically weakens this interaction by a factor of nearly 80. Furthermore, in a biological buffer containing mobile salt ions, the charge of any given group is "screened" by a cloud of counter-ions. This effect is captured by **Debye-Hückel theory**. The theory introduces a [characteristic length](@entry_id:265857) scale, the **Debye length** ($\lambda_D$ or $\kappa^{-1}$), over which the [electrostatic potential](@entry_id:140313) of a charge decays. The Debye length depends on the temperature, the solvent permittivity, and the **ionic strength** of the solution, $I$:

$$ I = \frac{1}{2} \sum_i c_i z_i^2 $$
$$ \lambda_D = \sqrt{\frac{\varepsilon_r \varepsilon_0 k_B T}{2000 N_A e^2 I}} $$

Here, $c_i$ and $z_i$ are the molar concentration and valence of ion species $i$, respectively. Note that multivalent ions contribute to the [ionic strength](@entry_id:152038) in proportion to $z_i^2$, making them particularly effective at screening. For a solution containing $100\,\mathrm{mM}$ NaCl and $10\,\mathrm{mM}$ MgCl$_2$, the total [ionic strength](@entry_id:152038) is $I = \frac{1}{2}(0.1 \cdot 1^2 + 0.01 \cdot 2^2 + 0.12 \cdot (-1)^2) = 0.13\,\mathrm{M}$. At $298\,\mathrm{K}$, this yields a Debye length of approximately $0.84\,\mathrm{nm}$ [@problem_id:2935880]. In this [electrolyte solution](@entry_id:263636), the interaction energy of the same [salt bridge](@entry_id:147432) at $0.40\,\mathrm{nm}$ is reduced to just $\approx -0.6\,\mathrm{kcal\,mol^{-1}}$ [@problem_id:2935873]. This dramatic attenuation in water is a primary reason why individual [salt bridges](@entry_id:173473) on a protein surface contribute modestly to overall stability.

#### Hydrogen Bonds

**Hydrogen bonds** are directional interactions between a hydrogen atom covalently bonded to an electronegative atom (like O or N, the **donor**) and another nearby electronegative atom (the **acceptor**). They are primarily electrostatic in nature. In a vacuum, a typical amide-carbonyl hydrogen bond has a strength of $5-10\,\mathrm{kcal\,mol^{-1}}$. However, in aqueous solution, the unfolded state's donor and acceptor groups form hydrogen bonds with water molecules. When a protein folds and forms an internal [hydrogen bond](@entry_id:136659), it does so at the cost of breaking its hydrogen bonds to water. Since the strengths of these bonds are comparable, the *net* stabilizing free energy of forming an internal [hydrogen bond](@entry_id:136659) is much smaller, typically only $1-3\,\mathrm{kcal\,mol^{-1}}$ [@problem_id:2935873]. Their primary contribution to [protein stability](@entry_id:137119) is not a large energy gain, but rather satisfying the hydrogen bonding potential of buried polar groups that would otherwise be highly destabilizing.

#### Van der Waals Interactions and the Hydrophobic Effect

**Van der Waals interactions** are [short-range forces](@entry_id:142823) that occur between all atoms. They comprise two components: a weak, attractive **London dispersion force** arising from transient, quantum-mechanical fluctuations in electron density, and a very strong, short-range **Pauli repulsion** that prevents atoms from overlapping. The attractive part is relatively insensitive to the solvent. The energy of a single van der Waals contact, for instance between two methylene groups, is very small, on the order of $0.1-0.3\,\mathrm{kcal\,mol^{-1}}$ [@problem_id:2935873]. However, in a well-packed protein core, the sheer number of these contacts makes their cumulative effect a major stabilizing force.

This packing is driven by the **[hydrophobic effect](@entry_id:146085)**, the tendency of nonpolar groups to minimize their contact with water. This is not a direct attraction between nonpolar molecules, but an effect driven by the [thermodynamics of water](@entry_id:165775). The nature of this effect is remarkably dependent on the size of the nonpolar solute.

- **Small-Scale (Entropic) Hydrophobicity**: When a small nonpolar solute (e.g., methane, radius $\approx 0.2\,\mathrm{nm}$) is placed in water, the surrounding water molecules arrange themselves into an ordered, ice-like "clathrate" cage. This rearrangement maximizes water-water [hydrogen bonding](@entry_id:142832) but comes at a large entropic cost ($\Delta S_{\text{hyd}}  0$). The process is slightly enthalpically favorable ($\Delta H_{\text{hyd}} \lesssim 0$). The overall unfavorable free energy of hydration ($\Delta G_{\text{hyd}} > 0$) is thus dominated by the negative entropy change [@problem_id:2935902].

- **Large-Scale (Enthalpic) Hydrophobicity**: For a large nonpolar surface (e.g., a nanoparticle, radius $\approx 2\,\mathrm{nm}$), water cannot form a complete, ordered cage. Instead, the [hydrogen bond network](@entry_id:750458) at the interface is significantly disrupted, leading to "dangling" hydrogen bonds. This is highly unfavorable enthalpically ($\Delta H_{\text{hyd}} > 0$). The entropy change is actually positive ($\Delta S_{\text{hyd}} > 0$), but it is not enough to overcome the large enthalpic penalty. The crossover between these two regimes occurs at a length scale of about $1\,\mathrm{nm}$ [@problem_id:2935902].

Protein folding is driven by the burial of numerous [nonpolar side chains](@entry_id:186313), which is largely an example of small-scale hydrophobicity. The release of ordered water molecules from the surfaces of these [side chains](@entry_id:182203) into the bulk solvent results in a large, positive entropy change for the solvent, which is a principal driving force for folding.

### Thermodynamics of Macromolecular Stability and Binding

#### Protein Stability: The Role of Heat Capacity

The stability of a protein's folded structure is marginal, typically only $5-15\,\mathrm{kcal\,mol^{-1}}$ under physiological conditions. This net stability, represented by the Gibbs free energy of folding ($\Delta G_{\text{fold}} = G_{\text{folded}} - G_{\text{unfolded}}$), is the result of a delicate balance between large, opposing forces. For a typical folding reaction, the formation of internal interactions is enthalpically favorable ($\Delta H_{\text{fold}}  0$), but the loss of conformational entropy of the [polypeptide chain](@entry_id:144902) is highly unfavorable ($\Delta S_{\text{fold}}  0$). The overall free energy is given by:

$$ \Delta G_{\text{fold}} = \Delta H_{\text{fold}} - T \Delta S_{\text{fold}} $$

A fascinating feature of protein folding is its temperature dependence, which is governed by the **heat capacity change**, $\Delta C_p = C_{p, \text{folded}} - C_{p, \text{unfolded}}$. For most proteins, $\Delta C_p$ is negative. This is a direct consequence of the hydrophobic effect: the unfolded state, with its exposed nonpolar surfaces, is surrounded by ordered water shells. As temperature increases, this structured water "melts," absorbing heat and giving the unfolded state a high heat capacity. The folded state, with these surfaces buried, lacks this effect and has a lower heat capacity, hence $\Delta C_p  0$ [@problem_id:2935872].

The temperature dependencies of enthalpy and entropy are given by:
$$ \Delta H(T) = \Delta H(T_r) + \Delta C_p (T - T_r) $$
$$ \Delta S(T) = \Delta S(T_r) + \Delta C_p \ln(T/T_r) $$

A negative $\Delta C_p$ means that as temperature increases, $\Delta H$ becomes more negative (more favorable) and $\Delta S$ also becomes more negative (more unfavorable). The resulting temperature dependence of $\Delta G(T)$ is parabolic and concave-up. This means that a protein has a temperature of maximum stability. Stability is lost at high temperatures (**heat denaturation**), where the large, unfavorable $-T\Delta S$ term dominates. Remarkably, stability can also be lost at low temperatures (**cold denaturation**), a counter-intuitive phenomenon where the now less favorable $\Delta H$ term can no longer overcome the entropic penalty. For a protein with $\Delta H_r^\circ = -60\,\mathrm{kJ\,mol^{-1}}$, $\Delta S_r^\circ = -0.17\,\mathrm{kJ\,mol^{-1}K^{-1}}$ at $298\,\mathrm{K}$, and $\Delta C_p = -0.3\,\mathrm{kJ\,mol^{-1}K^{-1}}$, it is stable at $298\,\mathrm{K}$ with $\Delta G = -9.3\,\mathrm{kJ\,mol^{-1}}$. However, at $350\,\mathrm{K}$, even though $\Delta H$ has become more favorable ($-75.6\,\mathrm{kJ\,mol^{-1}}$), the entropy has also become more unfavorable ($-0.218\,\mathrm{kJ\,mol^{-1}K^{-1}}$), and the $-T\Delta S$ term now dominates, making $\Delta G = +0.8\,\mathrm{kJ\,mol^{-1}}$ and rendering the folded state unstable [@problem_id:2935872].

#### Molecular Recognition: Relating Equilibrium Constants and Free Energy

The binding of a ligand ($L$) to a receptor ($R$) is a reversible equilibrium, $R + L \rightleftharpoons RL$. The strength of this interaction is quantified by the equilibrium constant. The **dissociation constant**, $K_d$, has units of concentration and is the concentration of ligand at which half the receptors are occupied.
$$ K_d = \frac{[R][L]}{[RL]} $$

The thermodynamic basis for this equilibrium is the **standard Gibbs free energy of association**, $\Delta G^\circ$, which is related to the [thermodynamic equilibrium constant](@entry_id:164623), $K_a^\circ$:
$$ \Delta G^\circ = -RT \ln K_a^\circ $$
It is critical to be precise about this relationship. The argument of a logarithm must be dimensionless. The thermodynamic constant $K_a^\circ$ is defined in terms of activities, which are themselves dimensionless ratios to a [standard state](@entry_id:145000):
$$ K_a^\circ = \frac{a_{RL}}{a_R a_L} $$
For solutes, the [standard state](@entry_id:145000) is a hypothetical ideal $1\,\mathrm{M}$ solution. In a dilute, ideal solution, we can approximate activities as $a_i \approx [i]/C^\circ$, where $C^\circ=1\,\mathrm{M}$. The thermodynamic constant is then related to the concentration-based [association constant](@entry_id:273525) $K_a = 1/K_d$ by:
$$ K_a^\circ \approx \frac{[RL]/C^\circ}{([R]/C^\circ)([L]/C^\circ)} = \frac{[RL]}{[R][L]} C^\circ = \frac{C^\circ}{K_d} $$
Therefore, the rigorous relationship between the experimentally measured $K_d$ and the standard free energy is:
$$ \Delta G^\circ = -RT \ln \left(\frac{C^\circ}{K_d}\right) $$
Mistaking $\ln(K_a)$ for the argument is a common and serious error [@problem_id:2935877].

In [non-ideal solutions](@entry_id:142298), such as a high [ionic strength](@entry_id:152038) buffer, this becomes even more important. The true thermodynamic constant $K^\circ$ is related to the measured concentration-based constant $K_c$ via the [activity coefficients](@entry_id:148405). For a reaction $M^{2+} + L^{-} \rightleftharpoons ML^{+}$, the relationship is:
$$ K^\circ = \frac{a_{ML}}{a_M a_L} = \frac{\gamma_{ML} c_{ML}}{\gamma_M c_M \gamma_L c_L} = K_c \frac{\gamma_{ML}}{\gamma_M \gamma_L} $$
This can be rearranged to find the apparent, concentration-based [equilibrium constant](@entry_id:141040) from the true thermodynamic one:
$$ K_c = K^\circ \left(\frac{\gamma_M \gamma_L}{\gamma_{ML}}\right) $$
This shows that changes in solution conditions that alter the [activity coefficients](@entry_id:148405) (e.g., changing ionic strength) will change the apparent binding affinity, even if the underlying thermodynamic constant $K^\circ$ is unchanged. For instance, if $\gamma_M=0.20$, $\gamma_L=0.80$, and $\gamma_{ML}=0.40$, the correction factor is $0.40$. The apparent [association constant](@entry_id:273525) $K_c$ would be $0.4$ times the thermodynamic constant $K^\circ$, indicating weaker binding in this medium. Equivalently, the apparent dissociation constant $K_{d, \text{app}}$ would be $2.5$ times the thermodynamic $K_d^\circ$ [@problem_id:2935909].

### The Kinetics of Biological Processes: Reaction Rates

While thermodynamics determines the [equilibrium position](@entry_id:272392) of a reaction, **kinetics** describes the path and rate at which equilibrium is approached. The temperature dependence of a rate constant, $k$, is often well-described empirically by the **Arrhenius equation**:

$$ k = A \exp(-E_a/RT) $$

where $A$ is the [pre-exponential factor](@entry_id:145277) and $E_a$ is the Arrhenius activation energy. A more physically grounded model is **Transition State Theory (TST)**, which postulates a quasi-equilibrium between reactants and a high-energy **transition state** species. The rate is then proportional to the concentration of this transient species. The height of the [free energy barrier](@entry_id:203446) to be overcome is the **[activation free energy](@entry_id:169953)**, $\Delta G^\ddagger = G_{\text{transition state}} - G_{\text{reactant}}$. This leads to the **Eyring equation**:

$$ k = \kappa \frac{k_B T}{h} \exp(-\Delta G^\ddagger / RT) $$

Here, $h$ is Planck's constant and $\kappa$ is the **[transmission coefficient](@entry_id:142812)**, a factor (usually less than or equal to 1) that accounts for the probability that a system crossing the barrier proceeds to products without re-crossing. Simple TST assumes $\kappa=1$.

The [activation free energy](@entry_id:169953) can be split into enthalpic and entropic components: $\Delta G^\ddagger = \Delta H^\ddagger - T \Delta S^\ddagger$. Comparing the Eyring and Arrhenius equations reveals a direct link between their parameters for a reaction in solution: the empirical activation energy $E_a$ is related to the [activation enthalpy](@entry_id:199775) $\Delta H^\ddagger$ by:

$$ E_a = \Delta H^\ddagger + RT $$

A plot of $\ln(k/T)$ versus $1/T$ (an Eyring plot) yields a straight line with slope $-\Delta H^\ddagger/R$ and intercept related to $\Delta S^\ddagger$, allowing for the experimental dissection of the [activation barrier](@entry_id:746233) into its enthalpic and entropic contributions [@problem_id:2935904].

The TST assumption that $\kappa=1$ is an idealization. Theories such as **Kramers theory** explicitly model the influence of [solvent friction](@entry_id:203566) on [barrier crossing](@entry_id:198645). In a viscous solvent (the high-friction limit), solvent collisions can cause trajectories to re-cross the transition state barrier, reducing the rate. In this regime, the [transmission coefficient](@entry_id:142812) $\kappa$ becomes less than 1 and is inversely proportional to the solvent viscosity. This makes the reaction rate dependent on the physical properties of the medium [@problem_id:2935904].

### Electrochemical Equilibria: The Donnan Effect

A classic example of bio-[electrochemical equilibrium](@entry_id:268744) occurs in cells, which contain a high concentration of charged macromolecules (proteins, nucleic acids) that cannot pass through the cell membrane. This leads to an unequal distribution of permeant small ions, a phenomenon known as the **Gibbs-Donnan equilibrium**.

Consider a cell containing impermeant macromolecules with a total negative charge concentration of $c_f$. The cell is permeable to small ions like $\mathrm{K}^+$ and $\mathrm{Cl}^-$ and is bathed in an external solution of $\mathrm{KCl}$. At equilibrium, two conditions must be met:
1.  **Equality of Electrochemical Potential**: For every permeant ion, its electrochemical potential must be the same inside and outside. This leads to the **Donnan ratio** equality:
    $$ \frac{[\mathrm{K}^+]_{\text{out}}}{[\mathrm{K}^+]_{\text{in}}} = \frac{[\mathrm{Cl}^-]_{\text{in}}}{[\mathrm{Cl}^-]_{\text{out}}} $$
2.  **Macroscopic Electroneutrality**: Each compartment (inside and outside) must be electrically neutral.
    $$ [\mathrm{K}^+]_{\text{out}} = [\mathrm{Cl}^-]_{\text{out}} $$
    $$ [\mathrm{K}^+]_{\text{in}} = [\mathrm{Cl}^-]_{\text{in}} + c_f $$

These conditions force an asymmetric distribution of the mobile ions. To balance the fixed negative charge $c_f$, the cell must accumulate positive $\mathrm{K}^+$ ions and expel negative $\mathrm{Cl}^-$ ions. For a cell with $c_f = 80\,\mathrm{mM}$ in a bath of $150\,\mathrm{mM KCl}$, solving these equations yields internal concentrations of $[\mathrm{K}^+]_{\text{in}} \approx 195.2\,\mathrm{mM}$ and $[\mathrm{Cl}^-]_{\text{in}} \approx 115.2\,\mathrm{mM}$ [@problem_id:2935906].

This unequal ion distribution creates a Nernst potential across the membrane, known as the **Donnan potential**. For any permeant ion, this potential is:
$$ \Delta\psi = \psi_{\text{in}} - \psi_{\text{out}} = \frac{RT}{zF} \ln\left(\frac{[ion]_{\text{out}}}{[ion]_{\text{in}}}\right) $$
Using the calculated potassium concentrations at $310\,\mathrm{K}$, the potential is $\Delta\psi \approx -7.0\,\mathrm{mV}$, with the inside negative relative to the outside. This potential is a direct consequence of the presence of impermeant solutes. The magnitude of the Donnan potential is reduced at higher external salt concentrations, as the relative difference between internal and external ion concentrations becomes smaller [@problem_id:2935906]. The Donnan effect is a fundamental principle underlying cellular resting membrane potentials and osmotic regulation.