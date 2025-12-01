## Introduction
The resting membrane potential—the steady electrical voltage across a neuron's membrane when it is not actively signaling—is the foundation upon which all of neurophysiology is built. It is the baseline state of readiness from which action potentials are launched and synaptic inputs are integrated. However, this seemingly quiescent negative voltage is anything but simple. It is the product of a dynamic and intricate interplay between fundamental laws of physics, the thermodynamics of chemical gradients, and the sophisticated molecular machinery embedded within the cell membrane. Understanding this potential requires moving beyond simple biological descriptions to a rigorous, quantitative biophysical framework.

This article dissects the resting potential from first principles, bridging the gap between abstract physics and concrete neuronal function. We will explore how the neuron establishes and maintains this critical electrical state, and how its disruption leads to disease. The material is organized into three distinct chapters to guide you from core theory to practical application.

First, **"Principles and Mechanisms"** lays the biophysical groundwork. We will model the membrane as a capacitor, define the electrochemical forces driving ion movement, derive the Nernst and Goldman-Hodgkin-Katz equations, and examine the structure and function of the ion channels and pumps that create [selective permeability](@entry_id:153701). Next, **"Applications and Interdisciplinary Connections"** demonstrates the explanatory power of these principles. We will see how they account for the rapid conduction in [myelinated axons](@entry_id:149971), the immense energy budget of the brain, the critical homeostatic role of [glial cells](@entry_id:139163), and the cellular basis of diseases like epilepsy and stroke. Finally, **"Hands-On Practices"** offers a set of quantitative problems, allowing you to actively apply these concepts to analyze realistic neurophysiological scenarios. We begin our journey by examining the fundamental physical properties of the neuronal membrane itself—the dielectric barrier that makes the resting potential possible.

## Principles and Mechanisms

### The Membrane as a Charged Capacitor: A Dielectric Barrier

The neuronal membrane's ability to maintain a voltage difference, the **membrane potential**, originates from its fundamental physical structure. The core of this structure is the **[lipid bilayer](@entry_id:136413)**, a remarkably thin sheet, approximately $5\,\mathrm{nm}$ thick, composed of phospholipid molecules. From an electrostatic perspective, this bilayer acts as an insulating material separating two conductive [aqueous solutions](@entry_id:145101): the intracellular cytosol and the extracellular fluid. In physics, such an insulating material is known as a **dielectric**.

A key property of a dielectric material is its **[relative permittivity](@entry_id:267815)** or **dielectric constant**, denoted by $\varepsilon_r$. This dimensionless quantity measures how effectively a material can store electrical energy by becoming polarized in an electric field, thereby reducing the field's strength within it. The [lipid bilayer](@entry_id:136413) is profoundly different from the water surrounding it in this regard. The nonpolar hydrocarbon tails of the lipids give the membrane a very low [relative permittivity](@entry_id:267815), $\varepsilon_{\mathrm{m}} \approx 2$, similar to that of oil. In stark contrast, water, a highly polar molecule, has a very high [relative permittivity](@entry_id:267815), $\varepsilon_{\mathrm{w}} \approx 80$.

This dramatic difference in dielectric properties is central to the membrane's electrical function. We can model the membrane as a simple planar capacitor to understand why [@problem_id:4507522]. Imagine the membrane as a thin dielectric slab of thickness $d$ and permittivity $\varepsilon_m = \varepsilon_0 \varepsilon_{\mathrm{m}}$, sandwiched between two layers of the aqueous solution with permittivity $\varepsilon_w = \varepsilon_0 \varepsilon_{\mathrm{w}}$. According to Gauss's law for dielectrics, in the absence of free charges within the material, the normal component of the **electric displacement field**, $\mathbf{D}$, must be continuous across the boundary between different [dielectrics](@entry_id:145763). If there is a net surface charge density $\pm \sigma$ on the "plates" of this biological capacitor (formed by layers of ions accumulated on either side of the membrane), then the magnitude of the displacement field throughout this layered structure is constant and equal to $\sigma$.

The relationship between the displacement field $\mathbf{D}$ and the **electric field** $\mathbf{E}$ is given by the [constitutive relation](@entry_id:268485) $\mathbf{D} = \varepsilon \mathbf{E}$. This leads to a profound consequence:

$E = \frac{D}{\varepsilon} = \frac{\sigma}{\varepsilon_0 \varepsilon_r}$

Because the displacement field $D$ is constant through both the membrane and the water, but their permittivities differ greatly, the electric fields within them must also differ:

$E_{\mathrm{m}} = \frac{\sigma}{\varepsilon_0 \varepsilon_{\mathrm{m}}}$ and $E_{\mathrm{w}} = \frac{\sigma}{\varepsilon_0 \varepsilon_{\mathrm{w}}}$

The ratio of the electric field strength inside the membrane to that in the adjacent water is:

$\frac{E_{\mathrm{m}}}{E_{\mathrm{w}}} = \frac{\varepsilon_{\mathrm{w}}}{\varepsilon_{\mathrm{m}}} \approx \frac{80}{2} = 40$

This means the electric field is concentrated within the low-dielectric [lipid bilayer](@entry_id:136413), being approximately 40 times stronger there than in the surrounding water for the same charge separation. The voltage drop, $\Delta V$, across a region of thickness $L$ with a uniform field $E$ is $\Delta V = E \cdot L$. Even if the charge layers are separated by a region of water of the same thickness as the membrane, the vast majority of the potential drop will occur across the membrane itself. For a typical membrane charge density of $\sigma \approx 0.01\,\mathrm{C/m^2}$ (corresponding to one [elementary charge](@entry_id:272261) per $\approx 16\,\mathrm{nm^2}$), the field inside the membrane is enormous, on the order of $10^7\,\mathrm{V/m}$, and the voltage drop across the $5\,\mathrm{nm}$ membrane is substantial, while the drop across an equivalent thickness of water is negligible [@problem_id:4507522]. The [lipid bilayer](@entry_id:136413), by virtue of its low permittivity, ensures that a small separation of charge generates a large and localized transmembrane potential.

### The Energetics of Ion Movement: The Electrochemical Potential

The existence of a membrane potential is only half the story. The neuron is a dynamic system, with charged ions constantly moving across the membrane. The direction and magnitude of this movement are not governed by concentration differences alone, nor by the electric field alone. Instead, they are dictated by a unified thermodynamic quantity: the **[electrochemical potential](@entry_id:141179)**.

The electrochemical potential, $\tilde{\mu}_i$, of an ion species $i$ is its partial molar Gibbs free energy. It represents the total energy required to add one mole of that ion to the system at a specific location, accounting for both chemical and [electrical work](@entry_id:273970) [@problem_id:4507498]. It is the sum of two components:

$\tilde{\mu}_i = \mu_i + z_i F \psi$

1.  **Chemical Potential ($\mu_i$)**: This term accounts for the energy associated with the concentration of the ion. It is given by:
    $\mu_i = \mu_i^0 + RT \ln a_i$
    Here, $\mu_i^0$ is the standard chemical potential (the potential under standard conditions of concentration, pressure, and temperature), $R$ is the [universal gas constant](@entry_id:136843) ($\approx 8.314\,\mathrm{J\,mol^{-1}\,K^{-1}}$), $T$ is the [absolute temperature](@entry_id:144687) in Kelvin, and $a_i$ is the dimensionless **activity** of the ion, which can be thought of as its "effective concentration". In the [dilute solutions](@entry_id:144419) of physiological systems, activity is often approximated by the molar concentration, $c_i$, normalized by a standard concentration ($c^\circ = 1\,\mathrm{M}$), i.e., $a_i \approx c_i/c^\circ$ [@problem_id:4507498].

2.  **Molar Electrical Potential Energy ($z_i F \psi$)**: This term represents the work done to move one mole of ions into a region with an electrical potential $\psi$. The term $z_i$ is the dimensionless integer **valence** of the ion (e.g., $+1$ for $\mathrm{K}^+$, $-1$ for $\mathrm{Cl}^-$, $+2$ for $\mathrm{Ca}^{2+}$). The **Faraday constant**, $F = N_A e \approx 96,485\,\mathrm{C\,mol^{-1}}$, is the total charge of one mole of elementary charges, where $N_A$ is Avogadro's number and $e$ is the [elementary charge](@entry_id:272261). Thus, $z_i F$ is the charge per mole of ion $i$. Multiplying this by the potential $\psi$ (in Volts, or Joules per Coulomb) gives the electrical potential energy in Joules per mole ($\mathrm{J\,mol^{-1}}$).

The complete expression for the electrochemical potential of an ion $i$ in a compartment (e.g., inside or outside the cell) with activity $a_i$ and [electrical potential](@entry_id:272157) $\psi$ is:

$\tilde{\mu}_i = \mu_i^0 + RT \ln a_i + z_i F \psi$

Ions will spontaneously move "downhill" from a region of higher [electrochemical potential](@entry_id:141179) to a region of lower [electrochemical potential](@entry_id:141179). The difference in electrochemical potential between the outside ($\text{out}$) and inside ($\text{in}$) of the cell, $\Delta \tilde{\mu}_i = \tilde{\mu}_{i,in} - \tilde{\mu}_{i,out}$, is the net driving force for that ion across the membrane.

### Ion Equilibrium and the Nernst Potential

What happens if an ion is allowed to move freely across the membrane? It will continue to do so until its electrochemical potential is the same on both sides. This condition of no net flux is **[thermodynamic equilibrium](@entry_id:141660)**.

$\tilde{\mu}_{i,in} = \tilde{\mu}_{i,out}$

Substituting the full expression for the [electrochemical potential](@entry_id:141179):

$\mu_i^0 + RT \ln a_{i,in} + z_i F \psi_{in} = \mu_i^0 + RT \ln a_{i,out} + z_i F \psi_{out}$

The standard potential $\mu_i^0$ is the same on both sides and cancels. Rearranging the terms to solve for the [potential difference](@entry_id:275724) across the membrane, $V_m = \psi_{in} - \psi_{out}$, gives:

$z_i F (\psi_{in} - \psi_{out}) = RT \ln a_{i,out} - RT \ln a_{i,in} = RT \ln\left(\frac{a_{i,out}}{a_{i,in}}\right)$

This specific membrane potential at which a given ion species is in equilibrium is called the **Nernst potential** or **equilibrium potential** for that ion, denoted $E_i$:

$E_i = \frac{RT}{z_i F} \ln\left(\frac{[i]_{out}}{[i]_{in}}\right)$

Here, we have replaced the activities with the more commonly used concentrations, $[i]$. The Nernst potential represents the precise voltage that would exactly balance the concentration gradient for a specific ion. If the membrane potential were equal to $E_i$, there would be no net movement of ion $i$ across the membrane, even if the membrane were highly permeable to it.

It is instructive to consider the case of an anion, such as chloride ($\mathrm{Cl}^-$), where $z_{\mathrm{Cl}} = -1$ [@problem_id:4507495]. A systematic application of the formula yields:

$E_{\mathrm{Cl}} = \frac{RT}{(-1)F} \ln\left(\frac{[\mathrm{Cl}^-]_{out}}{[\mathrm{Cl}^-]_{in}}\right) = -\frac{RT}{F} \ln\left(\frac{[\mathrm{Cl}^-]_{out}}{[\mathrm{Cl}^-]_{in}}\right)$

Using the logarithmic identity $-\ln(x/y) = \ln(y/x)$, this can be rewritten as:

$E_{\mathrm{Cl}} = \frac{RT}{F} \ln\left(\frac{[\mathrm{Cl}^-]_{in}}{[\mathrm{Cl}^-]_{out}}\right)$

This form, with the inverted concentration ratio, is often presented in textbooks but can be a source of confusion. It is not an arbitrary rule but a direct consequence of the negative valence. Sticking to the fundamental derivation with $z_i$ in the denominator avoids such ambiguity. In a typical neuron, where $[\mathrm{Cl}^-]_{out} > [\mathrm{Cl}^-]_{in}$, the logarithm is negative, resulting in a negative Nernst potential for chloride, often close to the neuron's resting potential.

### The Resting Neuron: A Non-Equilibrium Steady State

A crucial question is whether the resting neuron represents a system in equilibrium. We can answer this by comparing the measured **resting membrane potential** ($V_{rest}$), typically around $-65\,\mathrm{mV}$ to $-70\,\mathrm{mV}$, with the Nernst potentials of the key ions [@problem_id:4507523].

For a typical mammalian neuron at $37\,^{\circ}\mathrm{C}$ ($310\,\mathrm{K}$):
-   **Potassium (K+)**: With $[\mathrm{K}^+]_{out} \approx 4\,\mathrm{mM}$ and $[\mathrm{K}^+]_{in} \approx 140\,\mathrm{mM}$, $E_K \approx -95\,\mathrm{mV}$.
-   **Sodium (Na+)**: With $[\mathrm{Na}^+]_{out} \approx 145\,\mathrm{mM}$ and $[\mathrm{Na}^+]_{in} \approx 12\,\mathrm{mM}$, $E_{\mathrm{Na}} \approx +67\,\mathrm{mV}$.

Clearly, $V_{rest} (\approx -65\,\mathrm{mV})$ is not equal to either $E_K$ or $E_{\mathrm{Na}}$. This means that neither potassium nor sodium is in equilibrium at rest. At $-65\,\mathrm{mV}$:
-   The potential is more positive than $E_K$, so there is a net electrochemical driving force pushing $\mathrm{K}^+$ *out* of the cell.
-   The potential is far more negative than $E_{\mathrm{Na}}$, so there is a strong net [electrochemical driving force](@entry_id:156228) pushing $\mathrm{Na}^+$ *into* the cell.

If these ions can cross the membrane, there must be continuous fluxes: an outward "leak" of $\mathrm{K}^+$ and an inward "leak" of $\mathrm{Na}^+$. If left unchecked, these leaks would dissipate the concentration gradients and drive the membrane potential towards zero.

The neuron prevents this decay by using active transport. The **[sodium-potassium pump](@entry_id:137188) (Na$^+$/K$^+$ ATPase)** is a membrane protein that uses the energy from ATP hydrolysis to actively pump ions *against* their electrochemical gradients. For each molecule of ATP consumed, it transports $3$ $\mathrm{Na}^+$ ions out of the cell and $2$ $\mathrm{K}^+$ ions into the cell [@problem_id:4507556].

The "resting" state is therefore not a static equilibrium. It is a **[non-equilibrium steady state](@entry_id:137728)** [@problem_id:4507523]. In this state, the intracellular and extracellular concentrations remain constant over time because the passive leak of each ion down its electrochemical gradient is precisely counterbalanced by the [active transport](@entry_id:145511) of that ion in the opposite direction by the pump. This dynamic balance requires a continuous expenditure of metabolic energy (ATP) to maintain the ionic gradients that are the very foundation of the resting potential.

### The Biophysical Basis of Ion Permeability and Selectivity

#### The Role of Ion Channels

The passive "leak" of ions across the [lipid bilayer](@entry_id:136413) does not happen through the lipid itself, which is highly impermeable to charged particles. Instead, ions cross the membrane through specialized protein pores known as **ion channels**. These proteins form water-filled conduits that allow specific ions to pass through, driven by their [electrochemical potential](@entry_id:141179). The overall permeability of the membrane to a given ion is determined by the number of open channels for that ion and their individual ion-handling properties.

#### The Structural Basis of Selectivity

One of the most remarkable features of ion channels is their exquisite **selectivity**. For instance, [potassium channels](@entry_id:174108) are typically over 1000 times more permeable to $\mathrm{K}^+$ than to the smaller $\mathrm{Na}^+$ ion. This cannot be explained by simple size exclusion, as $\mathrm{Na}^+$ is smaller than $\mathrm{K}^+$. The mechanism was famously elucidated through the crystal structure of the KcsA potassium channel [@problem_id:4507514].

The explanation lies in a delicate thermodynamic balance between dehydration and resolvation.
1.  **Hydration**: In aqueous solution, ions are not naked. They are surrounded by a tightly bound shell of water molecules, the **[hydration shell](@entry_id:269646)**, oriented by the ion's charge. The energy released upon forming this shell is the **[hydration energy](@entry_id:138164)**. Smaller ions with higher charge density, like $\mathrm{Na}^+$, hold their water molecules more tightly and thus have a larger magnitude of [hydration energy](@entry_id:138164) than larger ions like $\mathrm{K}^+$.
2.  **Dehydration and Resolvation**: For an ion to pass through the narrowest part of a channel, the **selectivity filter**, it must shed most of its [hydration shell](@entry_id:269646). This process costs energy—the **[dehydration penalty](@entry_id:171539)**. To make this energetically feasible, the channel must provide substitute interactions that compensate for the lost water molecules.
3.  **The Selectivity Filter**: The [selectivity filter](@entry_id:156004) of a [potassium channel](@entry_id:172732) is a narrow pore lined with a precise, rigid arrangement of backbone carbonyl oxygen atoms. This structure is perfectly configured to mimic the first [hydration shell](@entry_id:269646) of a $\mathrm{K}^+$ ion. A potassium ion can enter the filter, shed its water molecules, and coordinate perfectly with the carbonyl oxygens, receiving [electrostatic stabilization](@entry_id:159391) that almost perfectly balances its large [dehydration penalty](@entry_id:171539). For $\mathrm{K}^+$, the net energy barrier to enter the filter is very low, allowing for rapid conduction.
4.  **Exclusion of Sodium**: A $\mathrm{Na}^+$ ion, being smaller, would prefer to coordinate with oxygen atoms at a shorter distance. The rigid filter cannot shrink to accommodate this. Consequently, when a $\mathrm{Na}^+$ ion enters the filter, its coordination with the carbonyl oxygens is geometrically suboptimal and energetically weak. This weak stabilization is insufficient to pay the high energy cost of dehydrating the $\mathrm{Na}^+$ ion. The net energy barrier for $\mathrm{Na}^+$ to enter the filter is therefore prohibitively high, effectively excluding it.

Selectivity is thus an emergent property of optimized energetic compensation, rooted in the precise atomic geometry of the channel protein.

#### Leak versus Voltage-Gated Channels at Rest

The channels responsible for the resting potential are often broadly termed "leak" channels. These are channels that have a significant probability of being open at or near the resting potential. The archetypal leak channels are the **two-pore-domain potassium (K2P) channels**, whose conductance is largely independent of voltage in the physiological range. Their high permeability to $\mathrm{K}^+$ is the primary reason the resting potential is close to the Nernst potential for potassium.

However, the distinction between "leak" and "voltage-gated" channels can be subtle when considering their contribution to the resting state [@problem_id:4507567]. Voltage-gated channels have a conductance that is a steep function of membrane potential, typically described by an activation variable $m(V)$. Even these channels can contribute to the resting state if their activation curve is not fully zero at $V_{rest}$.

A more rigorous way to classify a channel's behavior near rest is to analyze how its current, $I_i(V) = g_i(V)(V - E_i)$, changes with small voltage perturbations. A channel behaves in a "leak-like" manner if its conductance $g_i(V)$ is relatively constant around $V_{rest}$. This occurs when the slope of its activation curve, $dm_i/dV$, is small near $V_{rest}$. Conversely, if this slope is large, gating changes contribute significantly to the current response, which is the hallmark of voltage-gated behavior. A useful dimensionless metric, $S_i$, can be defined to quantify this:

$S_i = \left|\frac{(V_{\mathrm{rest}} - E_i)}{m_i(V_{\mathrm{rest}})} \frac{dm_i}{dV}\right|_{V_{\mathrm{rest}}}$

If $S_i \ll 1$, the channel's contribution to stabilizing the resting potential is effectively that of a simple resistor (a leak). If $S_i$ is of order one or greater, its voltage-dependent gating plays an active role.

### Modeling the Resting Potential: From Physics to Circuits

#### The Principle of Bulk Electroneutrality

A complete physical description of ion movement and potentials would involve solving the coupled Poisson-Nernst-Planck (PNP) equations throughout the cell and its surroundings—a formidable task. Fortunately, a powerful simplification arises from a fundamental physical principle: **bulk electroneutrality** [@problem_id:4507505].

In an [electrolyte solution](@entry_id:263636), any local accumulation of net charge is rapidly screened by the rearrangement of mobile counter-ions. The characteristic length scale of this screening is the **Debye length**, $\lambda_D$. In physiological saline, with an ionic strength of about $150\,\mathrm{mM}$, the Debye length is less than a nanometer ($\lambda_D \approx 0.8\,\mathrm{nm}$). This is orders of magnitude smaller than the dimensions of a neuron (e.g., a radius of $10\,\mu\mathrm{m} = 10,000\,\mathrm{nm}$).

This massive [scale separation](@entry_id:152215), $\lambda_D \ll L_{cell}$, implies that any significant net charge can only exist within a vanishingly thin layer (on the order of $\lambda_D$) adjacent to charged surfaces like the membrane. In the "bulk" of the cytosol and the extracellular fluid, the concentration of positive and negative charges must balance to a very high degree of precision, such that the net charge density $\rho = \sum_i z_i F c_i$ is approximately zero.

This principle allows us to treat the bulk intracellular and extracellular fluids as isopotential regions and to dispense with solving Poisson's equation there. The entire problem of calculating the resting potential simplifies to analyzing the currents flowing directly across the membrane itself.

#### The Equivalent Circuit Model and the Electrogenic Pump

The most intuitive framework for modeling transmembrane currents is the **[equivalent circuit model](@entry_id:269555)**. In this model:
-   The membrane acts as a capacitor, $C_m$.
-   Each ion-permeable pathway (a population of channels) is represented by a **conductance**, $g_i$, in series with a battery representing the Nernst potential, $E_i$. Conductance ($g$, in Siemens) is the inverse of resistance and describes the ease with which ions can flow.
-   The Na$^+$/K$^+$ pump, which generates a net current, is modeled as a [current source](@entry_id:275668), $I_{pump}$.

According to Kirchhoff's current law, at the steady-state resting potential ($V_{rest}$), the sum of all currents flowing across the membrane must be zero. If we first neglect the pump current, the total passive current is:

$I_{total} = \sum_i I_i = \sum_i g_i(V_{rest} - E_i) = 0$

Solving for $V_{rest}$ yields:

$V_{rest} = \frac{\sum_i g_i E_i}{\sum_i g_i}$

This reveals that the resting potential is a weighted average of the Nernst potentials of the permeant ions, where the weighting factor for each ion is its relative conductance. Because resting neurons are most permeable to $\mathrm{K}^+$, $g_K$ is the largest conductance, and $V_{rest}$ is drawn close to $E_K$.

Now, let's include the **electrogenic** current from the Na$^+$/K$^+$ pump [@problem_id:4507503]. The pump's stoichiometry of moving 3 $\mathrm{Na}^+$ out for every 2 $\mathrm{K}^+$ in results in a net extrusion of one positive charge per cycle. This constitutes a continuous outward current, $I_{pump}$. A single pump operating at $100\,\mathrm{Hz}$ generates a tiny current of about $1.6 \times 10^{-5}\,\mathrm{pA}$ [@problem_id:4507556]. However, with millions of pumps on the neuron surface, the total pump current is significant.

Including $I_{pump}$ in the current-balance equation:

$\sum_i g_i(V_{rest} - E_i) + I_{pump} = 0$

Solving for $V_{rest}$ now gives:

$V_{rest} = \frac{\sum_i g_i E_i}{\sum_i g_i} - \frac{I_{pump}}{g_{total}}$ where $g_{total} = \sum_i g_i$.

The [electrogenic pump](@entry_id:175576) current directly shifts the membrane potential. Since $I_{pump}$ is an outward positive current, the term $-I_{pump}/g_{total}$ is negative, making $V_{rest}$ more negative (hyperpolarized) than it would be from passive leaks alone. This hyperpolarizing influence of the pump can shift the resting potential by several millivolts, a small but physiologically crucial effect [@problem_id:4507503].

#### The Goldman-Hodgkin-Katz Model: Permeability vs. Conductance

An alternative and more physically detailed model is the **Goldman-Hodgkin-Katz (GHK) equation**. Derived from the Nernst-Planck [electrodiffusion](@entry_id:201732) theory under a "constant field" assumption, the GHK equation expresses the total current or voltage in terms of ionic **permeabilities** ($P_i$) rather than conductances. The GHK voltage equation for the principal monovalent ions is:

$V_{rest} = \frac{RT}{F} \ln\left(\frac{P_K[\mathrm{K}^+]_{out} + P_{Na}[\mathrm{Na}^+]_{out} + P_{Cl}[\mathrm{Cl}^-]_{in}}{P_K[\mathrm{K}^+]_{in} + P_{Na}[\mathrm{Na}^+]_{in} + P_{Cl}[\mathrm{Cl}^-]_{out}}\right)$

A frequent point of confusion is the relationship between permeability $P_i$ and conductance $g_i$ [@problem_id:4507536]. They are related but not identical.
-   **Permeability ($P_i$)** is a parameter in the GHK model that reflects the ion's ability to partition into and diffuse across the membrane. It is treated as a fundamental constant for a given channel type.
-   **Conductance ($g_i$)** is an empirical parameter from the [equivalent circuit model](@entry_id:269555). It is formally defined as the slope of the current-voltage (I-V) curve: $g_i = dI_i/dV$.

The I-V relationship predicted by the GHK *current* equation is generally non-linear (it does not obey Ohm's law). This means the slope conductance, $g_i$, is not constant but depends on voltage, concentrations, and temperature. By differentiating the GHK current equation, one can show that $g_i$ is directly proportional to $P_i$. However, the factor of proportionality is itself a complex function of voltage and other parameters. The two concepts are therefore deeply connected: permeability is the more fundamental physical parameter from which the effective [electrical conductance](@entry_id:261932) at any given voltage can be derived.