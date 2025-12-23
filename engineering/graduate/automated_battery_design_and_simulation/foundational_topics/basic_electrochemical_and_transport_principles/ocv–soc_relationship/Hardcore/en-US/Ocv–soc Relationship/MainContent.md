## Introduction
The relationship between Open-Circuit Voltage (OCV) and State of Charge (SOC) is a foundational concept in battery science, serving as the unique thermodynamic fingerprint of an [electrochemical cell](@entry_id:147644). For engineers and researchers in [automated battery design](@entry_id:1121262) and simulation, mastering this relationship is essential for creating accurate models, developing robust management systems, and diagnosing [battery health](@entry_id:267183). While often represented as a simple lookup table, the OCV-SOC curve encapsulates a wealth of information about a battery's internal state, from its fundamental chemistry to its degradation history. This article aims to bridge the gap between abstract thermodynamic theory and its practical, high-impact applications.

This article will guide you through a comprehensive exploration of the OCV-SOC relationship across three chapters. First, in "Principles and Mechanisms," we will delve into the thermodynamic foundations, deriving the OCV from Gibbs free energy and chemical potentials, and explain how material [phase changes](@entry_id:147766) create the characteristic voltage plateaus and hysteresis seen in many systems. Next, "Applications and Interdisciplinary Connections" will demonstrate how this curve is the backbone of real-world Battery Management Systems for SOC estimation, [cell balancing](@entry_id:1122184), and thermal modeling, and how it serves as a powerful non-destructive tool for diagnosing aging. Finally, "Hands-On Practices" will offer practical exercises to solidify your understanding of these core principles, from designing a cell's voltage profile through electrode balancing to quantifying the impact of hysteresis on SOC estimation.

## Principles and Mechanisms

The relationship between Open-Circuit Voltage (OCV) and State of Charge (SOC) is a cornerstone of battery science and engineering. It serves as the thermodynamic fingerprint of an [electrochemical cell](@entry_id:147644), reflecting the fundamental energy changes that occur as lithium ions are shuttled between the positive and negative electrodes. In [automated battery design](@entry_id:1121262) and simulation, a deep understanding of the OCV-SOC relationship is indispensable for state estimation, thermal management, and degradation diagnostics. This chapter elucidates the core principles governing this relationship, from its thermodynamic origins to the complex mechanisms that shape its appearance in real-world systems.

### Thermodynamic Foundations of Open-Circuit Voltage

At its most fundamental level, the Open-Circuit Voltage of an [electrochemical cell](@entry_id:147644) is the potential difference measured between its terminals when no external current is flowing ($I=0$) and all internal electrochemical and physical processes have reached a state of equilibrium. This equilibrium condition, which in practice may require a significant relaxation time ($t \to \infty$), distinguishes the OCV from the terminal voltage measured under load. The OCV is an intrinsic thermodynamic property of the cell at a given composition, temperature, and pressure.

The voltage of a cell arises from the change in Gibbs free energy ($\Delta_r G$) associated with the overall cell reaction. For a reversible process, this relationship is given by:

$$ \Delta_r G = -n F V_{\mathrm{oc}} $$

where $n$ is the number of moles of electrons transferred in the reaction as written, and $F$ is the Faraday constant ($96485.33 \text{ C/mol}$). In a lithium-ion cell, the overall reaction is the transfer of lithium from the negative electrode (anode) host to the positive electrode (cathode) host. Since this involves a single electron per lithium ion, $n=1$.

The Gibbs free energy change, in turn, is determined by the difference in the chemical potential of the species in their final and initial states. The **chemical potential** ($\mu_i$) of a species $i$ represents the change in the free energy of a system per mole of that species added. For the transfer of lithium from the negative electrode host (chemical potential $\mu_n$) to the positive electrode host (chemical potential $\mu_p$), the free energy change is:

$$ \Delta_r G = \mu_p - \mu_n $$

For a spontaneous discharge process, the free energy must decrease ($\Delta_r G \lt 0$), which implies that the chemical potential of lithium must be higher in the anode than in the cathode ($\mu_n \gt \mu_p$). Combining these [thermodynamic relations](@entry_id:139032) yields the fundamental expression for OCV :

$$ V_{\mathrm{oc}} = -\frac{\Delta_r G}{F} = -\frac{\mu_p - \mu_n}{F} = \frac{\mu_n - \mu_p}{F} $$

This equation reveals that the OCV is a direct measure of the difference in the chemical potential of lithium between the two electrodes. It represents the maximum [electrical work](@entry_id:273970) that can be extracted from the cell at a given state.

It is crucial to distinguish the OCV from the **terminal voltage** ($V_{\mathrm{term}}$) observed when the battery is under load (i.e., being charged or discharged with a current $I \neq 0$). Under load, the cell voltage deviates from its equilibrium value due to various irreversible losses, or **overpotentials**. These losses include:
*   **Activation Overpotential** ($\eta_{act}$): The energy barrier that must be overcome to drive the [charge-transfer](@entry_id:155270) reaction at the electrode-electrolyte interface at a finite rate.
*   **Concentration Overpotential** ($\eta_{conc}$): Voltage loss due to spatial variations in the concentration of lithium ions in the electrolyte or within the solid active material particles.
*   **Ohmic Drop** ($IR_{\mathrm{ohm}}$): Voltage loss resulting from the resistance to the flow of ions in the electrolyte and electrons in the solid components (active materials, current collectors).

The terminal voltage during discharge ($I \gt 0$) is therefore always lower than the OCV, and during charge ($I \lt 0$) it is always higher. A general expression for the terminal voltage can be written as :

$$ V_{\mathrm{term}} = V_{\mathrm{oc}} - \eta_{p} - \eta_{n} - I R_{\mathrm{ohm}} $$

where $\eta_p$ and $\eta_n$ represent the total positive magnitudes of overpotentials at the positive and negative electrodes, respectively, and $R_{\mathrm{ohm}}$ is the total [ohmic resistance](@entry_id:1129097) of the cell. The OCV is thus the idealized, loss-free voltage that a cell can provide.

### From Stoichiometry to State of Charge: The Composition Axis

The chemical potentials $\mu_p$ and $\mu_n$ are not constant; they are strong functions of the amount of lithium within each electrode's host structure. To quantify this, we use the concept of **lithium stoichiometry**, denoted by $x$. For a given electrode, $x$ is defined as the number of moles of intercalated lithium per mole of available host sites, $x = n_{\mathrm{Li}} / n_{\mathrm{host}}$ . The OCV is therefore a function of the stoichiometries of both electrodes, $V_{\mathrm{oc}}(x_p, x_n)$.

While stoichiometry $x$ is the fundamental physical variable, in practice it is more convenient to use the macroscopic **State of Charge (SOC)**. SOC is typically defined as the normalized amount of charge stored in the battery relative to its maximum capacity. For a single electrode, the relationship between SOC and stoichiometry is linear. The charge $Q$ required to change the stoichiometry from a minimum value $x_{\min}$ to a value $x$ is given by Faraday's law:

$$ Q = F \cdot n_{\mathrm{host}} \cdot (x - x_{\min}) $$

The maximum charge capacity, $Q_{\max}$, corresponds to the full operating range from $x_{\min}$ to $x_{\max}$:

$$ Q_{\max} = F \cdot n_{\mathrm{host}} \cdot (x_{\max} - x_{\min}) $$

Dividing these two equations gives a direct, linear mapping between SOC and stoichiometry :

$$ \mathrm{SOC} = \frac{Q}{Q_{\max}} = \frac{x - x_{\min}}{x_{\max} - x_{\min}} $$

This simple relationship is the bridge between the microscopic state of the material ($x$) and the macroscopic state of the battery (SOC). For this mapping to be consistent and meaningful, especially when comparing different materials in a design pipeline, the basis for [stoichiometry](@entry_id:140916)—the "host unit"—must be precisely defined. For example, in graphite anodes, the host unit is typically taken as $\mathrm{C}_6$ because the fully lithiated phase is $\mathrm{Li}_1\mathrm{C}_6$, so $x$ in $\mathrm{Li}_x\mathrm{C}_6$ ranges from near 0 to 1. For [layered oxide cathodes](@entry_id:1127115) like NMC (e.g., $\mathrm{LiNi}_{y}\mathrm{Mn}_{z}\mathrm{Co}_{1-y-z}\mathrm{O}_2$), the host unit is the transition metal oxide [formula unit](@entry_id:145960), and $x$ in $\mathrm{Li}_x(\mathrm{TMO}_2)$ likewise varies over a specific range.

### Constructing the Full-Cell OCV

The OCV of a full cell is constructed from the individual potential curves of its constituent electrodes. Each electrode's potential, $U_p(x_p)$ and $U_n(x_n)$, is defined as its [equilibrium potential](@entry_id:166921) measured against a common reference. In lithium-ion battery research, the standard reference is a Li/Li$^+$ half-cell (pure metallic lithium in contact with an electrolyte containing Li$^+$ ions).

At equilibrium, the [potential difference](@entry_id:275724) between the solid phase ($\phi_s$) and the electrolyte phase ($\phi_e$) at each electrode interface is equal to the electrode's [equilibrium potential](@entry_id:166921), $U_k(x_k)$, where $k \in \{p, n\}$. Under open-circuit conditions, there is no ionic current, so the electrolyte potential $\phi_e$ is uniform throughout the cell. We can therefore write:

$$ \phi_s^p - \phi_e = U_p(x_p) $$
$$ \phi_s^n - \phi_e = U_n(x_n) $$

The full-cell OCV is the difference in electric potential between the positive and negative current collectors, $V_{\mathrm{OCV}} = \phi_s^p - \phi_s^n$. Subtracting the two equations above directly yields the expression for the full-cell OCV :

$$ V_{\mathrm{OCV}} = U_p(x_p) - U_n(x_n) $$

This fundamental equation shows that the full-cell OCV is simply the difference between the cathode and anode equilibrium potentials, when both are expressed relative to the same reference. A critical point for numerical simulation is that this measurable potential difference is **gauge-invariant**. This means it is independent of the absolute value chosen for the electrolyte potential $\phi_e$. Shifting $\phi_e$ by a constant value will shift both $\phi_s^p$ and $\phi_s^n$ by the same amount, leaving their difference, the OCV, unchanged.

During cell operation, the stoichiometries $x_p$ and $x_n$ are not independent. They are coupled through a lithium conservation constraint. For every lithium ion that leaves the anode, one must enter the cathode. This links the evolution of $x_p$ and $x_n$ to the overall cell SOC, allowing the full-cell OCV to be expressed as a single function of SOC, $V_{\mathrm{OCV}}(s)$.

### The Shape of the OCV-SOC Curve: From Free Energy to Voltage Plateaus

The characteristic shape of an OCV-SOC curve—whether it is steeply sloped, flat, or has steps—is a direct reflection of the thermodynamics of the electrode materials. Specifically, the shape of the potential curve $U(x)$ is dictated by the electrode's molar Gibbs free energy function, $g(x)$. The chemical potential is the derivative of the free energy with respect to composition, $\mu(x) = dg/dx$. Since $U(x) \propto -\mu(x)$, the slope of the voltage curve is related to the second derivative of the free energy: $dU/dx \propto -d^2g/dx^2$.

A useful model to understand this is the **regular solution model**, which describes the free energy of a [binary mixture](@entry_id:174561) (e.g., lithium and vacancies on a lattice) :

$$ g(x) = RT\left[x\ln x + (1-x)\ln(1-x)\right] + \Omega x(1-x) $$

Here, the first term is the ideal entropy of mixing contribution to the free energy, and the second term is an enthalpic term describing the interaction between lithium atoms and vacancies, with $\Omega$ as the [interaction parameter](@entry_id:195108). The chemical potential and corresponding electrode potential can be derived as:

$$ \mu_{\mathrm{Li}}(x) = \frac{dg}{dx} = RT \ln\left(\frac{x}{1-x}\right) + \Omega(1-2x) $$
$$ U(x) = -\frac{\mu_{\mathrm{Li}}(x)}{F} = -\frac{1}{F}\left[RT \ln\left(\frac{x}{1-x}\right) + \Omega(1-2x)\right] $$

This model provides profound insight into the shape of the OCV curve . The stability of the solid solution is determined by the convexity of the free energy function, $d^2g/dx^2 > 0$.
*   **Monotonic OCV Curve**: If interactions are weakly repulsive or attractive ($\Omega \lt 2RT$), the entropic term dominates, making the free energy function $g(x)$ globally convex. The chemical potential changes smoothly and monotonically with composition, resulting in a sloped OCV-SOC curve.
*   **OCV Plateau**: If repulsive interactions are strong ($\Omega \gt 2RT$), the enthalpic term causes the free energy function $g(x)$ to become non-convex (concave) in a certain composition range. A single-phase material in this range is unstable and will spontaneously separate into two distinct phases: a lithium-poor phase of composition $x_{\alpha}$ and a lithium-rich phase of composition $x_{\beta}$. Throughout this two-[phase coexistence](@entry_id:147284) region, the chemical potential of lithium is constant, fixed by the common tangent to the free energy curve at $x_{\alpha}$ and $x_{\beta}$. This constant chemical potential translates directly into a constant voltage, or a **[voltage plateau](@entry_id:1133882)**, in the OCV-SOC curve.

For an electrode with an overall stoichiometry $\bar{x}$ that falls within the two-phase region ($x_{\alpha} \lt \bar{x} \lt x_{\beta}$), the fraction of each phase can be determined by the **[lever rule](@entry_id:136701)**, derived from mass balance . The fraction of the lithium-rich phase, $f_{\beta}$, is given by:

$$ f_{\beta} = \frac{\bar{x} - x_{\alpha}}{x_{\beta} - x_{\alpha}} $$

The length of this plateau as a fraction of the total usable SOC range of the electrode is determined by the stoichiometric width of the two-phase region relative to the total operating window:

$$ \Delta \mathrm{SOC}_{\text{plateau}} = \frac{x_{\beta} - x_{\alpha}}{x_{\max} - x_{\min}} $$

This explains the very flat voltage profiles of materials like Lithium Iron Phosphate (LFP), which operate via a two-phase [reaction mechanism](@entry_id:140113).

### Complexities and Non-Ideal Behavior

The idealized picture of the OCV-SOC relationship is modulated by several real-world factors that are critical for accurate [battery modeling](@entry_id:746700).

#### Temperature Dependence and the Entropic Coefficient

The OCV is a function not only of SOC but also of temperature. This dependence is governed by the entropy change of the cell reaction. From the fundamental [thermodynamic identity](@entry_id:142524) $dG = -S dT + V dp$, we can derive the Gibbs-Helmholtz relation for an [electrochemical cell](@entry_id:147644). This relates the change in OCV with temperature to the partial molar entropy change of the reaction, $\Delta \bar{S}$. For a [half-cell reaction](@entry_id:263894), this relationship, often called the **entropic coefficient**, is :

$$ \left(\frac{\partial U}{\partial T}\right)_{p, \mathrm{SOC}} = \frac{\Delta_{r}\bar{S}}{F} $$

where $\Delta_{r}\bar{S}$ is the partial molar entropy change for the intercalation reaction (products minus reactants). The [entropic coefficient](@entry_id:1124550), which itself varies with SOC, is a crucial parameter. In battery management systems, it is used to correct OCV-based SOC estimates for temperature variations . In thermal simulations, it is used to calculate the reversible (entropic) heat generated or absorbed during operation, $q_{\mathrm{rev}} = I \cdot T \cdot (\partial U / \partial T)$.

#### OCV Hysteresis

In many [battery materials](@entry_id:1121422), particularly those that undergo first-order phase transformations, the OCV measured during charging (lithiation) is slightly different from the OCV measured during discharging (delithiation), even when measurements are taken slowly to approximate equilibrium. This rate-independent phenomenon is known as **OCV hysteresis**.

This is not a [kinetic overpotential](@entry_id:1126930) effect. Instead, it arises from path-dependent thermodynamics within the solid state . The Gibbs free energy of the active material can be a function of not only composition ($x$) but also [internal state variables](@entry_id:750754) like mechanical strain ($\varepsilon$) and microstructure ($\xi$). During the large volume changes associated with lithiation and delithiation, the material may follow different, path-dependent metastable states. For example, the sequence of phase [nucleation and growth](@entry_id:144541) can be different on insertion versus extraction. This leads to two distinct free energy paths, $g_{\mathrm{in}}^{*}(x)$ and $g_{\mathrm{out}}^{*}(x)$.

The resulting OCV paths, $U_{\mathrm{in}}(x)$ and $U_{\mathrm{out}}(x)$, will also be different. The [voltage hysteresis](@entry_id:1133881), $\Delta U(x) = U_{\mathrm{out}}(x) - U_{\mathrm{in}}(x)$, originates from the dependence of the chemical potential on these different path-dependent internal states. Advanced battery models must often account for this phenomenon by storing and using two separate OCV-SOC maps—one for charge and one for discharge—to achieve high fidelity.

### The OCV-SOC Relationship in Battery Diagnostics and Aging

The OCV-SOC curve is not static over a battery's lifetime; it evolves as the cell degrades. Analyzing these changes provides a powerful, non-invasive tool for diagnosing the State of Health (SOH) and identifying the underlying degradation mechanisms. It is crucial to recognize that aging primarily alters the mapping between the macroscopic SOC and the microscopic electrode stoichiometries, rather than altering the fundamental [potential functions](@entry_id:176105) $U_p(x)$ and $U_n(x)$ themselves [@problem_id:3934079, @problem_id:3934041].

Two primary degradation modes have distinct signatures in the OCV-SOC curve :

1.  **Loss of Lithium Inventory (LLI)**: This occurs when cyclable lithium becomes trapped in irreversible side reactions, most commonly in the formation and growth of the [solid-electrolyte interphase](@entry_id:159806) (SEI) on the anode. This reduces the total amount of lithium available to shuttle between the electrodes. Because LLI does not change the amount of active material, it does not alter how much charge is needed to change an electrode's stoichiometry by a given amount. Instead, it creates an offset in the relative lithiation of the two electrodes. This manifests as a **horizontal shift** or re-phasing of the full-cell OCV-SOC curve along the SOC axis.

2.  **Loss of Active Material (LAM)**: This involves the physical or chemical deactivation of electrode material, rendering it unable to store lithium. This can occur at either the positive or negative electrode. LAM reduces the number of available host sites ($n_{\mathrm{host}}$). Consequently, a smaller amount of charge transfer is needed to produce the same change in the [stoichiometry](@entry_id:140916) ($x$) of the *remaining* active material. This causes the OCV-SOC curve to become steeper, leading to a **compression or rescaling** of the curve along the SOC axis.

By carefully measuring the OCV-SOC curve at different points in a cell's life and analyzing its shift and scaling, automated diagnostic algorithms can deconvolve these degradation modes, providing critical insights into the battery's health and remaining useful life. The OCV-SOC relationship thus transcends its role as a simple [state estimator](@entry_id:272846), becoming a rich source of information about the internal state and history of the battery.