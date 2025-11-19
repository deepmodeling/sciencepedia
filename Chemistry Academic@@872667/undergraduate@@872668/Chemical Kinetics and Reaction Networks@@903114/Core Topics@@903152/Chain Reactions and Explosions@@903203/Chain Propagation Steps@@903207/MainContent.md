## Introduction
Chain reactions are a [fundamental class](@entry_id:158335) of chemical transformations responsible for processes as diverse as the synthesis of plastics, the chemistry of our atmosphere, and the combustion of fuels. While these reactions are defined by a sequence of initiation, propagation, and termination steps, it is the propagation phase that forms the self-sustaining engine of the reaction, responsible for converting the vast majority of reactants into products. Understanding the principles that govern these steps is therefore paramount for controlling and predicting the behavior of these complex systems. This article addresses the critical need to dissect this core mechanism, moving beyond a simple definition to a deep, functional understanding.

This article will guide you through the intricate world of [chain propagation](@entry_id:182302). In the "Principles and Mechanisms" chapter, you will learn the defining characteristics of propagation steps, how they form cyclic [reaction pathways](@entry_id:269351), and the thermodynamic and kinetic factors, such as activation energy and intermediate stability, that dictate their rates and selectivity. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate the real-world relevance of these principles, showing how propagation steps drive outcomes in [organic synthesis](@entry_id:148754), polymer science, [atmospheric chemistry](@entry_id:198364), and even essential biological systems. Finally, the "Hands-On Practices" section will allow you to apply this knowledge, solidifying your grasp of the concepts by working through targeted problems in chemical kinetics.

## Principles and Mechanisms

Following the initial formation of [reactive intermediates](@entry_id:151819) in the initiation stage of a chain reaction, the core of the chemical transformation occurs through a series of **[chain propagation](@entry_id:182302) steps**. These steps are responsible for converting the bulk of the reactants into products and form the cyclic, self-sustaining heart of the [chain mechanism](@entry_id:150289). This chapter elucidates the fundamental principles governing these crucial steps, their energetic and kinetic characteristics, and their role in determining the overall outcome of a reaction.

### The Defining Characteristic of Chain Propagation

A chain reaction proceeds via **[reactive intermediates](@entry_id:151819)**, also known as **[chain carriers](@entry_id:197278)**. These are typically highly reactive species such as [free radicals](@entry_id:164363), which possess one or more unpaired electrons. The mechanism of a [chain reaction](@entry_id:137566) is broadly divided into three phases: initiation, propagation, and termination. Each phase is defined by its net effect on the total population of these [chain carriers](@entry_id:197278).

An elementary step is classified as a **[propagation step](@entry_id:204825)** if the total number of [reactive intermediates](@entry_id:151819) is conserved from reactants to products. In the most common scenario, one [chain carrier](@entry_id:200641) is consumed, and precisely one new [chain carrier](@entry_id:200641) is generated. This conservation is the defining feature of propagation [@problem_id:1475571].

This contrasts sharply with the other two phases:
- **Initiation**: Characterized by a net *increase* in the number of [reactive intermediates](@entry_id:151819). For example, the homolytic cleavage of a stable molecule like $\text{Cl}_2$ by heat or light produces two radical [chain carriers](@entry_id:197278): $\text{Cl}_2 \rightarrow 2\text{Cl}\cdot$.
- **Termination**: Characterized by a net *decrease* in the number of [reactive intermediates](@entry_id:151819). This typically involves the combination of two radicals to form a stable, non-radical molecule, such as $\cdot\text{CH}_3 + \cdot\text{Cl} \rightarrow \text{CH}_3\text{Cl}$.

Consider the [elementary step](@entry_id:182121) from the free-radical chlorination of methane, a classic example of a [chain reaction](@entry_id:137566) [@problem_id:1475550]:
$$ \cdot\text{Cl} + \text{CH}_4 \rightarrow \text{HCl} + \cdot\text{CH}_3 $$
To classify this step, we count the number of radical species on each side of the reaction equation. The reactants contain one radical, the chlorine atom ($\cdot\text{Cl}$). The products also contain one radical, the methyl radical ($\cdot\text{CH}_3$). Since one radical is consumed and one is produced, the total number of radicals remains unchanged. Therefore, this is a quintessential [propagation step](@entry_id:204825). The formation of the stable product $\text{HCl}$ and a new radical that can continue the reaction is the hallmark of this phase.

### The Propagation Cycle: Sustaining the Chain

While single propagation steps conserve the number of radicals, their true power lies in their ability to link together into a **propagation cycle**. This cycle is a sequence of two or more propagation steps that, when combined, accomplish two critical functions: they convert stable reactants into stable products, and they regenerate the original radical [chain carrier](@entry_id:200641), allowing the sequence to repeat thousands or even millions of times.

The gas-phase chlorination of ethane to chloroethane provides an excellent illustration of such a cycle [@problem_id:1475532]. The overall [stoichiometry](@entry_id:140916) of the reaction is:
$$ \text{CH}_3\text{CH}_3 + \text{Cl}_2 \rightarrow \text{CH}_3\text{CH}_2\text{Cl} + \text{HCl} $$
This transformation is accomplished via a two-step propagation cycle involving two [chain carriers](@entry_id:197278): the chlorine radical ($\cdot\text{Cl}$) and the ethyl radical ($\cdot\text{CH}_2\text{CH}_3$).

**Step 1: Hydrogen Abstraction**
$$ \cdot\text{Cl} + \text{CH}_3\text{CH}_3 \rightarrow \text{HCl} + \cdot\text{CH}_2\text{CH}_3 $$
In this step, the initial chlorine radical abstracts a hydrogen atom from an ethane molecule. This consumes the $\cdot\text{Cl}$ radical but produces a new ethyl radical, $\cdot\text{CH}_2\text{CH}_3$.

**Step 2: Halogen Abstraction**
$$ \cdot\text{CH}_2\text{CH}_3 + \text{Cl}_2 \rightarrow \text{CH}_3\text{CH}_2\text{Cl} + \cdot\text{Cl} $$
The newly formed ethyl radical then reacts with a stable chlorine molecule. It abstracts a chlorine atom to form the final organic product, chloroethane, and crucially, regenerates the original chlorine radical, $\cdot\text{Cl}$.

The regenerated $\cdot\text{Cl}$ radical is now free to initiate another cycle by reacting with another ethane molecule. The two radicals, $\cdot\text{Cl}$ and $\cdot\text{CH}_2\text{CH}_3$, are the primary **[chain carriers](@entry_id:197278)**. Notice that if we sum these two propagation steps, the radical intermediates cancel out, yielding the overall [reaction stoichiometry](@entry_id:274554). This [cyclic process](@entry_id:146195) is the engine of the [chain reaction](@entry_id:137566), responsible for the high [quantum yield](@entry_id:148822) observed in such processes.

### Energetics and Thermodynamics of Propagation

The feasibility and directionality of a [propagation step](@entry_id:204825) are governed by its thermodynamics. The [enthalpy change](@entry_id:147639) ($\Delta H_{\text{rxn}}$) for a [propagation step](@entry_id:204825) can often be estimated by considering the bonds broken and the bonds formed. The **[bond dissociation enthalpy](@entry_id:149221) (BDE)**, or $D(\text{X-Y})$, is the energy required to cleave the bond between X and Y homolytically. The [enthalpy change](@entry_id:147639) for the reaction is approximately the sum of the BDEs of all bonds broken minus the sum of the BDEs of all bonds formed.

$$ \Delta H_{\text{rxn}} \approx \sum D(\text{bonds broken}) - \sum D(\text{bonds formed}) $$

For instance, in the hydrogen abstraction from methane by a fluorine radical [@problem_id:1475561], a C-H bond is broken and an H-F bond is formed:
$$ \cdot\text{F} + \text{CH}_4 \rightarrow \text{HF} + \cdot\text{CH}_3 $$
Given that the BDE for the C-H bond in methane is approximately $439 \, \text{kJ/mol}$ and for the H-F bond is $565 \, \text{kJ/mol}$, the [reaction enthalpy](@entry_id:149764) is:
$$ \Delta H_{\text{rxn}} \approx D(\text{H-CH}_3) - D(\text{H-F}) = 439 \, \text{kJ/mol} - 565 \, \text{kJ/mol} = -126 \, \text{kJ/mol} $$
The reaction is strongly exothermic, which is characteristic of reactions involving the highly reactive fluorine atom. In general, a [propagation step](@entry_id:204825) must be thermodynamically favorable (or at least not prohibitively unfavorable) to occur at a significant rate.

The spontaneity of a reaction is ultimately determined by the Gibbs free energy change, $\Delta G = \Delta H - T\Delta S$. While many propagation steps are simple atom transfers with small entropy changes, some, like [polymerization](@entry_id:160290), involve significant changes in order. In [free-radical polymerization](@entry_id:143255), the [propagation step](@entry_id:204825) involves the addition of a monomer to a growing polymer chain [@problem_id:1475580]:
$$ R-(\text{CH}_2-\text{CH}_2)_n\cdot + \text{CH}_2=\text{CH}_2 \rightleftharpoons R-(\text{CH}_2-\text{CH}_2)_{n+1}\cdot $$
This reaction is exothermic ($\Delta H^\circ  0$) because a relatively weak $\pi$-bond in [ethylene](@entry_id:155186) is replaced by a stronger $\sigma$-bond in the polymer backbone. However, it is also accompanied by a large negative entropy change ($\Delta S^\circ  0$) because two separate molecules are combined into one, leading to a more ordered state.

The temperature dependence of $\Delta G^\circ$ reveals a critical threshold. At low temperatures, the favorable enthalpy term ($\Delta H^\circ$) dominates, and [polymerization](@entry_id:160290) is spontaneous ($\Delta G^\circ  0$). As temperature increases, the unfavorable entropy term ($-T\Delta S^\circ$) becomes more significant. The temperature at which $\Delta G^\circ = 0$ is known as the **[ceiling temperature](@entry_id:139986)**, $T_c$.
$$ T_c = \frac{\Delta H^\circ}{\Delta S^\circ} $$
Above this temperature, $\Delta G^\circ > 0$, and the reverse reaction, **depropagation**, becomes thermodynamically favored. For polyethylene, with $\Delta H^\circ = -92.5 \, \text{kJ/mol}$ and $\Delta S^\circ = -158 \, \text{J/(mol K)}$, the [ceiling temperature](@entry_id:139986) is approximately $585 \, \text{K}$. This concept is of immense practical importance in industrial [polymerization](@entry_id:160290) processes.

### Kinetics and Selectivity in Propagation

Beyond thermodynamic feasibility, the kinetics of propagation steps determine the overall reaction rate and [product distribution](@entry_id:269160).

#### Factors Governing Reaction Rate

The rate of an elementary [propagation step](@entry_id:204825) is dictated by its rate constant, $k$, which is related to the activation energy, $E_a$, through the Arrhenius equation. For a series of related reactions, such as the abstraction of a hydrogen atom by the same radical from different substrates, the **Bell-Evans-Polanyi (BEP) principle** provides a powerful correlation. It states that for a homologous series of reactions, the activation energy is often a linear function of the [reaction enthalpy](@entry_id:149764):
$$ E_a = \alpha \Delta H_{\text{rxn}} + c $$
where $\alpha$ and $c$ are constants for the series. This implies that more [exothermic reactions](@entry_id:199674) tend to have lower activation energies and are therefore faster.

This principle explains the selectivity observed in the chlorination of [alkanes](@entry_id:185193) [@problem_id:1475535]. Hydrogen abstraction from ethane ($\Delta H^\circ = -8 \, \text{kJ/mol}$) is faster than from methane ($\Delta H^\circ = +8 \, \text{kJ/mol}$). Abstraction of a secondary hydrogen from propane ($\Delta H^\circ = -18 \, \text{kJ/mol}$) is even faster. The increasing exothermicity is due to the formation of progressively more stable alkyl radicals (primary in ethane, secondary in propane). The BEP relationship quantifies this trend, allowing for the prediction of rate constants for one reaction based on data from others in the same family.

#### Regioselectivity and Intermediate Stability

When a radical can react at multiple sites on a molecule, the reaction often exhibits high **regioselectivity**. The guiding principle is that the reaction will preferentially proceed through the pathway that forms the most stable radical intermediate. The stability of carbon-centered radicals follows the order: tertiary $>$ secondary $>$ primary $>$ methyl.

This is clearly demonstrated in the free-radical addition of HBr to alkenes in the presence of peroxides, which famously proceeds with **anti-Markovnikov** regioselectivity [@problem_id:1475534]. In the reaction with 1-butene, the first [propagation step](@entry_id:204825) is the addition of a bromine radical ($\text{Br}\cdot$) to the double bond. Two pathways are possible:

1.  Addition to the internal carbon (C2): $\text{Br}\cdot + \text{CH}_3\text{CH}_2\text{CH=CH}_2 \rightarrow \text{CH}_3\text{CH}_2\text{CH(Br)CH}_2\cdot$ (forms a primary radical)
2.  Addition to the terminal carbon (C1): $\text{Br}\cdot + \text{CH}_3\text{CH}_2\text{CH=CH}_2 \rightarrow \text{CH}_3\text{CH}_2\text{CH}\cdot\text{CH}_2\text{Br}$ (forms a secondary radical)

Because the secondary radical is more stable than the primary radical, the second pathway is strongly favored. The bromine atom adds to the less substituted carbon, leading to the more stable radical intermediate. This intermediate then abstracts a hydrogen atom from HBr in the next [propagation step](@entry_id:204825) to yield the final anti-Markovnikov product, 1-bromobutane. The regioselectivity of the overall reaction is therefore dictated by the kinetic preference in the first [propagation step](@entry_id:204825) to form the most stable radical.

#### Competing Propagation Pathways

A single reactive intermediate may have several different propagation pathways available to it. The dominant pathway is determined by the relative rates of these [competing reactions](@entry_id:192513), a phenomenon known as **[kinetic control](@entry_id:154879)**. The [branching ratio](@entry_id:157912) between the pathways depends on their respective activation energies and pre-exponential factors.

A notable example is the fate of the tert-butoxy radical ($t\text{BuO}\cdot$), which can undergo two competing unimolecular propagation reactions [@problem_id:1475565]:
1.  **Beta-scission**: $t\text{BuO}\cdot \rightarrow (\text{CH}_3)_2\text{CO} + \cdot\text{CH}_3$
2.  **Isomerization**: $t\text{BuO}\cdot \rightarrow \cdot\text{CH}_2\text{C}(\text{CH}_3)_2\text{OH}$

The beta-scission has a higher activation energy but also a higher [pre-exponential factor](@entry_id:145277) compared to the isomerization. At low temperatures, the reaction with the lower activation energy (isomerization) will dominate. At high temperatures, the reaction with the higher [pre-exponential factor](@entry_id:145277) (beta-scission) will become more significant. The temperature at which the two rates become equal can be calculated by setting their [rate constants](@entry_id:196199) equal, $k_{\beta}(T) = k_{\text{iso}}(T)$, and solving for $T$. This illustrates how temperature can be used as a tool to control the [product distribution](@entry_id:269160) in systems with competing propagation steps.

### Common and Specialized Propagation Reactions

Propagation steps can be classified into several common types:

- **Hydrogen Abstraction**: A radical removes a hydrogen atom from a stable molecule. This is a key step in alkane halogenation and many [combustion](@entry_id:146700) processes, such as in the Rice-Herzfeld mechanism for [acetaldehyde decomposition](@entry_id:184098), where a methyl radical abstracts a hydrogen from acetaldehyde [@problem_id:1475569]:
$$ \cdot\text{CH}_3 + \text{CH}_3\text{CHO} \rightarrow \text{CH}_4 + \cdot\text{CH}_3\text{CO} $$

- **Addition to a Pi System**: A radical adds across a double or [triple bond](@entry_id:202498). This is the fundamental chain-growth step in most radical polymerizations and in reactions like the anti-Markovnikov addition of HBr.

- **Beta-Scission**: The unimolecular fragmentation of a radical, where a bond beta to the [radical center](@entry_id:175001) breaks. This is the reverse of an addition reaction and is common in high-temperature [radical chemistry](@entry_id:168962), as seen with the tert-butoxy radical.

- **Chain-Branching Propagation**: A particularly important class of propagation steps is **[chain branching](@entry_id:178490)**, where a single radical reacts to produce *more than one* new radical. These steps are responsible for the exponential acceleration of [reaction rates](@entry_id:142655) that can lead to [thermal runaway](@entry_id:144742) and explosions. The combustion of hydrogen and oxygen provides the archetypal example [@problem_id:1475554]:
$$ \text{H}\cdot + \text{O}_2 \rightarrow \text{OH}\cdot + \text{O}\cdot $$
In this crucial step, one radical reactant ($\text{H}\cdot$) produces two radical products ($\text{OH}\cdot$ and $\text{O}\cdot$, an oxygen diradical). This net gain of one radical per event creates an avalanche of [chain carriers](@entry_id:197278), causing the reaction rate to increase exponentially. This is distinct from linear propagation, which merely sustains the radical population.

### The Role of Propagation in Overall Reaction Kinetics

The rates of the individual propagation steps are essential components in deriving the overall rate law for a [chain reaction](@entry_id:137566). Because radical intermediates are so reactive, their concentrations are typically very low and do not change significantly after an initial induction period. This observation is the basis of the **[steady-state approximation](@entry_id:140455) (SSA)**, a powerful analytical tool. The SSA assumes that the net rate of change of the concentration of each reactive intermediate is zero.
$$ \frac{d[\text{Radical}]}{dt} = (\text{Rate of formation}) - (\text{Rate of consumption}) \approx 0 $$

Applying the SSA allows us to solve for the steady-state concentrations of the radicals in terms of the concentrations of stable species and the [rate constants](@entry_id:196199) of the [elementary steps](@entry_id:143394). For the classic H₂-Br₂ reaction mechanism, we can apply the SSA to the $\text{H}\cdot$ radical [@problem_id:1475590]. The $\text{H}\cdot$ radical is formed in one [propagation step](@entry_id:204825) and consumed in two others (one being an "inhibition" step, which is mechanistically still a [propagation step](@entry_id:204825)).
$$ \frac{d[\text{H}\cdot]}{dt} = k_{p1}[\text{Br}\cdot][\text{H}_2] - k_{p2}[\text{H}\cdot][\text{Br}_2] - k_{in}[\text{H}\cdot][\text{HBr}] = 0 $$
Solving for the concentration of $\text{H}\cdot$ gives:
$$ k_{p1}[\text{Br}\cdot][\text{H}_2] = (k_{p2}[\text{Br}_2] + k_{in}[\text{HBr}])[\text{H}\cdot] $$
This equation can be rearranged to express the ratio of the steady-state concentrations of the two [chain carriers](@entry_id:197278):
$$ \frac{[\text{H}\cdot]_{ss}}{[\text{Br}\cdot]_{ss}} = \frac{k_{p1}[\text{H}_2]}{k_{p2}[\text{Br}_2] + k_{in}[\text{HBr}]} $$
This result demonstrates how the [relative abundance](@entry_id:754219) of the [chain carriers](@entry_id:197278), and thus the overall behavior of the reaction, is determined by a competition between the various propagation steps consuming and producing them. The study of [chain propagation](@entry_id:182302) is therefore not just the study of individual steps, but of a dynamic system of [competing reactions](@entry_id:192513) that collectively determine the fate of the chemical system.