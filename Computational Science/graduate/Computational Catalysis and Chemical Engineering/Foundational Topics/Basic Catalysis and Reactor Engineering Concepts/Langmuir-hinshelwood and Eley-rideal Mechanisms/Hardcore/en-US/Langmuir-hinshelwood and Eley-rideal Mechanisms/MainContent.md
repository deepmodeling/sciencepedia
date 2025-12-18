## Introduction
Heterogeneous catalysis, where reactions occur at the interface between a solid catalyst and a fluid phase, is fundamental to chemical manufacturing, energy production, and [environmental remediation](@entry_id:149811). The ability to control and optimize these processes hinges on a deep understanding of the underlying surface [reaction mechanisms](@entry_id:149504). However, the sequence of elementary steps occurring on a catalyst surface is often complex and not directly observable. The Langmuir-Hinshelwood (LH) and Eley-Rideal (ER) mechanisms provide two foundational yet powerful kinetic models that form the cornerstone for interpreting and predicting the behavior of these surface reactions. This article bridges the gap between the microscopic events of adsorption and reaction and the macroscopic, measurable reaction rates.

Across the following chapters, you will embark on a journey from first principles to practical application. The "Principles and Mechanisms" chapter will meticulously derive the [rate laws](@entry_id:276849) for the LH and ER pathways, starting from the [statistical thermodynamics](@entry_id:147111) of adsorption and elucidating their distinct kinetic signatures. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these models are employed to solve real-world problems, from discriminating between mechanisms in the lab to designing industrial reactors and understanding phenomena in materials and environmental science. Finally, the "Hands-On Practices" chapter will provide a series of problems designed to solidify your ability to apply these concepts, guiding you through [rate law](@entry_id:141492) derivation, mechanism discrimination, and the analysis of experimental data. By the end, you will have a robust framework for analyzing and modeling the kinetics of reactions on solid surfaces.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and kinetic mechanisms governing reactions on solid surfaces, focusing on the canonical Langmuir-Hinshelwood (LH) and Eley-Rideal (ER) models. We will construct these models from first principles, beginning with the [statistical thermodynamics](@entry_id:147111) of adsorption and progressing to the derivation of complex rate expressions, their analysis, and the methods for experimental discrimination.

### Fundamental Concepts of Surface Adsorption

At the heart of [heterogeneous catalysis](@entry_id:139401) lies the process of **adsorption**, where gas-phase or liquid-phase molecules bind to a solid surface. The quantitative description of surface processes begins with the concept of **[surface coverage](@entry_id:202248)**.

#### Surface Coverage

Surface coverage, denoted by the symbol $\theta$, is a dimensionless quantity that represents the fraction of available adsorption sites on a surface that are occupied by an adsorbate. For a uniform surface with a known density of equivalent [adsorption sites](@entry_id:1120832), $N_s$ (measured in sites per unit area), and an experimentally determined adsorbate [areal density](@entry_id:1121098), $N_{\text{ads}}$, the coverage is defined simply as the ratio:

$$
\theta = \frac{N_{\text{ads}}}{N_s}
$$

For instance, if a single-crystal metal surface possesses an atop site density of $N_s = 1.5 \times 10^{19}\ \mathrm{m^{-2}}$ and experimental measurements under specific conditions reveal a carbon monoxide (CO) adsorbate density of $N_{\text{ads}} = 7.5 \times 10^{18}\ \mathrm{m^{-2}}$, the surface coverage is $\theta = 0.50$ . By its definition as a fraction of occupied sites, the coverage for a single monolayer cannot exceed unity, i.e., $0 \le \theta \le 1$. Claims of coverage exceeding unity for a specific site type based on [dissociative adsorption](@entry_id:199140) processes are inconsistent with this fundamental definition .

#### Physisorption and Chemisorption

Adsorption processes are broadly classified into two categories based on the nature of the surface-adsorbate bond.

*   **Physisorption** ([physical adsorption](@entry_id:170714)) is a weak, long-range interaction mediated by van der Waals forces, analogous to the forces responsible for the condensation of gases. It does not involve the formation of a chemical bond. Consequently, the enthalpy of physisorption is typically low, generally less than $40 \text{ kJ mol}^{-1}$.

*   **Chemisorption** ([chemical adsorption](@entry_id:169918)) involves the formation of a chemical bond between the adsorbate and the surface, which may involve significant [electron transfer](@entry_id:155709) and [orbital hybridization](@entry_id:140298). This is a much stronger interaction, with typical adsorption enthalpies ranging from $40$ to over $800 \text{ kJ mol}^{-1}$. A measured initial [heat of adsorption](@entry_id:199302) for CO on a metal surface of $110 \text{ kJ mol}^{-1}$ is a clear indicator of [chemisorption](@entry_id:149998), not physisorption . While [chemisorption](@entry_id:149998) can be an activated process with a significant energy barrier, many systems, such as CO on [transition metals](@entry_id:138229), exhibit non-[activated chemisorption](@entry_id:204128) with a negligible barrier.

The kinetic models discussed in this chapter primarily concern chemisorbed species, which act as the [reactive intermediates](@entry_id:151819) in [catalytic cycles](@entry_id:151545).

### The Langmuir Model of Adsorption

The simplest and most foundational model for describing [chemisorption](@entry_id:149998) equilibrium is the **Langmuir adsorption model**. To derive kinetic expressions for surface reactions, we must first understand the relationship between the gas-phase conditions (pressure, temperature) and the surface coverages of reactants. The Langmuir model provides this relationship under a set of idealizing assumptions. From a statistical mechanics perspective, these assumptions can be stated with precision :

1.  **Identical Adsorption Sites**: The surface is treated as a uniform lattice of $N_s$ energetically equivalent sites. The [adsorption energy](@entry_id:180281), $E_{\text{ads}}$, is the same for every site. This assumption is justified for well-ordered single-crystal terraces where DFT calculations may show energy variations of less than $0.02 \text{ eV}$, a value comparable to thermal energy at typical catalytic temperatures .

2.  **No Lateral Interactions**: Adsorbed molecules do not interact with each other. The energy of an adsorbed molecule is independent of the occupancy of neighboring sites. The total energy of the adlayer is simply the sum of the energies of the individual adsorbates. This assumption is most valid at low coverage, where adsorbates are, on average, far apart. On metal surfaces, the high mobility of [conduction electrons](@entry_id:145260) provides efficient screening of electrostatic fields, strongly dampening long-range [dipole-dipole interactions](@entry_id:144039). Experimental evidence supporting this assumption includes an [isosteric heat of adsorption](@entry_id:151208) that is independent of coverage and a pair-[correlation function](@entry_id:137198) $g(r) \approx 1$ from [surface scattering](@entry_id:268452) experiments, indicating a random, uncorrelated arrangement of adsorbates .

3.  **Single Occupancy**: Each site can accommodate at most one adsorbate molecule. This is a consequence of the finite size of adsorbates and the strong, localized nature of the chemical bond formed during [chemisorption](@entry_id:149998), which creates a zone of steric exclusion.

When these three assumptions hold, the adsorption process can be described by a simple kinetic balance or, more formally, by equating the chemical potentials of the gas-phase and adsorbed-phase species.

### Adsorption Equilibria and Isotherms

#### The Competitive Langmuir Isotherm

In many catalytic reactions, multiple species compete for the same set of surface sites. Consider a binary gas mixture of species $A$ and $B$ in contact with a uniform surface. Both species adsorb non-dissociatively and reversibly:

$A(\text{g}) + * \rightleftharpoons A*$

$B(\text{g}) + * \rightleftharpoons B*$

Here, $*$ denotes a vacant surface site, and $A*$ and $B*$ represent the adsorbed species. Under the Langmuir assumptions, and assuming the adsorption steps are at quasi-equilibrium, we can write equilibrium expressions relating the coverages to the [partial pressures](@entry_id:168927), $P_A$ and $P_B$. Let $K_A$ and $K_B$ be the adsorption equilibrium constants. The coverages of adsorbed $A$ and $B$, $\theta_A$ and $\theta_B$, can be expressed in terms of the vacant site fraction, $\theta_*$:

$\theta_A = K_A P_A \theta_*$

$\theta_B = K_B P_B \theta_*$

The system is constrained by the **site balance equation**, which states that the sum of all fractional coverages must equal one:

$\theta_A + \theta_B + \theta_* = 1$

By substituting the equilibrium expressions into the site balance and solving for the coverages, we arrive at the **competitive Langmuir [adsorption isotherms](@entry_id:148975)** :

$$
\theta_A = \frac{K_A P_A}{1 + K_A P_A + K_B P_B}
$$

$$
\theta_B = \frac{K_B P_B}{1 + K_A P_A + K_B P_B}
$$

The fraction of vacant sites is given by $\theta_* = \frac{1}{1 + K_A P_A + K_B P_B}$. These equations are fundamental. They show that the coverage of one species depends not only on its own [partial pressure](@entry_id:143994) but also on the [partial pressure](@entry_id:143994) and adsorption strength of the competing species. The term $(K_A P_A + K_B P_B)$ in the denominator represents the total demand for surface sites; as it increases, the number of available vacant sites decreases, and competition becomes more intense.

### The Langmuir-Hinshelwood (LH) Mechanism

The **Langmuir-Hinshelwood (LH) mechanism** describes a [surface reaction](@entry_id:183202) in which two co-adsorbed species react with each other. For a bimolecular reaction between reactants $A$ and $B$, the elementary surface reaction is:

$A* + B* \rightarrow \text{Products}$

#### Rate Law Derivation and Analysis

Assuming this [surface reaction](@entry_id:183202) is the [rate-determining step](@entry_id:137729), its rate, $r$, is proportional to the product of the coverages of the reacting species, $\theta_A$ and $\theta_B$:

$r = k_r \theta_A \theta_B$

where $k_r$ is the intrinsic surface [reaction rate constant](@entry_id:156163). By substituting the competitive Langmuir [isotherms](@entry_id:151893) for $\theta_A$ and $\theta_B$ into this expression, we obtain the general rate law for a bimolecular LH reaction :

$$
r_{LH} = \frac{k_r K_A K_B P_A P_B}{(1 + K_A P_A + K_B P_B)^2}
$$

This rate law exhibits a rich and characteristic dependence on reactant pressures. The behavior can be understood by examining its asymptotic limits :

*   **Low-Coverage Limit** ($K_A P_A \ll 1$ and $K_B P_B \ll 1$): The denominator approaches 1, and the surface is mostly vacant ($\theta_* \approx 1$). The rate simplifies to $r_{LH} \approx k_r K_A K_B P_A P_B$. The reaction is first-order in both $P_A$ and $P_B$. The rate increases with pressure because the coverages of both reactants are increasing.

*   **High-Coverage, A-Dominated Limit** ($K_A P_A \gg 1$ and $K_A P_A \gg K_B P_B$): The surface becomes saturated with species $A$ ($\theta_A \approx 1$). The denominator is dominated by the $K_A P_A$ term, so $(1 + K_A P_A + K_B P_B)^2 \approx (K_A P_A)^2$. The rate expression becomes:
    $$
    r_{LH} \approx \frac{k_r K_A K_B P_A P_B}{(K_A P_A)^2} = \frac{k_r K_B P_B}{K_A P_A}
    $$
    In this regime, the rate is first-order in $P_B$ but **negative first-order** in $P_A$. This counter-intuitive result arises from **inhibition**. As $P_A$ increases, it further populates the surface with $A*$, displacing the few remaining $B*$ species needed for the reaction. The scarcity of vacant sites, for which $B$ must compete against a dominant $A$, causes $\theta_B$ to decrease proportionally to $1/P_A$, leading to an overall decrease in the reaction rate. A symmetric result ($r_{LH} \propto P_A / P_B$) holds if species $B$ dominates the surface.

This bell-shaped dependence of the rate on a reactant's partial pressure is a hallmark of the Langmuir-Hinshelwood mechanism.

### The Eley-Rideal (ER) Mechanism

The **Eley-Rideal (ER) mechanism** posits a different mode of interaction, where a gas-phase molecule reacts directly with an adsorbed species upon collision, without first adsorbing itself. For a reaction between gas-phase $A$ and adsorbed $B$, the [elementary step](@entry_id:182121) is:

$A(\text{g}) + B* \rightarrow \text{Products}$

#### Rate Law Derivation and Analysis

According to the law of [mass action](@entry_id:194892) for this [elementary step](@entry_id:182121), the rate is proportional to the concentration of the gas-phase reactant (i.e., its partial pressure $P_A$) and the [surface concentration](@entry_id:265418) of the adsorbed reactant (its coverage $\theta_B$) :

$r_{ER} = k_{ER} P_A \theta_B$

The kinetic behavior of the ER mechanism is typically simpler than that of the LH mechanism. For instance, if the coverage of $B$ is held constant by a large, buffered supply, the ER rate is strictly first-order in $P_A$ across all pressures: $r_{ER} \propto P_A$ . Unlike the LH mechanism, the ER rate does not exhibit a maximum or decrease at high pressures of the gas-phase reactant, because that reactant does not compete for surface sites.

#### Microscopic Origin of the ER Rate Constant

The Eley-Rideal rate constant, $k_{ER}$, is not merely an empirical parameter but can be connected to the microscopic physics of gas-surface collisions . A first-principles derivation shows that $k_{ER}$ encapsulates several factors:

$$
k_{\mathrm{ER}} = \frac{N_s \sigma_{\mathrm{geo}}}{\sqrt{2\pi m_A k_B T_g}} \exp\left(-\frac{E_a}{\alpha_E k_B T_g}\right)
$$

This expression can be deconstructed as follows:
*   The term $\frac{1}{\sqrt{2\pi m_A k_B T_g}}$ comes from the **Hertz-Knudsen equation** of kinetic gas theory and represents the molecular impingement flux per unit pressure.
*   $N_s \sigma_{\mathrm{geo}}$ represents the total reactive cross-sectional area presented by the adsorbates on the surface, where $\sigma_{\mathrm{geo}}$ is the geometric cross-section of a single adsorbed reactant.
*   The exponential term is an Arrhenius-like factor representing the probability that an impinging molecule has sufficient energy to overcome the [reaction barrier](@entry_id:166889) $E_a$. The model here includes an **energy [accommodation coefficient](@entry_id:151152)** $\alpha_E$, which represents the fraction of the incident molecule's normal [translational energy](@entry_id:170705) that is effectively channeled into the [reaction coordinate](@entry_id:156248) to surmount the barrier. This detailed view connects the macroscopic rate constant to fundamental parameters of collision dynamics and surface structure.

### Kinetic Analysis and Mechanistic Discrimination

Deriving and applying these [rate laws](@entry_id:276849) often involves simplifying assumptions about the relative speeds of different [elementary steps](@entry_id:143394).

#### The Quasi-Equilibrium and Quasi-Steady-State Approximations

Two key approximations are central to simplifying complex microkinetic models :

1.  **Quasi-Equilibrium Approximation (QEA)**: This approximation is applied to a specific reversible step (e.g., adsorption: $A(g) + * \rightleftharpoons A*$) when the rates of its forward and reverse processes are much faster than the rates of any subsequent steps that consume its products. This implies that the reversible step is always in a state of partial equilibrium, nearly balanced. The condition for validity is that the characteristic frequency of adsorption/desorption (e.g., $k_a^A P_A + k_d^A$) must be much greater than the frequency of consumption of the adsorbate (e.g., $k_r \theta_B$ for an LH step). Under the QEA, the net flux through the equilibrated step is negligible compared to the gross forward and reverse fluxes, allowing the use of an algebraic equilibrium expression (an isotherm) to relate coverages to pressures.

2.  **Quasi-Steady-State Approximation (QSSA)**: This is a more general approximation applied to a highly reactive, low-concentration intermediate. It assumes that the net rate of change of the intermediate's concentration (or coverage) is approximately zero, meaning its rate of formation is balanced by its total rate of consumption. For an adsorbate $A*$, this means $\frac{d\theta_A}{dt} \approx 0$. Unlike the QEA, the QSSA does not require the adsorption and desorption steps to be individually balanced; it only requires that the total production of $A*$ balances its total consumption (via desorption and reaction). The QSSA is justified when the relaxation timescale of the intermediate is much shorter than the timescale over which the overall reaction proceeds. The QEA is a special, more restrictive case of the QSSA.

#### Experimental Discrimination between LH and ER Mechanisms

The distinct pressure dependencies of the LH and ER mechanisms provide a powerful experimental tool for telling them apart . By measuring the reaction rate, $r$, as a function of a reactant partial pressure, say $P_A$, while keeping other conditions constant, one can determine the **apparent [reaction order](@entry_id:142981)**, $n_A = \frac{d\ln r}{d\ln P_A}$.

*   For a simple **ER mechanism** ($r_{ER} \propto P_A$), a plot of $\ln r$ versus $\ln P_A$ will yield a straight line with a slope of $n_A = 1$ over the entire pressure range.

*   For an **LH mechanism**, the apparent order changes with pressure. At low pressures, $n_A \approx 1$. As the pressure increases and the surface begins to saturate, the order decreases, eventually passing through zero and potentially becoming negative at very high pressures due to inhibition. Thus, a plot of $\ln r$ versus $\ln P_A$ will be a curve with a continuously decreasing slope.

This difference in the behavior of the apparent [reaction order](@entry_id:142981) provides a clear kinetic signature to distinguish the two mechanistic pathways.

#### Apparent Activation Energy

The temperature dependence of a reaction rate is characterized by its activation energy. However, for a multi-step surface reaction, the experimentally measured **apparent activation energy**, $E_{\text{app}}$, is a composite quantity that reflects the temperature dependence of all contributing steps. $E_{\text{app}}$ is defined from an Arrhenius plot:

$$
E_{\text{app}} = -R \frac{\partial \ln r}{\partial (1/T)}
$$

For the bimolecular LH rate law, applying this definition shows that $E_{\text{app}}$ is not equal to the true activation energy of the [surface reaction](@entry_id:183202), $E_a$. Instead, it also incorporates the enthalpies of adsorption of the reactants, $\Delta H_A$ and $\Delta H_B$, which are typically negative (exothermic). A full derivation yields :

$$
E_{\text{app}} = E_a + \Delta H_A + \Delta H_B - 2 \frac{K_A P_A \Delta H_A + K_B P_B \Delta H_B}{1 + K_A P_A + K_B P_B}
$$

This expression reveals that $E_{\text{app}}$ is a function of both temperature and pressure (through the coverage-dependent terms $K_i P_i$). In the low-coverage limit, the fractional term vanishes, and $E_{\text{app}} \approx E_a + \Delta H_A + \Delta H_B$. Since adsorption is exothermic ($\Delta H_i  0$), the apparent activation energy is often lower than the true activation energy. This analysis is critical for correctly interpreting experimental kinetic data and extracting fundamental energetic parameters.

### Beyond the Ideal Model: The Role of Lateral Interactions

The Langmuir model's assumption of non-interacting adsorbates is a powerful simplification, but it breaks down at higher coverages where adsorbates are forced into close proximity.

#### The Frumkin-Fowler-Guggenheim Isotherm

To account for lateral interactions on a uniform surface, we can use a mean-field [lattice-gas model](@entry_id:141303). In this model, each adsorbate is assumed to experience an average interaction energy proportional to the overall coverage, $\theta$. By equating the chemical potential of the gas with the mean-field chemical potential of the adlayer, one derives the **Frumkin-Fowler-Guggenheim isotherm**  :

$$
K P = \frac{\theta}{1-\theta} \exp(\alpha \theta)
$$

Here, $K$ is the intrinsic adsorption equilibrium constant, and $\alpha$ is a dimensionless parameter representing the strength of the lateral interactions (scaled by $RT$). For **repulsive interactions**, $\alpha > 0$; for **attractive interactions**, $\alpha  0$. When $\alpha = 0$, the equation reduces to the standard Langmuir isotherm.

#### Consequences of Lateral Interactions

Lateral interactions can significantly alter both adsorption equilibria and reaction kinetics. Consider the case of repulsive interactions ($\alpha > 0$) :

1.  **Effect on Coverage**: The term $\exp(\alpha \theta)$ is greater than 1. To maintain equilibrium at a given pressure $P$, the pre-factor $\frac{\theta}{1-\theta}$ must be smaller than in the ideal case. This means that for any given pressure, the [surface coverage](@entry_id:202248) $\theta$ will be **lower** in the presence of repulsive interactions. The repulsions destabilize the adlayer, making it harder to populate the surface.

2.  **Effect on Reaction Kinetics**: This change in coverage directly impacts the [reaction kinetics](@entry_id:150220). For a unimolecular LH reaction ($r = k_r \theta_A$), since the coverage is lower, the rate will also be lower than predicted by the ideal Langmuir model. More subtly, the apparent [reaction order](@entry_id:142981), $n_A$, is also affected. The general expression for the apparent order derived from the Frumkin isotherm is:
    $$
    n_{A} = \frac{1-\theta_A}{1 + \alpha\theta_A(1-\theta_A)}
    $$
    At low coverage ($\theta_A \to 0$), the order approaches 1, regardless of $\alpha$. However, at higher coverages, the repulsive interactions ($\alpha > 0$) increase the denominator, but more importantly, they keep $\theta_A$ smaller than it would be otherwise. This "desaturation" effect means the rate remains more sensitive to pressure changes. Consequently, for a given pressure in a high-coverage regime, the apparent [reaction order](@entry_id:142981) will be **larger** (closer to 1) for a system with repulsive interactions than for an ideal system . Understanding these deviations is crucial for accurately modeling catalytic systems, especially under conditions where surface coverage is high.