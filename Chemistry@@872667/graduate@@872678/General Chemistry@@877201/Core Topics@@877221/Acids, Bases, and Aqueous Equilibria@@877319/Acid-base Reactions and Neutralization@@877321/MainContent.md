## Introduction
Acid-base reactions are among the most fundamental and ubiquitous processes in chemistry, governing outcomes from [industrial synthesis](@entry_id:267352) to the very functions of life. While introductory studies provide a basic framework, a deeper, quantitative understanding is essential for advanced scientific inquiry and application. This article bridges that gap, moving from familiar concepts to the sophisticated models used by practicing chemists. It addresses the complexities of real-world systems where factors like solvent, temperature, and molecular structure profoundly influence acid-base behavior.

The following chapters are structured to build a comprehensive and rigorous understanding of the topic. In "Principles and Mechanisms," we will deconstruct the theoretical frameworks that define [acids and bases](@entry_id:147369), explore the thermodynamic and kinetic laws that govern their interactions, and introduce powerful analytical tools like [linear free-energy relationships](@entry_id:200208). Following this, "Applications and Interdisciplinary Connections" will illustrate how these core principles are applied across diverse fields, from [enzyme catalysis](@entry_id:146161) in molecular biology to surface chemistry in materials science. Finally, "Hands-On Practices" will provide opportunities to apply this knowledge through guided problem-solving, solidifying your grasp of both theoretical derivations and practical analysis.

## Principles and Mechanisms

The conceptual and quantitative understanding of [acid-base reactions](@entry_id:137934) represents a cornerstone of modern chemistry. Building upon the introductory concepts, this chapter delves into the fundamental principles and mechanisms that govern these ubiquitous processes. We will explore the theoretical frameworks used to define [acids and bases](@entry_id:147369), the [thermodynamic forces](@entry_id:161907) that dictate their equilibrium behavior, and the kinetic pathways that characterize their reactions. Our exploration will move from foundational definitions to advanced models that describe the influence of structure, solvent, and temperature, equipping the reader with a rigorous and versatile toolkit for analyzing acid-base phenomena across diverse chemical systems.

### Evolving Definitions of Acidity and Basicity

The definition of an acid and a base has evolved over time, with each successive theory expanding the scope of phenomena encompassed. Understanding the domain and limitations of each framework—Arrhenius, Brønsted–Lowry, and Lewis—is critical for correctly interpreting chemical behavior.

The **Arrhenius theory**, the earliest of the formal definitions, is fundamentally solvent-centric, specifically tailored to [aqueous solutions](@entry_id:145101). An **Arrhenius acid** is a substance that increases the concentration of protons (hydronium ions, $\text{H}_3\text{O}^+$) when dissolved in water. A classic example is hydrochloric acid, $\text{HCl}$, which ionizes to produce $\text{H}_3\text{O}^+$ and $\text{Cl}^-$. An **Arrhenius base** is a substance that increases the concentration of hydroxide ions, $\text{OH}^-$, in water. While substances containing hydroxide, like $\text{NaOH}$, are clear examples, the definition also includes species like ammonia, $\text{NH}_3$, which produces $\text{OH}^-$ through a reaction with water: $\text{NH}_3 + \text{H}_2\text{O} \rightleftharpoons \text{NH}_4^+ + \text{OH}^-$. The major limitation of this theory is its restriction to aqueous media and its inability to classify as acids substances that do not intrinsically contain hydrogen, such as $\text{BF}_3$ or $\text{AlCl}_3$, even though they produce acidic solutions [@problem_id:2918417].

The **Brønsted–Lowry theory** provides a more general, proton-centric definition. A **Brønsted–Lowry acid** is a proton ($\text{H}^+$) donor, and a **Brønsted–Lowry base** is a [proton acceptor](@entry_id:150141). This framework is independent of the solvent and elegantly describes reactions like the gas-phase formation of ammonium chloride from $\text{HCl}$ and $\text{NH}_3$. In this view, every [acid-base reaction](@entry_id:149679) involves two **[conjugate acid-base pairs](@entry_id:147155)**. For example, in the reaction of $\text{HCl}$ with $\text{H}_2\text{O}$, $\text{HCl}$ (acid) donates a proton to form its [conjugate base](@entry_id:144252), $\text{Cl}^-$, while $\text{H}_2\text{O}$ (base) accepts the proton to form its conjugate acid, $\text{H}_3\text{O}^+$. Species that can act as either a Brønsted–Lowry acid or base, such as water, are termed **amphoteric**. While broader than the Arrhenius theory, the Brønsted–Lowry definition is still confined to reactions involving proton transfer and fails to classify aprotic substances like $\text{BF}_3$ as acids [@problem_id:2918417].

The most general and encompassing of the classical theories is the **Lewis theory**, which is electron-centric. A **Lewis acid** is an electron-pair acceptor, and a **Lewis base** is an electron-pair donor. The reaction between a Lewis acid and base results in the formation of a [coordinate covalent bond](@entry_id:141411), often called a Lewis adduct. This definition includes all Brønsted–Lowry reactions; the proton is an electron-pair acceptor, and the Brønsted–Lowry base is the electron-pair donor. Crucially, the Lewis theory also classifies reactions with no protons, such as the formation of the adduct $\text{F}_3\text{B-NH}_3$ from the Lewis acid $\text{BF}_3$ (which has an empty p-orbital on boron) and the Lewis base $\text{NH}_3$ (which has a lone pair on nitrogen). Other important examples of Lewis acids include metal cations and molecules with incomplete octets like $\text{AlCl}_3$ [@problem_id:2918417].

At the graduate level, it is instructive to consider the relationship between Brønsted–Lowry and Lewis theories from an electronic structure perspective. A [proton transfer](@entry_id:143444) can be seen as a specific case of Lewis [adduct formation](@entry_id:746281) where the electron pair from the Lewis base is donated to the vacant $1s$ orbital of a proton. The two descriptions are most clearly equivalent when a base with a localized lone pair (its Highest Occupied Molecular Orbital, or **HOMO**) interacts with an unscreened proton, forming a localized two-center, two-electron ($2c-2e$) bond. In such cases, computational methods like Natural Bond Orbital (NBO) analysis show a single, dominant orbital interaction, and the Quantum Theory of Atoms in Molecules (QTAIM) reveals a single [bond critical point](@entry_id:175677) between the base and the proton [@problem_id:2918411].

However, this equivalence breaks down in more complex scenarios. In symmetric systems like the Zundel cation, $\text{H}_5\text{O}_2^+$, the proton is equally shared between two water molecules. This is better described as a delocalized three-center, four-electron ($3c-4e$) bond, and neither a simple "proton transfer" nor a single "Lewis adduct" is an adequate description. The descriptions also diverge in processes like **Proton-Coupled Electron Transfer (PCET)**, where the movement of a proton is mechanistically coupled to the transfer of an electron between different sites. Such reactions involve open-shell intermediates and changes in oxidation states, phenomena that fall outside the scope of a simple closed-shell Lewis adduct model [@problem_id:2918411].

### Thermodynamics of Acid-Base Equilibria

The strength of an acid in a given solvent is quantified by its [acid dissociation constant](@entry_id:138231), $K_a$, for the equilibrium $\text{HA} \rightleftharpoons \text{H}^+ + \text{A}^-$. For convenience, this is typically expressed on a logarithmic scale as the **$pK_a$**, defined as $pK_a = -\log_{10} K_a$. The thermodynamic foundation for this value is the standard Gibbs free energy of deprotonation, $\Delta G^\circ_{\text{deprot}}$, to which it is related by the equation:

$$ \Delta G^\circ_{\text{deprot}} = -RT \ln K_a = (RT \ln 10) pK_a $$

A stronger acid, which dissociates more readily, has a larger $K_a$, a more negative $\Delta G^\circ_{\text{deprot}}$, and a smaller $pK_a$. These thermodynamic quantities are not fixed but depend on temperature, solvent, and other solution conditions.

#### Temperature Dependence of Acidity

The effect of temperature on an equilibrium constant is described by the **van't Hoff equation**. We can derive its impact on $pK_a$ starting from fundamental principles. By differentiating the relationship $\ln K_a = -(\ln 10) pK_a$ with respect to temperature $T$ at constant pressure, we obtain:

$$ \left( \frac{\partial \ln K_a}{\partial T} \right)_p = -(\ln 10) \left( \frac{\partial pK_a}{\partial T} \right)_p $$

The van't Hoff equation states that $\left( \frac{\partial \ln K_a}{\partial T} \right)_p = \frac{\Delta H^\circ}{RT^2}$, where $\Delta H^\circ$ is the standard enthalpy change of the reaction. Equating these expressions and solving for the derivative of $pK_a$ yields:

$$ \left( \frac{\partial pK_a}{\partial T} \right)_p = -\frac{\Delta H^\circ_{\text{diss}}}{(\ln 10) RT^2} $$

This important result shows that the sign of the temperature dependence of $pK_a$ is determined by the sign of the enthalpy of [dissociation](@entry_id:144265), $\Delta H^\circ_{\text{diss}}$. For an endothermic dissociation ($\Delta H^\circ_{\text{diss}} > 0$), increasing the temperature will decrease the $pK_a$ (increase acidity), as predicted by Le Châtelier's principle. For an exothermic dissociation ($\Delta H^\circ_{\text{diss}}  0$), the opposite is true.

If we assume $\Delta H^\circ_{\text{diss}}$ is approximately constant over a moderate temperature range (which is equivalent to assuming the change in heat capacity, $\Delta C_p^\circ$, is negligible), we can integrate this equation to predict the $pK_a$ at a new temperature $T_2$ from a known value at $T_1$ [@problem_id:2918388]:

$$ pK_a(T_2) = pK_a(T_1) + \frac{\Delta H^\circ_{\text{diss}}}{(\ln 10) R} \left( \frac{1}{T_2} - \frac{1}{T_1} \right) $$

For example, for a hypothetical acid with a $pK_a$ of $4.756$ at $298.15\,\text{K}$ and a nearly constant $\Delta H^\circ_{\text{diss}}$ of $+1.30 \times 10^3\,\text{J mol}^{-1}$, its $pK_a$ at $350\,\text{K}$ can be estimated to be approximately $4.722$. The small, positive enthalpy of dissociation leads to a slight increase in [acidity](@entry_id:137608) upon heating [@problem_id:2918388].

#### Solvent Effects and Acidity Inversion

The solvent plays a paramount role in determining [acid strength](@entry_id:142004). The [acidity](@entry_id:137608) measured in the gas phase, known as **intrinsic acidity**, can be drastically different from that observed in solution. The difference is due to the **differential [solvation](@entry_id:146105)** of the neutral acid (HA) and its constituent ions (H$^+$ and A$^-$).

We can quantitatively analyze these effects using a **thermodynamic cycle** [@problem_id:2918415]. The standard Gibbs free energy of deprotonation in solution ($\Delta G^\circ_{\text{aq,deprot}}$) is related to the gas-phase deprotonation energy ($\Delta G^\circ_{\text{gas,deprot}}$) and the standard free energies of [solvation](@entry_id:146105) ($\Delta G^\circ_{\text{solv}}$) for each species:

$$ \Delta G^\circ_{\text{aq,deprot}} = \Delta G^\circ_{\text{gas,deprot}} + \Delta G^\circ_{\text{solv}}(\text{A}^-) + \Delta G^\circ_{\text{solv}}(\text{H}^+) - \Delta G^\circ_{\text{solv}}(\text{HA}) $$

This relationship reveals that a solvent will lower the $pK_a$ (increase [acidity](@entry_id:137608)) if it solvates the products ($\text{H}^+$ and $\text{A}^-$) more favorably than it solvates the reactant ($\text{HA}$). Since ions are generally much more strongly solvated than neutral molecules, nearly all acids are stronger in polar solvents than in the gas phase.

More subtly, differential solvation can even invert the relative acidity of two different acids. Consider two isomers, $\text{HA}_\text{I}$ and $\text{HA}_\text{II}$. It is possible for $\text{HA}_\text{I}$ to be the stronger acid in the gas phase ($\Delta G^\circ_{\text{gas,deprot}}(\text{HA}_\text{I})  \Delta G^\circ_{\text{gas,deprot}}(\text{HA}_\text{II})$), while $\text{HA}_\text{II}$ becomes the stronger acid in water. This inversion occurs if the solvent provides a sufficiently large differential stabilization for the [conjugate base](@entry_id:144252) $\text{A}_\text{II}^-$, for instance if its charge is more exposed to the solvent. The change in relative [acidity](@entry_id:137608) ($\Delta pK_a$) is driven by the sum of the differences in intrinsic [acidity](@entry_id:137608) and the differential solvation energies of the conjugate bases and neutral acids. A dominant differential solvation of one of the anions is often the primary cause for such acidity inversions [@problem_id:2918415].

The ability of a solvent to stabilize ions can be dissected into two main contributions [@problem_id:2918371]:
1.  **Non-specific Electrostatic Solvation**: Governed by the solvent's bulk dielectric constant, $\varepsilon$. High-dielectric solvents like DMSO ($\varepsilon = 47$) are effective at separating and stabilizing ions, lowering the free energy cost of deprotonation.
2.  **Specific Donor-Acceptor Interactions**: These are short-range, Lewis acid-base type interactions. Cation solvation (e.g., of H$^+$) is enhanced by solvents with high Lewis basicity, quantified by the **Gutmann Donor Number (DN)**. Anion [solvation](@entry_id:146105) (e.g., of A$^-$) is enhanced by solvents with high Lewis [acidity](@entry_id:137608), quantified by the **Gutmann Acceptor Number (AN)**. For example, a solvent like hexafluoro-2-propanol (HFIP) has a modest dielectric constant and low DN, but its exceptionally high AN makes it a powerful hydrogen-bond donor, leading to immense stabilization of anionic conjugate bases like carboxylates. This specific anion stabilization can be so dominant that it makes an acid stronger in HFIP than in DMSO, despite DMSO's much higher [dielectric constant](@entry_id:146714) and donor number [@problem_id:2918371].

#### Effects of Non-Ideality: Ionic Strength

In real ionic solutions, solute-solute interactions cause deviations from ideal behavior. The thermodynamic concept of **activity** ($a_i$) is introduced to account for this, where $a_i = \gamma_i c_i$, with $\gamma_i$ being the **[activity coefficient](@entry_id:143301)** and $c_i$ the molar concentration. While the [thermodynamic equilibrium constant](@entry_id:164623) $K^\circ$ is defined with activities, experimental measurements often yield a concentration-based "observed" constant, $K^{\text{obs}}$.

The **Debye-Hückel limiting law** provides a theoretical model for the activity coefficients of ions at low **[ionic strength](@entry_id:152038)** ($I$). For an ion of charge $z_i$, it states $\log_{10} \gamma_i = - A z_i^2 \sqrt{I}$, where $A$ is a constant for a given solvent and temperature. Using this, we can relate the observed $pK^{\text{obs}}$ to the thermodynamic $pK^\circ$:

$$ pK^{\text{obs}} = pK^\circ - A \sqrt{I} (\Delta z^2) $$

where $\Delta z^2 = z_{\text{products}}^2 - z_{\text{reactants}}^2$ is the sum of the squares of the charges of the products minus that of the reactants. This equation shows that $pK^{\text{obs}}$ is a linear function of $\sqrt{I}$ at low ionic strength.

This relationship has practical consequences for experimental accuracy. An uncertainty in the [ionic strength](@entry_id:152038), $u(I)$, will propagate into an uncertainty in the measured $pK^{\text{obs}}$. The sensitivity of $pK^{\text{obs}}$ to changes in $I$ is given by the derivative $\left|\frac{\partial pK^{\text{obs}}}{\partial I}\right| = \left|\frac{A \Delta z^2}{2\sqrt{I}}\right|$. This sensitivity depends on the charge types involved in the equilibrium. For the [dissociation](@entry_id:144265) of a neutral monoprotic acid ($\text{HA} \rightleftharpoons \text{H}^+ + \text{A}^-$), $\Delta z^2 = 2$. For the second dissociation of a diprotic acid ($\text{HA}^- \rightleftharpoons \text{H}^+ + \text{A}^{2-}$), $\Delta z^2 = 4$. Consequently, the measurement of the second $pK_a$ is twice as sensitive to uncertainties in [ionic strength](@entry_id:152038) as the measurement of the first, a crucial consideration in the design and analysis of experiments [@problem_id:2918386].

### Kinetics and Mechanisms of Acid-Base Catalysis

Acids and bases are frequently employed as catalysts. A key mechanistic distinction exists between **general** and **specific** catalysis, which can be diagnosed by analyzing the reaction's rate law.

In **[specific acid catalysis](@entry_id:170160) (SAC)**, the rate is proportional only to the activity of the protonated solvent (e.g., $\text{H}_3\text{O}^+$ in water). This typically occurs when the reaction involves a rapid pre-equilibrium protonation of the substrate, followed by a slower, rate-determining unimolecular step of the protonated substrate. For a substrate $S$ and [rate-determining step](@entry_id:137729) $SH^{+} \xrightarrow{k_c} \text{products}$, the derived pseudo-first-order rate constant $k_{\text{obs}}$ is [@problem_id:2918372]:

$$ k_{\text{obs}}^{\text{SAC}} = \left(\frac{k_c K_{eq} \gamma_S}{\gamma_{SH^{+}}}\right) \frac{a_{\text{H}_3\text{O}^+}}{a_{\text{H}_2\text{O}}} $$

Here, $K_{eq}$ is the equilibrium constant for protonation, and the rate depends only on $a_{\text{H}_3\text{O}^+}$.

In **[general acid catalysis](@entry_id:147970) (GAC)**, the rate depends on the concentrations of all available Brønsted acids in the solution, not just $\text{H}_3\text{O}^+$. This mechanism implies that the proton transfer occurs in the rate-determining step itself, in a concerted fashion. For a reaction catalyzed by $\text{H}_3\text{O}^+$ and a series of buffer acids $\text{B}_j\text{H}^+$, the overall rate is the sum of rates from each catalytic pathway. The derived pseudo-first-order rate constant is [@problem_id:2918372]:

$$ k_{\text{obs}}^{\text{GAC}} = c^\circ \left( \frac{k_H a_{\text{H}_3\text{O}^+}}{\gamma_{\text{H}_3\text{O}^+}} + \sum_{j=1}^{n} \frac{k_j a_{\text{B}_j\text{H}^+}}{\gamma_{\text{B}_j\text{H}^+}} \right) $$

where $k_H$ and $k_j$ are the second-order [rate constants](@entry_id:196199) for catalysis by each acid. Observing a linear dependence of the rate on the concentration of a buffer acid (at constant pH) is the hallmark of [general acid catalysis](@entry_id:147970).

### Linear Free-Energy Relationships

**Linear free-energy relationships (LFERs)** are powerful tools that correlate changes in [reaction rates](@entry_id:142655) or equilibria with changes in structure. They provide deep mechanistic insight by quantifying the sensitivity of a reaction to structural perturbations.

#### The Brønsted Catalysis Law

The **Brønsted catalysis law** is an LFER that relates the rate constant ($k$) for a general acid- or base-catalyzed reaction to the equilibrium constant ($K_a$) of the acid-base catalyst. It is expressed as:

$$ \log k = \alpha \log K_a + C \quad \text{or} \quad \log k = \beta pK_a + C' $$

The slope, $\alpha$ (for GAC) or $\beta$ (for GBC), is the **Brønsted coefficient**. It typically ranges from $0$ to $1$ and is interpreted as a measure of the degree of [proton transfer](@entry_id:143444) in the transition state. An $\alpha$ value near $1$ suggests a transition state that closely resembles the products (a late transition state), while a value near $0$ suggests a reactant-like (early) transition state.

A deeper theoretical understanding of the Brønsted coefficient comes from **Marcus theory**, originally developed for [electron transfer](@entry_id:155709). Applying a similar model of intersecting [parabolic free-energy surfaces](@entry_id:189292) to proton transfer, we can derive an expression for the [activation free energy](@entry_id:169953), $\Delta G^{\ddagger}$ [@problem_id:2918377]:

$$ \Delta G^{\ddagger} = \frac{(\lambda + \Delta G^\circ)^2}{4\lambda} $$

Here, $\Delta G^\circ$ is the overall free energy change of the reaction (the driving force), and $\lambda$ is the **reorganization energy**, the energy cost to distort the reactants to the product geometry without transferring the proton. From this, the Brønsted coefficient $\alpha = \frac{d \ln k}{d \ln K} = \frac{d \Delta G^{\ddagger}}{d \Delta G^\circ}$ can be derived as:

$$ \alpha = \frac{1}{2} + \frac{\Delta G^\circ}{2\lambda} $$

This result predicts that the Brønsted plot ($\log k$ vs. $\log K_a$ or $pK_a$) is not necessarily linear. The slope $\alpha$ depends on the driving force $\Delta G^\circ$. For a reaction with zero driving force ($\Delta G^\circ = 0$), $\alpha = 0.5$. As the reaction becomes more exergonic ($\Delta G^\circ  0$), $\alpha$ decreases. When $\Delta G^\circ = -\lambda$, the reaction becomes barrierless ($\Delta G^{\ddagger} = 0$) and $\alpha = 0$. In the highly exergonic regime ($-\Delta G^\circ \gg \lambda$), $\alpha$ can become negative, leading to the counterintuitive **Marcus inverted region** where the reaction rate decreases as it becomes more thermodynamically favorable [@problem_id:2918377].

#### The Hammett Equation

The **Hammett equation** is another prominent LFER that quantifies the effect of aromatic substituents on [reaction rates](@entry_id:142655) and equilibria. For the [dissociation](@entry_id:144265) of a series of para- or meta-substituted benzoic acids, it takes the form:

$$ \log \left( \frac{K_a(\text{X})}{K_a(\text{H})} \right) = \rho \sigma $$

Here, $K_a(\text{X})$ is the [acid dissociation constant](@entry_id:138231) for a benzoic acid with [substituent](@entry_id:183115) X, and $K_a(\text{H})$ is for the unsubstituted parent acid. The **[substituent constant](@entry_id:198177)**, $\sigma$, is an empirical parameter that quantifies the electronic effect (inductive and resonance) of [substituent](@entry_id:183115) X; a positive $\sigma$ indicates an electron-withdrawing group, while a negative $\sigma$ indicates an electron-donating group. The **reaction constant**, $\rho$, measures the sensitivity of the reaction to these electronic effects.

By relating the equilibrium constants to $pK_a$ values, the Hammett equation can be written as [@problem_id:2918403]:

$$ pK_a(\text{H}) - pK_a(\text{X}) = \rho \sigma_p(\text{X}) \quad \text{or} \quad pK_a(\text{X}) = pK_a(\text{H}) - \rho \sigma_p(\text{X}) $$

For the [dissociation](@entry_id:144265) of benzoic acids in water at $298\,\text{K}$, the reaction constant $\rho$ is defined to be $1.00$. A positive $\rho$ value for any reaction indicates that the reaction is aided by [electron-withdrawing groups](@entry_id:184702), which implies that negative charge is built up during the reaction (or positive charge is lost). By performing a [linear regression](@entry_id:142318) of $pK_a$ versus $\sigma$ for a series of compounds, one can experimentally determine $\rho$ and gain valuable insight into the reaction mechanism and charge distribution in the transition state [@problem_id:2918403].

### Extremes of Acidity: Superacids and Acidity Functions

The familiar aqueous $pK_a$ scale is limited in its ability to differentiate the strengths of very [strong acids](@entry_id:202580). Any acid significantly stronger than $\text{H}_3\text{O}^+$ will be completely dissociated in water, a phenomenon known as the **[leveling effect](@entry_id:153934)**. To an observer in water, acids like $\text{HClO}_4$, $\text{HBr}$, and $\text{HI}$ all appear to have the same strength—that of $\text{H}_3\text{O}^+$.

To quantify and compare the acidity of **superacids**—acids stronger than 100% [sulfuric acid](@entry_id:136594)—a different approach is needed. The **Hammett [acidity](@entry_id:137608) function, $H_0$**, provides an operational measure of a medium's protonating power. It is defined by measuring the extent of protonation of a series of very weak indicator bases (B) within the acidic medium itself:

$$ H_0 \equiv pK_a(\text{BH}^+) - \log_{10} \frac{[\text{BH}^+]}{[\text{B}]} $$

where $pK_a(\text{BH}^+)$ is the known aqueous $pK_a$ of the indicator's conjugate acid. Extremely negative $H_0$ values signify immense protonating ability. Unlike $pK_a$, which is a property of a molecule in a specific solvent, $H_0$ is a property of the bulk medium. This is crucial because in concentrated, non-ideal superacidic media, the concept of a simple dissociation equilibrium breaks down. The medium is a complex mixture of species, and [acidity](@entry_id:137608) arises from the collective behavior of the system [@problem_id:2918381].

The exceptional strength of superacids like fluorosulfonic acid ($\text{FSO}_3\text{H}$, $H_0 = -15.1$) or "Magic Acid" ($\text{FSO}_3\text{H}/\text{SbF}_5$, $H_0 \approx -23$) arises from the formation of an extremely stable, weakly basic, and poorly coordinating conjugate anion (e.g., $\text{SbF}_6^-$). This anion has very little affinity for the proton, leaving the proton "unencumbered" and exceptionally reactive. The $H_0$ scale is capable of differentiating the strengths of these acids, a task for which the aqueous $pK_a$ scale is completely inadequate due to the [leveling effect](@entry_id:153934) of water [@problem_id:2918381] [@problem_id:2918381].