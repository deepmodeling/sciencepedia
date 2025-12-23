## Introduction
Pourbaix diagrams are indispensable maps in electrochemistry, providing a visual guide to the thermodynamic stability of materials in aqueous environments. Traditionally constructed from experimental data, these diagrams offer crucial insights into corrosion, [passivation](@entry_id:148423), and immunity. However, a purely empirical approach can be limiting when exploring novel materials or extreme conditions where data is scarce. This creates a need for a robust, first-principles method to predict electrochemical stability from the ground up, based on the fundamental laws of quantum mechanics and thermodynamics.

This article provides a comprehensive guide to constructing Pourbaix diagrams using computational methods. The **Principles and Mechanisms** section lays the theoretical foundation, delving into the grand canonical thermodynamics and the step-by-step computational workflow from Density Functional Theory (DFT) calculations. The **Applications and Interdisciplinary Connections** section explores the far-reaching impact of this technique, showcasing its use in [corrosion science](@entry_id:158948), geochemistry, and the rational design of electrocatalysts. Finally, the **Hands-On Practices** section allows you to apply these concepts through guided computational exercises, bridging theory with practical implementation.

## Principles and Mechanisms

This chapter delves into the fundamental [thermodynamic principles](@entry_id:142232) that underpin Pourbaix diagrams and the computational mechanisms used to construct them from first-principles [electronic structure calculations](@entry_id:748901). We will establish the theoretical framework, explore the interpretation of diagram features, detail the step-by-step computational workflow, and discuss advanced topics related to accuracy, non-ideality, and kinetics.

### Thermodynamic Foundations of Pourbaix Diagrams

At their core, Pourbaix diagrams are graphical representations of thermodynamic equilibrium for an electrochemical system. Understanding their construction requires a firm grasp of the principles governing equilibrium in systems open to their environment.

#### The Equilibrium Condition in Open Electrochemical Systems

For a [closed system](@entry_id:139565) at constant temperature ($T$) and pressure ($p$), the condition for [thermodynamic equilibrium](@entry_id:141660) is the minimization of the Gibbs free energy ($G$). However, an [electrochemical interface](@entry_id:1124268), such as a metal electrode immersed in water, is not a closed system. It is open to the exchange of particles with its surroundings, which act as large reservoirs fixing the chemical potential of the exchanged species. In the context of a Pourbaix diagram, the two most important reservoirs are the aqueous solution, which acts as a **proton reservoir** controlled by the **pH**, and the external circuit, which acts as an **electron reservoir** controlled by the **electrode potential ($E$)**.

To find the equilibrium state of such an open system, we must use a [thermodynamic potential](@entry_id:143115) appropriate for the fixed variables ($T$, $p$, and the chemical potentials of exchanged species). This potential is the **[grand potential](@entry_id:136286)**, $\Psi$ (also known as the semi-[grand potential](@entry_id:136286) or Gibbs [grand potential](@entry_id:136286)), which is obtained by a Legendre transformation of the Gibbs free energy. For a given phase (solid, liquid, or gas) that can be formed by consuming $n_i$ particles of species $i$ from a reservoir with chemical potential $\mu_i$, its grand potential is given by:

$$
\Psi = G - \sum_{i} n_i \mu_i
$$

The most stable phase under a given set of conditions ($E, \mathrm{pH}$) is the one that minimizes this [grand potential](@entry_id:136286), $\Psi$. The boundaries in a Pourbaix diagram are the loci in the $(E, \mathrm{pH})$ plane where two phases have equal grand potential, signifying they are in equilibrium. This equilibrium basis is the reason Pourbaix diagrams map thermodynamically stable species, not kinetically accessible ones  .

#### Chemical and Electrochemical Potentials

To apply the [grand potential](@entry_id:136286) formalism, we must precisely define the chemical potentials of the exchanged particles. The **chemical potential** of a neutral species $i$, $\mu_i$, is defined as its partial molar Gibbs free energy:

$$
\mu_i = \left( \frac{\partial G}{\partial n_i} \right)_{T, p, \{n_{j \neq i}\}}
$$

For a charged species $i$ with charge $z_i$ in a region of electric potential $\phi$, the relevant quantity is the **electrochemical potential**, $\tilde{\mu}_i$, which includes the [electrical work](@entry_id:273970) term:

$$
\tilde{\mu}_i = \mu_i + z_i F \phi
$$

where $F$ is the Faraday constant. The driving force for the transfer of a species between two phases (e.g., from phase $\alpha$ to $\beta$) is the difference in its [electrochemical potential](@entry_id:141179). At equilibrium, there is no net transfer, which requires the electrochemical potential of the species to be uniform throughout the system: $\tilde{\mu}_i^\alpha = \tilde{\mu}_i^\beta$ . For a neutral species ($z_i=0$), the [electrochemical potential](@entry_id:141179) is identical to the chemical potential.

In the context of Pourbaix diagrams, the chemical potential of protons in solution is a function of pH, and the chemical potential of electrons in the electrode is a function of the [electrode potential](@entry_id:158928) $E$. We will explore these relationships in detail later.

### The Geometry and Interpretation of Pourbaix Diagrams

The equilibrium condition, expressed through the Nernst equation, dictates the geometry of the lines that partition the $E$-pH plane into domains of stability.

#### Boundary Lines from the Nernst Equation

Consider a general [half-reaction](@entry_id:176405) involving $m$ protons and $n$ electrons:

$$
a\mathrm{A} + m\mathrm{H}^+ + n\mathrm{e}^- \rightleftharpoons b\mathrm{B} + c\mathrm{H}_2\mathrm{O}
$$

At equilibrium, the [electrode potential](@entry_id:158928) $E$ is given by the Nernst equation:

$$
E = E^\circ - \frac{RT}{nF} \ln\left(\frac{a_{\mathrm{B}}^b a_{\mathrm{H}_2\mathrm{O}}^c}{a_{\mathrm{A}}^a a_{\mathrm{H}^+}^m}\right)
$$

where $a_i$ is the activity of species $i$. The activity of a pure solid or liquid solvent is, by convention, set to unity . This is not an approximation but a direct consequence of defining the [standard state](@entry_id:145000) for a pure condensed phase as that phase itself at the standard pressure of $1\,\text{bar}$. In its standard state, a substance has $\mu = \mu^\circ$, which from the definition $\mu = \mu^\circ + RT \ln a$ requires its activity $a$ to be exactly 1.

Using the definition $\mathrm{pH} = -\log_{10}(a_{\mathrm{H}^+})$, which implies $\ln(a_{\mathrm{H}^+}) = -\mathrm{pH} \ln(10)$, the Nernst equation can be rearranged into the form of a line in the $E$-pH plane:

$$
E = E' - \left(\frac{\ln(10)RT}{F}\right) \frac{m}{n} \mathrm{pH}
$$

Here, $E'$ is a constant that depends on the standard potential $E^\circ$ and the activities of species A and B. From this equation, we can derive the slope of the boundary line :

$$
\frac{dE}{d(\mathrm{pH})} = - \frac{m}{n} \left(\frac{\ln(10)RT}{F}\right)
$$

At standard temperature ($T=298.15\,\mathrm{K}$), the prefactor $\frac{\ln(10)RT}{F}$ is approximately $0.05916\,\mathrm{V}$.

This slope relationship allows for a direct physical interpretation of the boundary lines:
1.  **Horizontal Lines ($m=0$):** If the reaction does not involve protons or hydroxide ions, the equilibrium potential $E$ is independent of pH. The boundary is a horizontal line. These represent purely electrochemical [redox reactions](@entry_id:141625), such as the dissolution of a metal into its ion: $\mathrm{M} \rightleftharpoons \mathrm{M}^{z+} + z\mathrm{e}^-$.  .
2.  **Vertical Lines ($n=0$):** If the reaction does not involve [electron transfer](@entry_id:155709), the equilibrium is independent of potential $E$. The equilibrium condition fixes the pH to a constant value, resulting in a vertical line. These represent purely chemical acid-base or hydrolysis reactions, such as the dissolution of a metal hydroxide: $\mathrm{M(OH)_2} + 2\mathrm{H}^+ \rightleftharpoons \mathrm{M}^{2+} + 2\mathrm{H}_2\mathrm{O}$. .
3.  **Sloped Lines ($m \neq 0, n \neq 0$):** If the reaction involves both protons and electrons (a [proton-coupled electron transfer](@entry_id:154600), or PCET, reaction), the boundary is a sloped line. The slope is negative and proportional to the ratio of protons to electrons ($m/n$). An example is the [passivation](@entry_id:148423) of a metal to its hydroxide: $\mathrm{M} + 2\mathrm{H_2O} \rightleftharpoons \mathrm{M(OH)_2} + 2\mathrm{H}^+ + 2\mathrm{e}^-$. Here, $m=2$ and $n=2$, so the slope is $-0.05916\,\mathrm{V/pH}$ .

#### The Water Stability Window

The operational range of potentials in aqueous electrochemistry is bounded by the [redox reactions](@entry_id:141625) of water itself. These two critical boundaries define the [water stability](@entry_id:1133973) window.
-   The lower boundary is the **[hydrogen evolution reaction](@entry_id:184471) (HER)**:
    $$ 2\mathrm{H}^+ + 2\mathrm{e}^- \rightleftharpoons \mathrm{H}_2(g) $$
    The Nernst equation gives $E = 0.0\,\mathrm{V} - 0.05916 \cdot \mathrm{pH}$ (vs. SHE, for $p_{\mathrm{H}_2}=1\,\text{bar}$).
-   The upper boundary is the **[oxygen evolution reaction](@entry_id:1129268) (OER)**:
    $$ 2\mathrm{H}_2\mathrm{O} \rightleftharpoons \mathrm{O}_2(g) + 4\mathrm{H}^+ + 4\mathrm{e}^- $$
    The Nernst equation gives $E = 1.23\,\mathrm{V} - 0.05916 \cdot \mathrm{pH}$ (vs. SHE, for $p_{\mathrm{O}_2}=1\,\text{bar}$).

Both lines are pH-dependent and are parallel, defining a parallelogram of [thermodynamic stability](@entry_id:142877) for liquid water. Conditions below the HER line favor the reduction of water to hydrogen gas, while conditions above the OER line favor the oxidation of water to oxygen gas .

#### Interpreting Stability Domains

The lines of the Pourbaix diagram divide it into domains, each representing a region of potential and pH where a single species (solid or dissolved) is thermodynamically predominant. In the context of [corrosion science](@entry_id:158948), these domains are given special names :
-   **Immunity:** The region where the pure, unreacted metal is the most stable phase. In this domain, the metal is thermodynamically immune to corrosion.
-   **Corrosion:** Regions where a dissolved ionic species of the metal is stable. The metal will tend to corrode or dissolve in these conditions.
-   **Passivation:** Regions where a solid, insoluble compound (typically an oxide or hydroxide) is stable. This compound can form a thin, protective "[passive film](@entry_id:273228)" on the metal surface that may kinetically inhibit further corrosion.

It is crucial to remember that these are regions of *thermodynamic stability*, reflecting minima of the [grand potential](@entry_id:136286), and they provide no information about the *rates* of reaction .

### The Computational Workflow: From DFT to Diagrams

Constructing a Pourbaix diagram from first principles involves a multi-step workflow that translates quantum mechanical calculations into a macroscopic thermodynamic phase diagram. This is accomplished by leveraging the computational framework of *ab initio* thermodynamics .

#### Step 1: Calculating 0 K Energies with DFT

The starting point for most computational Pourbaix diagrams is Density Functional Theory (DFT). For each solid phase being considered (e.g., pure metals, oxides, hydroxides), a DFT calculation is performed to obtain the total electronic energy of the static crystal lattice at $T=0\,\mathrm{K}$, which we denote as $E_{\mathrm{DFT}}$.

#### Step 2: Corrections to Finite Temperature Gibbs Free Energy

The $T=0\,\mathrm{K}$ electronic energy is not the Gibbs free energy at the desired conditions (e.g., $T=298.15\,\mathrm{K}$, $p=1\,\text{bar}$). Several corrections must be added to convert $E_{\mathrm{DFT}}$ into $G(T,p)$ for each solid phase . The Gibbs free energy is approximated as:

$$
G(T,p) \approx E_{\mathrm{DFT}} + E_{\mathrm{ZP}} + F_{\mathrm{vib}}^{\mathrm{th}}(T) - T S_{\mathrm{conf}} + pV
$$

Let's examine each correction term:
-   **Zero-Point Energy ($E_{\mathrm{ZP}}$):** A quantum mechanical effect where atoms vibrate even at absolute zero. It is calculated from the harmonic phonon frequencies ($\omega_i$) of the crystal as $E_{\mathrm{ZP}} = \sum_i \frac{1}{2}\hbar\omega_i$. This term is always positive and is typically in the range of $0.01$–$0.10\,\mathrm{eV/atom}$, being larger for compounds with light elements like hydrogen or oxygen.
-   **Thermal Vibrational Free Energy ($F_{\mathrm{vib}}^{\mathrm{th}}$):** This accounts for the change in [vibrational free energy](@entry_id:1133800) ($U_{\mathrm{vib}} - TS_{\mathrm{vib}}$) upon heating from $0\,\mathrm{K}$ to $T$. It is always negative, representing [entropic stabilization](@entry_id:1124555), and its magnitude is typically $0.01$–$0.10\,\mathrm{eV/atom}$ at room temperature.
-   **Pressure-Volume Term ($pV$):** For condensed phases at ambient pressure ($p=1\,\text{bar}$), this term is exceptionally small, on the order of $10^{-5}\,\mathrm{eV/atom}$, and is almost always negligible compared to other energy contributions.
-   **Configurational Entropy ($S_{\mathrm{conf}}$):** This term accounts for disorder. For a perfectly ordered stoichiometric crystal, it is zero. For a disordered phase, such as a [solid solution](@entry_id:157599) or a material with site vacancies, it is non-zero and can be calculated using statistical mechanics (e.g., using the Boltzmann formula, $S_{\mathrm{conf}} = k_B \ln \Omega$, where $\Omega$ is the number of configurations).

#### Step 3: Handling the Electrochemical Environment

Connecting the calculated solid-phase free energies to the aqueous environment requires a consistent thermodynamic framework for the exchanged species (protons, electrons, and dissolved ions).

##### The Computational Hydrogen Electrode (CHE) Model

Calculating the free energy of a solvated proton and an electron in an electrode from first principles is notoriously difficult. The **Computational Hydrogen Electrode (CHE) model**, proposed by Nørskov and coworkers, provides an elegant and powerful solution by sidestepping this problem . The model establishes a computational reference for the chemical potential of a proton-electron pair by linking it to the equilibrium of the hydrogen electrode reaction:

$$
\mathrm{H}^+(aq) + \mathrm{e}^- \rightleftharpoons \frac{1}{2}\mathrm{H}_2(g)
$$

By definition, this reaction is at equilibrium under standard conditions ($U=0\,\mathrm{V}$ vs. SHE, $\mathrm{pH}=0$, $p_{\mathrm{H}_2}=1\,\text{bar}$). This implies that the chemical potential of a proton-electron pair under standard conditions is equal to the chemical potential of half a [hydrogen molecule](@entry_id:148239): $\mu_{\mathrm{H}^+}^\circ + \mu_{\mathrm{e}^-}^\circ = \frac{1}{2}\mu_{\mathrm{H}_2}^\circ$. The chemical potential of a hydrogen molecule, $\mu_{\mathrm{H}_2}$, is readily calculated using DFT.

By extending this reference to any arbitrary potential $U$ and pH, we arrive at the central equation of the CHE model:

$$
\mu_{\mathrm{H}^+} + \mu_{\mathrm{e}^-} = \frac{1}{2} G_{\mathrm{H}_2(g)} - eU - k_{\mathrm{B}}T \ln(10) \cdot \mathrm{pH}
$$

This remarkable result allows us to replace the difficult-to-calculate chemical potentials of the solvated proton and the electrode electron with the easily computable gas-phase energy of $\mathrm{H}_2$ and terms that depend linearly on the experimental control variables $U$ and pH. This makes the calculation of free energies for PCET reactions computationally feasible.

##### Aligning Potential Scales

DFT calculations are performed on an absolute energy scale, typically referenced to the vacuum level. Experimental electrochemical potentials, however, are measured relative to a reference electrode, such as the Standard Hydrogen Electrode (SHE). To make a meaningful comparison, the two scales must be aligned .

The bridge between these scales is the **absolute potential of the SHE**, which is the potential of the SHE relative to the vacuum level. Although subject to some experimental uncertainty, a widely accepted value is approximately $U_{\mathrm{abs,SHE}} = 4.44\,\mathrm{V}$.

The absolute potential of a given electrode, $U_{\mathrm{abs}}$, can be calculated from its **work function**, $\Phi$, which is the energy required to move an electron from the Fermi level to the vacuum. The relationship is $U_{\mathrm{abs}} = \Phi/e$. Critically, for an electrode in solution, one must use the **solvated work function**, $\Phi_{\mathrm{sol}}$, not the vacuum work function, $\Phi_{\mathrm{vac}}$. This is because the interaction with the solvent (e.g., water) creates an interfacial dipole layer that modifies the potential drop at the surface.

Once the solvated work function is computed with DFT, the potential of the electrode on the SHE scale can be found:

$$
U_{\mathrm{vs. SHE}} = U_{\mathrm{abs}} - U_{\mathrm{abs,SHE}} = (\Phi_{\mathrm{sol}}/e) - 4.44\,\mathrm{V}
$$

This alignment is essential for determining key properties like the [potential of zero charge](@entry_id:264934) and for placing the entire Pourbaix diagram on the correct experimental potential scale.

#### Step 4: Assembling the Diagram with the Convex Hull

For systems with more than one non-reservoir element (e.g., a ternary oxide like CuAlO₂), determining the stable phase requires comparing not only individual phases but also all possible mixtures of phases. The most efficient way to do this is with the **compositional [convex hull construction](@entry_id:747862)** .

The procedure is as follows:
1.  For each candidate solid phase, calculate its Gibbs free energy $G$.
2.  At a chosen ($E$, pH), calculate the grand potential $\Psi$ for each phase by performing the Legendre transform: $\Psi = G - \sum_i n_i \mu_i$, where the sum is over reservoir species like H and O whose chemical potentials are set by $E$ and pH.
3.  Plot the [grand potential](@entry_id:136286) per [formula unit](@entry_id:145960) versus the composition of the non-reservoir elements.
4.  The **lower convex envelope** of these points is the [convex hull](@entry_id:262864).
    -   Phases that lie *on* the hull are thermodynamically stable.
    -   A point on the hull that corresponds to a single phase means that phase is stable at that composition.
    -   A straight line segment (a "[tie-line](@entry_id:196944)") on the hull connecting two phases indicates that a mixture of those two phases is the stable state for compositions between them.
    -   Phases that lie *above* the hull are unstable and will decompose into the stable phase or phase mixture on the hull directly below them.

By repeating this [convex hull construction](@entry_id:747862) for a grid of ($E$, pH) points, one can map out the stable solid phases across the entire Pourbaix diagram.

### Advanced Topics and Refinements

The basic framework described above provides a powerful tool, but several refinements are necessary for achieving high accuracy and a more nuanced understanding.

#### Accuracy and Benchmarking of DFT Functionals

The accuracy of a computational Pourbaix diagram is limited by the accuracy of the underlying DFT calculations. Different exchange-correlation (XC) functionals can yield significantly different results. Standard functionals like the Generalized Gradient Approximation (GGA) are known to have [systematic errors](@entry_id:755765), particularly in the description of the oxygen molecule ($\mathrm{O}_2$), which leads to consistent errors in oxide formation energies .

To obtain reliable results, a benchmarking and correction scheme is essential. A highly effective strategy is to anchor the entire energy scale to the experimental Gibbs free energy of formation of water. This is because water is the ubiquitous component of the system, and its [redox reactions](@entry_id:141625) define the boundaries of the Pourbaix diagram itself. The procedure involves :
1.  Calculate the error in the DFT-calculated water formation free energy for a given XC functional: $\Delta\Delta G_f(\mathrm{H_2O}) = \Delta G_f^{\mathrm{DFT}}(\mathrm{H_2O}) - \Delta G_f^\circ(\mathrm{H_2O})$.
2.  Attribute this error to a systematic error in the DFT chemical potential of oxygen, $\delta\mu_\mathrm{O}$. For the reaction $\mathrm{H}_2 + \frac{1}{2}\mathrm{O}_2 \to \mathrm{H_2O}$, the correction is $\delta\mu_\mathrm{O} = -2\Delta\Delta G_f(\mathrm{H_2O})$.
3.  Apply this stoichiometric correction to the calculated [formation energy](@entry_id:142642) of any oxide $\mathrm{M_xO_y}$:
    $$ \Delta G_{f, \text{corr}}^\circ = \Delta G_{f, \text{uncorr}}^{\mathrm{DFT}} + y \cdot \delta\mu_\mathrm{O} $$
This approach not only improves the accuracy of the oxide energies but, crucially, it ensures **thermodynamic consistency**. By forcing the water formation energy to be correct, it guarantees that the [water stability](@entry_id:1133973) lines are correctly positioned, and the [stability regions](@entry_id:166035) of all oxides are placed on a scale that is consistent with this fundamental frame of reference. A simpler approach, like applying a uniform offset to all oxides, would break this consistency.

#### Non-Ideality: The Effect of Ionic Strength

The basic thermodynamic treatment assumes [ideal solutions](@entry_id:148303), where activities are equal to concentrations. In real solutions, especially those with dissolved salts, electrostatic interactions between ions become significant. The **[ionic strength](@entry_id:152038)** of the solution, $I = \frac{1}{2}\sum_i c_i z_i^2$, quantifies this effect.

The activity of an ion $i$, $a_i$, is related to its concentration $c_i$ by an [activity coefficient](@entry_id:143301), $\gamma_i$: $a_i = \gamma_i c_i$. This coefficient can be estimated using theories like the Debye-Hückel model. For an equilibrium involving a dissolved ion, such as $\mathrm{M} \rightleftharpoons \mathrm{M}^{z+} + z\mathrm{e}^-$, the Nernst equation becomes:

$$
E = E^\circ + \frac{RT}{zF} \ln(a_{\mathrm{M}^{z+}}) = E^\circ + \frac{RT}{zF} \ln(c_{\mathrm{M}^{z+}}) + \frac{RT}{zF} \ln(\gamma_{\mathrm{M}^{z+}})
$$

The term involving $\ln(\gamma_{\mathrm{M}^{z+}})$ represents a shift in the potential of the boundary line relative to the ideal case. Since $\gamma_i \neq 1$ in [non-ideal solutions](@entry_id:142298), this term results in a vertical shift of any boundary involving dissolved ions. In systems with a supporting electrolyte, the [ionic strength](@entry_id:152038) is approximately constant and independent of pH, meaning the activity coefficients are also constant. This results in a uniform vertical shift of the relevant boundary lines without changing their slopes .

#### Beyond Bulk: Surface Pourbaix Diagrams

Conventional Pourbaix diagrams describe the stability of bulk, three-dimensional phases. However, in fields like catalysis and corrosion, the state of the material's *surface* is of primary interest. A **surface Pourbaix diagram** is a powerful extension that maps the thermodynamic stability of different *adsorbate coverages* on a specific crystal facet as a function of $E$ and pH .

The construction is analogous to the bulk case: it uses a grand-canonical framework to find the state that minimizes the surface free energy. However, the candidate "phases" are not different bulk materials but rather different arrangements of adsorbates (e.g., H, OH, O, or vacancies) on a fixed substrate. These diagrams allow researchers to predict how a catalyst surface changes under reaction conditions, identifying the specific surface structure that is active for a given electrochemical process.

#### Beyond Equilibrium: Kinetics and Metastability

The most important caveat in using Pourbaix diagrams is that they are equilibrium constructs. They predict the ultimate thermodynamic fate of a material, but they say nothing about the *rate* at which that state will be reached. In many real-world scenarios, a material can exist in a **metastable** state, persisting for long periods outside its thermodynamic stability domain .

Metastability is a kinetic phenomenon. A transformation from a metastable phase to a stable phase requires overcoming an **[activation free energy](@entry_id:169953) barrier**, $\Delta G^\ddagger$. The rate of the reaction is exponentially dependent on this barrier. In electrochemistry, the barrier is a function of the **overpotential**, $\eta = E - E_\mathrm{eq}$, which is the "extra" potential applied beyond the equilibrium value. A fraction of this overpotential acts to lower the activation barrier.

A phase can be considered kinetically persistent on an experimental timescale $\tau$ if the rate of its transformation, $k(\eta)$, is very slow, i.e., $k(\eta) \ll 1/\tau$. This leads to the concept of a **critical overpotential**, $\eta_c$. For $|\eta|  |\eta_c|$, the transformation rate is negligible, and the metastable phase can be observed experimentally. This [kinetic stability](@entry_id:150175) window is defined by the height of the intrinsic activation barrier and the observation time. Therefore, while a Pourbaix diagram might predict that a metal should passivate and form an oxide, the formation of this protective layer might be so slow that the metal continues to corrode for a significant time. A complete understanding of an electrochemical system requires considering both the thermodynamic predictions of the Pourbaix diagram and the kinetic barriers to phase transformations.