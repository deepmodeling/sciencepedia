## Introduction
The neuronal membrane is the fundamental computational element of the nervous system. This thin, fluid barrier, less than 10 nanometers thick, is the stage upon which all electrical signaling, from the subtlest synaptic whisper to the propagating shout of an action potential, takes place. But how do simple biological materials—lipids and proteins—assemble to create such a sophisticated and dynamic device? This article addresses this question by deconstructing the [neuronal membrane](@entry_id:182072) to reveal the physical principles and molecular machinery that govern its function.

Across three distinct chapters, we will build a comprehensive understanding of this critical structure. The journey begins with **"Principles and Mechanisms,"** where we will explore the biophysical forces that shape the [lipid bilayer](@entry_id:136413) and the elegant molecular designs of the proteins embedded within it, such as ion channels and pumps. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these fundamental principles scale up to explain complex phenomena, from the material science of myelin that enables rapid nerve conduction to the molecular organization of the synapse. Finally, the **"Hands-On Practices"** section will provide an opportunity to solidify this knowledge by applying these concepts to solve quantitative biophysical problems. By the end, you will have a clear picture of how the membrane's structure gives rise to its electrical function, forming the basis of all [neurobiology](@entry_id:269208).

## Principles and Mechanisms

### The Lipid Bilayer: The Fundamental Barrier

The [neuronal membrane](@entry_id:182072) is a sophisticated, dynamic structure whose primary role is to establish a controlled barrier between the intracellular and extracellular environments. This barrier is not merely a passive wall but an active interface that is fundamental to all aspects of [neuronal signaling](@entry_id:176759). The foundation of this structure is the [lipid bilayer](@entry_id:136413).

#### Spontaneous Assembly and the Hydrophobic Effect

The formation of a cell membrane is a remarkable example of spontaneous self-assembly, a process driven by fundamental [thermodynamic principles](@entry_id:142232). The primary constituents, **[phospholipids](@entry_id:141501)**, are **amphipathic** molecules, meaning they possess a dual nature: a polar or charged "head" group that is hydrophilic (water-loving) and one or more nonpolar hydrocarbon "tail" groups that are hydrophobic (water-fearing).

When these lipids are placed in an aqueous environment, the system naturally seeks to minimize its **Gibbs free energy** ($G$). A state in which individual lipid monomers are dispersed would maximize the unfavorable contact between the hydrophobic tails and water molecules. This forces the surrounding water into highly ordered, cage-like structures, which is entropically costly. This phenomenon, known as the **[hydrophobic effect](@entry_id:146085)**, is the primary driving force for lipid aggregation. The free energy penalty for this exposure can be modeled as being proportional to the exposed hydrophobic surface area, $\Delta G_{\text{exposure}} \approx \gamma A_{\text{exposed}}$, where $\gamma$ is the [interfacial free energy](@entry_id:183036) per unit area.

To minimize this penalty, lipids aggregate to sequester their hydrophobic tails away from water. The geometry of the resulting aggregate depends on the shape of the lipid molecules. Lipids with a large headgroup and a single, narrow tail are cone-shaped and tend to form spherical **micelles**. However, the major phospholipids in neuronal membranes typically have two acyl chain tails, giving them an approximately cylindrical shape. For these molecules, arranging into a planar **lipid bilayer** is the most energetically favorable configuration. A bilayer structure allows the cylindrical lipids to pack efficiently without creating energetically costly voids or stresses, while simultaneously minimizing the exposure of the [hydrophobic core](@entry_id:193706) to the aqueous surroundings [@problem_id:5042618].

#### Physical Properties of the Bilayer

The specific composition of the lipid tails significantly influences the physical properties of the membrane. Two key parameters are chain length and saturation.

Increasing the **length** of the acyl chains increases the thickness of the bilayer's hydrophobic core. Longer chains also exhibit stronger attractive van der Waals interactions with their neighbors, which favors a more ordered state.

The degree of **saturation** refers to the presence of double bonds in the hydrocarbon tails. **Saturated** chains lack double bonds and are straight, allowing them to pack tightly together. In contrast, **unsaturated** chains containing cis-double bonds have a permanent kink. This kink disrupts the orderly packing of adjacent lipids, effectively increasing the space between them and creating a more disordered, fluid membrane.

The order within the bilayer can be quantified by parameters such as the **deuterium [nuclear magnetic resonance](@entry_id:142969) (NMR) order parameter**, $S_{CD}$. This parameter measures the alignment of the C-H (or C-D) bonds in the acyl chains with the axis perpendicular to the bilayer surface (the bilayer normal). A value of $S_{CD}=1$ corresponds to perfect alignment, while $S_{CD}=0$ indicates random orientation. Increasing acyl chain saturation (removing kinks) and increasing chain length both promote more extended, aligned chain conformations. This leads to an increase in both the bilayer **thickness**, $d$, and the **order parameter**, $S_{CD}$, resulting in a less fluid and thicker membrane [@problem_id:5042618].

#### Lipid Asymmetry and Its Functional Consequences

A crucial feature of the neuronal plasma membrane is **[lipid asymmetry](@entry_id:176576)**: the composition of the inner (cytosolic) leaflet is different from that of the outer (extracellular) leaflet. This asymmetry is actively maintained by ATP-dependent enzymes and has profound functional implications.

Typically, the inner leaflet is enriched in phospholipids with negatively charged headgroups, such as **phosphatidylserine (PS)** and polyphosphoinositides like **phosphatidylinositol 4,5-bisphosphate (PIP2)**. The outer leaflet is enriched in **[glycosphingolipids](@entry_id:169163)** (lipids with attached carbohydrate chains), such as the ganglioside **GM1**, and cholesterol.

This asymmetry creates distinct functional platforms on each side of the membrane. One major consequence is the generation of a **surface charge**. Consider a patch of neuronal membrane where the inner leaflet contains $20\%$ PS (charge $q_{\text{PS}} \approx -1e$) and $5\%$ PIP2 (charge $q_{\text{PIP2}} \approx -4e$), while the outer leaflet contains $10\%$ GM1 (charge $q_{\text{GM1}} \approx -1e$), with an average [area per lipid](@entry_id:746510) of $0.60 \, \text{nm}^2$. The surface charge density, $\sigma$, can be calculated as the average charge per lipid divided by the [area per lipid](@entry_id:746510).

For the inner leaflet, the average charge per lipid is $(0.20)(-1e) + (0.05)(-4e) = -0.40e$. This results in a significant negative surface charge density:
$$ \sigma_{\text{inner}} = \frac{(-0.40)(1.602 \times 10^{-19} \, \text{C})}{0.60 \times 10^{-18} \, \text{m}^2} \approx -0.11 \, \text{C/m}^2 $$
For the outer leaflet, the average charge is $(0.10)(-1e) = -0.10e$, yielding a much smaller surface charge density:
$$ \sigma_{\text{outer}} = \frac{(-0.10)(1.602 \times 10^{-19} \, \text{C})}{0.60 \times 10^{-18} \, \text{m}^2} \approx -0.027 \, \text{C/m}^2 $$

The dense negative charge on the cytosolic face acts as an electrostatic recruitment platform, attracting and binding signaling proteins that contain **polybasic domains** (clusters of positively charged lysine and arginine residues). Furthermore, PS is a critical binding partner for proteins containing **C2 domains**, often in a calcium-dependent manner. On the extracellular side, the [glycosphingolipids](@entry_id:169163), along with cholesterol, are thought to co-assemble into ordered microdomains known as **[lipid rafts](@entry_id:147056)**. These rafts serve as scaffolds that concentrate specific receptors and signaling molecules, facilitating efficient signal transduction at the cell surface [@problem_id:5042552].

### Membrane Proteins: The Functional Gatekeepers

While the lipid bilayer provides the fundamental barrier, it is the embedded proteins that endow the membrane with its specific functions of transport, signaling, and adhesion.

#### Embedding Proteins in the Membrane

For a protein to reside stably within the hydrophobic core of the bilayer, the portion of the polypeptide that spans the membrane must itself be hydrophobic. The most common structure for a transmembrane segment is an **$\alpha$-helix**. An $\alpha$-helix is stabilized by internal hydrogen bonds between backbone amide and carbonyl groups, satisfying the hydrogen-bonding potential of the [polypeptide backbone](@entry_id:178461) in a nonpolar environment.

The hydrophobic core of a typical [neuronal membrane](@entry_id:182072) is about $30 \, \text{\AA}$ thick. Since an $\alpha$-helix rises approximately $1.5 \, \text{\AA}$ per amino acid residue, a [transmembrane helix](@entry_id:176889) requires a stretch of about $20$ predominantly hydrophobic residues to span the bilayer.

Computational methods can be used to predict the topology of a membrane protein from its primary amino acid sequence. A **[hydropathy plot](@entry_id:177372)**, such as one using the Kyte-Doolittle scale, calculates the average hydrophobicity over a sliding window of about 19-21 residues. Stretches of the sequence that show strong hydrophobic peaks are candidate transmembrane helices. However, hydrophobicity alone is not sufficient. The presence of helix-breaking residues like [proline](@entry_id:166601) or charged residues within a hydrophobic segment makes it an unlikely transmembrane span.

Furthermore, for [eukaryotic plasma membrane](@entry_id:172867) proteins, the orientation is governed by the **[positive-inside rule](@entry_id:154875)**. This empirical rule states that the loops connecting transmembrane helices on the cytosolic side are significantly enriched in positively [charged amino acids](@entry_id:173747) (lysine and arginine) compared to loops on the extracellular side. By identifying candidate helices from a [hydropathy plot](@entry_id:177372) and then examining the charge distribution in the intervening loops, a consistent topological model can be built. For instance, if a model predicts a $10$-span protein, one would expect to find five highly positive loops alternating with five loops of low positive charge. This pattern allows for the assignment of N- and C-terminal orientation. An even number of spans means both termini are on the same side of the membrane, while an odd number places them on opposite sides [@problem_id:5042620].

#### A Functional Taxonomy of Membrane Proteins

Neuronal [membrane proteins](@entry_id:140608) can be broadly classified based on their function, [energy coupling](@entry_id:137595), stoichiometry, and kinetics [@problem_id:5042565].

*   **Ion Channels:** These proteins form a water-filled pore through the membrane. When open, they allow ions to flow passively down their [electrochemical gradient](@entry_id:147477). This process is very fast, with single-channel fluxes on the order of $10^6$ to $10^8$ ions per second. Because ions flow continuously, there is no fixed stoichiometry per "cycle." A prime example is the [voltage-gated sodium channel](@entry_id:170962) ($\text{Na}_\text{v}$) responsible for the rising phase of the action potential.

*   **Transporters (Carriers):** Unlike channels, transporters do not form a continuous pore. They operate via an **[alternating-access mechanism](@entry_id:171684)**, where the protein undergoes a conformational change to expose a binding site first to one side of the membrane and then to the other. This mechanism imposes a fixed **stoichiometry** (a specific number of substrate molecules per cycle) and results in much slower transport rates, typically $10^0$ to $10^4$ cycles per second.
    *   **Facilitated Diffusion:** Passive transporters that move substrates down their concentration gradient (e.g., GLUT [glucose transporters](@entry_id:138443)).
    *   **Secondary Active Transport:** These transporters couple the "uphill" movement of one substrate against its gradient to the "downhill" movement of another, typically $\text{Na}^+$. The energy stored in the $\text{Na}^+$ gradient (which is maintained by pumps) drives the transport. An example is the GABA transporter GAT1, which co-transports one GABA molecule with two $\text{Na}^+$ ions and one $\text{Cl}^-$ ion into the cell.

*   **Pumps (Primary Active Transporters):** These are transporters that perform **[primary active transport](@entry_id:147900)**, directly coupling the transport process to an energy source, usually the hydrolysis of ATP. They move substrates against steep electrochemical gradients. The canonical example is the **$\text{Na}^+/\text{K}^+$-ATPase**, which pumps three $\text{Na}^+$ ions out of the cell and two $\text{K}^+$ ions into the cell for every molecule of ATP hydrolyzed, thereby maintaining the crucial ion gradients for [neuronal excitability](@entry_id:153071). Its kinetics are similar to other transporters, with turnover rates around $10^2$ cycles per second.

*   **Receptors:** These proteins are specialized for signal transduction. They bind to specific ligands (e.g., [neurotransmitters](@entry_id:156513)) and initiate an intracellular response without transporting the ligand across the membrane. **Metabotropic receptors**, like the metabotropic [glutamate receptor](@entry_id:164401) (mGluR), are a major class that couple to G-proteins to activate downstream [signaling cascades](@entry_id:265811).

*   **Adhesion Molecules:** These proteins mediate cell-cell and cell-extracellular matrix interactions. They play structural roles in holding tissues together and are critical for forming and maintaining synapses. Examples include **Neuroligins** and the **Neural Cell Adhesion Molecule (NCAM)**.

### Mechanisms of Ion Channels: A Closer Look

Ion channels are central to [neurobiology](@entry_id:269208), mediating the rapid changes in membrane potential that constitute nerve impulses. Their function hinges on two key properties: selectivity and gating.

#### The Challenge of Selectivity: A Snug Fit

Ion channels are remarkably selective. A potassium ($\text{K}^+$) channel, for instance, can be over 10,000 times more permeable to $\text{K}^+$ than to the slightly smaller sodium ($\text{Na}^+$) ion. This exquisite selectivity is not based on simple [steric hindrance](@entry_id:156748). The mechanism was elegantly revealed by the crystal structure of a bacterial $\text{K}^+$ channel.

The selectivity arises from an energetic trade-off. An ion in aqueous solution is surrounded by a shell of oriented water molecules, its **[hydration shell](@entry_id:269646)**. For an ion to enter a narrow channel pore, it must shed these water molecules, a process that requires a significant amount of energy (the **dehydration energy**). The magnitude of this energy is larger for smaller ions like $\text{Na}^+$ due to their higher charge density.

To overcome this energy barrier, the channel must provide an environment that compensates for the lost hydration. The **[selectivity filter](@entry_id:156004)** of the $\text{K}^+$ channel is a narrow pore lined by a precise arrangement of backbone carbonyl oxygen atoms from a conserved [sequence motif](@entry_id:169965). These oxygens present a cage of partial negative charges that mimics the geometry of the water molecules in the [hydration shell](@entry_id:269646) of a $\text{K}^+$ ion.

For a $\text{K}^+$ ion, the pore is a "snug fit." The ion can coordinate perfectly with the surrounding carbonyl oxygens, and the favorable energy gained from this **coordination** almost exactly matches the energy cost of dehydration. This results in a very low net energy barrier for [permeation](@entry_id:181696). A smaller $\text{Na}^+$ ion, however, is too small to coordinate optimally with the rigidly held carbonyls in the filter. It "rattles" in the site, resulting in weak coordination that is insufficient to compensate for its larger dehydration energy. This creates a large net energy barrier, effectively excluding $\text{Na}^+$ from the pore [@problem_id:5042611].

#### The Mechanism of Voltage Gating

Many crucial ion channels are **voltage-gated**, meaning their probability of being open is regulated by the membrane potential. Voltage-gated sodium, potassium, and calcium channels all share a common architecture based on subunits containing six transmembrane helices (S1-S6).

These helices are organized into two distinct functional domains [@problem_id:5042518]:
1.  The **Pore Domain (PD)** is formed by helices S5 and S6, along with a re-entrant "P-loop" between them. The P-loop forms the selectivity filter at the extracellular side of the pore, while the intracellular ends of the S6 helices form the **activation gate**, which physically opens and closes the conduction pathway.
2.  The **Voltage-Sensing Domain (VSD)** is composed of helices S1 through S4. This domain detects changes in the membrane's electric field.

The key to voltage sensing is the **S4 helix**. This segment is unique in that it contains a series of regularly spaced, positively charged residues (typically arginine or lysine) every third or fourth position. At rest, the inside of the neuron is negative relative to the outside, creating a strong inward-directed electric field across the membrane. This field exerts an inward electrostatic force on the positive charges of the S4 helix, pulling it toward the cytoplasm and holding the activation gate in a closed conformation.

When the membrane **depolarizes** (becomes less negative inside), the strength of the inward electric field is reduced. This lessens the inward pull on the S4 helix. In response, the S4 helix undergoes a conformational change, typically moving and rotating outward toward the extracellular side. This movement of positive charge across the electric field is the source of the experimentally measurable **[gating current](@entry_id:167659)**.

This physical movement of the S4 helix is mechanically coupled to the pore domain, often via a linker region known as the S4-S5 linker. The outward movement of S4 pulls on this linker, which in turn pulls on the S6 helices of the pore. This action causes the S6 helices to splay apart, opening the activation gate and allowing ions to flow through the channel.

### Electrochemical Consequences: From Potentials to Propagation

The interplay between the semipermeable membrane and its embedded pumps and channels establishes the electrochemical environment that is the basis for all [neuronal signaling](@entry_id:176759).

#### The Origin of Membrane Potential: Equilibrium vs. Steady State

The **$\text{Na}^+/\text{K}^+$-ATPase** expends energy to create steep concentration gradients, with $\text{K}^+$ high inside the cell and $\text{Na}^+$ high outside. If the membrane were permeable to only a single ion species, say $\text{K}^+$, the membrane potential ($V_m$, defined by convention as $V_{\text{inside}} - V_{\text{outside}}$) would settle at that ion's **[equilibrium potential](@entry_id:166921)**, also known as the **Nernst potential**. At this potential, the outward chemical driving force (due to the concentration gradient) is exactly balanced by the inward electrical driving force. The Nernst equation describes this potential:
$$ E_{\text{ion}} = \frac{RT}{zF} \ln \frac{[\text{ion}]_{\text{out}}}{[\text{ion}]_{\text{in}}} $$
where $R$ is the gas constant, $T$ is temperature, $z$ is the ion's valence, and $F$ is Faraday's constant. For a typical neuron with $[\text{K}^+]_{\text{in}} = 140 \, \text{mM}$ and $[\text{K}^+]_{\text{out}} = 5 \, \text{mM}$ at $310 \, \text{K}$, the Nernst potential for potassium is approximately $E_{\text{K}} \approx -89 \, \text{mV}$.

However, at rest, the [neuronal membrane](@entry_id:182072) is permeable to multiple ions, primarily $\text{K}^+$, $\text{Na}^+$, and $\text{Cl}^-$. The resulting **resting membrane potential** ($V_{\text{rest}}$) is not an equilibrium but a **steady state**. At $V_{\text{rest}}$, the net flow of charge across the membrane is zero ($\sum I_{\text{ion}} = 0$), but the individual currents for each ion are generally non-zero. These steady leak currents are counteracted by active pumps to maintain the concentration gradients over the long term.

The resting potential is determined by the concentration gradients and the relative permeabilities of the ions, as described by the **Goldman-Hodgkin-Katz (GHK) equation**:
$$ V_{\text{rest}} = \frac{RT}{F} \ln \frac{P_{\text{K}}[\text{K}^+]_{\text{out}} + P_{\text{Na}}[\text{Na}^+]_{\text{out}} + P_{\text{Cl}}[\text{Cl}^-]_{\text{in}}}{P_{\text{K}}[\text{K}^+]_{\text{in}} + P_{\text{Na}}[\text{Na}^+]_{\text{in}} + P_{\text{Cl}}[\text{Cl}^-]_{\text{out}}} $$
Because the resting permeability to $\text{K}^+$ ($P_{\text{K}}$) is much higher than that for $\text{Na}^+$ ($P_{\text{Na}}$), the resting potential lies close to $E_{\text{K}}$, but is slightly depolarized by the small influx of $\text{Na}^+$. For typical neuronal values (e.g., relative permeabilities $P_{\text{K}}:P_{\text{Na}}:P_{\text{Cl}} = 1:0.05:0.45$), the GHK equation yields a resting potential of approximately $V_{\text{rest}} \approx -65 \, \text{mV}$ [@problem_id:5042601].

#### The Membrane as an Electrical Circuit

For analyzing electrical signaling, it is useful to model a patch of membrane as a simple electrical circuit. The [lipid bilayer](@entry_id:136413), being a thin insulator separating two conductors, acts as a capacitor, with a **[specific membrane capacitance](@entry_id:177788)** $C_m$ (typically $\approx 1 \, \mu\text{F/cm}^2$). The various ion channels that allow current to pass through the membrane collectively act as a resistor, with a **[specific membrane resistance](@entry_id:166665)** $R_m$ (or its inverse, **specific leak conductance** $g_L = 1/R_m$).

Because the capacitive and resistive pathways are both subject to the same transmembrane voltage, they are modeled as being in **parallel**. The ionic pathway is further modeled as a conductor ($g_L$) in series with a battery representing the net [reversal potential](@entry_id:177450) of the [leak channels](@entry_id:200192) ($E_L$, which is equivalent to $V_{\text{rest}}$). By [conservation of charge](@entry_id:264158) (Kirchhoff's law), any current injected into the cell, $i_{\text{inj}}$, must either charge the capacitor or flow through the resistive [leak channels](@entry_id:200192):
$$ i_{\text{inj}} = C_m \frac{dV}{dt} + g_L (V - E_L) $$

This is the fundamental equation for a passive membrane patch. In response to a step injection of current, the membrane potential $V$ does not change instantaneously. Instead, it changes exponentially toward a new steady-state value of $V_{\infty} = E_L + i_{\text{inj}}/g_L$. The speed of this response is characterized by the **membrane time constant**, $\tau_m$:
$$ \tau_m = R_m C_m $$
The time constant represents the time it takes for the voltage to reach approximately $63\%$ of its final change. It is a crucial parameter for determining how a neuron integrates synaptic inputs over time [@problem_id:5042594].

#### Spatial Propagation: Cable Theory

Neurons are not simple isopotential spheres; their complex dendritic and axonal structures require us to consider the spatial propagation of voltage signals. A passive dendrite can be modeled as a cylindrical **cable**. In addition to the membrane resistance that allows current to leak out, there is an **axial resistance** to current flowing along the length of the cylinder's cytoplasm.

We can define resistance per unit length for the membrane ($r_m$, in $\Omega \cdot \text{m}$) and for the axial path ($r_i$, in $\Omega/\text{m}$). These depend on the specific material properties ($R_m, R_i$) and the cable radius ($a$): $r_m = R_m / (2\pi a)$ and $r_i = R_i / (\pi a^2)$. The competition between current flowing down the cable and current leaking out of the membrane is captured by the **[length constant](@entry_id:153012)**, $\lambda$:
$$ \lambda = \sqrt{\frac{r_m}{r_i}} $$

For a steady-state voltage applied at one point, the [length constant](@entry_id:153012) is the distance over which that voltage decays to $1/e$ (about $37\%$) of its initial value. A larger [length constant](@entry_id:153012) means signals can propagate passively over longer distances. Notably, $\lambda$ scales with the square root of the radius, $\lambda \propto \sqrt{a}$. The **input resistance** ($R_{\text{in}}$) of the cable—the voltage change at the injection site for a given current injection—depends on $\lambda$ and describes how effectively a local input can change the membrane potential [@problem_id:5042540].

#### A Refined View: The Role of Surface Potential

The standard model of membrane potential considers the voltage difference between the bulk solutions. However, the voltage directly experienced by a membrane protein's voltage sensor is a more local quantity, influenced by the fixed surface charges on the lipid leaflets.

As discussed earlier, the asymmetric distribution of charged lipids creates a negative **[surface charge density](@entry_id:272693)** on both the inner and outer membrane surfaces. According to the **Gouy-Chapman theory** of the electrostatic double layer, this fixed charge attracts a cloud of counter-ions from the bulk solution, creating a **surface potential**. For a negative surface charge, the potential at the membrane surface is negative relative to the bulk solution on that same side. Let's call these surface potentials $\psi_{\text{in}}$ and $\psi_{\text{out}}$.

The [effective voltage](@entry_id:267211) difference, $V_{\text{eff}}$, sensed by a protein's voltage sensor spanning the membrane is the difference between the surface potentials, not the bulk potentials:
$$ V_{\text{eff}} = \phi_{\text{in,surface}} - \phi_{\text{out,surface}} $$
This can be related to the bulk transmembrane voltage, $V_m = \phi_{\text{in,bulk}} - \phi_{\text{out,bulk}}$, as follows:
$$ V_{\text{eff}} = V_m + \psi_{\text{in}} - \psi_{\text{out}} $$

This equation shows that the bulk voltage required to reach a certain effective activation threshold is shifted by the surface potentials. For instance, consider a channel that requires an effective local depolarization of $V_{\text{eff,thr}} = +20 \, \text{mV}$ to open. If we have leaflet charge densities of $\sigma_{\text{in}} = -0.010 \, \text{C/m}^2$ and $\sigma_{\text{out}} = -0.020 \, \text{C/m}^2$ in a $0.15 \, \text{M}$ electrolyte, these produce surface potentials of approximately $\psi_{\text{in}} \approx -11 \, \text{mV}$ and $\psi_{\text{out}} \approx -22 \, \text{mV}$. The required bulk voltage for activation is then:
$$ V_m = V_{\text{eff,thr}} - \psi_{\text{in}} + \psi_{\text{out}} = 20 \, \text{mV} - (-11 \, \text{mV}) + (-22 \, \text{mV}) \approx +9 \, \text{mV} $$
In this case, the negative surface potentials mean that a much smaller bulk depolarization is needed to achieve the required local field for [channel activation](@entry_id:186896). This demonstrates how lipid composition can directly modulate the electrical excitability of a neuron, a beautiful integration of the membrane's structural and electrical properties [@problem_id:5042556].