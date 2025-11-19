## Introduction
Chemical reactions transform matter, but the balanced equation tells only part of the story—the beginning and the end. It doesn't tell us how fast the transformation occurs or the precise molecular journey from reactants to products. This is the realm of reaction kinetics, the study of reaction rates and mechanisms. This article bridges that gap, moving from the 'what' of [stoichiometry](@entry_id:140916) to the 'how' and 'how fast' of kinetics. 

The first chapter, "Principles and Mechanisms", will lay the groundwork, defining [reaction rates](@entry_id:142655), [rate laws](@entry_id:276849), and the energetic landscape of reactions, including the crucial roles of activation energy and temperature. We will explore how complex reactions are sequences of [elementary steps](@entry_id:143394) and introduce advanced concepts like Hammond's Postulate and the Curtin-Hammett principle. The second chapter, "Applications and Interdisciplinary Connections", will demonstrate how these principles are powerful tools used to elucidate mechanisms in [organic chemistry](@entry_id:137733), model drug behavior in pharmacology, and even explain complex [pattern formation](@entry_id:139998) in biology. Finally, "Hands-On Practices" will provide opportunities to apply these concepts to solve practical problems. By understanding these principles, you will gain a deeper insight into controlling and predicting chemical transformations.

## Principles and Mechanisms

### Defining and Measuring Reaction Rates

The study of chemical kinetics begins with a fundamental question: how fast does a reaction proceed? The **reaction rate** is a quantitative measure of the change in the concentration of a chemical species over time. For a substance being consumed, such as a reactant, its concentration decreases, leading to a negative rate of change. For a substance being formed, such as a product, its concentration increases, yielding a positive rate of change. By convention, the rate of a reaction is always expressed as a positive value. Therefore, for a reactant $R$, the rate of its consumption is defined as $-\frac{d[R]}{dt}$, while for a product $P$, the rate of its formation is $\frac{d[P]}{dt}$.

However, the rates of change for different species in a reaction are often not equal due to [stoichiometry](@entry_id:140916). Consider a generic reaction:

$$aA + bB \rightarrow cC + dD$$

The rate at which reactant $A$ is consumed is not necessarily the same as the rate at which product $C$ is formed. The stoichiometric coefficients dictate their relationship. For every $a$ moles of $A$ that react, $c$ moles of $C$ are produced. To define a single, unambiguous rate for the entire reaction, denoted by the symbol $v$, we normalize the rates of change of each species by their respective stoichiometric coefficients:

$$v = -\frac{1}{a}\frac{d[A]}{dt} = -\frac{1}{b}\frac{d[B]}{dt} = +\frac{1}{c}\frac{d[C]}{dt} = +\frac{1}{d}\frac{d[D]}{dt}$$

This unified rate, $v$, has units of concentration per time (e.g., mol L⁻¹ s⁻¹) and provides a consistent measure of the reaction's progress, independent of the particular species being monitored.

In many practical settings, such as [industrial synthesis](@entry_id:267352) or biological pathways, multiple reactions occur simultaneously, forming a [reaction network](@entry_id:195028). In such cases, the overall observed rate of change for a given species is the net result of all reactions involving that species. Let's examine a scenario where a desired primary reaction, $4A + B \rightarrow 2C$, is accompanied by an unwanted [side reaction](@entry_id:271170), $A \rightarrow D$ [@problem_id:2193797]. If we define the rate of the primary reaction as $v_1$ and the rate of the [side reaction](@entry_id:271170) as $v_2$, we can write the overall rate of change for species $A$ and $C$ by summing their contributions from each reaction. The [stoichiometric coefficient](@entry_id:204082) for a reactant is negative, and for a product, it is positive.

For reactant $A$: it is consumed in both reactions. In the first reaction, its [stoichiometric coefficient](@entry_id:204082) is $-4$, and in the second, it is $-1$. Thus, the total rate of change of $[A]$ is:
$$\frac{d[A]}{dt} = (-4)v_1 + (-1)v_2 = -4v_1 - v_2$$

For product $C$: it is formed only in the first reaction, where its [stoichiometric coefficient](@entry_id:204082) is $+2$. It does not participate in the second reaction. Thus:
$$\frac{d[C]}{dt} = (+2)v_1 + (0)v_2 = 2v_1$$

If an analytical chemist can measure the overall rate of consumption of $A$, $R_A = -\frac{d[A]}{dt}$, and the overall rate of formation of $C$, $R_C = \frac{d[C]}{dt}$, we can establish a system of equations:
$$R_A = 4v_1 + v_2$$
$$R_C = 2v_1$$

This system allows us to dissect the network. From the second equation, we can express the rate of the primary reaction in terms of the observable rate of product formation: $v_1 = R_C / 2$. Substituting this into the first equation enables us to isolate the rate of the unwanted [side reaction](@entry_id:271170):
$$R_A = 4\left(\frac{R_C}{2}\right) + v_2 = 2R_C + v_2$$
$$v_2 = R_A - 2R_C$$

This powerful result demonstrates how, by carefully accounting for stoichiometry, we can determine the rates of individual, unobserved reaction steps from macroscopic measurements of concentration changes. This principle is fundamental to the analysis of complex chemical and biochemical systems.

### The Rate Law: Concentration's Influence

While [stoichiometry](@entry_id:140916) describes the quantitative relationship between reacting species, it does not, in general, predict how the reaction rate depends on their concentrations. This relationship is captured by the **rate law** (or [rate equation](@entry_id:203049)), an experimentally determined mathematical expression. For a general reaction, the rate law often takes the form of a power law:

$$\text{Rate} = k[A]^m[B]^n \dots$$

Here, $k$ is the **rate constant**, a proportionality constant that is specific to a particular reaction at a given temperature. The exponents $m$ and $n$ are the **reaction orders** with respect to reactants $A$ and $B$, respectively. It is crucial to understand that these orders are not necessarily equal to the stoichiometric coefficients ($a$ and $b$) and must be determined through experiment. They can be positive, negative, or zero, and need not be integers. The sum of all the individual orders ($m+n+\dots$) is the **overall [reaction order](@entry_id:142981)**.

A common experimental technique for determining a rate law is the **[method of initial rates](@entry_id:145088)**. This method involves running a series of experiments from the same starting temperature but with different initial concentrations of reactants. By measuring the initial rate of the reaction (the instantaneous rate at time $t=0$) for each experiment, one can systematically deduce the order of each reactant.

Let's consider the synthesis of a hypothetical drug, "Catalysine," from precursors $P$ and $Q$, accelerated by a catalyst $C$ [@problem_id:2193814]. The general form of the [rate law](@entry_id:141492) is assumed to be $\text{Rate} = k[P]^m[Q]^n[C]^p$. We can determine the orders $m$, $n$, and $p$ by comparing pairs of experiments:

| Experiment | Initial $[P]$ (mol/L) | Initial $[Q]$ (mol/L) | Initial $[C]$ (mol/L) | Initial Rate (mol L⁻¹ s⁻¹) |
| :---: | :---: | :---: | :---: | :---: |
| 1 | 0.10 | 0.20 | 0.05 | $1.50 \times 10^{-4}$ |
| 2 | 0.20 | 0.20 | 0.05 | $6.00 \times 10^{-4}$ |
| 3 | 0.10 | 0.40 | 0.05 | $1.50 \times 10^{-4}$ |
| 4 | 0.10 | 0.20 | 0.10 | $3.00 \times 10^{-4}$ |

1.  **To find the order in P (m):** Compare Experiments 1 and 2, where $[Q]$ and $[C]$ are held constant. Doubling $[P]$ from $0.10$ M to $0.20$ M causes the rate to increase by a factor of ($6.00 \times 10^{-4}) / (1.50 \times 10^{-4}) = 4$. We can write the ratio of the rates as:
    $$\frac{\text{Rate}_2}{\text{Rate}_1} = \frac{k(0.20)^m(0.20)^n(0.05)^p}{k(0.10)^m(0.20)^n(0.05)^p} = \left(\frac{0.20}{0.10}\right)^m = 2^m$$
    Since $2^m = 4$, we find that $m=2$. The reaction is second-order with respect to $P$.

2.  **To find the order in Q (n):** Compare Experiments 1 and 3, where $[P]$ and $[C]$ are constant. Doubling $[Q]$ from $0.20$ M to $0.40$ M has no effect on the rate, which remains $1.50 \times 10^{-4}$ mol L⁻¹ s⁻¹.
    $$\frac{\text{Rate}_3}{\text{Rate}_1} = \left(\frac{0.40}{0.20}\right)^n = 2^n$$
    Since $2^n = 1$, we find that $n=0$. The reaction is zero-order with respect to $Q$. This means the concentration of $Q$ does not affect the reaction rate under these conditions, even though it is a reactant in the overall [stoichiometry](@entry_id:140916).

3.  **To find the order in C (p):** Compare Experiments 1 and 4, where $[P]$ and $[Q]$ are constant. Doubling $[C]$ from $0.05$ M to $0.10$ M causes the rate to double.
    $$\frac{\text{Rate}_4}{\text{Rate}_1} = \left(\frac{0.10}{0.05}\right)^p = 2^p$$
    Since $2^p = 2$, we find that $p=1$. The reaction is first-order with respect to the catalyst $C$.

Combining these results, the experimentally determined [rate law](@entry_id:141492) is:
$$\text{Rate} = k[P]^2 [Q]^0 [C]^1 = k[P]^2 [C]$$
This example underscores the empirical nature of [rate laws](@entry_id:276849) and highlights that the order of a reaction cannot be simply inferred from the [balanced chemical equation](@entry_id:141254).

### Reaction Mechanisms and Elementary Steps

The discrepancy between stoichiometric coefficients and reaction orders arises because most chemical reactions do not occur in a single event. Instead, they proceed through a sequence of one or more fundamental steps called **[elementary reactions](@entry_id:177550)**. This sequence constitutes the **[reaction mechanism](@entry_id:140113)**. Each [elementary reaction](@entry_id:151046) represents a single molecular event, such as a collision between two molecules, the decomposition of a single molecule, or a reaction with a surface.

The number of reactant species that collide and participate in the transition state of an [elementary reaction](@entry_id:151046) is called its **[molecularity](@entry_id:136888)**.
- A **unimolecular** step involves a single molecule (e.g., isomerization, decomposition).
- A **bimolecular** step involves the collision of two species.
- A **termolecular** step, which is rare, involves the simultaneous collision of three species.

Molecularity is a theoretical concept that applies only to individual [elementary steps](@entry_id:143394). This is where it profoundly differs from the reaction order, which is an empirical quantity describing the overall reaction. The critical connection is this: **for an elementary step, and only for an elementary step, the [reaction order](@entry_id:142981) with respect to each reactant is equal to its [stoichiometric coefficient](@entry_id:204082) in that step.**

Consider a critical elementary step in the catalytic destruction of atmospheric ozone by chlorine [free radicals](@entry_id:164363) [@problem_id:2193778]:
$$O_3(g) + Cl(g) \rightarrow ClO(g) + O_2(g)$$

Since this is stated to be an [elementary reaction](@entry_id:151046), we can deduce its kinetics directly from its [stoichiometry](@entry_id:140916).
- **Molecularity:** The reaction involves one ozone molecule and one chlorine atom colliding. Therefore, it has a [molecularity](@entry_id:136888) of two and is classified as **bimolecular**.
- **Rate Law:** Because it is an elementary step, the rate law can be written directly from the reactant [stoichiometry](@entry_id:140916). The [stoichiometric coefficient](@entry_id:204082) for both $O_3$ and $Cl$ is 1. Thus, the [rate law](@entry_id:141492) is:
  $$\text{Rate} = k[O_3]^1 [Cl]^1 = k[O_3][Cl]$$
The overall order of this [elementary step](@entry_id:182121) is $1 + 1 = 2$. This direct correspondence provides a powerful link between the microscopic picture of [molecular collisions](@entry_id:137334) and the macroscopic [rate law](@entry_id:141492). The overall [rate law](@entry_id:141492) for a multi-step reaction is determined by the kinetics of these individual [elementary steps](@entry_id:143394), often being governed by the slowest step in the sequence.

### The Energetics of Reaction: From Collision to Transition State

For a reaction to occur, reactant molecules must not only meet but must do so with sufficient energy and in the correct orientation. This forms the basis of **[collision theory](@entry_id:138920)**. The minimum kinetic energy that colliding molecules must possess for a reaction to occur is called the **activation energy**, denoted as $E_a$.

We can visualize the energy changes during a reaction using a **[reaction coordinate diagram](@entry_id:171078)**. This diagram plots the potential energy of the system against the reaction coordinate, an abstract measure of the progress from reactants to products.

- **Reactants (R)** and **Products (P)** are located at the energy minima at the beginning and end of the coordinate.
- The **[enthalpy of reaction](@entry_id:137819) ($\Delta H$)** is the difference in energy between products and reactants: $\Delta H = E_P - E_R$. If $\Delta H \lt 0$, the reaction is **exothermic** (releases heat). If $\Delta H \gt 0$, it is **endothermic** (absorbs heat).
- The **transition state (TS or ‡)** is the point of maximum potential energy along the [reaction path](@entry_id:163735). It represents an unstable, fleeting arrangement of atoms as bonds are being broken and formed.
- The **activation energy ($E_a$)** is the energy barrier that must be overcome, defined as the difference in energy between the transition state and the reactants: $E_a = E_{TS} - E_R$.

The magnitude of the activation energy is directly related to the reaction rate. A low activation energy corresponds to a fast reaction, as a larger fraction of [molecular collisions](@entry_id:137334) will have sufficient energy to surmount the barrier. Conversely, a high activation energy implies a slow reaction [@problem_id:2193745]. For example, a reaction observed to be very fast at room temperature and to release significant heat can be described as having a relatively small activation energy ($E_a$) and a negative enthalpy change ($\Delta H$).

For multi-step reactions, the [reaction coordinate diagram](@entry_id:171078) will feature multiple peaks (transition states) separated by valleys (intermediates). An **intermediate** is a species that is formed in one elementary step and consumed in a subsequent one. It is a true chemical species, albeit often unstable and short-lived, corresponding to a local minimum on the energy profile. The elementary step with the highest-energy transition state (i.e., the largest activation energy) is the slowest step in the mechanism and is known as the **[rate-determining step](@entry_id:137729) (RDS)** or [rate-limiting step](@entry_id:150742). The overall rate of the multi-step reaction is governed by the rate of the RDS.

Consider a two-step [solvolysis reaction](@entry_id:192589) where a substrate R-L first slowly dissociates to a [carbocation intermediate](@entry_id:204002) R⁺, which is then rapidly trapped by a solvent SOH [@problem_id:2193784].
$$ \text{Step 1: R-L} \rightleftharpoons \text{R}^{+} + \text{L}^{-} \quad (\text{slow}) $$
$$ \text{Step 2: R}^{+} + \text{SOH} \rightarrow \text{R-OS} + \text{H}^{+} \quad (\text{fast}) $$
If the overall reaction is known to be endothermic (products are higher in energy than reactants), and the first step is slow, the [reaction coordinate diagram](@entry_id:171078) would show two peaks. The first transition state, leading to the high-energy [carbocation intermediate](@entry_id:204002), would be higher than the second, reflecting that Step 1 is the slow, rate-determining step. The final products would be shown at a higher energy level than the initial reactants, indicating an overall [endothermic process](@entry_id:141358).

### The Role of Temperature: The Arrhenius Equation

Reaction rates are exquisitely sensitive to temperature. Increasing the temperature increases the average kinetic energy of molecules, leading to more frequent and more energetic collisions. This relationship is quantified by the **Arrhenius equation**:

$$k = A \exp\left(-\frac{E_a}{RT}\right)$$

This equation relates the rate constant $k$ to the absolute temperature $T$. Here, $R$ is the [universal gas constant](@entry_id:136843), $E_a$ is the activation energy, and $A$ is the **[pre-exponential factor](@entry_id:145277)** or [frequency factor](@entry_id:183294).

The Arrhenius equation beautifully dissects the requirements for a reaction:
- The **exponential term**, $\exp(-E_a/RT)$, represents the fraction of molecules that possess at least the minimum energy required for reaction, $E_a$. As $T$ increases, this fraction grows exponentially, causing a dramatic increase in the rate constant.
- The **[pre-exponential factor](@entry_id:145277) ($A$)** represents the rate of collisions with the correct geometry, essentially the maximum possible rate if every collision had sufficient energy.

Collision theory provides a more detailed physical interpretation of the [pre-exponential factor](@entry_id:145277), expressing it as $A = pZ$, where $Z$ is the collision frequency factor (the total number of collisions per unit time and concentration) and $p$ is the **[steric factor](@entry_id:140715)**. The [steric factor](@entry_id:140715) is a value between 0 and 1 that represents the fraction of collisions having the correct spatial orientation for the reaction to occur. For a simple collision of two spherical atoms, $p$ might be close to 1. For a complex enzyme-substrate interaction, where a specific active site must be approached in a precise manner, $p$ can be very small. For a given reaction, if $k$, $E_a$, $T$, and $Z$ are known, the [steric factor](@entry_id:140715) can be calculated, providing insight into the geometric constraints of the reaction [@problem_id:2193758]. For example, in the hydrolysis of a polymer, a calculated [steric factor](@entry_id:140715) of $1.21 \times 10^{-3}$ implies that only about 1 in 825 collisions has the appropriate orientation to lead to bond cleavage.

### Catalysis: Providing an Alternative Reaction Pathway

A **catalyst** is a substance that increases the rate of a chemical reaction without itself being consumed in the process. It achieves this not by altering the thermodynamics of the reaction (the energies of reactants and products, and thus $\Delta H$, remain unchanged) but by altering the kinetics. A catalyst provides an alternative [reaction mechanism](@entry_id:140113)—a different pathway from reactants to products—that has a lower overall activation energy, $E_{a, \text{cat}}$.

According to the Arrhenius equation, lowering $E_a$ has an exponential effect on the rate constant. Even a modest reduction in the activation energy can lead to a dramatic increase in reaction rate. A catalyst lowers the highest energy barrier on the path to products, effectively creating a "tunnel" through the energy mountain.

The effect of a catalyst is itself temperature-dependent. Consider a reaction whose rate is increased by a factor of 4000 by a catalyst at $310.0 \text{ K}$ [@problem_id:2193792]. Assuming the pre-exponential factor $A$ is the same for the catalyzed and uncatalyzed reactions, we can use the Arrhenius equation to find the reduction in activation energy, $\Delta E_a = E_{a, \text{uncat}} - E_{a, \text{cat}}$.
$$\frac{k_{\text{cat}}}{k_{\text{uncat}}} = 4000 = \frac{A \exp(-E_{a, \text{cat}}/RT)}{A \exp(-E_{a, \text{uncat}}/RT)} = \exp\left(\frac{E_{a, \text{uncat}} - E_{a, \text{cat}}}{RT_1}\right)$$
This allows us to solve for $\Delta E_a$. Once known, we can predict the rate enhancement at a different temperature, say $T_2 = 370.0 \text{ K}$:
$$\frac{k_{\text{cat}}}{k_{\text{uncat}}}(T_2) = \exp\left(\frac{\Delta E_a}{RT_2}\right) = \left[\exp\left(\frac{\Delta E_a}{RT_1}\right)\right]^{\frac{T_1}{T_2}} = (4000)^{\frac{310.0}{370.0}}$$
This calculation predicts a rate enhancement of approximately $1.04 \times 10^3$ at the higher temperature. This result reveals a general principle: while a catalyst is effective at all temperatures, the *relative* rate enhancement it provides is more pronounced at lower temperatures than at higher temperatures.

### Advanced Principles in Reaction Kinetics

Building upon these foundational concepts, several powerful principles allow for a deeper understanding and prediction of reaction outcomes.

#### Hammond's Postulate: Linking Transition State Structure and Energy

While we can draw a transition state as a single point on a [reaction coordinate diagram](@entry_id:171078), what is its actual geometric structure? **Hammond's Postulate** provides a powerful qualitative answer: **the structure of a transition state resembles the species (reactant, intermediate, or product) to which it is closest in energy**.

- For a highly **exothermic** reaction ($\Delta H \ll 0$), the reactants are much higher in energy than the products. The transition state, being at the peak of the energy barrier, is therefore closer in energy to the reactants than to the products. Consequently, the transition state will be **"early"** and **reactant-like**. Bond breaking and [bond formation](@entry_id:149227) have only just begun.

- For a highly **endothermic** reaction ($\Delta H \gg 0$), the transition state is closer in energy to the high-energy products. The transition state will be **"late"** and **product-like**. Bond breaking and [bond formation](@entry_id:149227) are nearly complete.

This principle is invaluable for rationalizing selectivity. For example, consider the hydrogen abstraction from an alkane R-H by a bromine radical, a fast and highly exothermic step [@problem_id:2193787]. According to Hammond's Postulate, the transition state for this reaction will be early and reactant-like. This means that at the transition state, the R-H bond will be only slightly stretched, and the H-Br bond will have barely begun to form. This has profound implications for selectivity, as the structure and stability of the forming alkyl radical R• have a relatively small influence on the transition state energy.

#### Kinetic versus Thermodynamic Control

When a single reactant can undergo competing irreversible reactions to form different products, the [product distribution](@entry_id:269160) is determined by the relative rates of formation. The product formed via the pathway with the lowest activation energy is called the **[kinetic product](@entry_id:188509)**, as it is formed the fastest.

$$ S \xrightarrow{k_A} A \quad (\text{lower } E_{a,A}) $$
$$ S \xrightarrow{k_B} B \quad (\text{higher } E_{a,B}) $$

At low temperatures, where there is not enough energy to overcome the higher barrier to B, or if the reactions are irreversible, the product mixture will be enriched in the [kinetic product](@entry_id:188509), A.

However, if the reactions are reversible and the system is allowed to reach equilibrium, the final [product distribution](@entry_id:269160) will be determined by the relative stabilities of the products themselves. The more stable product (the one with the lower Gibbs free energy) is called the **[thermodynamic product](@entry_id:203930)**. At high temperatures, even if the [kinetic product](@entry_id:188509) A is formed first, the system has enough energy for the reverse reaction ($A \rightarrow S$) to occur, allowing the system to eventually settle into an equilibrium dominated by the most stable species.

The balance between [kinetic and thermodynamic control](@entry_id:148847) is temperature-dependent. There exists a specific temperature at which the rates of formation of the two products are equal [@problem_id:2193802]. By setting the Arrhenius expressions for the two rate constants equal, $k_A = k_B$, we can solve for this [crossover temperature](@entry_id:181193):
$$A_A \exp\left(-\frac{E_{a,A}}{RT}\right) = A_B \exp\left(-\frac{E_{a,B}}{RT}\right)$$
$$\ln\left(\frac{A_A}{A_B}\right) = \frac{E_{a,A} - E_{a,B}}{RT}$$
$$T = \frac{E_{a,A} - E_{a,B}}{R \ln(A_A/A_B)}$$

Below this temperature, the pathway with the lower activation energy will be faster, favoring the [kinetic product](@entry_id:188509). Above this temperature, the pathway with the larger pre-exponential factor and higher activation energy can become dominant, shifting the [product distribution](@entry_id:269160). This principle allows chemists to select for a desired product by carefully choosing the reaction temperature.

#### The Curtin-Hammett Principle: Reactions of Equilibrating Conformers

Many molecules exist as a mixture of rapidly interconverting isomers, such as the chair conformers of a substituted cyclohexane. What happens when these different conformers react to form different products?
$$ P \xleftarrow{k_P} A_{ax} \rightleftharpoons A_{eq} \xrightarrow{k_Q} Q $$
One might intuitively assume that if one conformer (e.g., $A_{eq}$) is much more stable and thus more populated, the product derived from it (Q) will be the major product. This is often incorrect.

The **Curtin-Hammett principle** applies when the rate of interconversion between the conformers is much faster than the rate at which either conformer reacts. In this scenario, the ratio of products formed is determined *not* by the relative populations of the ground-state conformers, but by the difference in the Gibbs free energies of the transition states leading to each product.

The ratio of products is given by the ratio of their formation rates:
$$\frac{[P]}{[Q]} = \frac{k_P[A_{ax}]}{k_Q[A_{eq}]}$$
Since the conformers are in rapid equilibrium, their concentration ratio is given by the Boltzmann distribution, $[A_{ax}]/[A_{eq}] = \exp(-\Delta G^\circ_{\text{conf}}/RT)$, where $\Delta G^\circ_{\text{conf}} = G^\circ(A_{ax}) - G^\circ(A_{eq})$. The [rate constants](@entry_id:196199) are given by the Eyring equation, $k \propto \exp(-\Delta G^\ddagger/RT)$. Substituting these relationships, a remarkable cancellation occurs: the ground-state energy difference cancels out, leaving a simple expression [@problem_id:2193812]:

$$\frac{[P]}{[Q]} = \exp\left(-\frac{G^\circ(TS_P) - G^\circ(TS_Q)}{RT}\right)$$

This powerful result shows that the product ratio depends only on the relative heights of the two transition state energy barriers, measured from a common reference. It does not matter whether a product is formed from a minor, high-energy conformer or a major, low-energy one; all that matters is the absolute energy of the transition state on its [reaction pathway](@entry_id:268524). The system effectively acts as if the total pool of reactant molecules can choose the path of lowest resistance—the lowest energy transition state—regardless of which conformer that path originates from. Kinetics, once again, is a story of mountains, not valleys.