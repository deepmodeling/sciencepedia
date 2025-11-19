## Introduction
Hypersonic flight pushes vehicles through atmospheric conditions so extreme that the very air surrounding them changes its chemical makeup and energetic state. At speeds exceeding Mach 5, the assumptions of classical thermodynamics break down, creating a state of chemical and [thermal nonequilibrium](@entry_id:191586). This departure from equilibrium presents a critical challenge for [aerospace engineering](@entry_id:268503), as it fundamentally alters aerodynamic forces, surface heating, and communication systems, rendering traditional models inaccurate. This article addresses this knowledge gap by providing a comprehensive framework for understanding and modeling these complex phenomena. Across three chapters, you will first explore the fundamental "Principles and Mechanisms" that govern nonequilibrium, including the competing timescales and multi-temperature models. Next, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied to vehicle design, materials science, and computational methods. Finally, a series of "Hands-On Practices" will allow you to solidify your understanding of these advanced concepts.

## Principles and Mechanisms

The [hypersonic flight](@entry_id:272087) environment is characterized by extremes of temperature and pressure, particularly within the [shock layer](@entry_id:197110) surrounding a vehicle. As established in the introductory chapter, these conditions are sufficient to alter the chemical composition and the internal energy state of the gas. The assumption of a simple, uniform gas in thermodynamic equilibrium breaks down. To accurately predict the aerodynamic forces, surface heat transfer, and communication properties of a hypersonic system, we must develop a framework that accounts for these **nonequilibrium** effects. This chapter delves into the fundamental principles and mechanisms governing chemical and [thermal nonequilibrium](@entry_id:191586) in high-temperature gases.

### The Breakdown of Thermodynamic Equilibrium

The classical concept of temperature, as enshrined in the Zeroth Law of Thermodynamics, relies on the system being in a state of **internal [thermodynamic equilibrium](@entry_id:141660)**. In such a state, intensive properties like temperature and pressure are uniform throughout. However, many systems of practical interest, such as the turbulent, chemically reacting exhaust plume of a [scramjet](@entry_id:269493) engine, are fundamentally not in equilibrium [@problem_id:1897094]. Measurements taken at different locations within such a system at the same instant would yield different local temperatures, demonstrating that a single temperature cannot be assigned to the system as a whole.

The departure from equilibrium in hypersonic flows is a direct consequence of the competition between different physical processes occurring at finite rates. We can conceptualize this by comparing the characteristic timescales of these processes:

1.  The **characteristic flow time (${\tau_{flow}}$)**: This represents the time a fluid parcel takes to traverse a region of interest. For a region of length $L$ with flow velocity $U$, a simple estimate is $\tau_{flow} \approx L/U$.
2.  The **characteristic [relaxation time](@entry_id:142983) (${\tau_{relax}}$)**: This is the time required for an internal energy mode of the gas molecules (such as vibration) to equilibrate with the other modes after a disturbance.
3.  The **characteristic chemical time (${\tau_{chem}}$)**: This is the time required for chemical reactions (such as molecular dissociation) to reach equilibrium at the local temperature and pressure.

When the flow time is much longer than the relaxation and chemical times ($\tau_{flow} \gg \tau_{relax}$ and $\tau_{flow} \gg \tau_{chem}$), the gas has ample time to adjust its internal state and composition to the local conditions. The flow can be considered to be in **[local thermodynamic equilibrium](@entry_id:139579) (LTE)**. Conversely, when the flow time is much shorter than these internal process times ($\tau_{flow} \ll \tau_{relax}$ or $\tau_{flow} \ll \tau_{chem}$), the internal state of the gas does not have time to change as it flows; it is said to be **frozen**.

The most complex and interesting regime occurs when these timescales are of the same order of magnitude ($\tau_{flow} \approx \tau_{relax}$ or $\tau_{flow} \approx \tau_{chem}$). In this **nonequilibrium** regime, the internal state of the gas evolves concurrently with its movement, necessitating a more detailed physical description. The ratio of the flow time to a process time, known as the **Damköhler number** ($Da = \tau_{flow} / \tau_{process}$), provides a quantitative measure of the degree of nonequilibrium.

### Chemical Nonequilibrium

A hypersonic vehicle re-entering the atmosphere creates a strong [bow shock](@entry_id:203900) that abruptly heats the air to several thousand Kelvin. At these temperatures, diatomic oxygen ($O_2$) and nitrogen ($N_2$) molecules begin to dissociate into their atomic constituents ($O$ and $N$). This process is not instantaneous.

Immediately downstream of the shock wave, the gas is suddenly compressed and heated, but its chemical composition remains unchanged from its freestream state for a brief moment. Here, the temperature is high, so the chemical timescale $\tau_{chem}$ becomes finite, but the flow time through this thin post-shock region is very short. This region, where $\tau_{flow}$ and $\tau_{chem}$ are comparable, is characterized by significant **[chemical nonequilibrium](@entry_id:265362)** [@problem_id:1763312]. As the fluid parcel decelerates towards the vehicle's stagnation point, its residence time $\tau_{flow}$ increases dramatically. The chemical reactions proceed, and the composition shifts towards its equilibrium state for the high-temperature, high-pressure conditions in the stagnation region. Conversely, as the flow expands around the vehicle's shoulder, it accelerates and cools. The temperature drop causes $\tau_{chem}$ to increase exponentially, while the high speed makes $\tau_{flow}$ very short. This leads to a **chemically frozen** flow, where the dissociated composition from the hot nose region is "locked in" as it flows downstream [@problem_id:1763312].

While the mass fractions of individual molecular and atomic species are not conserved during these reactions, the fundamental atomic elements are. For a gas mixture composed of $N_s$ species made from $N_e$ elements, the conservation of an individual species $s$ is given by:
$$
\frac{\partial \rho_s}{\partial t} + \nabla \cdot (\rho_s \mathbf{v}) + \nabla \cdot \mathbf{j}_s = \dot{\omega}_s
$$
where $\rho_s$ is the partial density, $\mathbf{v}$ is the [mass-averaged velocity](@entry_id:149575), $\mathbf{j}_s$ is the diffusion mass flux, and $\dot{\omega}_s$ is the mass production rate from chemical reactions.

The mass fraction of an element $j$ in the mixture, $Y_j^*$, is the sum of its mass fractions across all species, $Y_j^* = \sum_s \phi_{sj} Y_s$, where $\phi_{sj}$ is the constant [mass fraction](@entry_id:161575) of element $j$ in species $s$. By multiplying the species [continuity equation](@entry_id:145242) by $\phi_{sj}$ and summing over all species, we can derive a conservation equation for the element [mass fraction](@entry_id:161575) [@problem_id:463281]:
$$
\frac{\partial}{\partial t}(\rho Y_j^*) + \nabla\cdot(\rho Y_j^*\mathbf{v} + \mathbf{j}_j^*) = \sum_{s=1}^{N_s} \phi_{sj}\dot{\omega}_s
$$
Here, $\mathbf{j}_j^* = \sum_s \phi_{sj} \mathbf{j}_s$ is the elemental [diffusion flux](@entry_id:267074). The crucial insight is that the source term on the right-hand side is identically zero. This is because any chemical reaction, such as $N_2 \rightleftharpoons 2N$, merely rearranges atoms between different molecular forms. For any reaction, the total mass of each element is conserved. Therefore, $\sum_s \phi_{sj}\dot{\omega}_s = 0$, and we arrive at the elemental conservation equation:
$$
\frac{\partial}{\partial t}(\rho Y_j^*) + \nabla\cdot(\rho Y_j^*\mathbf{v} + \mathbf{j}_j^*) = 0
$$
This principle is powerful, as it reduces the number of conservation equations that must be solved in a numerical simulation from the number of species ($N_s$) to the number of elements ($N_e$), which is typically much smaller.

### Thermal Nonequilibrium

The internal energy of a molecule is partitioned among several modes: translation (motion of the molecule's center of mass), rotation, vibration, and [electronic excitation](@entry_id:183394). Collisions between molecules are the mechanism for transferring energy between these modes. In a high-temperature gas, the rates of energy exchange are not equal for all modes.

Collisions are very efficient at equilibrating translational and rotational energies. Consequently, these two modes can typically be described by a single **translational-rotational temperature, $T$**. However, the transfer of energy into and out of the vibrational and electronic modes is much less efficient, requiring many more collisions. This leads to a state of **[thermal nonequilibrium](@entry_id:191586)**, where the population of vibrational and electronic energy levels may correspond to a temperature different from the translational-rotational temperature. A widely used simplification, known as the **[two-temperature model](@entry_id:180856)**, assumes that the vibrational and electronic modes are in equilibrium with each other at a single **vibrational-electronic temperature, $T_v$** [@problem_id:2472751].

#### Vibrational Relaxation

The process by which the vibrational energy of the gas, $E_{vib}$, approaches its equilibrium value at the local translational temperature, $E_{vib}^*$, is called **[vibrational relaxation](@entry_id:185056)**. This process is often modeled by the macroscopic **Landau-Teller equation**:
$$
\frac{dE_{vib}}{dt} = \frac{E_{vib}^*(T) - E_{vib}(T_v)}{\tau_v}
$$
where $\tau_v$ is the [vibrational relaxation](@entry_id:185056) time. This equation shows that the rate of [energy transfer](@entry_id:174809) is proportional to the deviation from equilibrium.

This macroscopic model has a firm microscopic foundation. By considering the collisional transitions between individual vibrational quantum levels, governed by a set of **master equations**, one can derive the Landau-Teller form. For a pure diatomic gas of simple harmonic oscillators, this derivation [@problem_id:463199] yields a precise expression for the relaxation time:
$$
\tau_v = \frac{1}{N K_{1,0}[1 - \exp(-\theta_v/T)]}
$$
where $N$ is the total [number density](@entry_id:268986), $K_{1,0}$ is the rate constant for de-excitation from the first to the ground vibrational level, and $\theta_v$ is the [characteristic vibrational temperature](@entry_id:153344) of the molecule.

#### Consequences of Thermal Nonequilibrium

Thermal nonequilibrium has profound effects on the macroscopic properties of the gas. One example is the **speed of sound**. An acoustic wave is a small pressure disturbance that propagates through the gas. The speed of propagation, $a$, depends on the gas's compressibility, which in turn depends on its [specific heat ratio](@entry_id:145177), $\gamma$. If the wave frequency is very high, the compressions and expansions happen too quickly for vibrational energy to be exchanged ($\tau_{process} \ll \tau_v$). The vibrational mode remains "frozen," and the gas behaves as if it only has translational and rotational specific heats. This gives the **[frozen speed of sound](@entry_id:184302), $a_f$**. If the frequency is very low ($\tau_{process} \gg \tau_v$), the vibrational mode remains in equilibrium throughout the wave's passage, contributing fully to the specific heat. This gives the **[equilibrium speed of sound](@entry_id:197618), $a_e$**. Since the equilibrium specific heat is larger, the equilibrium gas is more compressible, and $a_e  a_f$. For a model gas, the difference can be explicitly calculated [@problem_id:463277]:
$$
a_f^2 - a_e^2 = \frac{R^2 T\,c_{v,i}}{c_{v,f}(c_{v,f}+c_{v,i})}
$$
where $c_{v,f}$ is the specific heat of the active (frozen) modes and $c_{v,i}$ is the contribution from the relaxing internal mode.

A more critical consequence for vehicle design is the effect on **surface heat transfer**. In the [hypersonic boundary layer](@entry_id:750484) over a vehicle, [viscous dissipation](@entry_id:143708) converts the flow's kinetic energy into thermal energy, creating a very hot region. If [vibrational relaxation](@entry_id:185056) is slow compared to the time the gas spends in the boundary layer ($\tau_v \gg \tau_{flow}$), the vast amount of energy from [viscous heating](@entry_id:161646) is channeled primarily into the translational and [rotational modes](@entry_id:151472). This causes the translational temperature $T$ to be significantly higher than it would be in an equilibrium flow where the energy could be shared with the vibrational mode. The heat flux to the vehicle's surface, $q_w$, is driven by the gradient of the translational temperature at the wall, according to Fourier's law: $q_w = -k(T) \frac{\partial T}{\partial y}|_w$. A higher overall profile for $T$ results in a steeper gradient at a cold wall, and thus a substantially larger heat flux [@problem_id:2472751]. Accurately predicting this heat flux is paramount for designing an effective [thermal protection system](@entry_id:154014).

### Coupled Thermochemical Nonequilibrium

In reality, thermal and [chemical nonequilibrium](@entry_id:265362) are not independent phenomena; they are intimately coupled. The rate of chemical reactions depends on the vibrational state of the molecules, and chemical reactions, in turn, alter the vibrational energy content of the gas.

The dissociation of a molecule like $N_2$ is not simply a matter of a sufficiently energetic collision. A molecule that is already in a high vibrational state is "stretched" and closer to its dissociation limit, making it much more likely to dissociate upon collision. This principle of **vibration-[dissociation](@entry_id:144265) coupling** means that the dissociation rate constant, $k_f$, is a function of both the translational temperature $T$ (which governs collision energy) and the vibrational temperature $T_v$ (which governs the internal state).

A highly successful [phenomenological model](@entry_id:273816) for this coupling was proposed by Park. In **Park's [two-temperature model](@entry_id:180856)**, the Arrhenius rate expression is controlled by a geometric average of the two temperatures:
$$
k_f(T, T_v) \propto \exp\left(-\frac{E_d}{k_B T_a}\right), \quad \text{with } T_a = \sqrt{T T_v}
$$
where $E_d$ is the [dissociation energy](@entry_id:272940). This form can be rationalized with a microscopic collision model [@problem_id:463240]. If one assumes that a reaction occurs when the geometric mean of the collisional kinetic energy ($E_c$) and the molecule's vibrational energy ($E_v$) exceeds a threshold, then the most probable [reaction path](@entry_id:163735) (the path of "least resistance") leads directly to this controlling temperature, $T_a = \sqrt{T T_v}$.

The relationship is bidirectional. Dissociation preferentially removes molecules from high vibrational states, acting as a sink for [vibrational energy](@entry_id:157909). Conversely, recombination of atoms often produces molecules in highly excited vibrational states, acting as a source. Immediately behind a shock, the gas is vibrationally cold. Energy from the hot translational mode begins to flow into both vibrational excitation (governed by $\tau_v$) and dissociation (governed by $\tau_{chem}$). The competition between these two pathways determines the thermochemical state of the gas as it evolves [@problem_id:463290].

### A Unified Modeling Framework

To simulate a [hypersonic flow](@entry_id:263090) with these coupled effects, one must solve a system of governing equations that accounts for all relevant phenomena. This typically includes the conservation of mass, momentum, and total energy, supplemented by additional conservation equations for species and [vibrational energy](@entry_id:157909).

The source terms in these equations encapsulate the nonequilibrium physics. The species source term, $\dot{\omega}_s$, depends on [reaction rates](@entry_id:142655) $k_f(T, T_v)$ that are functions of both temperatures. To ensure the system relaxes to the correct chemical equilibrium when $T_v \to T$, the forward ($k_f$) and reverse ($k_r$) rates must be related through a generalized law of mass action. This relationship can be derived from statistical mechanics [@problem_id:463205] and takes the form:
$$
\frac{k_f(T, T_v)}{k_r(T)} = K_c(T) \frac{Q_{A_2,vib}(T)}{Q_{A_2,vib}(T_v)} \frac{Q_{A_2,elec}(T)}{Q_{A_2,elec}(T_v)}
$$
where $K_c(T)$ is the standard one-temperature [equilibrium constant](@entry_id:141040) and the $Q$ terms are partition functions.

The complexity also appears in the transport fluxes, particularly the **total heat flux vector, $\mathbf{q}$**. It is composed of conduction due to temperature gradients and enthalpy transport due to species diffusion. A full derivation [@problem_id:463296] reveals its structure:
$$
\mathbf{q} = - \left( \lambda_{tr} + \frac{1}{T}\sum_{s=1}^{N_s} h_s D_s^T \right) \nabla T - \lambda_v \nabla T_v - \sum_{s=1}^{N_s} h_s \rho D_{sm} \nabla Y_s
$$
This expression elegantly summarizes the interwoven transport mechanisms:
- The first term is the effective heat flux driven by the translational temperature gradient $\nabla T$. It includes standard Fourier conduction ($\lambda_{tr}$) and the energy carried by thermal diffusion (the Soret effect), where species diffuse in response to a temperature gradient.
- The second term, $-\lambda_v \nabla T_v$, is the conductive heat flux driven by the vibrational temperature gradient, a term that exists only in multi-temperature models.
- The third term represents the transport of [specific enthalpy](@entry_id:140496) $h_s$ by species as they diffuse due to concentration gradients $\nabla Y_s$ (ordinary diffusion).

This comprehensive modeling framework, built upon the principles of competing timescales and coupled energy exchange, is essential for the analysis and design of vehicles that operate in the challenging [hypersonic flight](@entry_id:272087) regime.