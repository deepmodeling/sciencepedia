## Introduction
Heterogeneous catalysis is a cornerstone of the modern chemical industry, enabling the efficient production of everything from fuels to pharmaceuticals. The performance of a catalyst hinges on the intricate sequence of events occurring at the gas-solid or liquid-solid interface. To design better catalysts and optimize reaction conditions, it is essential to move beyond a black-box understanding and delve into the fundamental mechanisms governing these surface reactions. The central challenge lies in deciphering the [elementary steps](@entry_id:143394) of adsorption, [surface diffusion](@entry_id:186850), and chemical transformation that dictate the overall reaction rate and selectivity.

This article addresses this challenge by providing a comprehensive exploration of the two [canonical models](@entry_id:198268) for bimolecular surface reactions: the Langmuir-Hinshelwood (LH) and Eley-Rideal (ER) mechanisms. By mastering these frameworks, you will gain the ability to construct quantitative kinetic models, interpret experimental data, and understand the [thermodynamic principles](@entry_id:142232) that drive catalytic processes. The following chapters are structured to build this expertise systematically:

- **Principles and Mechanisms** will lay the theoretical groundwork, starting with the foundational Langmuir isotherm for [surface adsorption](@entry_id:268937) and culminating in the derivation and kinetic analysis of the LH and ER [rate laws](@entry_id:276849).

- **Applications and Interdisciplinary Connections** will bridge theory and practice, demonstrating how these models are tested with advanced experimental techniques and applied in diverse fields from reactor engineering to [computational chemistry](@entry_id:143039) and prebiotic evolution.

- **Hands-On Practices** will offer a series of targeted problems designed to solidify your understanding of the core concepts, from [dimensional analysis](@entry_id:140259) of kinetic parameters to the derivation of complex rate expressions.

We begin our journey by establishing the principles of [surface adsorption](@entry_id:268937), the crucial first step in any heterogeneous [catalytic cycle](@entry_id:155825).

## Principles and Mechanisms

The overall rate of a heterogeneous catalytic reaction is a convolution of multiple elementary steps: transport of reactants to the surface, adsorption, [surface diffusion](@entry_id:186850), chemical transformation, and desorption and transport of products away from the surface. In many cases, the surface processes—adsorption and reaction—are rate-controlling. Understanding the kinetics of these surface processes is therefore paramount to designing and optimizing catalytic systems. This chapter delves into the principles of [surface adsorption](@entry_id:268937) and the two canonical mechanisms for bimolecular surface reactions: the Langmuir-Hinshelwood and Eley-Rideal mechanisms.

### The Foundation: Adsorption Equilibria

The interaction of gas-phase molecules with a catalytic surface begins with [adsorption](@entry_id:143659). The relationship between the gas-phase pressure and the [amount of substance](@entry_id:145418) adsorbed at a constant temperature is described by an [adsorption isotherm](@entry_id:160557). The simplest and most foundational model for this process is the Langmuir isotherm.

#### Kinetic Derivation of the Langmuir Isotherm

The Langmuir model is based on several key assumptions: (1) adsorption is limited to a single monolayer; (2) the surface is energetically uniform, consisting of a fixed number of identical [adsorption](@entry_id:143659) sites; (3) adsorbed molecules do not interact with each other (no lateral interactions); and (4) [adsorption](@entry_id:143659) is a reversible process.

Consider a single gas species $A$ adsorbing non-dissociatively onto a vacant surface site, denoted by $*$:

$A(\mathrm{g}) + * \rightleftharpoons A*$

Let $\theta_A$ be the **fractional [surface coverage](@entry_id:202248)**, which is the fraction of total sites occupied by $A$, and let $1 - \theta_A$ be the fraction of vacant sites. The rate of adsorption, $r_{\mathrm{ads}}$, is proportional to the [partial pressure](@entry_id:143994) of $A$, $P_A$, and the fraction of available vacant sites. The rate of desorption, $r_{\mathrm{des}}$, is proportional to the fraction of sites already occupied by $A$.

$r_{\mathrm{ads}} = k_{\mathrm{ads}} P_A (1 - \theta_A)$

$r_{\mathrm{des}} = k_{\mathrm{des}} \theta_A$

Here, $k_{\mathrm{ads}}$ and $k_{\mathrm{des}}$ are the [rate constants](@entry_id:196199) for [adsorption](@entry_id:143659) and desorption, respectively. At [dynamic equilibrium](@entry_id:136767), the rates of [adsorption](@entry_id:143659) and desorption are equal: $r_{\mathrm{ads}} = r_{\mathrm{des}}$.

$k_{\mathrm{ads}} P_A (1 - \theta_A) = k_{\mathrm{des}} \theta_A$

Solving this equation for $\theta_A$ yields the celebrated **Langmuir isotherm**:

$\theta_A = \frac{k_{\mathrm{ads}} P_A}{k_{\mathrm{des}} + k_{\mathrm{ads}} P_A} = \frac{K_A P_A}{1 + K_A P_A}$

where $K_A = k_{\mathrm{ads}}/k_{\mathrm{des}}$ is the **adsorption equilibrium constant**. This constant reflects the relative affinity of the adsorbate for the surface.

The behavior of the isotherm can be examined in two important limits [@problem_id:2669635].

1.  **Low-Pressure (or Weak Adsorption) Limit**: When $K_A P_A \ll 1$, the denominator approaches 1, and the isotherm simplifies to a [linear relationship](@entry_id:267880) known as **Henry's Law**:
    $\theta_A \approx K_A P_A$
    In this regime, the [surface coverage](@entry_id:202248) is directly proportional to the partial pressure, as the surface is sparsely populated and sites are abundantly available. The validity of this [linear approximation](@entry_id:146101) depends on the dimensionless product $K_A P_A$ being much less than unity, not simply on $P_A$ being "small" in some arbitrary unit system. A Taylor [series expansion](@entry_id:142878) of the Langmuir isotherm about $P_A=0$ reveals this behavior explicitly:
    $\theta_A = K_A P_A - (K_A P_A)^2 + \mathcal{O}(P_A^3)$
    The linear approximation is valid when the quadratic term is negligible compared to the linear term, which leads directly to the condition $K_A P_A \ll 1$.

2.  **High-Pressure (or Strong Adsorption) Limit**: When $K_A P_A \gg 1$, the denominator is dominated by the $K_A P_A$ term, and the isotherm approaches its saturation limit:
    $\theta_A \approx \frac{K_A P_A}{K_A P_A} = 1$
    In this regime, the surface is nearly fully covered by a monolayer of adsorbates, and the rate of adsorption becomes insensitive to further increases in pressure.

#### Competitive Adsorption

In most catalytic processes, more than one species is present in the gas phase and can compete for the same [adsorption](@entry_id:143659) sites. Consider a [binary mixture](@entry_id:174561) of gases $A$ and $B$, both adsorbing non-dissociatively on the same set of uniform sites [@problem_id:2669668].

$A(\mathrm{g}) + * \rightleftharpoons A*$
$B(\mathrm{g}) + * \rightleftharpoons B*$

Following the same kinetic derivation, the equilibrium relationships are:
$\theta_A = K_A P_A \theta_*$
$\theta_B = K_B P_B \theta_*$

where $\theta_*$ is the fraction of vacant sites. The crucial difference is the site balance equation, which now includes all species on the surface:
$\theta_A + \theta_B + \theta_* = 1$

Substituting the equilibrium expressions into the site balance allows us to solve for $\theta_*$:
$K_A P_A \theta_* + K_B P_B \theta_* + \theta_* = 1 \implies \theta_* = \frac{1}{1 + K_A P_A + K_B P_B}$

Substituting this back gives the **competitive Langmuir [isotherms](@entry_id:151893)**:

$\theta_A = \frac{K_A P_A}{1 + K_A P_A + K_B P_B}$

$\theta_B = \frac{K_B P_B}{1 + K_A P_A + K_B P_B}$

These equations show that the coverage of one species depends not only on its own [partial pressure](@entry_id:143994) but also on the [partial pressure](@entry_id:143994) and adsorption strength of the competing species. The term for each competitor in the denominator acts as an inhibition factor, reducing the coverage of the other species.

#### Beyond the Ideal Model: The Role of Lateral Interactions

The Langmuir model's assumption of non-interacting adsorbates is a significant simplification. In reality, adsorbed molecules can exert attractive or repulsive forces on their neighbors. These **lateral interactions** can significantly alter [adsorption](@entry_id:143659) behavior [@problem_id:2669676].

To account for weak lateral interactions on a uniform lattice, we can employ a mean-field approximation. If an adsorbed molecule has a coordination number $z$ (number of nearest-neighbor sites) and a pairwise interaction energy $w$ with its neighbors ($w>0$ for repulsion, $w0$ for attraction), the average interaction energy experienced by an adsorbate is $z w \theta$, where $\theta$ is the total coverage. This interaction energy modifies the effective [heat of adsorption](@entry_id:199302).

By equating the chemical potentials of the gas and the adsorbed layer under this mean-field approximation, one arrives at the **Fowler-Guggenheim isotherm** (also known as the Frumkin isotherm):

$\frac{\theta}{1-\theta} = K P \exp\left(-\frac{z w \theta}{k_B T}\right)$

where $K$ is the adsorption equilibrium constant in the limit of zero coverage, and $k_B$ is the Boltzmann constant. The exponential term captures the effect of lateral interactions. For repulsive interactions ($w>0$), the term $\exp(-\frac{z w \theta}{k_B T})$ is less than 1, making it harder to adsorb molecules as coverage increases. Conversely, for attractive interactions ($w0$), this term is greater than 1, leading to cooperative adsorption where the presence of adsorbates makes further adsorption more favorable. For weak interactions, where $|\frac{z w \theta}{k_B T}| \ll 1$, this isotherm can be linearized to $\frac{\theta}{1-\theta} \approx K P (1 - \frac{z w \theta}{k_B T})$.

### Canonical Mechanisms of Bimolecular Surface Reactions

For a [bimolecular reaction](@entry_id:142883) $A + B \to \text{Products}$, two primary mechanisms are typically considered, distinguished by the state of the reactants prior to the [rate-determining step](@entry_id:137729).

#### The Langmuir-Hinshelwood (LH) Mechanism

In the **Langmuir-Hinshelwood (LH) mechanism**, both reactants must first adsorb onto the catalyst surface. The reaction then occurs between the two adsorbed species, $A*$ and $B*$. The [elementary steps](@entry_id:143394) are:

1.  $A(\text{g}) + * \rightleftharpoons A*$ (fast, quasi-equilibrated adsorption)
2.  $B(\text{g}) + * \rightleftharpoons B*$ (fast, quasi-equilibrated adsorption)
3.  $A* + B* \to \text{Products}$ (slow, [rate-determining step](@entry_id:137729))

The rate of the overall reaction, $r$, is determined by the rate of the slow [surface reaction](@entry_id:183202) step. Assuming [mass-action kinetics](@entry_id:187487) for the surface species, the rate is proportional to the product of the fractional coverages of the adsorbed reactants:

$r_{LH} = k \theta_A \theta_B$

where $k$ is the intrinsic surface [reaction rate constant](@entry_id:156163). Since the preceding [adsorption](@entry_id:143659) steps are assumed to be in quasi-equilibrium, we can substitute the expressions for $\theta_A$ and $\theta_B$ from the competitive Langmuir model. This yields the general LH [rate law](@entry_id:141492) for a [bimolecular reaction](@entry_id:142883):

$r_{LH} = \frac{k K_A K_B P_A P_B}{(1 + K_A P_A + K_B P_B)^2}$

This equation reveals the complex, [non-linear dependence](@entry_id:265776) of the LH rate on reactant pressures, a direct consequence of the competition for finite surface sites.

#### The Eley-Rideal (ER) Mechanism

In the **Eley-Rideal (ER) mechanism**, only one of the reactants adsorbs onto the surface. The other reactant, in the gas phase, collides directly with the adsorbed species to form the product. For a reaction where $B$ adsorbs and $A$ reacts from the gas phase, the steps are:

1.  $B(\text{g}) + * \rightleftharpoons B*$ (fast, quasi-equilibrated [adsorption](@entry_id:143659))
2.  $A(\text{g}) + B* \to \text{Products}$ (slow, rate-determining step)

The rate of the reaction is proportional to the [partial pressure](@entry_id:143994) of the gaseous reactant ($A$) and the surface coverage of the adsorbed reactant ($B*$):

$r_{ER} = k_{ER} P_A \theta_B$

Here, the coverage of $B$, $\theta_B$, is not in competition with $A$, as $A$ does not adsorb. Therefore, we use the single-component Langmuir isotherm for $B$:

$\theta_B = \frac{K_B P_B}{1 + K_B P_B}$

Substituting this into the rate expression gives the general ER rate law:

$r_{ER} = \frac{k_{ER} K_B P_A P_B}{1 + K_B P_B}$

The distinct mathematical forms of the LH and ER [rate laws](@entry_id:276849) give rise to different kinetic signatures, which can be used to distinguish between the two mechanisms.

### Kinetic Analysis and Mechanistic Discrimination

Determining the operative mechanism is a central goal of kinetic studies. The differing dependencies of the LH and ER [rate laws](@entry_id:276849) on reactant pressures provide a powerful means of discrimination.

#### Apparent Reaction Orders as Mechanistic Probes

The **apparent [reaction order](@entry_id:142981)**, $n_i$, with respect to a species $i$ is defined as the [logarithmic derivative](@entry_id:169238) of the rate with respect to its [partial pressure](@entry_id:143994): $n_i \equiv (\partial \ln r / \partial \ln P_i)_{T, P_{j \ne i}}$. Analyzing these orders in various pressure regimes is highly informative.

For the **Langmuir-Hinshelwood** mechanism, the apparent orders are highly dependent on [surface coverage](@entry_id:202248) [@problem_id:2669654] [@problem_id:2669666].
*   **Low Coverage ($K_A P_A \ll 1, K_B P_B \ll 1$):** The denominator of the LH [rate law](@entry_id:141492) approaches 1. The rate simplifies to $r_{LH} \approx k K_A K_B P_A P_B$. The reaction is first-order in both $A$ and $B$ ($n_A = 1, n_B = 1$).
*   **High Coverage, A-dominated ($K_A P_A \gg 1 + K_B P_B$):** The surface is nearly saturated with $A$ ($\theta_A \approx 1$). The coverage of $B$ becomes $\theta_B \approx K_B P_B / K_A P_A$. The rate becomes $r_{LH} \approx k \cdot 1 \cdot (K_B P_B / K_A P_A)$. Here, the apparent orders are $n_A = -1$ and $n_B = 1$. The negative order in $A$ is a hallmark of the LH mechanism. It arises because an excess of $A$ acts as a poison, blocking sites required for the [adsorption](@entry_id:143659) of $B$, thereby reducing the rate.
*   **High Coverage, B-dominated ($K_B P_B \gg 1 + K_A P_A$):** By symmetry, the orders are $n_A = 1$ and $n_B = -1$.
*   **High Total Pressure:** If both $P_A$ and $P_B$ increase together, the rate eventually becomes independent of pressure (overall zero order), as the surface saturates and the individual coverages approach constant values determined by the competition, $\theta_A \to K_A P_A / (K_A P_A + K_B P_B)$ and $\theta_B \to K_B P_B / (K_A P_A + K_B P_B)$.

For the **Eley-Rideal** mechanism ($A(\text{g}) + B* \to \text{P}$), the analysis is different [@problem_id:2669666].
*   The rate is always directly proportional to $P_A$, the pressure of the gas-phase reactant. Thus, **$n_A = 1$ under all conditions**.
*   The order in $B$ depends on its coverage, $\theta_B$. At low $P_B$ ($K_B P_B \ll 1$), $\theta_B \approx K_B P_B$, so the rate is proportional to $P_B$ and $n_B = 1$. At high $P_B$ ($K_B P_B \gg 1$), the surface saturates with $B$ ($\theta_B \approx 1$), the rate becomes independent of $P_B$, and $n_B = 0$.

The most striking difference is that the simple ER mechanism never predicts a negative [reaction order](@entry_id:142981), whereas the LH mechanism can, due to [competitive adsorption](@entry_id:195910). Observing a negative order in a reactant is strong evidence for an LH pathway.

#### A Diagnostic Experiment: Rate Dependence under Saturation

A well-designed experiment can effectively distinguish the two mechanisms [@problem_id:2669661]. Consider an experiment where the initial reaction rate, $r_0$, is measured as a function of $P_A$ while holding $P_B$ at a fixed, high value such that the surface is saturated with $B^*$ (i.e., $K_B P_B \gg 1$).

*   For the **Eley-Rideal** mechanism ($A(\text{g}) + B^* \to \text{P}$), the rate is $r_{ER} = k_{ER} P_A \theta_B$. Since the surface is saturated with $B$, its coverage $\theta_B$ is approximately constant ($\theta_B \approx 1$). The [rate law](@entry_id:141492) simplifies to $r_{ER} \approx k_{ER} P_A$. Therefore, a plot of $r_0$ versus $P_A$ should yield a straight line.

*   For the **Langmuir-Hinshelwood** mechanism, the rate is $r_{LH} = k \theta_A \theta_B$. At high, fixed $P_B$, the rate expression becomes $r_{LH} = \frac{k K_A K_B P_A P_B}{(1 + K_A P_A + K_B P_B)^2}$. Since $P_A$ is the variable, the rate takes the form $r_0 = \frac{C_1 P_A}{(C_2 + C_3 P_A)^2}$. This function is not linear. As $P_A$ increases from zero, $A$ begins to compete with and displace the pre-adsorbed $B$, causing $\theta_B$ to decrease. The rate initially rises as $\theta_A$ increases but then curves over and may even pass through a maximum as the displacement of $B$ becomes severe.

Therefore, observing a linear dependence of rate on $P_A$ over a broad range is strong evidence for an ER mechanism, while a sublinear, curving response points towards an LH mechanism.

### Thermodynamic Perspectives on Surface Reactions

A complete understanding of a catalytic cycle requires not only kinetic models but also an appreciation of the underlying thermodynamics of [adsorption](@entry_id:143659) and activation.

#### Thermodynamics of Adsorption

The [adsorption](@entry_id:143659) [equilibrium constant](@entry_id:141040), $K_A$, is a thermodynamic quantity related to the standard Gibbs free energy of [adsorption](@entry_id:143659), $\Delta G^\circ_{\mathrm{ads}}$:
$\Delta G^\circ_{\mathrm{ads}} = -RT \ln K$
This can be further broken down into enthalpic and entropic contributions:
$\ln K = -\frac{\Delta H^\circ_{\mathrm{ads}}}{RT} + \frac{\Delta S^\circ_{\mathrm{ads}}}{R}$

This is the **van 't Hoff equation**. It provides a powerful method to extract the standard enthalpy ($\Delta H^\circ_{\mathrm{ads}}$) and entropy ($\Delta S^\circ_{\mathrm{ads}}$) of [adsorption](@entry_id:143659) from experimental data [@problem_id:2669611]. The procedure involves:
1.  Measuring [adsorption isotherms](@entry_id:148975) ($\theta_A$ vs. $P_A$) at several different temperatures, $T$.
2.  For each isotherm, linearizing the data to find the equilibrium constant. For the Langmuir model, plotting $\theta_A/(1-\theta_A)$ versus $P_A$ yields a straight line with slope $K_A(T)$.
3.  Constructing a **van 't Hoff plot** of $\ln K_A$ versus $1/T$. This plot should be linear if $\Delta H^\circ_{\mathrm{ads}}$ and $\Delta S^\circ_{\mathrm{ads}}$ are reasonably constant over the temperature range.
4.  The slope of the van 't Hoff plot is equal to $-\Delta H^\circ_{\mathrm{ads}}/R$, and the y-intercept is $\Delta S^\circ_{\mathrm{ads}}/R$.

This analysis provides fundamental thermodynamic parameters. For most spontaneous [chemisorption](@entry_id:149998) and physisorption, adsorption is exothermic, so $\Delta H^\circ_{\mathrm{ads}}$ is negative.

#### The Apparent Activation Energy

The temperature dependence of the overall reaction rate is often analyzed using an Arrhenius plot of $\ln r$ versus $1/T$. The slope of this plot gives the **apparent activation energy**, $E_{\text{app}}$. It is crucial to recognize that $E_{\text{app}}$ is generally *not* the same as the true activation energy, $E_a$, of the elementary [surface reaction](@entry_id:183202) step. Instead, it is a composite value that includes contributions from the temperature-dependent [adsorption](@entry_id:143659) equilibria of the reactants.

For the **Langmuir-Hinshelwood** mechanism, the full derivation yields [@problem_id:2669662]:
$E_{\text{app}} = E_a + \Delta H_A + \Delta H_B - 2 \frac{K_A P_A \Delta H_A + K_B P_B \Delta H_B}{1 + K_A P_A + K_B P_B}$
where $E_a$ is the true barrier for the $A*+B*$ reaction, and $\Delta H_A$ and $\Delta H_B$ are the enthalpies of adsorption.

For the **Eley-Rideal** mechanism ($A(\text{g}) + B* \to \text{P}$), the expression is [@problem_id:2669649]:
$E_{\text{app}} = E_{\text{ER}} + \frac{\Delta H_{\text{ads},B}}{1 + K_B P_B}$
where $E_{\text{ER}}$ is the true barrier for the gas-[surface reaction](@entry_id:183202) and $\Delta H_{\text{ads},B}$ is the [enthalpy of adsorption](@entry_id:171774) for B.

Let's analyze the ER expression in its limits. Since [adsorption](@entry_id:143659) is exothermic ($\Delta H_{\text{ads},B}  0$):
*   **Low Coverage ($K_B P_B \ll 1$):** $E_{\text{app}} \to E_{\text{ER}} + \Delta H_{\text{ads},B}$. The apparent activation energy is *lower* than the true barrier. This is because increasing the temperature has two opposing effects: it increases the intrinsic reaction rate (promoting the reaction), but it also decreases the [surface coverage](@entry_id:202248) of $B$ via Le Châtelier's principle (inhibiting the reaction). The net effect measured is a smaller temperature dependence, i.e., a lower $E_{\text{app}}$.
*   **High Coverage ($K_B P_B \gg 1$):** $E_{\text{app}} \to E_{\text{ER}}$. At saturation, the surface coverage $\theta_B$ is fixed at $\approx 1$ and is no longer sensitive to temperature. The temperature dependence of the rate is now governed solely by the intrinsic activation energy of the [surface reaction](@entry_id:183202).

This analysis underscores that $E_{\text{app}}$ is not a fundamental constant but a function of the experimental conditions (pressures and temperature range).

#### Entropy of Activation and the Pre-exponential Factor

A deeper insight into the difference between LH and ER mechanisms comes from Transition State Theory (TST). The rate constant is related to the Gibbs [free energy of activation](@entry_id:182945), $\Delta G^\ddagger$:

$k = \frac{k_B T}{h} \exp\left(-\frac{\Delta G^\ddagger}{RT}\right) = \frac{k_B T}{h} \exp\left(\frac{\Delta S^\ddagger}{R}\right) \exp\left(-\frac{\Delta H^\ddagger}{RT}\right)$

The term $\exp(\Delta S^\ddagger/R)$ is a major component of the Arrhenius pre-exponential factor. The **[entropy of activation](@entry_id:169746)**, $\Delta S^\ddagger$, reflects the change in order when moving from the reactants to the transition state.

For surface reactions, this is dominated by the loss of translational and [rotational degrees of freedom](@entry_id:141502) [@problem_id:2669660].
*   In the **LH mechanism**, the transition state is formed from two species ($A*$ and $B*$) that were independently mobile on the 2D surface. Forcing them into a single, constrained [activated complex](@entry_id:153105) ($[A-B]^\ddagger$) results in a significant loss of translational entropy. Consequently, $\Delta S_{\mathrm{LH}}^{\ddagger}$ is typically large and negative.
*   In the **ER mechanism**, the transition state is formed from a gas-phase species ($A$) colliding with an adsorbed species ($B*$). This involves the loss of the three [translational degrees of freedom](@entry_id:140257) of the gaseous molecule. This is also a significant entropic penalty, but it is generally *less severe* than constraining two already adsorbed species. Therefore, $\Delta S_{\mathrm{ER}}^{\ddagger}$ is also negative, but typically less so than $\Delta S_{\mathrm{LH}}^{\ddagger}$.

This entropic difference has profound kinetic consequences. Consider a hypothetical case where both mechanisms have the same [activation enthalpy](@entry_id:199775), $\Delta H^\ddagger$. The ratio of their [rate constants](@entry_id:196199) would be:

$\frac{k_{\mathrm{ER}}}{k_{\mathrm{LH}}} = \exp\left(\frac{\Delta S_{\mathrm{ER}}^{\ddagger} - \Delta S_{\mathrm{LH}}^{\ddagger}}{R}\right)$

Since $\Delta S_{\mathrm{ER}}^{\ddagger} > \Delta S_{\mathrm{LH}}^{\ddagger}$, the argument of the exponential is positive, and $k_{\mathrm{ER}} \gg k_{\mathrm{LH}}$. For a plausible difference, such as $\Delta S_{\mathrm{ER}}^{\ddagger} - \Delta S_{\mathrm{LH}}^{\ddagger} \approx 80 \ \mathrm{J\ mol^{-1}\ K^{-1}}$, the ER pathway could be favored by several orders of magnitude at moderate temperatures, solely due to entropic effects. Thus, the ER mechanism is often described as having a more "favorable" [pre-exponential factor](@entry_id:145277), making it a kinetically potent pathway even if its enthalpic barrier is not particularly low.