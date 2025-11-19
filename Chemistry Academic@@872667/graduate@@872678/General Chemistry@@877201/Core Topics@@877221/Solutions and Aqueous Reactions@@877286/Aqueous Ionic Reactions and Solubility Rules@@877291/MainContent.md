## Introduction
Aqueous ionic reactions are the cornerstone of chemistry, governing processes that range from the formation of minerals in the earth's crust to the intricate [biochemical pathways](@entry_id:173285) of life. At the heart of these reactions lies the concept of [solubility](@entry_id:147610)—the ability of an ionic solid to dissolve in water. While introductory chemistry often relies on a set of empirical [solubility](@entry_id:147610) rules for quick predictions, these generalizations frequently fail to capture the complexity of real-world systems. This discrepancy creates a knowledge gap, leaving us unable to explain why a "soluble" salt might precipitate or an "insoluble" one might dissolve under specific conditions.

This article bridges that gap by guiding you from simple [heuristics](@entry_id:261307) to a deep, thermodynamic understanding of ionic equilibria. You will learn to move beyond qualitative rules and master the quantitative tools needed to predict and manipulate solubility with precision. The journey is structured across three comprehensive chapters. Chapter 1, "Principles and Mechanisms," establishes the foundational language of ionic equations and delves into the thermodynamic machinery—chemical potential, activity, and the [solubility product](@entry_id:139377) ($K_{sp}$)—that truly governs [solubility](@entry_id:147610). Chapter 2, "Applications and Interdisciplinary Connections," demonstrates how these principles are applied to solve complex problems in diverse fields like [analytical chemistry](@entry_id:137599), [environmental science](@entry_id:187998), and biochemistry. Finally, Chapter 3, "Hands-On Practices," offers the opportunity to solidify your understanding by tackling practical problems that integrate these advanced concepts. By the end, you will possess a robust framework for analyzing any aqueous ionic system.

## Principles and Mechanisms

### Describing Reactions in Aqueous Solution: Ionic Equations

Aqueous ionic reactions can be represented with varying levels of detail, each serving a distinct pedagogical or analytical purpose. The **[molecular equation](@entry_id:145191)** shows all reactants and products as electrically neutral formula units, which, while simple, obscures the ionic nature of the species in solution. A more revealing representation is the **complete ionic equation**. In this form, all [strong electrolytes](@entry_id:142940)—substances that exist almost entirely as free-moving [ions in solution](@entry_id:143907), such as [strong acids](@entry_id:202580), strong bases, and most soluble salts—are written as dissociated ions. Weak [electrolytes](@entry_id:137202) (e.g., weak acids and bases), gases, and insoluble precipitates, which exist predominantly as intact species, are written in their undissociated form.

The most chemically incisive representation is the **[net ionic equation](@entry_id:137630)**. This is derived from the complete ionic equation by identifying and removing **[spectator ions](@entry_id:146899)**. Spectator ions are those that do not participate in the chemical transformation; they appear with an identical formula, charge, phase, and [stoichiometric coefficient](@entry_id:204082) on both the reactant and product sides of the complete ionic equation. By eliminating these bystander species, the [net ionic equation](@entry_id:137630) focuses exclusively on the [chemical change](@entry_id:144473) that occurs.

Consider a reaction initiated by mixing [aqueous solutions](@entry_id:145101) of hydrochloric acid (a strong acid), sodium fluoride (a soluble salt), and silver nitrate (a soluble salt). The constituent [ions in solution](@entry_id:143907) are $\text{H}^+$, $\text{Cl}^-$, $\text{Na}^+$, $\text{F}^-$, $\text{Ag}^+$, and $\text{NO}_3^-$. Based on standard chemical principles, two key reactions will occur: the [precipitation](@entry_id:144409) of silver chloride ($\text{AgCl}$), which is insoluble, and the formation of hydrofluoric acid ($\text{HF}$), a [weak electrolyte](@entry_id:266880). The complete ionic equation is therefore:

$$
\text{H}^+\text{(aq)} + \text{Cl}^-\text{(aq)} + \text{Na}^+\text{(aq)} + \text{F}^-\text{(aq)} + \text{Ag}^+\text{(aq)} + \text{NO}_3^-\text{(aq)} \rightarrow \text{AgCl(s)} + \text{HF(aq)} + \text{Na}^+\text{(aq)} + \text{NO}_3^-\text{(aq)}
$$

To find the [net ionic equation](@entry_id:137630), we identify the [spectator ions](@entry_id:146899). The sodium ion, $\text{Na}^+\text{(aq)}$, and the nitrate ion, $\text{NO}_3^-\text{(aq)}$, appear unchanged on both sides. Removing them reveals the net reaction [@problem_id:2918957]:

$$
\text{H}^+\text{(aq)} + \text{F}^-\text{(aq)} + \text{Ag}^+\text{(aq)} + \text{Cl}^-\text{(aq)} \rightarrow \text{HF(aq)} + \text{AgCl(s)}
$$

This equation, which must be balanced for both mass and charge, concisely shows the formation of a [weak electrolyte](@entry_id:266880) and a precipitate from their constituent ions. The net charge on both sides is $(+1) + (-1) + (+1) + (-1) = 0$, confirming charge conservation.

### Empirical Solubility Rules: A Qualitative Guide

Before delving into the quantitative thermodynamic framework, it is useful to be familiar with a set of empirical **[solubility](@entry_id:147610) rules**. These are generalizations, derived from extensive experimental observation, that allow for rapid prediction of whether an ionic compound is likely to be soluble or insoluble in water at or near room temperature. While these rules are [heuristics](@entry_id:261307) and have exceptions, they provide an excellent starting point for chemical analysis.

A standard set of these rules for common [ionic compounds](@entry_id:137573) in water at $25\,^{\circ}\text{C}$ is as follows [@problem_id:2918979]:

1.  **Generally Soluble Compounds:**
    *   Salts containing alkali metal cations ($\text{Li}^+$, $\text{Na}^+$, $\text{K}^+$, $\text{Rb}^+$, $\text{Cs}^+$) and the ammonium cation ($\text{NH}_4^+$) are soluble.
    *   Salts containing the nitrate anion ($\text{NO}_3^-$) are soluble.
    *   Salts containing halide anions ($\text{Cl}^-$, $\text{Br}^-$, $\text{I}^-$) are soluble. **Exceptions:** Halides of $\text{Ag}^+$, $\text{Pb}^{2+}$, and $\text{Hg}_2^{2+}$ are insoluble.
    *   Salts containing the sulfate anion ($\text{SO}_4^{2-}$) are soluble. **Exceptions:** Sulfates of $\text{Ba}^{2+}$, $\text{Sr}^{2+}$, and $\text{Pb}^{2+}$ are insoluble. Calcium sulfate ($\text{CaSO}_4$) and silver sulfate ($\text{Ag}_2\text{SO}_4$) are sparingly soluble.

2.  **Generally Insoluble Compounds:**
    *   Salts containing carbonate ($\text{CO}_3^{2-}$) or phosphate ($\text{PO}_4^{3-}$) anions are insoluble. **Exceptions:** Salts of [alkali metals](@entry_id:139133) and ammonium are soluble.
    *   Salts containing hydroxide ($\text{OH}^-$) or sulfide ($\text{S}^{2-}$) [anions](@entry_id:166728) are insoluble. **Exceptions:** Hydroxides and sulfides of [alkali metals](@entry_id:139133) are soluble. Hydroxides of the heavier [alkaline earth metals](@entry_id:142937) ($\text{Ca}^{2+}$, $\text{Sr}^{2+}$, $\text{Ba}^{2+}$) are sparingly to moderately soluble. Sulfides of the [alkaline earth metals](@entry_id:142937) are also soluble.

These rules provide a powerful qualitative framework, but to understand their origin and their limitations, we must turn to the principles of [chemical thermodynamics](@entry_id:137221).

### The Thermodynamic Basis of Solubility

The dissolution of an ionic solid is an equilibrium process governed by the same [thermodynamic principles](@entry_id:142232) as any other chemical reaction. The limitations of empirical rules become apparent when we consider the quantitative nature of this equilibrium.

#### Chemical Potential and Activity

The fundamental quantity that governs chemical equilibrium is the **chemical potential**, $\mu_i$, which can be thought of as the partial molar Gibbs free energy of a species $i$. For any species in a mixture, its chemical potential is given by:

$$
\mu_i = \mu_i^{\circ} + RT\ln a_i
$$

where $\mu_i^{\circ}$ is the standard chemical potential (the chemical potential in a defined standard state), $R$ is the gas constant, $T$ is the absolute temperature, and $a_i$ is the **activity** of the species. The activity is a dimensionless measure of the "effective concentration" of a species, which accounts for deviations from ideal behavior due to intermolecular or interionic interactions. For a solute $i$ on the [molality](@entry_id:142555) scale, its activity is defined as:

$$
a_i = \gamma_i \frac{m_i}{m^{\circ}}
$$

Here, $m_i$ is the [molality](@entry_id:142555) of the solute, $m^{\circ}$ is the standard [molality](@entry_id:142555) ($1\,\text{mol}\,\text{kg}^{-1}$), and $\gamma_i$ is the dimensionless **activity coefficient**. The [activity coefficient](@entry_id:143301) quantifies the deviation from ideality; for an ideal solution, $\gamma_i = 1$. In real ionic solutions, electrostatic interactions between ions cause $\gamma_i$ to deviate from unity. As the solution becomes infinitely dilute, these interactions vanish, and $\gamma_i \rightarrow 1$ [@problem_id:2918891].

For electrolytes, it is impossible to experimentally isolate cations from [anions](@entry_id:166728), so we cannot measure individual ionic activity coefficients ($\gamma_+$ and $\gamma_-$). Instead, we define a measurable quantity, the **[mean ionic activity coefficient](@entry_id:153862)**, $\gamma_{\pm}$. For a salt $A_{\nu_+}B_{\nu_-}$ that dissolves into $\nu_+$ cations and $\nu_-$ [anions](@entry_id:166728), $\gamma_{\pm}$ is defined as the geometric mean of the individual coefficients:

$$
\gamma_{\pm}^{\nu} = \gamma_+^{\nu_+} \gamma_-^{\nu_-} \quad \text{where} \quad \nu = \nu_+ + \nu_-
$$

This definition allows us to treat the non-ideality of the electrolyte as a whole in a thermodynamically consistent manner.

#### The Solubility Product, $K_{sp}$

For the dissolution equilibrium of a sparingly soluble salt $A_{\nu_+}B_{\nu_-}(s) \rightleftharpoons \nu_+\,A^{z_+}(aq) + \nu_-\,B^{z_-}(aq)$, the equilibrium condition is met when the chemical potential of the solid equals the sum of the chemical potentials of its constituent aqueous ions. This leads to the definition of the **thermodynamic [solubility product constant](@entry_id:143661)**, $K_{sp}$:

$$
K_{sp} = a_+^{\nu_+} a_-^{\nu_-}
$$

Because $K_{sp}$ is defined in terms of activities and is related to the standard Gibbs free energy of solution ($\Delta G_{\text{sol}}^{\circ} = -RT \ln K_{sp}$), its value depends only on temperature and pressure. It is a true constant, independent of the presence of other ions or the overall composition of the solution [@problem_id:2918891] [@problem_id:2918913].

In contrast, an **apparent [solubility product](@entry_id:139377)**, $K'_{sp}$, can be defined in terms of molar concentrations (or molalities), for instance, $K'_{sp} = [A^{z+}]^{\nu_+} [B^{z-}]^{\nu_-}$. This quantity is not constant; it depends on the ionic environment because it neglects the activity coefficients. The relationship between the two is:

$$
K_{sp} = ([A^{z+}]\gamma_+)^{\nu_+} ([B^{z-}]\gamma_-)^{\nu_-} = K'_{sp} (\gamma_+^{\nu_+} \gamma_-^{\nu_-}) = K'_{sp} \gamma_{\pm}^{\nu}
$$

This equation is central to understanding the behavior of real ionic solutions. It shows that $K'_{sp}$ is equal to $K_{sp}$ only in the limit of infinite dilution where $\gamma_{\pm} \rightarrow 1$.

#### Predicting Precipitation: The Ion Activity Product, $Q_{sp}$

To predict whether a salt will dissolve or precipitate under a given set of non-equilibrium conditions, we use the **ion activity product**, $Q_{sp}$. This quantity has the same mathematical form as $K_{sp}$ but is calculated using the instantaneous activities of the ions in the solution, not their equilibrium values.

$$
Q_{sp} = a_+^{\nu_+} a_-^{\nu_-} \quad (\text{at any moment})
$$

The relationship between $Q_{sp}$ and $K_{sp}$ determines the thermodynamic driving force for the system [@problem_id:2918938]:

*   **$Q_{sp}  K_{sp}$**: The solution is **undersaturated**. The activities of the ions are lower than their equilibrium values. The forward reaction (dissolution) is spontaneous, and more solid can dissolve. The Gibbs free energy of dissolution, $\Delta_r G = RT\ln(Q_{sp}/K_{sp})$, is negative.

*   **$Q_{sp} = K_{sp}$**: The solution is **saturated**. The system is at equilibrium, and the rates of dissolution and precipitation are equal. $\Delta_r G = 0$.

*   **$Q_{sp} > K_{sp}$**: The solution is **supersaturated**. The ion activities are higher than their equilibrium values. The reverse reaction ([precipitation](@entry_id:144409)) is spontaneous. $\Delta_r G > 0$ for dissolution. A solution can remain in a metastable supersaturated state if there are kinetic barriers to nucleation, but the system is thermodynamically poised to precipitate.

For example, consider a solution where $[\text{Ca}^{2+}] = 1.0 \times 10^{-3}\,\text{M}$ and $[\text{F}^{-}] = 2.5 \times 10^{-3}\,\text{M}$, with corresponding activity coefficients $\gamma_{\text{Ca}^{2+}} = 0.62$ and $\gamma_{\text{F}^{-}} = 0.78$. The ion activity product for $\text{CaF}_2$ is:
$Q_{sp} = a_{\text{Ca}^{2+}} (a_{\text{F}^{-}})^2 = (\gamma_{\text{Ca}^{2+}}[\text{Ca}^{2+}])(\gamma_{\text{F}^{-}}[\text{F}^{-}])^2$
$Q_{sp} = (0.62 \times 1.0 \times 10^{-3})(0.78 \times 2.5 \times 10^{-3})^2 \approx 2.4 \times 10^{-9}$.
Given that $K_{sp}(\text{CaF}_2) = 1.5 \times 10^{-10}$, we see that $Q_{sp} > K_{sp}$. The solution is supersaturated, and precipitation of $\text{CaF}_2$ is thermodynamically favored [@problem_id:2918938].

### Reconciling Rules and Reality: Why Solubility is Context-Dependent

The thermodynamic framework explains why empirical solubility rules, while useful, often fail to predict behavior in complex systems. The actual [solubility](@entry_id:147610) of a salt is not an [intrinsic property](@entry_id:273674) but is highly dependent on the solution's composition.

#### The Inert Electrolyte Effect

The solubility of a sparingly soluble salt is affected by the presence of **inert electrolytes** ([spectator ions](@entry_id:146899)). While these ions do not participate in the reaction and thus do not alter the value of $K_{sp}$, they do increase the overall **[ionic strength](@entry_id:152038)** of the solution, $I = \frac{1}{2}\sum_i c_i z_i^2$. According to theories such as the Debye-Hückel theory, increasing the [ionic strength](@entry_id:152038) lowers the activity coefficients of ions ($\gamma_i  1$).

Consider the dissolution of a salt $MX(s) \rightleftharpoons M^+(aq) + X^-(aq)$. The [molar solubility](@entry_id:141822) is $s = [M^+] = [X^-]$. The equilibrium condition is $K_{sp} = a_{M^+} a_{X^-} = (\gamma_{M^+}s)(\gamma_{X^-}s) = s^2 \gamma_{\pm}^2$. Solving for [solubility](@entry_id:147610) gives:

$$
s = \frac{\sqrt{K_{sp}}}{\gamma_{\pm}}
$$

Since $\gamma_{\pm}$ decreases as ionic strength increases, the [molar solubility](@entry_id:141822) $s$ must *increase* to keep the activity product constant. This phenomenon is known as the **[salt effect](@entry_id:146160)** or the inert electrolyte effect [@problem_id:2918950]. For a salt like $\text{CaSO}_4$, which is on the borderline of solubility, this effect can be dramatic. In pure water, its ion product might exceed $K_{sp}$, causing [precipitation](@entry_id:144409). However, in a solution with a high background ionic strength (e.g., $0.50\,\text{M}$ $\text{NaNO}_3$), the activity coefficients of $\text{Ca}^{2+}$ and $\text{SO}_4^{2-}$ are significantly reduced, which can lower $Q_{sp}$ below $K_{sp}$ and prevent [precipitation](@entry_id:144409) entirely [@problem_id:2918927].

#### Competing Equilibria: Complexation and pH

The [solubility](@entry_id:147610) of a salt can be drastically altered if one of its ions participates in a separate, competing equilibrium.

*   **Complex Ion Formation:** If a ligand that forms a stable complex with the cation is present, it will reduce the concentration of the free aqueous cation. By Le Châtelier's principle, this will shift the dissolution equilibrium to the right, increasing the overall [solubility](@entry_id:147610). A classic example is the dissolution of silver chloride, $\text{AgCl}$, in aqueous ammonia. The empirical rule correctly states that $\text{AgCl}$ is insoluble. However, in the presence of ammonia, the free silver ion, $\text{Ag}^+$, is sequestered into the highly stable diamminesilver(I) complex, $\text{Ag(NH}_3)_2^+$. This [complexation](@entry_id:270014) reduces the free $[Ag^+]$ to such a low level that the ion activity product, $Q_{sp} = a_{\text{Ag}^+}a_{\text{Cl}^-}$, may not reach the value of $K_{sp}$, thus preventing [precipitation](@entry_id:144409) or causing already-precipitated $\text{AgCl}$ to dissolve [@problem_id:2918927].

*   **pH Effects:** If the anion of a sparingly soluble salt is the [conjugate base](@entry_id:144252) of a weak acid (e.g., $\text{F}^-$, $\text{OH}^-$, $\text{CO}_3^{2-}$), its [solubility](@entry_id:147610) will be pH-dependent. In acidic solutions, the anion is protonated, reducing its free concentration and increasing the salt's solubility. For example, the solubility of magnesium hydroxide, $\text{Mg(OH)}_2$, increases dramatically as pH is lowered because the $\text{OH}^-$ ions are neutralized by $\text{H}^+$ to form water.

#### Concentration Dependence

Finally, the empirical rules are qualitative statements that do not account for concentration levels. A salt classified as "insoluble," such as lead(II) chloride ($\text{PbCl}_2$), will still not precipitate if the initial concentrations of its ions are too low. Precipitation only occurs if the ion activity product $Q_{sp}$ exceeds the thermodynamic constant $K_{sp}$. For very [dilute solutions](@entry_id:144419), $Q_{sp}$ can easily remain below $K_{sp}$, and no solid will form, contrary to the simple rule [@problem_id:2918927].

### Thermodynamic Rationalization of Solubility Trends

The magnitudes of [solubility](@entry_id:147610) products and the resulting [solubility](@entry_id:147610) trends can be rationalized by examining the Gibbs free energy of solution, $\Delta G_{\text{sol}}^{\circ}$, which can be dissected into enthalpic and entropic components:

$$
\Delta G_{\text{sol}}^{\circ} = \Delta H_{\text{sol}}^{\circ} - T \Delta S_{\text{sol}}^{\circ}
$$

The standard [enthalpy of solution](@entry_id:139285), $\Delta H_{\text{sol}}^{\circ}$, can be viewed as the sum of two competing terms: the **[lattice enthalpy](@entry_id:153402)** ($\Delta H_{\text{lat}}^{\circ}$), which is the large, positive (endothermic) energy required to break apart the ionic crystal into gaseous ions, and the sum of **hydration enthalpies** ($\sum \Delta H_{\text{hyd}}^{\circ}$), which is the large, negative (exothermic) energy released when the gaseous ions are solvated by water molecules.

$$
\Delta H_{\text{sol}}^{\circ} = \Delta H_{\text{lat}}^{\circ} + \sum \Delta H_{\text{hyd}}^{\circ}
$$

The standard entropy of solution, $\Delta S_{\text{sol}}^{\circ}$, also has competing contributions. There is a large, positive entropy change associated with the dispersal of ions from an ordered lattice into a disordered solution. However, this is counteracted by a negative [entropy change](@entry_id:138294) from the ordering of solvent molecules into structured hydration shells around the ions.

The trend in [solubility](@entry_id:147610) of the alkaline earth hydroxides provides an excellent case study. Magnesium hydroxide, $\text{Mg(OH)}_2$, is significantly less soluble than calcium hydroxide, $\text{Ca(OH)}_2$. This can be explained by considering the properties of the $\text{Mg}^{2+}$ and $\text{Ca}^{2+}$ ions [@problem_id:2918969].

1.  **Enthalpy:** The $\text{Mg}^{2+}$ ion is smaller and has a higher charge density than the $\text{Ca}^{2+}$ ion. This leads to two competing effects:
    *   The smaller size results in stronger [electrostatic forces](@entry_id:203379) in the $\text{Mg(OH)}_2$ crystal, making its [lattice enthalpy](@entry_id:153402) much larger (more positive) than that of $\text{Ca(OH)}_2$. This factor disfavors dissolution.
    *   The higher charge density causes $\text{Mg}^{2+}$ to be hydrated much more strongly, making its [hydration enthalpy](@entry_id:142032) much more negative than that of $\text{Ca}^{2+}$. This factor favors dissolution.
    For Group 2 hydroxides, the change in [lattice enthalpy](@entry_id:153402) is more pronounced than the change in [hydration enthalpy](@entry_id:142032). Thus, the unfavorable [lattice enthalpy](@entry_id:153402) term for $\text{Mg(OH)}_2$ dominates, making its overall $\Delta H_{\text{sol}}^{\circ}$ more positive (less favorable) than that of $\text{Ca(OH)}_2$.

2.  **Entropy:** The high [charge density](@entry_id:144672) of $\text{Mg}^{2+}$ also causes it to induce a more extensive and ordered [hydration shell](@entry_id:269646) than $\text{Ca}^{2+}$. This greater ordering of the solvent results in a more negative entropic contribution. Consequently, $\Delta S_{\text{sol}}^{\circ}$ is less positive for $\text{Mg(OH)}_2$ than for $\text{Ca(OH)}_2$. The term $-T\Delta S_{\text{sol}}^{\circ}$ is therefore more positive for $\text{Mg(OH)}_2$, also disfavoring its dissolution.

Both the enthalpic and entropic factors work in the same direction, making $\Delta G_{\text{sol}}^{\circ}$ for $\text{Mg(OH)}_2$ significantly more positive than for $\text{Ca(OH)}_2$, which accounts for its much lower [solubility](@entry_id:147610).

### Kinetics vs. Thermodynamics of Dissolution

It is crucial to distinguish between the **thermodynamic [solubility](@entry_id:147610)**, which defines the final equilibrium state, and the **kinetic dissolution rate**, which describes how fast that equilibrium is approached. Thermodynamics tells us *where the system is going*, while kinetics tells us *how fast it will get there*. The time required to reach saturation is governed by the kinetics of the dissolution process [@problem_id:2918924].

The dissolution of a crystal is a heterogeneous process that involves at least two primary steps:

1.  **Surface Reaction:** The detachment of ions from the [crystal surface](@entry_id:195760) into the adjacent layer of solvent.
2.  **Mass Transport:** The diffusion of these dissolved ions away from the solid surface, through a thin, relatively stagnant diffusion boundary layer, into the bulk solution.

The overall rate is determined by the slower of these two steps. Several experimental factors influence these rates, but they do not affect the final equilibrium [solubility](@entry_id:147610):

*   **Particle Size (Surface Area):** For a given mass of solid, smaller particles have a greater total surface area. Since the dissolution rate is proportional to the available surface area, finer powders dissolve faster than coarse crystals.

*   **Agitation (Stirring):** Vigorous stirring reduces the thickness of the diffusion boundary layer at the particle surface. This steepens the [concentration gradient](@entry_id:136633) and accelerates the mass transport step, thereby increasing the overall dissolution rate.

*   **Surface Defects:** The surface of a real crystal is not perfect. It contains defects such as steps, kinks, and dislocations. Ions at these defect sites are less tightly bound to the lattice and have a lower activation energy for detachment. A crystal with a high density of [surface defects](@entry_id:203559) will exhibit a faster intrinsic [surface reaction](@entry_id:183202) rate and thus dissolve more quickly than a highly annealed, near-perfect crystal.

Therefore, while different preparations of a solid (e.g., fine vs. coarse, stirred vs. quiescent, defect-rich vs. annealed) will reach saturation at different times, they will all approach the same final equilibrium solubility, as this is a thermodynamic property of the bulk material at a given temperature and pressure.

### A Final Distinction: Dissociation vs. Ionization

Finally, for clarity in describing how solutes produce ions, we distinguish between two processes [@problem_id:2918983].

**Dissociation** is a physical process in which a substance that is already composed of ions in its [pure state](@entry_id:138657) (typically an ionic solid) separates into its constituent ions upon dissolution. Soluble ionic salts like sodium chloride ($\text{NaCl}$) or ammonium chloride ($\text{NH}_4\text{Cl}$) dissociate. For these **[strong electrolytes](@entry_id:142940)**, the process is considered to go to completion. The van't Hoff factor, $i$, approaches the number of ions in the [formula unit](@entry_id:145960) (e.g., $i \rightarrow 2$ for $\text{NH}_4\text{Cl}$) as the solution is diluted.

**Ionization**, by contrast, is a chemical reaction in which a neutral molecular substance reacts with the solvent to generate ions. For example, [acetic acid](@entry_id:154041) ($\text{CH}_3\text{COOH}$) is a molecular compound that reacts with water in an equilibrium process to form hydronium and acetate ions:
$$
\text{CH}_3\text{COOH(aq)} + \text{H}_2\text{O(l)} \rightleftharpoons \text{H}_3\text{O}^+\text{(aq)} + \text{CH}_3\text{COO}^-\text{(aq)}
$$
This process is governed by a finite [equilibrium constant](@entry_id:141040) ($K_a$). For such **[weak electrolytes](@entry_id:138862)**, the [degree of ionization](@entry_id:264739) is typically small and increases with dilution. The van't Hoff factor starts near $1$ and increases towards its theoretical maximum (e.g., $2$ for acetic acid) only at infinite dilution. This distinction underscores the importance of understanding the nature of the solute itself when analyzing the behavior of aqueous ionic solutions.