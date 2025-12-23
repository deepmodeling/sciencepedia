## Introduction
Free energy diagrams are indispensable tools in modern [computational electrochemistry](@entry_id:747611), providing a visual and thermodynamic map of complex [reaction pathways](@entry_id:269351). They translate the abstract results of quantum mechanical simulations into an intuitive landscape of intermediates and energy barriers, allowing researchers to understand and predict chemical transformations at the atomic level. A central challenge in modeling [electrocatalysis](@entry_id:151613), however, is to accurately account for the influence of the electrode potential, which provides the thermodynamic driving force for the reaction. The ability to systematically construct a potential-dependent free energy landscape is therefore crucial for deciphering [reaction mechanisms](@entry_id:149504) and predicting catalyst performance under realistic operating conditions.

This article provides a comprehensive guide to this process, broken down into three chapters. The first chapter, "Principles and Mechanisms," lays the theoretical foundation, introducing the appropriate thermodynamic potential for electrochemical systems and detailing the widely-used Computational Hydrogen Electrode (CHE) model for building the diagrams. The second chapter, "Applications and Interdisciplinary Connections," explores how these diagrams are used to analyze catalytic performance, incorporate kinetic effects via [scaling relationships](@entry_id:273705), and rationally design novel catalysts, while also drawing connections to fields like [corrosion science](@entry_id:158948) and geochemistry. Finally, the "Hands-On Practices" section offers practical exercises to solidify your understanding and apply these methods directly. This structured journey will equip you with the knowledge to move from fundamental principles to practical application, starting with the core concepts that underpin the entire methodology.

## Principles and Mechanisms

This chapter delineates the fundamental principles and operational mechanisms underlying the construction of free energy diagrams for electrochemical reaction pathways. We begin by establishing the appropriate thermodynamic potential for an electrochemical system held at constant temperature, pressure, and electrode potential. We then introduce the Computational Hydrogen Electrode (CHE) model, a widely adopted framework that simplifies the treatment of [proton-coupled electron transfer](@entry_id:154600) steps. Subsequently, we provide a systematic guide to constructing these diagrams, from defining the reaction pathway and calculating the free energies of individual states to assembling the final potential-dependent landscape. Finally, we explore advanced topics that address common idealizations, including the effects of interfacial electric fields, adsorbate coverage, and the rigorous quantification of computational uncertainties.

### The Thermodynamic Potential for Electrochemical Systems

To describe the thermodynamics of an electrochemical reaction, we must first identify the correct potential that is minimized at equilibrium under the relevant experimental conditions. Electrochemical processes are typically studied at constant temperature ($T$), constant pressure ($p$), and constant electrode potential ($U$). The latter condition implies that the system is in contact with an electron reservoir of fixed chemical potential, $\mu_e$.

Our starting point is the [fundamental thermodynamic relation](@entry_id:144320) for the internal energy, $U$, of an [open system](@entry_id:140185):
$$dU = TdS - p dV + \sum_i \mu_i dN_i$$
where $S$ is entropy, $V$ is volume, and $\mu_i$ and $N_i$ are the chemical potential and number of particles of species $i$, respectively. This potential, $U$, is minimized for an isolated system at constant $S$, $V$, and $N_i$.

For a system at constant $T$ and $V$, a Legendre transformation with respect to the conjugate pair $(T, S)$ yields the **Helmholtz free energy, $A$**:
$$A = U - TS$$
$$dA = -SdT - p dV + \sum_i \mu_i dN_i$$

For a system at constant $T$ and $p$, a further Legendre transformation with respect to the pair $(p, V)$ yields the **Gibbs free energy, $G$**:
$$G = A + pV = U + pV - TS$$
$$dG = -SdT + V dp + \sum_i \mu_i dN_i$$
The Gibbs free energy is the natural choice for chemical reactions under standard benchtop conditions, where $N_i$ for each species is fixed.

However, an electrochemical system at constant potential $U$ is open with respect to electrons. The number of electrons, $N_e$, associated with an intermediate is not fixed, but the chemical potential of electrons, $\mu_e$, is. To find the appropriate potential for this ensemble, we must perform one more Legendre transformation on $G$, this time to replace the extensive variable $N_e$ with its conjugate intensive variable $\mu_e$. This defines an **electrochemical grand potential**, $\tilde{G}$:
$$\tilde{G} = G - N_e \mu_e$$
The differential is $d\tilde{G} = -SdT + V dp - N_e d\mu_e + \sum_{i \neq e} \mu_i dN_i$. The [natural variables](@entry_id:148352) of $\tilde{G}$ are $(T, p, \mu_e, \{N_{i \neq e}\})$, making it the potential that is minimized at equilibrium for a system at constant temperature, pressure, and electron chemical potential .

The chemical potential of an electron is related to the [electrode potential](@entry_id:158928) $U$ by the convention $\mu_e = -eU$, where $e$ is the elementary positive charge and $U$ is referenced to a standard electrode. Consequently, the change in the free energy of a state upon the transfer of $n$ electrons from the reference electrode is $-neU$. This term is the cornerstone of potential-dependent free energy diagrams.

### The Computational Hydrogen Electrode (CHE) Model

While the [thermodynamic formalism](@entry_id:270973) is exact, applying it requires values for the chemical potentials of solvated protons ($\mu_{\mathrm{H}^+}$) and electrons in the electrode ($\mu_{e^-}$). The Computational Hydrogen Electrode (CHE) model, pioneered by Nørskov and coworkers, provides a powerful and practical framework for this task by relating the free energy of a solvated proton-electron pair to that of gas-phase hydrogen.

The model is based on the equilibrium of the hydrogen electrode reaction:
$$\mathrm{H}^+ + e^- \rightleftharpoons \frac{1}{2} \mathrm{H}_2(\mathrm{g})$$
At equilibrium, the chemical potentials of the species on both sides are equal: $\mu(\mathrm{H}^+) + \mu(e^-) = \frac{1}{2}\mu(\mathrm{H}_2(\mathrm{g}))$. This equilibrium condition defines the potential of a hydrogen electrode.

#### Reference Electrode Scales

To apply this model, it is crucial to understand the different [reference electrode](@entry_id:149412) scales .

*   The **Standard Hydrogen Electrode (SHE)** is the primary thermodynamic standard. By convention, its potential is defined as exactly $0 \, \mathrm{V}$ at all temperatures, under the standard conditions of proton activity $a_{\mathrm{H}^+} = 1$ (approximated as pH 0) and hydrogen partial pressure $p_{\mathrm{H}_2} = 1 \, \mathrm{bar}$.

*   The **Reversible Hydrogen Electrode (RHE)** is a hydrogen electrode operating in the actual electrolyte of interest, which may have any pH. Its potential is "reversible" with respect to the local proton concentration. Consequently, the potential of the RHE, measured against the fixed SHE scale, shifts with pH according to the Nernst equation. For $p_{\mathrm{H}_2} = 1 \, \mathrm{bar}$, this shift is given by:
    $$U_{\mathrm{RHE}} (\text{vs. SHE}) = -\frac{RT}{F} \ln(a_{\mathrm{H}^+}) = -\frac{2.303RT}{F}\mathrm{pH} \approx -0.059 \, \mathrm{V} \times \mathrm{pH} \text{ at } 298.15 \, \mathrm{K}$$
    This means a potential $U$ measured versus SHE can be converted to the RHE scale via:
    $$U_{\mathrm{RHE}} = U_{\mathrm{SHE}} - U_{\mathrm{RHE}} (\text{vs. SHE}) = U_{\mathrm{SHE}} + \frac{2.303RT}{F}\mathrm{pH}$$

*   The **Normal Hydrogen Electrode (NHE)** is a historical term for a practical hydrogen electrode in a $1 \, \mathrm{M}$ acid solution. Due to non-ideal [activity coefficients](@entry_id:148405), its potential is close but not identical to the SHE. In modern literature, SHE is the preferred term for the ideal standard.

The CHE model leverages the RHE scale. By referencing potentials to the RHE, the hydrogen electrode equilibrium occurs at $U_{\mathrm{RHE}} = 0 \, \mathrm{V}$ by definition, *at any pH*. This allows us to express the chemical potential of the proton-electron pair as:
$$\mu(\mathrm{H}^+) + \mu(e^-) = \frac{1}{2}\mu(\mathrm{H}_2(\mathrm{g})) - eU_{\mathrm{RHE}}$$
This equation is the workhorse of the CHE model. It allows one to replace the challenging calculation of a solvated proton's free energy with the readily calculable free energy of gas-phase $\mathrm{H}_2$, with all potential and pH dependencies captured in a simple, universal way.

### Constructing a Free Energy Diagram: A Step-by-Step Guide

#### Defining the Reaction Pathway

The first step in constructing a [free energy diagram](@entry_id:1125307) is to hypothesize a plausible [reaction mechanism](@entry_id:140113), breaking down the overall chemical transformation into a sequence of [elementary steps](@entry_id:143394). These steps typically involve adsorption of reactants, a series of surface-mediated chemical transformations, and desorption of products.

Consider the electrochemical reduction of $\mathrm{CO}_2$ to $\mathrm{CO}$: $\mathrm{CO_2} + 2(\mathrm{H}^+ + e^-) \rightarrow \mathrm{CO} + \mathrm{H_2O}$. A widely accepted pathway on a gold surface involves the formation of a carboxyl ($*\mathrm{COOH}$) intermediate, where $*$ denotes a surface site. The [elementary steps](@entry_id:143394) and corresponding [thermodynamic states](@entry_id:755916) for the [free energy diagram](@entry_id:1125307) are defined as follows :

1.  **Initial State:** The system starts with a bare catalyst surface ($*$) and reactants in their [reference state](@entry_id:151465) (e.g., gaseous $\mathrm{CO}_2$).
    *   State 0: $* + \mathrm{CO_2(g)}$

2.  **First PCET:** A concerted proton-[electron transfer](@entry_id:155709) forms the first intermediate.
    *   Step: $* + \mathrm{CO_2(g)} + (\mathrm{H}^+ + e^-) \rightarrow *\mathrm{COOH}$
    *   State 1: $*\mathrm{COOH}$

3.  **Second PCET:** A second proton-[electron transfer](@entry_id:155709) occurs, forming adsorbed $\mathrm{CO}$ and a water molecule.
    *   Step: $*\mathrm{COOH} + (\mathrm{H}^+ + e^-) \rightarrow *\mathrm{CO} + \mathrm{H_2O(l)}$
    *   State 2: $*\mathrm{CO} + \mathrm{H_2O(l)}$

4.  **Product Desorption:** The adsorbed product desorbs into the gas phase, regenerating the catalyst site.
    *   Step: $*\mathrm{CO} \rightarrow * + \mathrm{CO(g)}$
    *   State 3: $* + \mathrm{CO(g)} + \mathrm{H_2O(l)}$

It is crucial to note that within the CHE framework, explicit protons and electrons are not listed as separate [thermodynamic states](@entry_id:755916) in the diagram. Their chemical potentials are incorporated into the energy calculation for each step involving a proton-electron transfer.

The addition of a hydrogen atom ($H^+ + e^-$) to an adsorbed species, known as a **Proton-Coupled Electron Transfer (PCET)**, can occur via two distinct mechanisms :

*   **Concerted PCET:** The proton and electron are transferred in a single elementary step. For a step transforming $*A \rightarrow *AH$, we have $\Delta n_e = 1$ and $\Delta n_{\mathrm{H}} = 1$. When referencing to SHE, the free energy change for this step will depend on both potential and pH: $\Delta G(U, \mathrm{pH}) = \Delta G_0 - eU - k_B T \ln(10) \mathrm{pH}$.

*   **Sequential PCET:** The transfer occurs in two distinct steps, either Electron Transfer (ET) followed by Proton Transfer (PT), or vice versa.
    *   An ET-only step ($*A + e^- \rightarrow *A^-$) involves $\Delta n_e = 1, \Delta n_{\mathrm{H}} = 0$. Its free energy depends only on potential: $\Delta G(U) = \Delta G_{\text{ET},0} - eU$.
    *   A PT-only step ($*A^- + \mathrm{H}^+ \rightarrow *AH$) involves $\Delta n_e = 0, \Delta n_{\mathrm{H}} = 1$. Its free energy depends only on pH: $\Delta G(\mathrm{pH}) = \Delta G_{\text{PT},0} - k_B T \ln(10) \mathrm{pH}$.

The CHE framework can model both concerted and sequential pathways by correctly assigning the electron and proton counts to each elementary step.

#### Calculating the Free Energy of Each State

The absolute free energy of each state in the diagram must be calculated relative to a common reference. This is typically done using Density Functional Theory (DFT) combined with statistical mechanics. The Gibbs free energy ($G$) of a species at temperature $T$ and pressure $p$ is assembled from its DFT-computed electronic energy ($E_{\mathrm{DFT}}$) and several corrections:
$$G = E_{\mathrm{DFT}} + \mathrm{ZPE} + \Delta H_{\mathrm{th}} - TS$$
Here, $\mathrm{ZPE}$ is the [zero-point vibrational energy](@entry_id:171039), $\Delta H_{\mathrm{th}}$ is the thermal correction to enthalpy from $0 \, \mathrm{K}$ to $T$, and $TS$ is the entropic contribution to the free energy.

As a concrete example, let's calculate the Gibbs free energy change, $\Delta G$, for hydrogen adsorption: $* + \frac{1}{2}\mathrm{H}_2 \rightarrow \mathrm{H}^*$ . The reaction free energy is $\Delta G = G(\mathrm{H}^*) - G(*) - \frac{1}{2}G(\mathrm{H}_2)$. This is computed as the sum of changes in each component:
$$\Delta G = \Delta E_{\mathrm{DFT}} + \Delta(\mathrm{ZPE}) + \Delta(\Delta H_{\mathrm{th}}) - \Delta(TS)$$
For a typical calculation at $298 \, \mathrm{K}$, these corrections are significant. For instance, the electronic binding energy $\Delta E_{\mathrm{DFT}}$ might be favorable (negative), but the loss of the large translational and rotational entropy of gas-phase $\mathrm{H}_2$ upon adsorption results in a large, unfavorable entropic penalty ($-\Delta(TS)$ is large and positive), often making the overall $\Delta G$ of adsorption positive.

The entropic term, $TS$, is particularly important for gas-phase species. It can be calculated from first principles using [statistical thermodynamics](@entry_id:147111). The total molar entropy is the sum of translational, rotational, vibrational, and electronic contributions: $S = S_{\mathrm{trans}} + S_{\mathrm{rot}} + S_{\mathrm{vib}} + S_{\mathrm{elec}}$. For a molecule like $\mathrm{CO}$ at standard conditions, the translational and [rotational modes](@entry_id:151472) contribute the most significantly to the entropy, while the vibrational contribution is often negligible at room temperature as the mode is largely unpopulated . For adsorbed species, translational and rotational motions are quenched, and their entropy is dominated by low-frequency [vibrational modes](@entry_id:137888).

#### Assembling the Potential-Dependent Diagram

Once the free energy of each state, $G_k$, is determined at a reference potential (typically $U=0 \, \mathrm{V}$ vs. RHE), the potential-dependent free energy is obtained by applying the CHE correction. If a state $k$ has been formed by the net transfer of $n_k$ proton-electron pairs relative to the initial state, its free energy at potential $U$ is:
$$G_k(U) = G_k(U=0) - n_k eU$$
Plotting $G_k(U)$ versus the reaction coordinate (the sequence of states) generates the [free energy diagram](@entry_id:1125307).

An important principle is that the choice of the absolute zero of energy is arbitrary. One may set the energy of the initial state ($* + \mathrm{CO_2(g)}$ in our example) to zero, or any other state, or even an external reference. Shifting the entire diagram vertically by a constant amount does not change the [physical observables](@entry_id:154692), which are the *differences* in free energy between states ($\Delta G_{\text{step}}$) . Consequently, key quantities derived from these differences, such as the reaction overpotential or the identity of the [potential-determining step](@entry_id:1129989) (the step with the largest positive $\Delta G$), are invariant to the choice of the energy zero.

### Advanced Topics and Refinements

The standard CHE model relies on several idealizations. Here, we discuss important refinements that lead to more accurate and realistic free energy diagrams.

#### Beyond the Ideal Model: Electric Field Effects

The standard CHE model is often implemented using DFT calculations on neutral surfaces in a vacuum, neglecting the influence of the [electrochemical double layer](@entry_id:160682) and the associated strong electric field. However, the energy of adsorbed intermediates can be significantly altered by this field, an effect known as the **electrochemical Stark effect**.

A more advanced approach separates the intrinsic chemical energy from the explicit field effect . In this "extrapolative" workflow, the reaction free energy is constructed by summing three distinct terms:
1.  **Intrinsic Chemistry ($\Delta G_{\mathrm{can}}$):** The reaction free energy calculated at zero field (e.g., at the [potential of zero charge](@entry_id:264934), $U_{\mathrm{PZC}}$).
2.  **Stark Field Effect ($\Delta G_{\mathrm{field}}$):** A correction, often linear in potential, that accounts for the interaction of the adsorbate's dipole moment with the interfacial field: $\Delta G_{\mathrm{field}}(U) = s(U - U_{\mathrm{PZC}})$, where $s$ is the Stark tuning slope.
3.  **CHE Electron Energy ($-neU$):** The standard thermodynamic free energy of the $n$ electrons transferred in the step.

The total reaction free energy is thus $\Delta G(U) = \Delta G_{\mathrm{can}} + \Delta G_{\mathrm{field}}(U) - neU$. It is critical to recognize that the CHE term (electron bookkeeping) and the Stark term (physical field response) are distinct and must both be included to avoid an incomplete model.

An even more rigorous approach is the **grand canonical** or **constant-potential** method. In this workflow, DFT calculations are performed at a fixed [electrode potential](@entry_id:158928), meaning the electronic structure is solved self-consistently in the presence of the corresponding [surface charge](@entry_id:160539) and electric field. The output of such a calculation, the reaction grand potential difference $\Delta \Omega(U)$, is by construction equivalent to the desired reaction Gibbs free energy $\Delta G(U)$. All potential effects, including the electron energy and Stark effects, are implicitly and automatically included. Adding any further potential-dependent terms would constitute double-counting.

#### Accounting for Coverage Effects: The Lattice-Gas Model

Free energy diagrams are often constructed in the zero-coverage limit, ignoring interactions between adsorbates. At finite coverage, these lateral interactions can significantly alter adsorption energies and reaction barriers. The **[lattice-gas model](@entry_id:141303)** provides a framework to account for these effects .

The surface is modeled as a lattice of [adsorption sites](@entry_id:1120832), where each site $i$ is either empty ($n_i=0$) or occupied ($n_i=1$). The **coverage**, $\theta$, is the fraction of occupied sites: $\theta = \frac{1}{N_s}\sum_i n_i$. The energy of a specific configuration of adsorbates is given by the lattice-gas Hamiltonian:
$$H(\\{n_i\\}) = \varepsilon \sum_i n_i + \frac{1}{2} \sum_{i \neq j} V_{ij} n_i n_j$$
Here, $\varepsilon$ is the on-site [adsorption energy](@entry_id:180281) (which can be potential-dependent, $\varepsilon(U)$), and $V_{ij}$ is the interaction energy between adsorbates at sites $i$ and $j$. The factor of $\frac{1}{2}$ prevents double-counting of pairs.

Within the simple **Bragg-Williams mean-field approximation**, the free energy per site, $f(\theta)$, can be derived. It consists of three terms: the average on-site energy, the average interaction energy, and the configurational entropy:
$$f(\theta) = \theta \varepsilon + \frac{z}{2}V\theta^2 + k_B T \big[\theta\ln\theta + (1-\theta)\ln(1-\theta)\big]$$
where $z$ is the [coordination number](@entry_id:143221) of the lattice and $V$ is the nearest-neighbor interaction energy. This model allows one to calculate coverage-dependent free energies, providing a more realistic picture of catalysis under operating conditions.

#### Quantifying Uncertainty in Free Energy Diagrams

The free energies computed via DFT and statistical mechanics are not exact values but estimates subject to multiple sources of uncertainty. Rigorous scientific practice demands that these uncertainties be quantified and propagated to the final [free energy diagram](@entry_id:1125307), yielding error bars on the computed energies.

The sources of uncertainty are numerous, including :
*   **Model Discrepancy:** Errors inherent to the chosen theoretical model, such as the choice of DFT functional (e.g., PBE vs. RPBE) or the solvation model (implicit continuum vs. [explicit solvent](@entry_id:749178)).
*   **Parameter Uncertainty:** Errors in estimating corrections, such as using the [harmonic approximation](@entry_id:154305) for vibrational frequencies and entropy.
*   **Finite-Size Effects:** Errors arising from the use of [periodic boundary conditions](@entry_id:147809) to model an extended surface with a finite simulation cell.
*   **Numerical Noise:** Errors from incomplete basis sets, convergence thresholds, or numerical integration grids.

A powerful tool for synthesizing these uncertainties is a **hierarchical Bayesian model**. This statistical framework can combine results from different computational setups (e.g., various functionals and cell sizes) and correctly account for the fact that calculations sharing a modeling choice (e.g., the same functional) will share a systematic bias. Such a model treats shared biases as [random effects](@entry_id:915431), which naturally induces correlations between the data points. The final output is not a single value for each free energy state, but a full [posterior probability](@entry_id:153467) distribution, from which a [credible interval](@entry_id:175131) (e.g., a 95% error bar) can be extracted. This approach represents the state-of-the-art in robustly assessing the reliability of computationally derived free energy diagrams.