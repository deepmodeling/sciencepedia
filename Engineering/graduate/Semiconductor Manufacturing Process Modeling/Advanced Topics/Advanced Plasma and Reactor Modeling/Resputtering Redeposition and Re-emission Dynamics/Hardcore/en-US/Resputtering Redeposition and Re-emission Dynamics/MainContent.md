## Introduction
In the world of semiconductor manufacturing, the quest to fabricate smaller, more complex nanoscale devices hinges on our ability to precisely control the deposition and etching of materials. As feature dimensions shrink and aspect ratios soar, the simple picture of particles arriving directly from a source breaks down. Instead, a complex dance of secondary [particle dynamics](@entry_id:1129385)—[resputtering](@entry_id:1130966), redeposition, and re-emission—takes center stage, often governing the final shape and performance of a device. Understanding and predicting these phenomena is a critical challenge, as they can be both a source of process-limiting defects and a powerful tool for profile engineering.

This article provides a comprehensive exploration of these crucial particle-surface interactions. In the first chapter, **Principles and Mechanisms**, we will deconstruct the fundamental physics, from the [flux balance](@entry_id:274729) at a surface to the collision cascades and transport regimes that dictate particle fates. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these principles are applied to solve real-world challenges in [semiconductor fabrication](@entry_id:187383), such as achieving conformal coverage in deep trenches, and explore their relevance in related fields like fusion energy. Finally, the **Hands-On Practices** section will provide an opportunity to apply these concepts to solve quantitative problems, solidifying your understanding of these complex dynamics. By navigating these chapters, you will gain a robust framework for modeling and controlling [surface evolution](@entry_id:636373) in modern plasma processes.

## Principles and Mechanisms

The evolution of a surface during plasma-assisted deposition or etching is a complex interplay of particle arrival, [surface reaction](@entry_id:183202), particle ejection, and transport. To understand and model these processes, we must first deconstruct them into their constituent physical mechanisms. This chapter lays out the fundamental principles governing these interactions, from the initial [flux balance](@entry_id:274729) at a surface element to the advanced dynamics in multicomponent and reactive systems.

### The Fundamental Flux Balance at the Surface

The net change in the material on a surface can be described by a [local conservation](@entry_id:751393) equation, or a **[flux balance](@entry_id:274729)**. Consider a differential element of the surface. The rate of change of film thickness, $h$, at this location is directly proportional to the net flux of atoms, $J_{net}$, that are incorporated into or removed from the surface. This relationship is given by:

$$
\frac{dh}{dt} = v_a J_{net}
$$

where $v_a$ is the volume occupied by a single atom in the film. The net flux $J_{net}$ is the algebraic sum of all source (mass gain) and sink ([mass loss](@entry_id:188886)) terms. In a typical [plasma processing](@entry_id:185745) environment, this balance can be expressed as follows :

$$
J_{net} = J_{dep} - J_{resput} + J_{redepos} - J_{etch}
$$

Each term in this equation represents a distinct physical process:

1.  **Direct Deposition ($J_{dep}$):** This is the primary source of material, representing the flux of atoms arriving from the plasma source (e.g., a sputtering target or a chemical precursor gas) that successfully adhere to the surface. It is a positive term, contributing to film growth.

2.  **Resputtering ($J_{resput}$):** This is a primary removal mechanism, representing the physical ejection of atoms from the film itself due to bombardment by energetic ions from the plasma. As it is a [mass loss](@entry_id:188886) process, it is a negative term in the balance.

3.  **Redeposition ($J_{redepos}$):** Atoms that are sputtered from one location on the surface can travel and deposit onto another location. This redeposition of previously sputtered material acts as a secondary source of deposition flux and is therefore a positive term.

4.  **Etching ($J_{etch}$):** This term encompasses other removal mechanisms, such as spontaneous chemical reactions that form volatile products or [thermal desorption](@entry_id:204072) of surface species. It is a negative term representing mass loss.

These processes are not independent; for instance, [resputtering](@entry_id:1130966) is the source for the material that is subsequently redeposited. To model [surface evolution](@entry_id:636373) accurately, we must understand the principles and governing parameters behind each of these flux components.

### Core Mechanisms of Particle-Surface Interaction

The terms in the [flux balance](@entry_id:274729) equation are macroscopic consequences of microscopic events at the atomic scale. The fate of any particle striking the surface, and the fate of the surface atoms themselves, are determined by a cascade of interactions governed by energy transfer, momentum conservation, and [chemical affinity](@entry_id:144580).

#### Sticking, Reflection, and Re-emission

When a particle (neutral atom or ion) arrives at a surface, it does not necessarily stay. The probability that an incident particle will be incorporated into the film is known as the **[sticking probability](@entry_id:192174)** (or sticking coefficient), denoted by $s$. This probability is a complex function of the particle's kinetic energy $E$, its [angle of incidence](@entry_id:192705) $\theta$ with respect to the surface normal, the surface temperature $T$, and the chemical nature of both the particle and the surface. In general, we write it as $s(E, \theta, T)$.

Particles that do not stick are said to be **re-emitted**. Re-emission is a collective term for any process where the incident particle scatters or reflects from the surface and returns to the gas phase. This process does not contribute to the local [mass balance](@entry_id:181721)—the particle never becomes part of the film—but it plays a crucial role in redistributing particle flux within high-aspect-ratio features like trenches and vias .

The reasons why the [sticking probability](@entry_id:192174) is often less than one ($s  1$) depend on the energy of the incident particle :

*   **For low-energy neutrals** (with kinetic energy $E$ on the order of thermal energies, $\sim 1 \, \mathrm{eV}$), typical in Physical Vapor Deposition (PVD), sticking is often a two-step process. First, the particle must be captured by the attractive [potential well](@entry_id:152140) at the surface. This capture probability, $P_{cap}$, depends on the particle dissipating its normal component of kinetic energy, often modeled as a function of $E \cos^2\theta$. Second, once temporarily trapped (physisorbed), the particle must fully dissipate its excess energy to the lattice before it can escape due to [thermal fluctuations](@entry_id:143642). The rate of [thermal desorption](@entry_id:204072) is described by an Arrhenius law, $k_{des}(T) = \nu \exp(-E_b / k_B T)$, where $E_b$ is the surface binding energy, $\nu$ is an attempt frequency, and $k_B$ is the Boltzmann constant. A particle with a short energy accommodation time, $\tau_{acc}$, has a higher chance of surviving desorption. Thus, for neutrals, $s  1$ can arise from inefficient initial energy transfer or rapid [thermal desorption](@entry_id:204072) due to high surface temperature $T$ or weak [chemical affinity](@entry_id:144580) (low $E_b$).

*   **For high-energy ions** (with $E \gg 10 \, \mathrm{eV}$), common in ion-assisted processes, the shallow potential well and [thermal desorption](@entry_id:204072) are less relevant. The primary reason for non-sticking is energetic **backscattering**, or elastic reflection. In this process, the ion undergoes one or more high-energy collisions with surface atoms and scatters back into the vacuum, retaining a substantial fraction of its initial energy. The probability of [backscattering](@entry_id:142561), $R_{back}(E, \theta)$, increases significantly at grazing angles of incidence and depends strongly on the [mass ratio](@entry_id:167674) of the ion to the surface atoms. For ions, sticking essentially means coming to rest within the film, either at the surface or embedded beneath it (implantation). The sticking probability is therefore determined by [probability conservation](@entry_id:149166): $s_i(E, \theta, T) \approx 1 - R_{back}(E, \theta)$.

The direct deposition flux, $J_{dep}$, is thus the flux of incident source atoms, $\Phi_n$, that successfully stick. Its mathematical form incorporates the sticking probability:
$$
J_{dep} = \int \! \int s(E, \theta, T) \Phi_n(E, \Omega) \cos\theta \, dE \, d\Omega
$$
where the integral is over all energies and incident solid angles $\Omega$, and the $\cos\theta$ term projects the directional flux onto the surface area. The re-emitted flux is simply the fraction $(1-s)$ of the incident flux.

#### Sputtering and Resputtering

While re-emission concerns the fate of the incident particle, **sputtering** describes the fate of the surface itself. Sputtering is a physical erosion process in which atoms from the solid target are ejected due to [momentum transfer](@entry_id:147714) from an energetic incident particle, typically an ion. It is crucial to distinguish this from re-emission: sputtering is a **mass removal** process that ejects target atoms, whereas re-emission is a **scattering** event that redirects the incident particle and involves no net mass change .

The mechanism of sputtering involves the incident ion initiating a **collision cascade** in the near-surface region of the target. Through a series of binary collisions, energy is distributed among target atoms. If a surface atom receives enough kinetic energy to overcome its **[surface binding energy](@entry_id:1132665) ($U_0$)**, it can be ejected, or sputtered. Within the context of film deposition, two terms are often used :

*   **Primary Sputtering:** The removal of atoms from the original substrate material (e.g., sputtering of silicon atoms from a wafer at the beginning of deposition).
*   **Resputtering:** The removal of atoms from the newly deposited film (e.g., sputtering of copper atoms from a growing copper film).

The key parameter quantifying the efficiency of this process is the **sputter yield, $Y(E_i, \theta_i)$**, defined as the average number of target atoms ejected per incident ion of energy $E_i$ and incidence angle $\theta_i$ . According to Sigmund's foundational linear cascade theory, the sputter yield is directly proportional to the amount of energy the ion deposits into nuclear collisions near the surface and inversely proportional to the [surface binding energy](@entry_id:1132665):

$$
Y(E_i, \theta_i) \propto \frac{\alpha(E_i, Z_1, Z_2) S_n(E_i)}{U_0}
$$

Here, $S_n(E_i)$ is the **[nuclear stopping power](@entry_id:1128948)**, which describes the ion's rate of energy loss due to [elastic collisions](@entry_id:188584), and $\alpha$ is a factor that depends on the masses of the ion ($Z_1$) and target atom ($Z_2$).

The dependence of the yield on the angle of incidence, $\theta_i$, is particularly important for profile evolution. For many ion-target combinations, the yield *increases* as the angle moves from [normal incidence](@entry_id:260681) ($\theta_i=0^\circ$) toward grazing angles. This is because at [oblique incidence](@entry_id:267188), the ion's trajectory is shallower, and the [collision cascade](@entry_id:1122653) deposits its energy closer to the surface, increasing the [escape probability](@entry_id:266710) of target atoms. This dependence is often approximated by the relation $Y(\theta_i) \approx Y(0)(\cos\theta_i)^{-f}$, where $f$ is typically between 1 and 2. At very grazing angles (e.g., $ 70-80^\circ$), the yield rapidly drops to zero as ion reflection becomes the dominant process .

The [resputtering](@entry_id:1130966) flux, $J_{resput}$, is therefore the integral of the local ion flux, $\Phi_i$, multiplied by the sputter yield over all ion energies and angles:
$$
J_{resput} = \int \! \int Y(E, \theta) \Phi_i(E, \Omega) \, dE \, d\Omega
$$

#### The Origin of Energetic Ions: Sheath Acceleration

The energy and angle of ions striking a surface, which are critical inputs for determining the [sputter yield](@entry_id:1132237), are not arbitrary. They are determined by the acceleration of ions across the plasma **sheath**, a thin, positively charged boundary layer that forms between the quasi-neutral bulk plasma and any surface in contact with it. The potential drop across the sheath provides the energy for [ion bombardment](@entry_id:196044) .

The distribution of ion energies arriving at the surface is known as the **Ion Energy Distribution Function (IEDF)**. The shape of the IEDF is dictated by the nature of the electrical bias applied to the substrate:

*   **DC Bias:** If a constant negative DC voltage, $V_w$, is applied, ions accelerate across a static potential drop of approximately $\Delta\Phi = V_p - V_w$, where $V_p$ is the [plasma potential](@entry_id:198190) (typically a small positive voltage). In a collisionless sheath, all ions gain nearly the same energy, $e\Delta\Phi$. This results in a narrow, nearly monoenergetic IEDF.

*   **RF Bias:** If a radio-frequency (RF) voltage is applied (e.g., at the standard industrial frequency of $13.56 \, \mathrm{MHz}$), the sheath potential oscillates in time. The resulting IEDF depends on the ratio of the **ion transit time** across the sheath, $\tau_i$, to the RF period, $T_{RF}$.
    *   If $\tau_i \gg T_{RF}$ (heavy ions, high frequency), ions are too slow to respond to the oscillating field and effectively feel only the time-averaged sheath potential. The IEDF is narrow, similar to the DC case.
    *   If $\tau_i \sim T_{RF}$ (a common regime for Ar$^+$ in a 13.56 MHz plasma), ions cross the sheath in a time comparable to one RF cycle. They experience a fraction of the oscillating field that depends on the phase at which they entered. This leads to a characteristic broadening of the IEDF, which often exhibits a bimodal, two-peaked structure.

Furthermore, if the pressure in the reactor is high enough, ions can undergo collisions within the sheath. The most important of these is **charge-exchange**, where a fast ion collides with a slow background neutral atom, creating a new slow ion and a fast neutral. The new slow ion is then accelerated only through the *remaining* potential drop of the sheath. This process populates the IEDF with a continuous **low-energy tail**, in addition to the main peaks from collisionless transit .

### Transport and Redeposition of Sputtered Material

Once an atom is sputtered from a surface, it travels through the processing chamber until it either escapes to the vacuum pumps or strikes another surface. Its journey determines where and how it might redeposit.

#### Ballistic versus Diffusive Transport Regimes

The nature of this transport depends on the frequency of collisions between the sputtered particle and the background gas atoms . This is quantified by the **mean free path, $\lambda$**, which is the average distance a particle travels between collisions. For a dilute gas, it is given by:

$$
\lambda = \frac{k_B T}{\sqrt{2} \pi d^2 p}
$$

where $p$ is the background gas pressure, $T$ is the gas temperature, and $d$ is the effective collision diameter of the gas atoms.

The transport regime is determined by comparing the mean free path $\lambda$ to the characteristic length scale of the system, $L$ (e.g., the width of a trench), via the dimensionless **Knudsen number**:

$$
Kn = \frac{\lambda}{L}
$$

*   **Ballistic Transport ($Kn \gg 1$):** When the mean free path is much larger than the feature size, as is common in low-pressure PVD systems, particles travel in straight lines without interruption by gas-phase collisions. Particle trajectories are governed purely by their initial ejection angle and line-of-sight geometry.

*   **Diffusive Transport ($Kn \ll 1$):** When the mean free path is much smaller than the feature size, particles undergo many collisions before reaching a surface. Their motion resembles a random walk, and transport is governed by diffusion. This randomizes their direction, leading to a more isotropic flux arriving at surfaces within a feature.

#### Modeling Ballistic Transport: The View Factor Method

In the common ballistic regime, the complex problem of [particle transport](@entry_id:1129401) and redeposition can be modeled with elegant mathematical tools borrowed from the field of radiative heat transfer . If we assume that re-emitted and sputtered particles leave the surface diffusely (with a **Lambertian** or $\cos\theta$ [angular distribution](@entry_id:193827)), then the fraction of particles leaving one surface patch, $A_i$, that directly arrive at another patch, $A_j$, can be described by a purely geometric quantity called the **view factor, $F_{ij}$**.

The view factor is given by the integral:

$$
F_{ij} = \frac{1}{A_i} \int_{A_i} \int_{A_j} V(\mathbf{x}_i, \mathbf{x}_j) \frac{\cos\theta_i \cos\theta_j}{\pi R^2} \, dA_j \, dA_i
$$

where $R$ is the distance between the differential surface elements $dA_i$ and $dA_j$, $\theta_i$ and $\theta_j$ are the angles between the line connecting them and their respective surface normals, and $V(\mathbf{x}_i, \mathbf{x}_j)$ is a [visibility function](@entry_id:756540) that is 1 if the two points have a direct line of sight and 0 otherwise.

This formulation has two powerful fundamental properties:

1.  **Reciprocity Relation:** $A_i F_{ij} = A_j F_{ji}$. The total number of particles exchanged between two surfaces is the same regardless of which is considered the source and which is the receiver.

2.  **Closure Rule:** $\sum_{j=1}^{N} F_{ij} = 1$. For any surface $A_i$ in a closed enclosure of $N$ surfaces, the sum of the [view factors](@entry_id:756502) from $A_i$ to all other surfaces (including itself, $F_{ii}$) must equal one, reflecting the conservation of particles.

These view factors form the basis of many feature-scale simulation tools, allowing the complex geometric problem of redeposition to be solved by calculating the geometric exchange of flux between discretized surface elements.

### Advanced Mechanisms and Consequences

The principles outlined above form the basis for understanding more complex phenomena that arise in technologically relevant processes, such as those involving reactive gases or multicomponent materials.

#### Reactive Environments and Chemically Enhanced Sputtering

In many processes, such as [reactive ion etching](@entry_id:195507) (RIE), the plasma contains not only inert ions (like Ar$^+$) but also chemically reactive neutral species (like fluorine or oxygen). In this case, the removal of surface atoms can be accelerated by a synergy between physical bombardment and chemical reaction . This is known as **chemically enhanced sputtering**.

The total yield, $Y_{total}$, can be phenomenologically described as the sum of three components:

$$
Y_{total} = Y_{phys} + Y_{chem} + Y_{synergy}
$$

*   $Y_{phys}$ is the yield from pure [physical sputtering](@entry_id:183733).
*   $Y_{chem}$ is the yield from spontaneous chemical etching (reaction forming a volatile product).
*   $Y_{synergy}$ is the additional yield arising from the interaction between the ion bombardment and [surface chemistry](@entry_id:152233). This synergistic effect can occur in two main ways: (1) the chemical reaction modifies the surface, for example by forming a compound with a lower [surface binding energy](@entry_id:1132665), making it easier to physically sputter; or (2) the ion bombardment provides the energy needed to break chemical bonds or desorb weakly volatile reaction products.

This synergy is often the key to achieving high etch rates and selectivity in semiconductor manufacturing.

#### Preferential Sputtering in Multicomponent Films

When a film is composed of more than one element (e.g., an alloy like SiGe or a compound like TiN), an additional complication arises: the different atomic species will generally have different sputter yields. The selective removal of the species with the higher [sputter yield](@entry_id:1132237) is known as **preferential sputtering** .

Consider a binary film of A and B, where the sputter yield of B is greater than that of A ($Y_B > Y_A$). When the surface is subjected to [ion bombardment](@entry_id:196044), species B will be removed at a higher rate relative to its concentration. To maintain a steady-state growth process where the composition of the film being formed is constant, the system must compensate for this differential removal. It does so by altering the composition of the very top surface layer. Specifically, the surface becomes **depleted** in the high-yield species (B) and **enriched** in the low-yield species (A).

This enrichment of the more sputter-resistant component (A) increases its likelihood of being struck by an ion, while the depletion of B decreases its likelihood. At steady state, a surface composition $c_A^*, c_B^*$ is reached where the removal rates of the two species are precisely balanced against their arrival fluxes, such that the net composition of the material being incorporated into the film is constant. For equal arrival fluxes, if $Y_B > Y_A$, the steady-state surface concentration will be $c_A^* > 0.5$ and $c_B^*  0.5$. This effect is a critical consideration in controlling the stoichiometry of compound thin films deposited using energetic processes. The effect is attenuated by local redeposition, as the redeposited flux partially replenishes the sputtered species, weakening the net compositional shift .