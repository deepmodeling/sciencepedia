## Introduction
High-Entropy Alloys (HEAs) represent a paradigm shift in materials science, offering vast compositional landscapes for designing materials with exceptional properties. Among the diverse microstructures achievable in HEAs, eutectic and lamellar architectures are particularly compelling, providing a unique combination of high strength, toughness, and functional anisotropy. However, the multicomponent nature of these alloys introduces significant complexity, making the prediction and control of these intricate structures a formidable challenge. This article provides a systematic framework for understanding and engineering these advanced materials, bridging the gap between fundamental theory and practical application.

Over the three subsequent sections, you will gain a comprehensive understanding of lamellar HEAs. The journey begins in **"Principles and Mechanisms,"** which delves into the core thermodynamics and kinetics that govern eutectic solidification, from phase partitioning and constitutional supercooling to the selection of lamellar spacing. Next, **"Applications and Interdisciplinary Connections"** connects this foundational knowledge to real-world scenarios, exploring how processing methods like additive manufacturing shape the microstructure and how this architecture dictates mechanical and physical properties. Finally, **"Hands-On Practices"** will solidify your learning by guiding you through practical problems that apply these concepts to predict microstructural evolution and material performance.

## Principles and Mechanisms

The formation of eutectic and lamellar microstructures in High-Entropy Alloys (HEAs) is governed by a sophisticated interplay of multicomponent thermodynamics, solidification kinetics, and interfacial phenomena. While the previous chapter introduced the general characteristics of these materials, this chapter delves into the fundamental principles and mechanisms that dictate their emergence and control their morphology. We will systematically dissect the process, beginning with the thermodynamic driving forces, proceeding to the kinetics of coupled growth, and concluding with an examination of the interfacial structures that define the final microstructure.

### Thermodynamic Foundations of Eutectic Reactions in Multicomponent Systems

At its core, a eutectic microstructure originates from a specific type of phase transformation where a single liquid phase solidifies into two or more solid phases simultaneously. In the context of lamellar HEAs, we are primarily concerned with the two-phase eutectic reaction:

$$
\mathrm{L} \to \alpha + \beta
$$

Here, a parent liquid phase ($L$) transforms into two distinct solid solution phases, $\alpha$ and $\beta$, which grow cooperatively. This reaction must be distinguished from other multiphase reactions involving a liquid. A **peritectic** reaction involves a liquid and a solid reacting to form a new solid ($\mathrm{L} + \alpha \to \beta$), while a **monotectic** reaction involves liquid-phase separation ($\mathrm{L}_1 \to \mathrm{L}_2 + \alpha$). The characteristic, periodic intergrowth of two solid phases, such as a lamellar pattern, is a hallmark of the eutectic pathway.

#### The Gibbs Phase Rule and Its Implications for HEAs

The thermodynamic variance, or the number of degrees of freedom ($F$), of a system at equilibrium is given by the Gibbs phase rule. For a system with $C$ components and $P$ phases at a fixed pressure, the rule is expressed as:

$$
F = C - P + 1
$$

In a classic binary alloy ($C=2$), the three-phase eutectic equilibrium ($P=3$) results in $F = 2 - 3 + 1 = 0$. This **invariance** means the reaction occurs at a single, fixed temperature (the eutectic temperature) and at fixed compositions of the three phases. However, for a multicomponent HEA (typically with $C \ge 4$), the situation is different. For the same three-phase equilibrium, the variance is $F = C - 3 + 1 = C - 2 \ge 2$. This means the eutectic reaction is no longer invariant and can occur over a range of temperatures and compositions, defining a "eutectic trough" or a higher-dimensional manifold in the phase space.

Despite this higher variance, experimental thermal analysis, such as Differential Scanning Calorimetry (DSC), on near-eutectic HEAs often reveals a single, sharp thermal arrest, mimicking the behavior of an invariant reaction. This occurs when the liquidus and solidus hypersurfaces in the multicomponent phase diagram are very steep and closely spaced along the alloy's solidification path. The transformation happens over a very narrow temperature range that is not resolved by the instrument, giving the appearance of invariance.

#### Partitioning and the Pseudobinary Approximation

The behavior of a multicomponent eutectic is dictated by how the constituent elements partition between the liquid, $\alpha$, and $\beta$ phases. The **element-specific partition coefficient**, $k_i^{\alpha}$, quantifies this behavior. For an element $i$ and a solid phase $\alpha$, it is defined as the ratio of the mole fraction of $i$ in the solid to that in the liquid at the interface:

$$
k_i^{\alpha} = \frac{x_i^{\alpha}}{x_i^{\mathrm{L}}}
$$

This coefficient is fundamentally linked to the chemical potentials of the components. At local equilibrium, where $\mu_i^{\alpha} = \mu_i^{\mathrm{L}}$, the partition coefficient can be formally expressed as:

$$
k_i^{\alpha} = \exp\left(\frac{\mu_i^{\mathrm{L},0} - \mu_i^{\alpha,0}}{R T}\right) \frac{\gamma_i^{\mathrm{L}}}{\gamma_i^{\alpha}}
$$

where $\mu_i^{\phi,0}$ is the chemical potential of pure component $i$ in phase $\phi$ at temperature $T$, $R$ is the gas constant, and $\gamma_i^{\phi}$ is the activity coefficient of $i$ in phase $\phi$. It is crucial to note that the numerical value of $k_i$ depends on the units of composition used; the expression above is derived using mole fractions ($x_i$), which is the natural choice for thermodynamic formalism.

An element $i$ that thermodynamically stabilizes the $\alpha$ phase will preferentially partition to it, resulting in $k_i^{\alpha} > 1$. For coupled eutectic growth to occur, this element must be rejected by the competing $\beta$ phase, meaning $k_i^{\beta}  1$. This differential partitioning, where an element is enriched in one solid lamella and depleted in the adjacent one, is known as **anti-segregation** and is the fundamental driver for the diffusive transport required for lamellar growth.

The complexity of a $C$-component phase diagram can be daunting. A powerful simplification is the **pseudobinary approximation**. This approximation is valid under a very specific thermodynamic condition: when a subset of the components does not partition between the coexisting phases. Consider a quinary ($C=5$) system of elements $\{A,B,C,D,E\}$. If the system is constrained to a compositional section where the ratios and total amount of $C$, $D$, and $E$ are fixed, this section can behave like a binary diagram of $A$ and $B$ only if the tie-lines connecting the compositions of the equilibrium phases ($L, \alpha, \beta$) lie entirely within this section. This occurs if elements $C$, $D$, and $E$ act as "spectators" with partition coefficients close to unity ($k_C \approx k_D \approx k_E \approx 1$) for both solid phases. In this special case, only $A$ and $B$ partition, and the three-phase equilibrium manifold of the quinary system intersects the section at what appears to be an invariant eutectic point, simplifying analysis considerably.

### Kinetics of Lamellar Growth

While thermodynamics dictates the possibility of a eutectic reaction, kinetics governs the morphology and scale of the resulting microstructure.

#### Cooperative vs. Divorced Eutectic Growth

The formation of a fine, periodic lamellar structure is the result of **cooperative growth**. In this mode, the $\alpha$ and $\beta$ solid phases grow side-by-side into the liquid, forming a coupled, macroscopically planar solid-liquid interface that advances at a common velocity. The growth of phase $\alpha$ rejects solutes that are consumed by the adjacent growing phase $\beta$, and vice versa. This establishes a lateral diffusion field in the liquid just ahead of the interface. For this exchange to be efficient, the diffusion fields from the neighboring $\alpha$-L and $\beta$-L interfaces must overlap.

This is in stark contrast to **divorced eutectic** formation, where the growth of the two solid phases is decoupled. One phase may nucleate and grow ahead of the other, leading to a long-range buildup of solute in the liquid. This solute enrichment eventually triggers the delayed and independent nucleation and growth of the second phase. The resulting microstructure is non-lamellar, often consisting of primary dendrites of one phase with the second phase appearing as discrete particles or a coarse network in the interdendritic regions. The key distinction lies in the kinematic coupling of the interfaces and the spatial organization of solute redistribution.

#### The Onset of Pattern Formation: Constitutional Supercooling

The stability of a planar solidification front is a prerequisite for understanding why patterned growth occurs at all. During solidification, solute partitioning creates a concentration gradient in the liquid ahead of the interface. This, in turn, creates a gradient in the local equilibrium liquidus temperature, $T_L(z)$. **Constitutional supercooling** arises when the actual temperature in the liquid, dictated by the externally imposed thermal gradient $G$, falls below this local liquidus temperature. This creates a region of liquid that is supercooled with respect to its local composition, providing a driving force for any protuberance to grow, thereby destabilizing the planar front.

For a multicomponent alloy, the contributions of all partitioning elements are additive. The criterion for a stable planar front, avoiding constitutional supercooling, can be expressed as:

$$
G \ge -R \sum_{i=1}^{N} \frac{m_i C_{0,i}(1-k_i)}{D_i k_i}
$$

where $R$ is the interface velocity, $C_{0,i}$ is the nominal alloy composition of element $i$, $D_i$ is its diffusivity in the liquid, and $m_i$ is the liquidus slope. A component $i$ contributes to instability (i.e., makes the right-hand side larger and positive) if the term $-m_i(1-k_i)/k_i$ is positive. For a typical solute that depresses the melting point ($m_i  0$) and is rejected into the liquid ($0  k_i  1$), this condition is met, and the component is destabilizing. When the stability condition is violated, the planar front breaks down, leading to the formation of patterns such as cells, dendrites, or, in the case of eutectic alloys, cooperative lamellar structures.

#### Lamellar Spacing Selection: The Jackson-Hunt Model

Once a lamellar pattern forms, what determines its characteristic spacing, $\lambda$? The seminal work of Jackson and Hunt provides the answer. Their model posits that for a given growth velocity $V$, the system self-organizes to a spacing that minimizes the total undercooling ($\Delta T$) at the interface. This total undercooling is the sum of two competing contributions:

1.  **Solutal Undercooling ($\Delta T_D$)**: This arises from the solute pile-up required to drive lateral diffusion between the lamellae. A larger spacing $\lambda$ means solute must diffuse over longer distances, requiring a greater concentration buildup and thus a larger undercooling. This contribution is proportional to the product of velocity and spacing: $\Delta T_D \propto V \lambda$.

2.  **Capillarity Undercooling ($\Delta T_\Gamma$)**: The solid-liquid interfaces between lamellae are curved. According to the Gibbs-Thomson effect, this curvature lowers the equilibrium temperature. The average curvature is inversely proportional to the spacing, so the undercooling from this effect scales as $\Delta T_\Gamma \propto 1/\lambda$. A finer spacing means higher curvature and a larger capillary undercooling.

The total undercooling is $\Delta T = A V \lambda + B/\lambda$, where $A$ and $B$ are material constants. Minimizing $\Delta T$ with respect to $\lambda$ ($\partial \Delta T / \partial \lambda = 0$) yields the famous scaling law for eutectic growth:

$$
\lambda^2 V = \text{constant} = \frac{B}{A}
$$

This relationship, which has been widely confirmed experimentally, shows that faster growth velocities lead to finer lamellar spacings. This framework is built on the condition that for steady cooperative growth, the interface must be isothermal, requiring a precise local balance between the solutal and capillary contributions to maintain a constant total undercooling $\Delta T$ across the entire front.

A complementary view comes from a variational argument, which frames the problem as the minimization of a total "cost" functional. This functional includes a penalty for creating interfacial area (proportional to $1/\lambda$) and a penalty for inefficient transport (proportional to the diffusion path length, which scales with $\lambda$). The minimization of this sum again leads to an optimal spacing. Furthermore, this perspective highlights why lamellar geometry is often preferred: planar interfaces minimize area for a given period, and straight-through diffusion paths minimize tortuosity, making the geometry efficient in both respects.

The physics of this competition can be formally captured by dimensionless groups derived from the governing equations. The **Péclet number**, $Pe = V\lambda/D_{\text{eff}}$, compares the rate of advection to diffusion over the length scale of the lamellae. The **capillary number**, $Ca_{\kappa} = \Gamma/(m_{\text{eff}}\Delta C_{\text{eff}}\lambda)$, compares the magnitude of capillary effects to solutal effects. These numbers define the operating regime of the solidification process.

### The Structure and Energy of Lamellar Interfaces

The lamellar microstructure is defined by the vast area of solid-solid interfaces between the $\alpha$ and $\beta$ phases. The nature of these interfaces is critical to the alloy's properties.

The **interphase boundary energy**, $\gamma_{\alpha/\beta}$, is the excess free energy per unit area associated with the creation of the interface. It is formally defined as the excess grand potential per unit area at fixed temperature, pressure, and chemical potentials. The structure and energy of these boundaries depend on the degree of atomic registry across them. We can classify them as:

1.  **Coherent Interfaces**: Lattice planes are continuous across the boundary. This perfect registry is only possible for small misfits and requires the storage of elastic coherency strain energy. These interfaces have the lowest energy, typically in the range of $10-100 \text{ mJ m}^{-2}$ for metals.

2.  **Semicoherent Interfaces**: The lattice mismatch is partially accommodated by a periodic array of misfit dislocations. This reduces the long-range strain energy at the cost of the energy of the dislocation network. These interfaces have intermediate energy, typically $100-400 \text{ mJ m}^{-2}$.

3.  **Incoherent Interfaces**: There is no systematic registry between the lattices on either side of the boundary. The structure resembles a high-angle grain boundary, resulting in the highest interfacial energy, often $0.5-2.0 \text{ J m}^{-2}$.

In many eutectic HEAs, particularly those involving FCC and BCC (or ordered B2) phases, the lamellae form semicoherent interfaces. To minimize energy, the two crystal lattices adopt a specific, low-energy **Orientation Relationship (OR)**. These ORs align the densest-packed planes and directions of the two structures. Two of the most commonly observed ORs are:

-   **Kurdjumov-Sachs (K-S) OR**: $(111)_{\text{FCC}} \parallel (110)_{\text{BCC}}$ and $[1\bar{1}0]_{\text{FCC}} \parallel [1\bar{1}1]_{\text{BCC}}$. This aligns the close-packed planes and a pair of close-packed directions within those planes.
-   **Nishiyama-Wasserman (N-W) OR**: $(111)_{\text{FCC}} \parallel (110)_{\text{BCC}}$ and $[11\bar{2}]_{\text{FCC}} \parallel [1\bar{1}0]_{\text{BCC}}$. This also aligns the close-packed planes but involves a different alignment of in-plane directions, rotated by about $5.26^\circ$ from the K-S relationship.

The establishment of a specific OR is a key mechanism for reducing the interfacial energy penalty, thereby stabilizing the lamellar morphology.

### Anisotropic Diffusion and Advanced Considerations

The models discussed thus far often assume isotropic liquid diffusion. However, in some systems, particularly those with strong short-range order in the liquid, diffusion can be anisotropic. This is represented by a diffusivity tensor $\mathbf{D}$ with non-zero off-diagonal terms. An off-diagonal component, such as $D_{xz} \ne 0$, has profound consequences. It means that a concentration gradient in the growth direction ($z$) can drive a diffusive flux in the lateral direction ($x$).

This cross-coupling has two main effects. First, it skews the solute boundary layer, causing iso-concentration contours to tilt relative to the interface. Second, and more dramatically, it breaks the symmetry of the solidification problem. A linear stability analysis reveals that the fastest-growing morphological instabilities are no longer perpendicular to the growth direction but are instead oblique modes. This can lead to the formation of macroscopic lamellar bands that are tilted with respect to the pulling direction, a feature sometimes observed in directionally solidified eutectics. Understanding such complexities is at the forefront of modeling solidification in complex alloys like HEAs.