## Introduction
Electrodialysis (ED) is a powerful, membrane-based electrochemical separation technology used to transport ions from one solution to another under the influence of an electric potential. Its unique ability to selectively remove, concentrate, or separate ionic species makes it indispensable in a wide array of industrial and environmental applications. While its use in desalination is well-known, a deeper understanding of its underlying principles is necessary to appreciate its full versatility and navigate its operational challenges. This article addresses this need by providing a structured journey from fundamental theory to practical application.

The following chapters will guide you through the complete landscape of electrodialysis. In **Principles and Mechanisms**, we will dissect the core of the ED system, examining [ion transport](@entry_id:273654) within a cell pair, the critical role of [ion-exchange membranes](@entry_id:267330), and performance-limiting phenomena such as [concentration polarization](@entry_id:266906) and [water splitting](@entry_id:156592). Building on this foundation, **Applications and Interdisciplinary Connections** will explore the technology's real-world impact, from energy-efficient [water treatment](@entry_id:156740) and resource recovery to its gentle application in food processing and its advanced role in [chemical synthesis](@entry_id:266967). Finally, **Hands-On Practices** will provide an opportunity to apply these concepts to solve quantitative problems, solidifying your understanding of ED system design and performance analysis.

## Principles and Mechanisms

### The Fundamental Electrodialysis Unit: The Cell Pair

The operational heart of an electrodialysis (ED) system is a structure known as the **electrodialysis stack**, which is composed of a series of repeating [fundamental units](@entry_id:148878). This basic unit, termed a **cell pair**, consists of a cation-exchange membrane (CEM), an [anion-exchange membrane](@entry_id:266578) (AEM), and the fluid compartments formed between them. To understand the entire process, we must first analyze the transport phenomena within a single cell pair.

Imagine a central compartment containing a salt solution, such as magnesium sulfate ($\text{MgSO}_4$), which dissociates into magnesium cations ($\text{Mg}^{2+}$) and sulfate [anions](@entry_id:166728) ($\text{SO}_4^{2-}$). This compartment is bounded on one side by an AEM and on the other by a CEM. The entire assembly is placed within an electric field, established by an anode (positive electrode) and a cathode (negative electrode) situated at the far ends of the stack.

Under the influence of this electric field, cations are driven toward the negatively charged cathode, and anions are driven toward the positively charged anode. The key to the separation process lies in the [selective permeability](@entry_id:153701) of the membranes.
*   The $\text{Mg}^{2+}$ ions, moving towards the cathode, encounter the CEM. As a membrane permeable to cations, it allows the $\text{Mg}^{2+}$ to pass through into the adjacent compartment.
*   Simultaneously, the $\text{SO}_4^{2-}$ ions, moving in the opposite direction toward the anode, encounter the AEM. The AEM is permeable to anions, so it allows the $\text{SO}_4^{2-}$ to pass through into the compartment on the other side.

The net result is that the central compartment is progressively depleted of both positive and negative ions. This desalinated or deionized stream is known as the **diluate**. Conversely, the adjacent compartments, which receive these migrating ions, become more concentrated. These streams are collectively referred to as the **concentrate** or brine [@problem_id:1556604]. An ED stack is constructed by repeating this alternating AEM/CEM pattern many times, creating a series of parallel diluate and concentrate channels. The ingenuity of this design is that a single applied electric field can simultaneously deionize dozens or hundreds of diluate streams.

### The Heart of Selectivity: Ion-Exchange Membranes

The remarkable ability of an ED system to separate ions from a solution hinges entirely on the properties of the **[ion-exchange membranes](@entry_id:267330) (IEMs)**. These are not simple physical filters; their selectivity is chemical in nature, arising from their unique molecular structure.

An IEM consists of a durable, water-insoluble polymer backbone to which a high density of charged [functional groups](@entry_id:139479) are covalently bonded. These charges are fixed within the polymer matrix and are responsible for the membrane's selective transport properties. There are two primary types of IEMs used in electrodialysis:

*   **Anion-Exchange Membranes (AEMs)** are designed to be permeable to [anions](@entry_id:166728). To achieve this, their polymer backbone is functionalized with fixed positive charges. The most common [functional groups](@entry_id:139479) used for this purpose are **quaternary ammonium groups** (e.g., $-NR_3^+$, where $R$ is an alkyl group). These groups maintain a permanent positive charge across a wide pH range, electrostatically attracting mobile [anions](@entry_id:166728) from the solution into the membrane while repelling mobile cations [@problem_id:1556608].

*   **Cation-Exchange Membranes (CEMs)** are, conversely, permeable to cations. This is accomplished by incorporating fixed negative charges into the polymer matrix. Typical functional groups include **sulfonic acid groups** ($-SO_3^-$) or **carboxylic acid groups** ($-COO^-$). These groups are negatively charged under most operating conditions and therefore attract mobile cations while repelling mobile anions.

This phenomenon, where the fixed charges on the membrane govern the partitioning of mobile ions between the bulk solution and the membrane phase, is known as **Donnan exclusion**, named after Frederick G. Donnan. The principle can be understood both qualitatively and quantitatively. Qualitatively, the dense population of fixed charges within the membrane matrix creates an electrostatic barrier. For a CEM with fixed negative charges, any mobile anions (called **co-ions**) that attempt to enter the membrane are strongly repelled. Mobile cations (called **counter-ions**), however, are attracted into the membrane to maintain local [electroneutrality](@entry_id:157680). Consequently, the concentration of counter-ions inside the membrane is much higher than that of co-ions, making the membrane far more conductive to counter-ions.

We can quantify this effect by considering the equilibrium between an external salt solution (phase $s$) and the membrane (phase $m$). At equilibrium, the electrochemical potential of any mobile ion species must be equal in both phases. For an ideal system, this leads to the **Donnan product relation**:
$c_+^m c_-^m = c_+^s c_-^s$
where $c_+$ and $c_-$ are the molar concentrations of the cation and anion, respectively.

Within the membrane, the condition of [electroneutrality](@entry_id:157680) must also be satisfied. For a CEM with a fixed negative charge concentration of $C_{fixed}$, this means the sum of positive charges must balance the sum of negative charges:
$z_+ c_+^m + z_- c_-^m + z_{fixed} C_{fixed} = 0$
For a simple 1:1 salt like NaCl ($z_+ = +1, z_- = -1$) and a CEM ($z_{fixed} = -1$), this simplifies to:
$c_+^m - c_-^m = C_{fixed}$

Combining these equations allows us to solve for the concentration of the co-ion (anion) inside the membrane. If the external solution has a salt concentration $C_{salt}$, so that $c_+^s = c_-^s = C_{salt}$, the co-ion concentration inside the membrane, $c_-^m$, is given by the positive root of the quadratic equation $c_-^m (c_-^m + C_{fixed}) = C_{salt}^2$:
$c_-^m = \frac{-C_{fixed} + \sqrt{C_{fixed}^2 + 4 C_{salt}^2}}{2}$

To appreciate the power of Donnan exclusion, consider a typical CEM with a fixed charge concentration of $C_{fixed} = 1.80 \, \text{mol/L}$ in equilibrium with a $0.0500 \, \text{mol/L}$ NaCl solution. The concentration of the chloride co-ion inside the membrane would be approximately $1.39 \times 10^{-3} \, \text{mol/L}$. The effectiveness of the exclusion can be expressed by the **co-ion exclusion coefficient**, the ratio of the co-ion concentration inside the membrane to that in the bulk solution. In this case, the coefficient is $1.39 \times 10^{-3} / 0.0500 \approx 0.0278$ [@problem_id:1556595]. This means the concentration of the rejected ion inside the membrane is less than 3% of its concentration in the external solution, demonstrating the high degree of selectivity achieved.

### The Electrodialysis Stack and System-Level Processes

While the cell pair is the functional unit, a practical ED system involves a stack of many such pairs, along with components that manage fluid flow and electrical input.

**Electrode Compartments and Reactions**

An ED stack is bounded by an anode and a cathode, which are housed in dedicated **electrode compartments**. A common misconception is that the ions of the salt being removed (e.g., Na⁺ and Cl⁻) are consumed at these electrodes. In most aqueous desalination applications, this is not the case. The concentrations are typically too low, and the electrochemical potentials are unfavorable for the direct deposition of [alkali metals](@entry_id:139133) or the oxidation of halides.

Instead, the primary electrochemical reactions occurring at the electrodes involve the [electrolysis](@entry_id:146038) of water itself [@problem_id:1556617].
*   At the **anode** (oxidation): $2\text{H}_2\text{O}(l) \rightarrow \text{O}_2(g) + 4\text{H}^{+}(aq) + 4e^{-}$
*   At the **cathode** (reduction): $2\text{H}_2\text{O}(l) + 2e^{-} \rightarrow \text{H}_2(g) + 2\text{OH}^{-}(aq)$

These reactions are crucial for completing the electrical circuit, but they produce significant changes in the local [water chemistry](@entry_id:148133). The anode compartment becomes acidic due to the production of protons ($\text{H}^+$), while the cathode compartment becomes alkaline due to the production of hydroxide ions ($\text{OH}^-$). This pH shift can cause serious operational problems. For instance, if the feed water contains divalent cations like magnesium ($\text{Mg}^{2+}$) or calcium ($\text{Ca}^{2+}$), the increased pH in the cathode compartment can cause the [precipitation](@entry_id:144409) of their hydroxides (e.g., $\text{Mg}(\text{OH})_2$), a phenomenon known as **scaling**. This solid scale can coat the electrode and nearby membranes, increasing electrical resistance and impeding flow.

The risk of scaling can be quantified. The production rate of $\text{OH}^-$ is directly proportional to the current, according to Faraday's laws. For a closed cathode compartment, the hydroxide concentration $[\text{OH}^-]$ increases over time $t$ as $[\text{OH}^-](t) = It / (FV)$, where $V$ is the compartment volume and $F$ is the Faraday constant. Precipitation begins when the ion product $[\text{Mg}^{2+}][\text{OH}^{-}]^2$ exceeds the [solubility product constant](@entry_id:143661), $K_{sp}$. For a given initial magnesium concentration, one can calculate the critical $[\text{OH}^-]$ and thus the maximum operating time before scaling begins. This time can be surprisingly short, often just a matter of seconds or minutes, highlighting the severity of the issue [@problem_id:1556635]. To mitigate this, most ED systems use a separate **electrode rinse solution**, which is circulated through the electrode compartments to flush away reaction products and control pH, preventing [precipitation](@entry_id:144409) and gas buildup.

**The Role of Spacers**

Between each pair of membranes, thin polymer meshes known as **spacers** are inserted. These seemingly simple components perform several critical functions that are essential for the stable and efficient operation of the stack [@problem_id:1556632]:
1.  **Mechanical Support**: Spacers maintain a fixed, uniform distance between the membranes, preventing them from touching or collapsing under pressure gradients. This ensures that the flow channels have a consistent thickness, which is vital for uniform current distribution and predictable hydraulic performance.
2.  **Flow Channel Definition**: The structure of the spacer defines the path that the diluate and concentrate streams follow as they move through the stack.
3.  **Enhanced Mass Transfer**: Spacers are designed not for smooth, laminar flow, but to intentionally induce turbulence and eddies. This mixing action disrupts the formation of stagnant [boundary layers](@entry_id:150517) at the membrane surface, promoting the transport of ions from the bulk solution to the membrane. As we will see, this is crucial for mitigating a key performance limitation known as [concentration polarization](@entry_id:266906).

### Quantifying Performance and Operational Limits

The performance of an electrodialysis system can be characterized by several key parameters that relate the operational inputs (current, voltage) to the desired output (salt removal).

**Desalination Rate and Current Efficiency**

The rate of ion removal is governed by Faraday's law of electrolysis, which states that the [amount of substance](@entry_id:145418) transformed at an electrode is proportional to the total electric charge passed. In electrodialysis, this principle applies to the transport of ions across membranes. For a salt composed of ions with valence $z$, the number of moles of salt removed from the diluate stream is proportional to the charge passed.

In a stack containing $N$ cell pairs, the ions cross $N$ membranes of each type in series. Thus, the total rate of salt removal is amplified by the number of cell pairs. The total moles of salt, $n_{removed}$, removed from the diluate over a time $t$ at a constant current $I$ can be expressed as:
$n_{removed} = \frac{\eta I t N}{F}$
Here, we have considered a monovalent salt like NaCl ($z=1$) for simplicity, and introduced a crucial parameter, the **[current efficiency](@entry_id:144989)** ($\eta$). The [current efficiency](@entry_id:144989) is a dimensionless factor (typically between 0.8 and 0.95) that accounts for the fact that not all of the current contributes to the desired salt transport. Some current may be lost to parallel phenomena like the transport of co-ions (due to imperfect membrane selectivity), water transport ([electro-osmosis](@entry_id:189291)), or transport through manifold leaks.

This relationship allows us to predict the performance of an ED unit. For example, in a batch desalination process with a diluate volume $V_d$ and initial concentration $c_0$, the final concentration $c_f$ after operating for time $t$ is:
$c_f = c_0 - \frac{\eta I t N}{F V_d}$
This equation forms the basis for designing and controlling ED processes [@problem_id:1556645].

**Concentration Polarization and Limiting Current Density**

While one might assume that simply increasing the applied current would proportionally increase the desalination rate, there is a fundamental transport limitation that prevents this. This limitation is known as **[concentration polarization](@entry_id:266906)**.

As ions are driven from the bulk of the diluate stream towards the membrane surface, a **depletion boundary layer** forms adjacent to the membrane. Within this layer, the ion concentration is lower than in the bulk solution because the rate of [electromigration](@entry_id:141380) towards the membrane can exceed the rate at which diffusion and convection can replenish the ions from the bulk. As the current is increased, this depletion becomes more severe, and the ion concentration at the membrane-solution interface, $c_m$, drops.

Eventually, a point is reached where $c_m$ approaches zero. At this point, the supply of ions to the membrane surface becomes the [rate-limiting step](@entry_id:150742) for the entire process. The current density (current per unit membrane area, $i=I/A$) at which this occurs is called the **[limiting current density](@entry_id:274733)**, or $i_{lim}$.

The behavior of an ED system is often visualized using a current-voltage ($I-V$) or current density-voltage ($i-V$) curve, which typically displays three distinct regions [@problem_id:1556590]:
1.  **Ohmic Region**: At low current densities ($i \lt i_{lim}$), the voltage drop across the cell pair is primarily due to the electrical resistance of the solutions and membranes, and it increases linearly with current, following Ohm's law ($V=IR_{cell}$).
2.  **Limiting Region**: As the current density approaches $i_{lim}$, the depletion of ions in the boundary layer causes a sharp increase in electrical resistance. The $I-V$ curve flattens, and a large increase in voltage is required to achieve a small increase in current.
3.  **Over-Limiting Region**: If the voltage is increased further such that $i \gt i_{lim}$, the current begins to rise again. This additional current is not carried by the salt ions (as they are already transport-limited) but by another mechanism, which we will discuss next.

The value of the [limiting current density](@entry_id:274733) is not a constant; it depends on the system's hydrodynamics, temperature, and most importantly, the bulk salt concentration in the diluate, $c_b$. For a given stack geometry and flow rate, the [limiting current density](@entry_id:274733) is approximately directly proportional to the diluate concentration:
$i_{lim} \propto c_b$
This relationship is critical because as desalination proceeds and $c_b$ decreases, the [limiting current density](@entry_id:274733) also decreases, making the process progressively less efficient [@problem_id:1556636].

**Operating in the Over-Limiting Region: Water Splitting**

Operating an ED system at current densities exceeding $i_{lim}$ is generally undesirable but provides insight into another fundamental electrochemical process: **[water splitting](@entry_id:156592)**. When the supply of salt ions to the membrane surface is exhausted, the applied electric field becomes strong enough to dissociate water molecules at the membrane-solution interface into protons and hydroxide ions:
$\text{H}_2\text{O} \rightleftharpoons \text{H}^{+} + \text{OH}^{-}$

These newly generated ions can then carry the "over-limiting" current. The consequences of this phenomenon depend on the type of membrane at which it occurs [@problem_id:1556639].
*   At an **AEM/diluate interface**, the generated $\text{OH}^-$ ions (anions) are transported through the AEM into the concentrate stream. The $\text{H}^+$ ions (cations), however, are repelled by the AEM's fixed positive charges and are forced back into the diluate stream. This leads to an **acidification (decrease in pH)** of the diluate.
*   At a **CEM/diluate interface**, the opposite occurs. The generated $\text{H}^+$ ions pass through the CEM, while the $\text{OH}^-$ ions are rejected into the diluate, causing an **alkalinization (increase in pH)**.

In many systems, [water splitting](@entry_id:156592) is found to occur more readily at the AEM interface than at the CEM interface. The net effect of operating in the over-limiting region is therefore often a significant decrease in the pH of the product water (diluate). This not only alters the quality of the product but can also exacerbate membrane fouling and scaling issues in the adjacent concentrate compartments. For these reasons, ED systems are typically designed to operate below the [limiting current density](@entry_id:274733) to maintain high efficiency and operational stability.