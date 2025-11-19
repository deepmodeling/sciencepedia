## Introduction
Electrolysis of molten salts is a powerful electrochemical technique that uses electrical energy to drive chemical reactions that would not otherwise occur, forming the backbone of several critical industrial processes. Its primary significance lies in the production of highly reactive metals, such as aluminum and sodium, which cannot be isolated from their compounds using more conventional methods like electrolysis in [aqueous solutions](@entry_id:145101). The core problem this method overcomes is the presence of water, which would be preferentially reduced over these reactive metals. By creating an ionically conductive medium at high temperatures and in the complete absence of water, [molten salt electrolysis](@entry_id:269101) unlocks the path to producing some of modern society's most essential materials.

This article will guide you through the core concepts of this fascinating process. In **Principles and Mechanisms**, you will learn about the behavior of molten salts as [electrolytes](@entry_id:137202), the fundamental [redox reactions](@entry_id:141625) at the electrodes, and the quantitative relationships defined by Faraday's laws and thermodynamics. The second chapter, **Applications and Interdisciplinary Connections**, explores cornerstone industrial processes like aluminum and sodium production and reveals connections to materials science, engineering, and physics. Finally, **Hands-On Practices** will provide an opportunity to apply your knowledge to solve practical problems related to electrochemical calculations and process efficiency.

## Principles and Mechanisms

### The Nature of Molten Salts as Electrolytes

Electrolysis is a process that uses electrical energy to drive a non-spontaneous chemical reaction. A fundamental prerequisite for electrolysis is the presence of an electrolyte—a substance that contains mobile ions and can therefore conduct electricity. While [aqueous solutions](@entry_id:145101) of salts are common [electrolytes](@entry_id:137202), many important industrial processes, particularly in electrometallurgy, rely on **molten salts**.

An ionic compound in its solid, crystalline state, such as sodium chloride ($\text{NaCl}$), consists of ions locked in a fixed crystal lattice. These ions can vibrate but are not free to move, rendering the solid an electrical insulator. However, when heated above its melting point, the ionic lattice breaks down. The resulting liquid phase is a disordered, fluid medium composed of mobile cations (e.g., $\text{Na}^{+}$) and [anions](@entry_id:166728) (e.g., $\text{Cl}^{-}$). This mobility of charged particles allows the molten salt to conduct electricity, making it a suitable electrolyte for [electrolysis](@entry_id:146038).

An [electrolytic cell](@entry_id:145661) for [molten salt electrolysis](@entry_id:269101) consists of three primary components:
1.  A container holding the molten salt electrolyte.
2.  Two electrodes, typically made of an inert material like graphite or platinum, immersed in the molten salt.
3.  An external direct current (DC) power supply that connects to the two electrodes.

The power supply creates an electric [potential difference](@entry_id:275724) between the electrodes. The electrode connected to the positive terminal of the supply becomes the **anode**, and the electrode connected to the negative terminal becomes the **cathode**.

### Ion Migration and Electrode Reactions

The electric field established by the external power source within the molten salt exerts a force on the mobile ions. This force compels the ions to migrate in a directed manner. Positively charged cations are attracted to the negatively charged cathode, while negatively charged [anions](@entry_id:166728) are attracted to the positively charged anode. This directed ion flow constitutes the electric current within the electrolyte. [@problem_id:1557405]

Upon reaching the electrodes, the ions undergo [redox reactions](@entry_id:141625).
*   At the **cathode**, cations accept electrons from the electrode and are **reduced**. The general form of a cathodic reaction is the deposition of a metal:
    $M^{n+}(\text{l}) + ne^{-} \rightarrow M(\text{l} \text{ or } \text{s})$
*   At the **anode**, [anions](@entry_id:166728) release electrons to the electrode and are **oxidized**. The general form of an anodic reaction is the formation of a non-metal element:
    $2X^{m-}(\text{l}) \rightarrow X_2(\text{g}) + 2me^{-}$

For example, in the electrolysis of molten lead(II) bromide ($\text{PbBr}_2$), lead(II) cations ($\text{Pb}^{2+}$) migrate to the cathode, and bromide anions ($\text{Br}^{-}$) migrate to the anode. At the electrodes, the following [half-reactions](@entry_id:266806) occur:

Cathode (Reduction): $\text{Pb}^{2+}(\text{l}) + 2e^{-} \rightarrow \text{Pb}(\text{l})$
Anode (Oxidation): $2\text{Br}^{-}(\text{l}) \rightarrow \text{Br}_{2}(\text{g}) + 2e^{-}$

Since the operating temperature is above the [melting point](@entry_id:176987) of lead, the product at the cathode is a silvery molten metal. The product at the anode is bromine, which is a reddish-brown gas at these temperatures. [@problem_id:1557399]

A particularly instructive case is the electrolysis of molten [metal hydrides](@entry_id:182213), such as lithium hydride ($\text{LiH}$) or calcium hydride ($\text{CaH}_2$). In these salts, the anion is the hydride ion ($\text{H}^{-}$). Consequently, during electrolysis, the hydride anions migrate to the anode to be oxidized, producing hydrogen gas. This is a crucial distinction from the electrolysis of [aqueous solutions](@entry_id:145101) or acids, where hydrogen gas is typically produced at the cathode from the reduction of $\text{H}^{+}$ or water.

For molten lithium hydride [@problem_id:1557398]:
Cathode: $\text{Li}^{+}(\text{l}) + e^{-} \to \text{Li}(\text{l})$
Anode: $2\text{H}^{-}(\text{l}) \to \text{H}_{2}(\text{g}) + 2e^{-}$

Similarly, for molten calcium hydride [@problem_id:1557429]:
Cathode: $\text{Ca}^{2+}(\text{l}) + 2e^{-} \to \text{Ca}(\text{l})$
Anode: $2\text{H}^{-}(\text{l}) \to \text{H}_{2}(\text{g}) + 2e^{-}$

These examples underscore the fundamental principle: oxidation always occurs at the anode, and reduction always occurs at the cathode, regardless of the specific chemical species involved.

### Quantitative Principles: Faraday's Laws of Electrolysis

The relationship between the amount of electricity passed through an [electrolytic cell](@entry_id:145661) and the quantity of [chemical change](@entry_id:144473) that occurs is described by **Faraday's Laws of Electrolysis**. These laws provide the quantitative foundation for electrochemical calculations.

The total electric charge ($Q$) passed through the cell is the product of the constant current ($I$) and the duration of time ($t$):
$$Q = I \times t$$
where $Q$ is in coulombs (C), $I$ is in amperes (A, or C/s), and $t$ is in seconds (s).

The fundamental unit of charge in electrochemistry is the charge of a single electron. For macroscopic calculations, we use **Faraday's constant ($F$)**, which is the total charge of one mole of electrons:
$$F \approx 96485 \text{ C/mol}$$

The number of moles of electrons ($n_{e^{-}}$) transferred during electrolysis is therefore directly proportional to the total charge passed:
$$n_{e^{-}} = \frac{Q}{F} = \frac{I \times t}{F}$$

This quantity, $n_{e^{-}}$, is the central link between the electrical measurements ($I, t$) and the [chemical stoichiometry](@entry_id:137450). The [half-reactions](@entry_id:266806) dictate the molar relationship between the electrons transferred and the substances produced. For instance, in the reduction of a rubidium ion, $\text{Rb}^{+} + e^{-} \to \text{Rb}$, one mole of electrons is required to produce one mole of rubidium metal. This allows for the direct calculation of the number of electrons involved in producing a given mass of product [@problem_id:1557376].

The power of Faraday's laws lies in their ability to connect the processes at the two electrodes. The number of electrons released at the anode must equal the number of electrons consumed at the cathode. This principle of electron conservation allows us to relate the amount of product formed at one electrode to the amount formed at the other.

Consider the [electrolysis](@entry_id:146038) of molten tin(II) chloride ($\text{SnCl}_2$) to produce metallic tin [@problem_id:1557422].
Cathode: $\text{Sn}^{2+}(\text{l}) + 2e^{-} \rightarrow \text{Sn}(\text{l})$
Anode: $2\text{Cl}^{-}(\text{l}) \rightarrow \text{Cl}_{2}(\text{g}) + 2e^{-}$

The stoichiometry shows that for every 2 moles of electrons transferred, 1 mole of $\text{Sn}$ is deposited and 1 mole of $\text{Cl}_2$ is generated. Therefore, the molar amounts of the products are equal: $n_{\text{Sn}} = n_{\text{Cl}_2}$. If one measures the mass of tin produced, one can calculate the moles of tin, which in turn gives the moles of chlorine gas evolved, from which its volume can be calculated using the ideal gas law ($PV=nRT$) [@problem_id:1557422] [@problem_id:1557377].

### Thermodynamics and Selectivity in Electrolysis

The [electrolysis](@entry_id:146038) of a molten salt is the decomposition of a stable compound into its elements, a thermodynamically non-[spontaneous process](@entry_id:140005). The minimum theoretical voltage required to drive this reaction is known as the **[decomposition potential](@entry_id:275442) ($V_{\text{decomp}}$)**. This potential is directly related to the standard Gibbs free energy change ($\Delta G^{\circ}$) for the overall cell reaction:
$$\Delta G^{\circ} = -nFE^{\circ}_{\text{cell}}$$
where $n$ is the number of moles of electrons transferred in the balanced overall reaction and $E^{\circ}_{\text{cell}}$ is the [standard cell potential](@entry_id:139386). For a [non-spontaneous reaction](@entry_id:137593), $\Delta G^{\circ} > 0$, which implies that $E^{\circ}_{\text{cell}}$ is negative. The [decomposition potential](@entry_id:275442) is the voltage that must be applied to overcome this thermodynamic barrier and is equal in magnitude to the cell potential:
$$V_{\text{decomp}} = -E^{\circ}_{\text{cell}} = E^{\circ}_{\text{anode, red}} - E^{\circ}_{\text{cathode, red}}$$
where the potentials are given as standard reduction potentials.

When the molten electrolyte contains a mixture of different ions, multiple reduction and oxidation reactions may be possible. In such cases, the principle of selective electrolysis applies.
*   At the **cathode**, the cation that is easiest to reduce will react first. This corresponds to the cation whose reduction [half-reaction](@entry_id:176405) has the **less negative (or more positive) [reduction potential](@entry_id:152796)**.
*   At the **anode**, the anion that is easiest to oxidize will react first. This corresponds to the anion whose oxidation half-reaction has the **more positive oxidation potential** (or, equivalently, whose corresponding reduction half-reaction has the less positive [reduction potential](@entry_id:152796)).

For example, in a molten mixture of $\text{KCl}$ and $\text{CaCl}_2$, both $\text{K}^{+}$ and $\text{Ca}^{2+}$ are present. Comparing their standard reduction potentials ($E^{\circ}_{\text{Ca}^{2+}/\text{Ca}} \approx -2.87 \text{ V}$ and $E^{\circ}_{\text{K}^{+}/\text{K}} \approx -2.93 \text{ V}$), we see that the potential for calcium is less negative. Therefore, $\text{Ca}^{2+}$ ions will be preferentially reduced at the cathode to form calcium metal [@problem_id:1557409].

The situation becomes more complex under non-standard conditions, where ion activities (the effective concentrations) are not unity and the temperature is elevated. In these cases, the **Nernst equation** must be used to calculate the actual potential for each [half-reaction](@entry_id:176405) under the specific operating conditions:
$$E = E^{\circ} - \frac{RT}{nF}\ln Q$$
Here, $R$ is the ideal gas constant, $T$ is the absolute temperature, and $Q$ is the [reaction quotient](@entry_id:145217), which depends on the activities of the species involved.

A comprehensive analysis using the Nernst equation allows for precise prediction of the cell's behavior. For instance, in a complex molten salt bath containing $\text{Ca}^{2+}$, $\text{K}^{+}$, $\text{Cl}^{-}$, and $\text{F}^{-}$ ions at 1100 K with known activities, one must calculate the Nernst potential for all possible cathodic and anodic reactions. The actual cathode reaction will be the reduction with the highest (least negative) calculated potential, and the actual anode reaction will be the oxidation corresponding to the lowest (least positive) calculated [reduction potential](@entry_id:152796). The minimum decomposition voltage for the cell is then the difference between these actual [anode and cathode](@entry_id:262146) potentials. This rigorous approach is essential for designing and optimizing industrial processes [@problem_id:1557392].

### Practical Aspects: Operating Voltage in Industrial Cells

The thermodynamic [decomposition potential](@entry_id:275442) represents an ideal minimum. In any real-world industrial [electrolytic cell](@entry_id:145661), the actual **operating voltage ($V_{\text{app}}$)** required is significantly higher. This additional voltage is needed to overcome two main factors: kinetic limitations and [electrical resistance](@entry_id:138948).

1.  **Overpotential ($\eta$)**: The [decomposition potential](@entry_id:275442) is a thermodynamic value calculated at equilibrium (zero current). To drive the reaction at a finite rate (i.e., to achieve a non-zero current), an additional voltage, known as **[overpotential](@entry_id:139429)**, must be applied. This extra potential provides the activation energy needed to overcome kinetic barriers at the electrode surfaces. Both the [anode and cathode](@entry_id:262146) have their own characteristic overpotentials ($\eta_a$ and $\eta_c$), which depend on the [current density](@entry_id:190690), temperature, and electrode materials. For example, the evolution of a gas like chlorine at a [graphite anode](@entry_id:269569) requires a significant anodic overpotential.

2.  **Ohmic Drop ($IR_{\text{int}}$)**: The molten salt electrolyte, electrodes, and electrical connectors are not perfect conductors; they possess a finite [internal resistance](@entry_id:268117) ($R_{\text{int}}$). According to Ohm's law, driving a current ($I$) through this resistance results in a voltage drop, $V_{\text{ohmic}} = I \times R_{\text{int}}$. This voltage does not contribute to the chemical reaction but is instead dissipated as heat. In industrial cells that operate at extremely high currents (tens of thousands of amperes), the [ohmic drop](@entry_id:272464) can be the largest single contributor to the total required voltage.

The total applied voltage is the sum of the thermodynamic requirement and these two loss terms:
$$V_{\text{app}} = V_{\text{decomp}} + \eta_a + |\eta_c| + IR_{\text{int}}$$
For example, in an industrial Downs cell for sodium production, the theoretical [decomposition potential](@entry_id:275442) might be around 4.1 V. However, when accounting for an anodic overpotential of 0.55 V, a cathodic overpotential of 0.28 V, and an [ohmic drop](@entry_id:272464) of over 2.0 V due to the high current, the actual operating voltage is around 7.0 V. This demonstrates that practical engineering considerations, especially managing internal resistance, are paramount for the efficient operation of large-scale electrolytic processes [@problem_id:1557401].