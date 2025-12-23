## Introduction
The vacuum vessel and cryostat are foundational components in the quest for [magnetic confinement fusion](@entry_id:180408), forming the physical boundary between the extreme environment of the plasma and the precision-engineered world of superconducting magnets. Their design is not a simple matter of containing a vacuum; it represents a complex interplay of competing requirements, where the demands of [plasma physics](@entry_id:139151), cryogenic thermal isolation, structural integrity, and nuclear safety must be met simultaneously. This article addresses the knowledge gap between isolated engineering principles and their integrated application in a fusion device.

The journey begins with **Principles and Mechanisms**, where we will dissect the fundamental physics of dual-vacuum systems, [gas dynamics](@entry_id:147692), and [thermal insulation](@entry_id:147689). This chapter lays the groundwork, explaining *why* [ultra-high vacuum](@entry_id:196222) is necessary and *how* heat leaks are minimized at cryogenic temperatures. Next, in **Applications and Interdisciplinary Connections**, we will explore the real-world engineering trade-offs, from selecting materials to withstand intense electromagnetic loads and [thermal stresses](@entry_id:180613) to designing systems that are both reliable and maintainable. Finally, **Hands-On Practices** will provide an opportunity to apply these concepts to solve practical design problems, solidifying your understanding of how to balance gas loads, manage thermal displacements, and ensure [system integrity](@entry_id:755778). Through this structured approach, you will gain a comprehensive understanding of the challenges and solutions inherent in designing the heart of a fusion machine.

## Principles and Mechanisms

The design and construction of the vacuum vessel and cryostat are cornerstones of [magnetic confinement fusion](@entry_id:180408) engineering. These components form the immediate environment for the plasma and the superconducting magnets, respectively, and their performance dictates critical aspects of machine operation, from plasma purity and stability to [thermal efficiency](@entry_id:142875) and structural safety. This chapter elucidates the fundamental physical principles and engineering mechanisms that govern their design, moving from the physics of vacuum and heat transfer to the complexities of [structural mechanics](@entry_id:276699) and system integration.

### The Dual-Vacuum Architecture

A key feature of a superconducting [magnetic confinement](@entry_id:161852) device, such as a tokamak, is its **dual-vacuum architecture**. This design consists of two nested, distinct vacuum volumes: the **primary vacuum** within the Vacuum Vessel (VV) and the **insulating vacuum** within the Cryostat. Understanding their profoundly different functions is the first step in appreciating their design requirements .

The **Vacuum Vessel (VV)** contains the fusion plasma. Its interior volume defines the primary vacuum, which must be maintained at Ultra-High Vacuum (UHV) conditions, typically with a **base pressure** (the pressure achieved before plasma operation) in the range of $10^{-6}$ to $10^{-8}\,\text{Pa}$. The scientific driver for this stringent requirement is **impurity control**. Residual neutral gas molecules within the vessel can interact with the hot plasma. For instance, a hot plasma ion can undergo a **charge-exchange** reaction with a cold neutral atom. In this process, the ion captures an electron from the neutral, becoming a fast, uncharged atom. This fast neutral is no longer confined by the magnetic field and escapes, striking the vessel wall and carrying away a significant amount of the plasma's thermal energy. The rate of such reactions is directly proportional to the density of the neutral gas, $n$. According to the [ideal gas law](@entry_id:146757), $p = n k_{\mathrm{B}} T$, minimizing the neutral density requires achieving the lowest possible pressure.

In stark contrast, the **Cryostat** is the large, room-temperature structure that encloses the VV and the superconducting magnet system. The volume between the outer wall of the VV and the inner wall of the cryostat, which also contains the magnets and their support structures, is evacuated to form the **insulating vacuum**. The primary function of this vacuum is not plasma purity but **[thermal insulation](@entry_id:147689)**. It serves to minimize heat transfer from the room-temperature cryostat wall to the cryogenic surfaces of the superconducting magnets, which must be maintained at temperatures of approximately $4\,\text{K}$. The pressure requirement for the insulating vacuum ($10^{-2}$ to $10^{-4}\,\text{Pa}$) is therefore much less demanding than for the primary vacuum, as it is dictated by heat transfer considerations rather than [plasma physics](@entry_id:139151).

### Vacuum Physics and Engineering

To create and maintain these distinct vacuum environments, a thorough understanding of gas dynamics and pumping technology is essential.

#### Gas Dynamics and Flow Regimes

The behavior of a gas is fundamentally dependent on the relationship between the average distance a molecule travels between collisions, known as the **[mean free path](@entry_id:139563)** ($\lambda$), and a characteristic dimension of the containing vessel, $L$. This relationship is quantified by the dimensionless **Knudsen number**, $\text{Kn} = \lambda/L$ .

From kinetic theory, the mean free path for a hard-sphere gas is inversely proportional to pressure:
$$
\lambda = \frac{k_B T}{\sqrt{2} \pi d^{2} P}
$$
where $k_B$ is the Boltzmann constant, $T$ is the temperature, $d$ is the molecular diameter, and $P$ is the pressure.

This pressure dependence leads to two distinct [flow regimes](@entry_id:152820):

1.  **Viscous (or Continuum) Flow ($P \gg P_\star$, $\text{Kn} \ll 1$)**: At high pressures (e.g., near atmosphere), the [mean free path](@entry_id:139563) is very short compared to the duct size. Molecules collide frequently with each other, and the gas behaves as a continuous fluid. Its flow is governed by [hydrodynamics](@entry_id:158871) and is characterized by a pressure-dependent viscosity. The conductance ($C_{visc}$) of a pumping duct in this regime is proportional to the average pressure, $C_{visc} \propto P$. This means that during the initial pump-down of a vessel, the conductance of the system decreases as the pressure drops.

2.  **Molecular Flow ($P \ll P_\star$, $\text{Kn} \gg 1$)**: At low pressures (in the high-vacuum and UHV regimes), the mean free path is much larger than the duct dimensions. Molecules rarely collide with each other; their dynamics are dominated by collisions with the chamber walls. The gas no longer behaves as a collective fluid. The conductance ($C_{mol}$) of a duct becomes independent of pressure and is determined solely by the geometry of the duct and the [thermal velocity](@entry_id:755900) of the gas molecules, scaling with temperature as $C_{mol} \propto \sqrt{T}$.

The **transition pressure**, $P_\star$, can be defined as the pressure at which $\text{Kn} = 1$, or $\lambda = L$. Solving for this pressure gives:
$$
P_\star = \frac{k_B T}{\sqrt{2} \pi d^{2} L}
$$
For typical fusion vacuum systems and duct dimensions, this transition occurs in the range of $1$ to $10^{-1}\,\text{Pa}$. This transition is critically important because below $P_\star$, the pressure-independent conductance of ducts and ports often becomes the primary bottleneck for the entire pumping system .

#### Pumping System Fundamentals

The performance of a vacuum system is characterized by three key parameters: **throughput** ($Q$), **pumping speed** ($S$), and **conductance** ($C$) .

-   **Throughput ($Q$)** is the quantity of gas flowing per unit time, with units of $\text{Pa} \cdot \text{m}^3/\text{s}$. In steady-state, it is equivalent to the total gas load entering the system.
-   **Pumping Speed ($S$)** is the [volumetric flow rate](@entry_id:265771) at which a pump removes gas, defined at a specific point by the relation $S = Q/P$, where $P$ is the pressure at that point. It has units of $\text{m}^3/\text{s}$.
-   **Conductance ($C$)** measures a vacuum component's ability to transmit gas. In the molecular flow regime, it relates the throughput to the pressure difference across the component: $Q = C(P_{\text{upstream}} - P_{\text{downstream}})$. It also has units of $\text{m}^3/\text{s}$.

When a pump with an intrinsic speed $S_p$ is connected to a vacuum vessel through a duct of conductance $C$, the components are in series. The throughput $Q$ is constant through the system. We have $Q = C(P_v - P_i)$ across the duct and $Q = S_p P_i$ at the pump inlet, where $P_v$ is the vessel pressure and $P_i$ is the pump inlet pressure. The vessel effectively "sees" a reduced pumping speed, $S_{\text{eff}}$, defined by $Q = S_{\text{eff}} P_v$. Combining these relations yields the fundamental equation for series pumping elements:
$$
\frac{1}{S_{\text{eff}}} = \frac{1}{S_p} + \frac{1}{C}
$$
This relationship shows that the component with the lowest value (be it $S_p$ or $C$) dominates and limits the overall system performance. For instance, if a pump with a speed $S_p = 3.0\,\text{m}^3/\text{s}$ is connected via a duct with a low conductance of $C = 0.75\,\text{m}^3/\text{s}$, the effective speed at the vessel is only $S_{\text{eff}} = (1/3.0 + 1/0.75)^{-1} = 0.60\,\text{m}^3/\text{s}$. The limited conductance of the duct drastically reduces the realized pumping speed, leading to a much higher vessel pressure than one might naively expect from the pump's catalog value .

#### Gas Sources in Vacuum Systems

Achieving UHV is not just about pumping gas out; it is equally about minimizing the rate at which gas enters the vacuum volume. This total gas influx is known as the **gas load**. In a leak-free, baked system, the dominant gas load comes from **[outgassing](@entry_id:753025)**—the spontaneous release of gas from the materials of the vessel itself . Outgassing is a composite phenomenon involving several distinct physical processes.

-   **Desorption**: This is the release of molecules that are physically adsorbed or chemically bound to the internal surfaces of the vessel. After exposure to air, vessel surfaces are covered with many monolayers of gas, predominantly water vapor. Desorption is a [thermally activated process](@entry_id:274558), meaning its rate increases exponentially with temperature according to an Arrhenius-type relation. A **bakeout**, heating the vessel to temperatures of $450\,\text{K}$ ($180\,^{\circ}\text{C}$) or higher under vacuum, dramatically increases the desorption rate of water and other volatile species, allowing them to be pumped away. This process is essential for achieving UHV. For example, for water with a typical binding energy of $E_w = 0.9\,\text{eV}$, increasing the temperature from $300\,\text{K}$ to $450\,\text{K}$ increases the desorption rate constant by a factor of approximately $10^5$ . At a constant temperature, the [outgassing](@entry_id:753025) rate from desorption decays with time, often as a power law ($q(t) \propto t^{-\alpha}$), as the surface coverage decreases.

-   **Diffusion**: This is the transport of dissolved species, most notably hydrogen, from within the bulk of the metallic vessel wall to the vacuum-facing surface. The rate is governed by Fick's laws, and the key parameter is the **diffusivity**, $D$, which is also strongly temperature-dependent. The [characteristic time](@entry_id:173472), $\tau_{diff}$, to deplete gas from a layer of thickness $L$ scales as $\tau_{diff} \propto L^2/D$. A high-temperature bakeout accelerates diffusion, causing hydrogen to migrate out of a significant near-surface layer of the metal. After the vessel is cooled, the diffusion rate drops dramatically, but the [outgassing](@entry_id:753025) rate is now limited by the much lower concentration gradient in the pre-depleted layer. This is why bakeout is crucial for reducing the long-term hydrogen [outgassing](@entry_id:753025) that often dominates the base pressure in a well-conditioned steel vessel [@problem_id:3724897, @problem_id:3724873].

-   **Permeation**: This is the transport of gas from the external environment, across the solid wall, and into the vacuum. It is a multi-step process involving [adsorption](@entry_id:143659) on the outer surface, diffusion through the bulk, and desorption from the inner surface. The steady-state [permeation](@entry_id:181696) flux is inversely proportional to the wall thickness and increases strongly with temperature. This process is generally a minor contributor in thick-walled UHV vessels operating near room temperature.

### Cryostat Design: Principles of Thermal Isolation

The singular purpose of the cryostat and its insulating vacuum is to thermally isolate the cold mass of the superconducting magnets from the ambient temperature environment. The total heat transfer rate, or **heat leak**, to the cryogenic system determines the required size and operating cost of the associated cryoplant. Minimizing this heat leak is a primary design driver. Heat transfer occurs through three mechanisms, and the [cryostat design](@entry_id:748089) must address all of them .

#### Mitigating Radiative Heat Transfer

Heat transfer via thermal radiation between a warm surface at temperature $T_h$ and a cold surface at $T_c$ is governed by the Stefan-Boltzmann law:
$$
Q_{\text{rad}} = \sigma \varepsilon A (T_h^4 - T_c^4)
$$
where $\sigma$ is the Stefan-Boltzmann constant, $A$ is the area, and $\varepsilon$ is the effective [emissivity](@entry_id:143288) of the surfaces. Given the fourth-power dependence on temperature, the radiative heat load from the $300\,\text{K}$ cryostat wall to the $4\,\text{K}$ magnet cold mass would be enormous without mitigation. Two key strategies are employed:

1.  **Multi-Layer Insulation (MLI)**: This consists of many layers of thin, highly reflective sheets (like aluminized Mylar) separated by vacuum. MLI acts as a series of radiation shields, drastically reducing the effective emissivity $\varepsilon$ between the warm and cold boundaries, often to values of $0.01-0.03$.

2.  **Thermal Shields**: A actively cooled intermediate surface, or **[thermal shield](@entry_id:755894)**, is placed between the $300\,\text{K}$ wall and the $4\,\text{K}$ cold mass. This shield is typically maintained at a moderately cryogenic temperature, such as $80\,\text{K}$ using liquid nitrogen. The shield intercepts the vast majority of the radiation from the $300\,\text{K}$ wall. The heat load to the $4\,\text{K}$ cold mass is then only due to radiation from the much colder $80\,\text{K}$ shield. As a quantitative example, consider a system where the radiative load from $300\,\text{K}$ to an $80\,\text{K}$ shield is calculated to be $4.6\,\text{kW}$. The subsequent radiative load from that $80\,\text{K}$ shield to the $4\,\text{K}$ mass is only about $18.6\,\text{W}$—a reduction of more than 200 times. This demonstrates the profound effectiveness of thermal shielding, shifting the bulk of the cooling duty to a cheaper, more efficient higher-temperature cryogenic circuit .

#### Mitigating Conductive Heat Transfer

Solid conduction occurs through any mechanical structures that bridge the temperature gap, such as supports for the magnet cold mass. The heat conducted is given by Fourier's law, $Q_{\text{cond}} = k A \Delta T / L$. To minimize this load, supports are designed to be long and slender (maximizing $L$, minimizing $A$) and are made from materials with low thermal conductivity, $k$. Furthermore, these supports are **thermally intercepted** at the [thermal shield](@entry_id:755894) temperature. This means a support does not run directly from $300\,\text{K}$ to $4\,\text{K}$; instead, it runs from $300\,\text{K}$ to $80\,\text{K}$, where the heat is removed by the $80\,\text{K}$ cooling circuit, and a separate support section runs from $80\,\text{K}$ to $4\,\text{K}$. This strategy, analogous to thermal shielding, dramatically reduces the heat leak to the coldest stage. In a well-designed system, the conductive load to the $4\,\text{K}$ level can be limited to just a few watts .

#### Mitigating Gas Conduction

Heat can also be transferred by residual gas molecules traveling between the warm and cold surfaces. In the molecular flow regime of the cryostat's insulating vacuum, this heat flux is directly proportional to the residual gas pressure, $q_{\text{gas}} \propto P$ . This is why a good vacuum is necessary. Doubling the pressure doubles the gas conduction heat load. The heat flux also depends on the gas species. From kinetic theory, the heat transfer is inversely proportional to the square root of the [molecular mass](@entry_id:152926), $M$. This means that light gases, like helium, are much better thermal conductors than heavier gases like nitrogen or argon at the same pressure. Therefore, a partial pressure of helium in the insulating vacuum is particularly detrimental to [thermal performance](@entry_id:151319). With a vacuum of $10^{-4}\,\text{Pa}$, the heat load from residual gas is typically negligible compared to radiation and solid conduction .

### Vacuum Vessel Design: Challenges of the Plasma Environment

While the cryostat's design is dominated by [thermal insulation](@entry_id:147689), the vacuum vessel faces a more complex set of challenges stemming from its proximity to the plasma and its role as a primary safety boundary.

#### Vacuum Performance and Wall Conditioning

As previously discussed, the VV must achieve UHV base pressures to ensure a clean plasma. This is accomplished through a combination of high pumping speed and rigorous control of the gas load. This leads to a distinction between two operational pressure states [@problem_id:372BG886]:

-   **Base Pressure ($P_{\text{base}}$)**: The pressure achieved between plasma discharges, determined by the balance between the residual [outgassing](@entry_id:753025) rate of the walls and the effective pumping speed: $P_{\text{base}} = Q_{\text{outgas}} / S_{\text{eff}}$. Reaching a low base pressure is a key indicator of successful **wall conditioning** (i.e., a low [outgassing](@entry_id:753025) rate achieved via bakeout).

-   **Dynamic Pressure ($P_{\text{dyn}}$)**: The pressure during a plasma discharge, determined by the balance of the external gas fueling rate ($Q_f$) and the pumping speed: $P_{\text{dyn}} \approx Q_f / S_{\text{eff}}$ (since $Q_f \gg Q_{\text{outgas}}$). This pressure is actively controlled to maintain the desired plasma density.

The operational window for the [dynamic pressure](@entry_id:262240) is bounded by physics and engineering constraints. The minimum pressure is set by the required fueling rate, while the maximum is limited by impurity control guidelines (i.e., keeping the neutral density below a threshold to limit charge-exchange losses) and by the maximum throughput capacity of the pumping system [@problem_id:372BG886].

To further improve vacuum conditions and [plasma-wall interaction](@entry_id:197715), advanced [surface engineering](@entry_id:155768) techniques may be employed. **Barrier coatings** like titanium nitride (TiN) can be deposited on the steel surface to block hydrogen diffusion from the bulk. **Non-Evaporable Getter (NEG)** coatings (e.g., Ti-Zr-V alloys) can be activated to act as distributed pumps, chemically capturing active gases like hydrogen, water, and carbon oxides, thereby dramatically lowering the base pressure and shifting the residual gas composition toward unpumped species like methane or noble gases .

#### Structural Demands

The vacuum vessel is a formidable structure, designed to withstand a host of extreme loads.

-   **Pressure Loads**: Like the cryostat, the VV is a vacuum component and must be designed to resist the inward-acting [atmospheric pressure](@entry_id:147632) of $\approx 10^5\,\text{Pa}$ without buckling. However, unlike the cryostat, the VV must also be designed as a [pressure vessel](@entry_id:191906) to contain potential **in-vessel loss-of-coolant accidents (LOCA)**. A break in a high-pressure water cooling pipe inside the vessel would lead to rapid vaporization and a significant internal overpressure event (on the order of $1-3 \times 10^5\,\text{Pa}$). The VV's role as the primary confinement boundary for radioactive materials (like tritium) makes its integrity during such events a paramount safety requirement .

-   **Electromagnetic (EM) Loads**: During a plasma **disruption**—a rapid loss of [plasma confinement](@entry_id:203546) and current—the decaying [plasma current](@entry_id:182365) induces powerful **[eddy currents](@entry_id:275449)** in the conductive walls of the VV. The interaction of these large [eddy currents](@entry_id:275449) with the strong, quasi-static [toroidal magnetic field](@entry_id:756057) generates immense transient Lorentz forces ($\mathbf{F} = I \mathbf{L} \times \mathbf{B}$) that can twist and crush the vessel. Designing the VV to withstand these EM loads is often the most significant structural challenge .

The design of a shell to resist external pressure is a problem of [structural stability](@entry_id:147935). The primary failure mode is **buckling**, an elastic instability that occurs at a stress level often far below the material's [yield strength](@entry_id:162154). For a given mass and enclosed volume, the most structurally efficient shape for resisting uniform external pressure is a perfect **sphere**, which experiences only uniform membrane compression. A **torus** is less efficient due to its complex curvature, and a **cylinder**, especially one with flat end caps, is significantly weaker, as the junctions and flat surfaces introduce bending stresses that precipitate [buckling](@entry_id:162815) at much lower pressures. For a fixed volume and mass, a spherical shell might withstand a critical pressure of $\approx 39\,\text{MPa}$, a comparable toroidal shell $\approx 30\,\text{MPa}$, and a cylindrical shell a mere $\approx 0.7\,\text{MPa}$ . This stark difference highlights why the toroidal shape of a tokamak VV, while necessary for [plasma confinement](@entry_id:203546), presents a significant [structural engineering](@entry_id:152273) challenge.

### Integrated System Design and Operation

#### Pumping System Configuration

The distinct requirements of the base vacuum and the high-throughput plasma exhaust lead to specialized, hybrid pumping systems .

-   **Roughing pumps** (e.g., scroll or screw pumps) are used for the initial pump-down from [atmospheric pressure](@entry_id:147632) into the viscous and transitional [flow regimes](@entry_id:152820).
-   **Turbomolecular pumps (TMPs)** are momentum-transfer pumps that are essential for establishing the base UHV and for continuously pumping gases that are not easily captured by other means, particularly [helium ash](@entry_id:750224) and other impurities. They are backed by roughing pumps.
-   **Cryopumps** are capture pumps that excel at providing very high pumping speeds for specific gases. They are ideally suited for handling the large flux of deuterium and tritium exhausted from the plasma. To be effective, they must be located as close as possible to the gas source (e.g., in the [divertor](@entry_id:748611)) with a high-conductance connection. Pumping hydrogen isotopes requires cryocondensation at temperatures near $4\,\text{K}$. Pumping helium requires cryosorption on a sorbent like activated charcoal, also at temperatures near $4\,\text{K}$. A cryopanel at $77\,\text{K}$ ([liquid nitrogen](@entry_id:138895) temperature) is completely ineffective for pumping hydrogen or helium .

A typical, robust configuration thus involves a set of TMPs for creating the base vacuum and for general-purpose impurity pumping, supplemented by large, localized cryopumps in the divertor region to handle the high-throughput plasma exhaust .

#### Codes, Standards, and Verification

The vacuum vessel and cryostat are safety-critical components. Their design, fabrication, and testing are governed by rigorous industrial codes and standards. In the European Union, for instance, a vacuum vessel is classified as **pressure equipment** under the Pressure Equipment Directive (PED) because it is designed to resist a pressure differential greater than $0.5\,\text{bar}$ .

Conformity is demonstrated by adhering to codes like **EN 13445** (European Standard for unfired pressure vessels) or other recognized codes such as the **ASME Boiler and Pressure Vessel Code, Section VIII**, with assessment by a Notified Body. These codes contain specific, detailed rules for designing shells against **[buckling](@entry_id:162815) under external pressure**, which, as discussed, is the primary failure mode.

The codes do not, however, prescribe specific leak tightness values. The **leak rate acceptance criterion** is a performance-based requirement derived by the project engineers from the [mass balance equation](@entry_id:178786) ($P = Q/S$) to ensure the target vacuum pressures can be achieved. Verification is performed using high-sensitivity **helium [mass spectrometer](@entry_id:274296) leak testing**, with results specified in units of $\text{Pa} \cdot \text{m}^3/\text{s}$. The leak tightness requirement for the primary vacuum vessel is typically orders of magnitude more stringent than that for the cryostat's insulating vacuum .